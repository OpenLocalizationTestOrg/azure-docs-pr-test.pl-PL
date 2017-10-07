---
title: "aaaScheduling i wykonywania z fabryką danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, planowania i wykonywania aspektów modelu aplikacji fabryki danych Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="0e2e8-103">Planowanie fabryki danych i wykonywania</span><span class="sxs-lookup"><span data-stu-id="0e2e8-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="0e2e8-104">W tym artykule opisano aspekty planowania i wykonywania hello modelu aplikacji hello fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-104">This article explains hello scheduling and execution aspects of hello Azure Data Factory application model.</span></span> <span data-ttu-id="0e2e8-105">W tym artykule przyjęto założenie, że rozumiesz podstawowe pojęcia modelu aplikacji fabryki danych, w tym działania, potoki połączonych usług i zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="0e2e8-106">Dla podstawowych pojęciach dotyczących usługi fabryka danych Azure Zobacz hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-106">For basic concepts of Azure Data Factory, see hello following articles:</span></span>

* [<span data-ttu-id="0e2e8-107">Wprowadzenie tooData fabryki</span><span class="sxs-lookup"><span data-stu-id="0e2e8-107">Introduction tooData Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="0e2e8-108">Potoki</span><span class="sxs-lookup"><span data-stu-id="0e2e8-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="0e2e8-109">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="0e2e8-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="0e2e8-110">Czas rozpoczęcia i zakończenia potoku</span><span class="sxs-lookup"><span data-stu-id="0e2e8-110">Start and end times of pipeline</span></span>
<span data-ttu-id="0e2e8-111">Potok jest aktywna tylko między jego **start** czasu i **zakończenia** czasu.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="0e2e8-112">Nie jest wykonywany przed godziną rozpoczęcia hello lub po godzinie zakończenia hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-112">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="0e2e8-113">Jeśli potoku hello jest wstrzymana, nie została wykonana niezależnie od jego czas rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-113">If hello pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="0e2e8-114">Dla toorun potoku jego powinien nie można wstrzymać.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-114">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="0e2e8-115">Te ustawienia (start, koniec wstrzymana) można znaleźć w definicji potoku hello:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-115">You find these settings (start, end, paused) in hello pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="0e2e8-116">Aby uzyskać więcej informacji zobacz te właściwości [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="0e2e8-117">Określ harmonogram dla działania</span><span class="sxs-lookup"><span data-stu-id="0e2e8-117">Specify schedule for an activity</span></span>
<span data-ttu-id="0e2e8-118">Nie jest hello potok, który jest wykonywany.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-118">It is not hello pipeline that is executed.</span></span> <span data-ttu-id="0e2e8-119">Działania hello w potoku hello, które są wykonywane w hello jest ogólnym kontekście hello potoku.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-119">It is hello activities in hello pipeline that are executed in hello overall context of hello pipeline.</span></span> <span data-ttu-id="0e2e8-120">Można określić harmonogramu cyklicznego dla działania za pomocą hello **harmonogramu** sekcji aktywność JSON.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-120">You can specify a recurring schedule for an activity by using hello **scheduler** section of activity JSON.</span></span> <span data-ttu-id="0e2e8-121">Na przykład można zaplanować działania toorun co godzinę w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-121">For example, you can schedule an activity toorun hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="0e2e8-122">Jak pokazano na powitania po diagramu, określanie harmonogramu dla działania tworzy serię windows wirowania z w hello potoku rozpoczęcia i zakończenia razy.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-122">As shown in hello following diagram, specifying a schedule for an activity creates a series of tumbling windows with in hello pipeline start and end times.</span></span> <span data-ttu-id="0e2e8-123">Windows wirowania są szereg przedziały czasu nienakładający, ciągły stałym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="0e2e8-124">Te okna wirowania logiczne dla działania są nazywane **okien działania**.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Przykład harmonogram działania](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="0e2e8-126">Witaj **harmonogramu** właściwość dla działania jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-126">hello **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="0e2e8-127">Jeśli określisz tej właściwości musi być zgodna hello okresach, które określisz w definicji zestawu danych wyjściowych dla działania hello hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-127">If you do specify this property, it must match hello cadence you specify in hello definition of output dataset for hello activity.</span></span> <span data-ttu-id="0e2e8-128">Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-128">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="0e2e8-129">Dlatego należy utworzyć wyjściowy zestaw danych, nawet wtedy, gdy działanie hello nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-129">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="0e2e8-130">Określ harmonogram dla zestawu danych</span><span class="sxs-lookup"><span data-stu-id="0e2e8-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="0e2e8-131">Działania w potoku fabryki danych może zająć zero lub więcej danych wejściowych **zestawów danych** i tworzące co najmniej jeden wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="0e2e8-132">Dla działania można określić hello okresach, w których hello danych wejściowych jest dostępna lub dane wyjściowe hello jest generowany przy użyciu hello **dostępności** części hello definicji zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-132">For an activity, you can specify hello cadence at which hello input data is available or hello output data is produced by using hello **availability** section in hello dataset definitions.</span></span> 

<span data-ttu-id="0e2e8-133">**Częstotliwość** w hello **dostępności** sekcja określa jednostkę czasu hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-133">**Frequency** in hello **availability** section specifies hello time unit.</span></span> <span data-ttu-id="0e2e8-134">Witaj dozwolone są wartości częstotliwości: minuty, godziny, dnia, tygodnia i miesiąca.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-134">hello allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="0e2e8-135">Witaj **interwał** właściwości w sekcji dostępności hello Określa mnożnik częstotliwości.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-135">hello **interval** property in hello availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="0e2e8-136">Na przykład: Jeśli częstotliwość hello ustawiono tooDay i interwał jest ustawiany too1 dla wyjściowego zestawu danych, danych wyjściowych hello jest tworzony codziennie.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-136">For example: if hello frequency is set tooDay and interval is set too1 for an output dataset, hello output data is produced daily.</span></span> <span data-ttu-id="0e2e8-137">Można określić częstotliwość hello jako minutę, zaleca się ustawienie hello interwał toono mniej niż 15.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-137">If you specify hello frequency as minute, we recommend that you set hello interval toono less than 15.</span></span> 

<span data-ttu-id="0e2e8-138">Poniższy przykład hello, hello danych wejściowych jest dostępne co godzinę i danych wyjściowych hello jest tworzone co godzinę (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-138">In hello following example, hello input data is available hourly and hello output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="0e2e8-139">**Wejściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="0e2e8-139">**Input dataset:**</span></span> 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


<span data-ttu-id="0e2e8-140">**Wyjściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="0e2e8-140">**Output dataset**</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="0e2e8-141">Obecnie **wyjściowego zestawu danych dysków hello harmonogram**.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-141">Currently, **output dataset drives hello schedule**.</span></span> <span data-ttu-id="0e2e8-142">Innymi słowy harmonogram hello określony dla zestawu danych wyjściowych hello jest używany toorun działania w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-142">In other words, hello schedule specified for hello output dataset is used toorun an activity at runtime.</span></span> <span data-ttu-id="0e2e8-143">Dlatego należy utworzyć wyjściowy zestaw danych, nawet wtedy, gdy działanie hello nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-143">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="0e2e8-144">Jeśli działanie hello nie przyjmuje żadnych danych, możesz pominąć tworzenie zestawu danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-144">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 

<span data-ttu-id="0e2e8-145">W następujących hello potoku definicji, hello **harmonogramu** właściwość jest używane toospecify harmonogram działania hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-145">In hello following pipeline definition, hello **scheduler** property is used toospecify schedule for hello activity.</span></span> <span data-ttu-id="0e2e8-146">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-146">This property is optional.</span></span> <span data-ttu-id="0e2e8-147">Obecnie hello harmonogram hello działania muszą być zgodne harmonogram hello określony dla hello wyjściowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-147">Currently, hello schedule for hello activity must match hello schedule specified for hello output dataset.</span></span>
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

<span data-ttu-id="0e2e8-148">W tym przykładzie co godzinę uruchomień działania hello między hello godziny rozpoczęcia i zakończenia hello potoku.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-148">In this example, hello activity runs hourly between hello start and end times of hello pipeline.</span></span> <span data-ttu-id="0e2e8-149">dane wyjściowe Hello jest tworzone co godzinę dla windows trzech godzin (8 AM - 9 AM, 9 AM - 10, a 10 AM - 11: 00).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-149">hello output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="0e2e8-150">Nosi nazwę każdej jednostki danych używane lub generowane przez działanie Uruchom **wycinka danych**.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="0e2e8-151">powitania po diagramie przedstawiono przykład działania o jeden wejściowy zestaw danych i jeden wyjściowy zestaw danych:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-151">hello following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Harmonogram dostępności](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="0e2e8-153">Hello diagram pokazuje hello co godzinę wycinków danych dla hello argument wejściowy i wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-153">hello diagram shows hello hourly data slices for hello input and output dataset.</span></span> <span data-ttu-id="0e2e8-154">Witaj diagram przedstawia trzy wycinków wejściowych, które są gotowe do przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-154">hello diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="0e2e8-155">działanie AM 10-11 Hello jest w toku, tworzenie wycinek danych wyjściowych AM 10-11 hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-155">hello 10-11 AM activity is in progress, producing hello 10-11 AM output slice.</span></span> 

<span data-ttu-id="0e2e8-156">Dostęp można uzyskać interwał czasu hello skojarzone z hello wycinek bieżący w zestawie danych hello JSON przy użyciu zmiennych: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) i [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-156">You can access hello time interval associated with hello current slice in hello dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="0e2e8-157">Podobnie można uzyskać dostępu do interwał czasu hello skojarzone z okna działania za pomocą hello WindowStart i WindowEnd.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-157">Similarly, you can access hello time interval associated with an activity window by using hello WindowStart and WindowEnd.</span></span> <span data-ttu-id="0e2e8-158">Harmonogram Hello działania muszą być zgodne hello harmonogram hello wyjściowego zestawu danych działania hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-158">hello schedule of an activity must match hello schedule of hello output dataset for hello activity.</span></span> <span data-ttu-id="0e2e8-159">W związku z tym hello SliceStart i SliceEnd wartości są hello takie same jak wartości WindowStart i WindowEnd odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-159">Therefore, hello SliceStart and SliceEnd values are hello same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="0e2e8-160">Aby uzyskać więcej informacji o tych zmiennych, zobacz [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md#data-factory-system-variables) artykułów.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="0e2e8-161">Te zmienne można użyć do różnych celów w Twoich działaniach w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="0e2e8-162">Na przykład można ich tooselect dane wejściowe i wyjściowe zestawy danych reprezentujący dane serii czas (na przykład: 8 AM too9 MAM).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-162">For example, you can use them tooselect data from input and output datasets representing time series data (for example: 8 AM too9 AM).</span></span> <span data-ttu-id="0e2e8-163">W tym przykładzie również używane **WindowStart** i **WindowEnd** tooselect odpowiednie dane dla działania uruchamiania i skopiuj go blob tooa z odpowiednią hello **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-163">This example also uses **WindowStart** and **WindowEnd** tooselect relevant data for an activity run and copy it tooa blob with hello appropriate **folderPath**.</span></span> <span data-ttu-id="0e2e8-164">Witaj **folderPath** jest toohave sparametryzowane oddzielny folder dla każdej godziny.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-164">hello **folderPath** is parameterized toohave a separate folder for every hour.</span></span>  

<span data-ttu-id="0e2e8-165">W hello poprzedzających przykład określony dla zestawów danych wejściowych i wyjściowych harmonogram hello jest hello takie same (co godzinę).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-165">In hello preceding example, hello schedule specified for input and output datasets is hello same (hourly).</span></span> <span data-ttu-id="0e2e8-166">Jeśli hello wejściowy zestaw danych dla działania hello jest dostępny w innej częstotliwości, powiedz co 15 minut, hello tworzącego tego zestawu danych wyjściowych nadal odbywa się działanie godzinę jako hello wyjściowy zestaw danych jest jakie dysków hello harmonogram działania.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-166">If hello input dataset for hello activity is available at a different frequency, say every 15 minutes, hello activity that produces this output dataset still runs once an hour as hello output dataset is what drives hello activity schedule.</span></span> <span data-ttu-id="0e2e8-167">Aby uzyskać więcej informacji, zobacz [modelu zestawów danych z różnych częstotliwości](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="0e2e8-168">Dostępność zestawu danych i zasady</span><span class="sxs-lookup"><span data-stu-id="0e2e8-168">Dataset availability and policies</span></span>
<span data-ttu-id="0e2e8-169">Jak już wspomniano użycia hello częstotliwość i interwał właściwości w sekcji dostępności hello definicji zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-169">You have seen hello usage of frequency and interval properties in hello availability section of dataset definition.</span></span> <span data-ttu-id="0e2e8-170">Istnieje kilka właściwości, które mają wpływ na powitania planowania i wykonywania działania.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-170">There are a few other properties that affect hello scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="0e2e8-171">Dostępność zestawu danych</span><span class="sxs-lookup"><span data-stu-id="0e2e8-171">Dataset availability</span></span> 
<span data-ttu-id="0e2e8-172">Witaj poniższej tabeli opisano właściwości można używać w hello **dostępności** sekcji:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-172">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="0e2e8-173">Właściwość</span><span class="sxs-lookup"><span data-stu-id="0e2e8-173">Property</span></span> | <span data-ttu-id="0e2e8-174">Opis</span><span class="sxs-lookup"><span data-stu-id="0e2e8-174">Description</span></span> | <span data-ttu-id="0e2e8-175">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0e2e8-175">Required</span></span> | <span data-ttu-id="0e2e8-176">Domyślne</span><span class="sxs-lookup"><span data-stu-id="0e2e8-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0e2e8-177">frequency</span><span class="sxs-lookup"><span data-stu-id="0e2e8-177">frequency</span></span> |<span data-ttu-id="0e2e8-178">Określa jednostkę czasu hello w środowisku produkcyjnym wycinek zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-178">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="0e2e8-179"><b>Obsługiwana częstotliwość</b>: minuty, godziny, dnia, tygodnia, miesiąca</span><span class="sxs-lookup"><span data-stu-id="0e2e8-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="0e2e8-180">Tak</span><span class="sxs-lookup"><span data-stu-id="0e2e8-180">Yes</span></span> |<span data-ttu-id="0e2e8-181">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0e2e8-181">NA</span></span> |
| <span data-ttu-id="0e2e8-182">interval</span><span class="sxs-lookup"><span data-stu-id="0e2e8-182">interval</span></span> |<span data-ttu-id="0e2e8-183">Określa mnożnik częstotliwości</span><span class="sxs-lookup"><span data-stu-id="0e2e8-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="0e2e8-184">"Interwał częstotliwości x" Określa, jak często hello wycinek jest generowany.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-184">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="0e2e8-185">Należy hello podzielona na godzinę toobe zestawu danych, należy ustawić <b>częstotliwość</b> za<b>godzina</b>, i <b>interwał</b> za<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-185">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="0e2e8-186"><b>Uwaga</b>: Jeśli określisz częstotliwość co minutę, firma Microsoft zaleca ustawienie hello interwał toono mniej niż 15</span><span class="sxs-lookup"><span data-stu-id="0e2e8-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="0e2e8-187">Tak</span><span class="sxs-lookup"><span data-stu-id="0e2e8-187">Yes</span></span> |<span data-ttu-id="0e2e8-188">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0e2e8-188">NA</span></span> |
| <span data-ttu-id="0e2e8-189">Styl</span><span class="sxs-lookup"><span data-stu-id="0e2e8-189">style</span></span> |<span data-ttu-id="0e2e8-190">Określa, czy wycinek hello powinien zostać utworzony w hello rozpoczęcia/zakończenia hello interwału.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-190">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="0e2e8-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="0e2e8-191">StartOfInterval</span></span></li><li><span data-ttu-id="0e2e8-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="0e2e8-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="0e2e8-193">Jeśli częstotliwość ustawiono tooMonth i styl jest ustawiony tooEndOfInterval, wycinek hello jest realizowane na powitania ostatni dzień miesiąca.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-193">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="0e2e8-194">Jeśli hello styl jest ustawiony tooStartOfInterval, wycinek hello jest realizowane na powitania pierwszego dnia miesiąca.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-194">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="0e2e8-195">Jeśli częstotliwość ustawiono tooDay i styl jest ustawiony tooEndOfInterval, wycinek hello jest tworzona w hello ostatniej godziny hello dnia.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-195">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="0e2e8-196">Jeśli częstotliwość ustawiono tooHour i styl jest ustawiony tooEndOfInterval, wycinek hello jest generowany na końcu hello hello godzinę.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-196">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="0e2e8-197">Na przykład dla wycinka okres 13: 00 – 14: 00, wycinek hello jest generowany na 14: 00.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-197">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="0e2e8-198">Nie</span><span class="sxs-lookup"><span data-stu-id="0e2e8-198">No</span></span> |<span data-ttu-id="0e2e8-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="0e2e8-199">EndOfInterval</span></span> |
| <span data-ttu-id="0e2e8-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="0e2e8-200">anchorDateTime</span></span> |<span data-ttu-id="0e2e8-201">Definiuje położenie bezwzględne hello w czasie używana przez granice wycinek dataset toocompute harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-201">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="0e2e8-202"><b>Uwaga</b>: hello AnchorDateTime ma części daty, które są bardziej szczegółowego niż częstotliwość hello następnie hello części bardziej szczegółowego są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-202"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="0e2e8-203">Na przykład, jeśli hello <b>interwał</b> jest <b>co godzinę</b> (częstotliwość: godzinę i interwał: 1) i hello <b>AnchorDateTime</b> zawiera <b>minut i sekund</b>, następnie hello <b>minut i sekund</b> części hello AnchorDateTime są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-203">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="0e2e8-204">Nie</span><span class="sxs-lookup"><span data-stu-id="0e2e8-204">No</span></span> |<span data-ttu-id="0e2e8-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="0e2e8-205">01/01/0001</span></span> |
| <span data-ttu-id="0e2e8-206">Przesunięcie</span><span class="sxs-lookup"><span data-stu-id="0e2e8-206">offset</span></span> |<span data-ttu-id="0e2e8-207">Zakres czasu, przez który hello przesunięte początku i końcu wszystkie fragmenty zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-207">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="0e2e8-208"><b>Uwaga</b>: Jeśli jest określony zarówno anchorDateTime, jak i przesunięcie wynik hello jest shift hello połączone.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-208"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="0e2e8-209">Nie</span><span class="sxs-lookup"><span data-stu-id="0e2e8-209">No</span></span> |<span data-ttu-id="0e2e8-210">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0e2e8-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="0e2e8-211">przykład przesunięcia</span><span class="sxs-lookup"><span data-stu-id="0e2e8-211">offset example</span></span>
<span data-ttu-id="0e2e8-212">Domyślnie codziennie (`"frequency": "Day", "interval": 1`) wycinków uruchomione w czasie UTC 00: 00 (północ).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="0e2e8-213">Czas UTC 6: 00 toobe czas rozpoczęcia hello zamiast tego, ustawić hello przesunięcie pokazane na powitania po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-213">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="0e2e8-214">przykład anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="0e2e8-214">anchorDateTime example</span></span>
<span data-ttu-id="0e2e8-215">W hello poniższy przykład hello dataset jest tworzony co 23 godz.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-215">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="0e2e8-216">Witaj pierwszego wycinka rozpoczyna się od czasu hello określonego przez anchorDateTime hello, która jest ustawiona zbyt`2017-04-19T08:00:00` (czas UTC).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-216">hello first slice starts at hello time specified by hello anchorDateTime, which is set too`2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="0e2e8-217">Przesunięcie i stylu przykład</span><span class="sxs-lookup"><span data-stu-id="0e2e8-217">offset/style Example</span></span>
<span data-ttu-id="0e2e8-218">Witaj następujący zestaw danych jest miesięczne zestawu danych i jest generowany na 3rd każdego miesiąca o godzinie 8:00 AM (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="0e2e8-218">hello following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="0e2e8-219">Zestaw danych zasad</span><span class="sxs-lookup"><span data-stu-id="0e2e8-219">Dataset policy</span></span>
<span data-ttu-id="0e2e8-220">Zestaw danych może mieć zdefiniowane zasady sprawdzania poprawności określający, jak mogą być sprawdzone hello dane generowane przez wykonanie wycinek przed jest gotowy do użycia.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-220">A dataset can have a validation policy defined that specifies how hello data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="0e2e8-221">W takich przypadkach po zakończeniu wykonywania, wycinek hello hello dane wyjściowe wycinek stan zmienia się zbyt**oczekiwania** z podstanu z **weryfikacji**.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-221">In such cases, after hello slice has finished execution, hello output slice status is changed too**Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="0e2e8-222">Po zweryfikowaniu wycinków hello zmiany stanu wycinka hello zbyt**gotowe**.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-222">After hello slices are validated, hello slice status changes too**Ready**.</span></span> <span data-ttu-id="0e2e8-223">Jeśli wycinek danych został utworzony, ale nie przeszedł sprawdzania poprawności hello, uruchomień działania podrzędne wycinki, które są zależne od tego wycinka nie są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-223">If a data slice has been produced but did not pass hello validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="0e2e8-224">[Monitorowanie i zarządzanie nimi potoki](data-factory-monitor-manage-pipelines.md) obejmuje hello różnych stanów wycinków danych z fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers hello various states of data slices in Data Factory.</span></span>

<span data-ttu-id="0e2e8-225">Witaj **zasad** sekcja w definicji zestawu danych definiuje kryteria hello lub konieczne jest spełnienie warunku hello hello wycinków zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-225">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <span data-ttu-id="0e2e8-226">Witaj poniższej tabeli opisano właściwości można używać w hello **zasad** sekcji:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-226">hello following table describes properties you can use in hello **policy** section:</span></span>

| <span data-ttu-id="0e2e8-227">Nazwa zasad</span><span class="sxs-lookup"><span data-stu-id="0e2e8-227">Policy Name</span></span> | <span data-ttu-id="0e2e8-228">Opis</span><span class="sxs-lookup"><span data-stu-id="0e2e8-228">Description</span></span> | <span data-ttu-id="0e2e8-229">Stosowane za</span><span class="sxs-lookup"><span data-stu-id="0e2e8-229">Applied too</span></span>| <span data-ttu-id="0e2e8-230">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0e2e8-230">Required</span></span> | <span data-ttu-id="0e2e8-231">Domyślne</span><span class="sxs-lookup"><span data-stu-id="0e2e8-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="0e2e8-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="0e2e8-232">minimumSizeMB</span></span> | <span data-ttu-id="0e2e8-233">Sprawdza poprawność danych hello w **obiektów blob platformy Azure** spełnia hello wymagań minimalny rozmiar (w MB).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-233">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="0e2e8-234">Obiekt bob Azure</span><span class="sxs-lookup"><span data-stu-id="0e2e8-234">Azure Blob</span></span> |<span data-ttu-id="0e2e8-235">Nie</span><span class="sxs-lookup"><span data-stu-id="0e2e8-235">No</span></span> |<span data-ttu-id="0e2e8-236">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0e2e8-236">NA</span></span> |
| <span data-ttu-id="0e2e8-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="0e2e8-237">minimumRows</span></span> | <span data-ttu-id="0e2e8-238">Sprawdza poprawność danych hello w **bazy danych Azure SQL** lub **tabeli platformy Azure** zawiera hello minimalną liczbę wierszy.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-238">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="0e2e8-239">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0e2e8-239">Azure SQL Database</span></span></li><li><span data-ttu-id="0e2e8-240">Tabeli platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0e2e8-240">Azure Table</span></span></li></ul> |<span data-ttu-id="0e2e8-241">Nie</span><span class="sxs-lookup"><span data-stu-id="0e2e8-241">No</span></span> |<span data-ttu-id="0e2e8-242">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0e2e8-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="0e2e8-243">Przykłady</span><span class="sxs-lookup"><span data-stu-id="0e2e8-243">Examples</span></span>
<span data-ttu-id="0e2e8-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="0e2e8-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="0e2e8-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="0e2e8-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="0e2e8-246">Aby uzyskać więcej informacji na temat tych właściwości i przykłady, zobacz [utworzyć zestawy danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="0e2e8-247">Zasady dotyczące działań</span><span class="sxs-lookup"><span data-stu-id="0e2e8-247">Activity policies</span></span>
<span data-ttu-id="0e2e8-248">Zasady wpływają na zachowanie środowiska wykonawczego hello działania, w szczególności, podczas przetwarzania wycinka hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-248">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="0e2e8-249">w poniższej tabeli Hello zawiera szczegóły hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-249">hello following table provides hello details.</span></span>

| <span data-ttu-id="0e2e8-250">Właściwość</span><span class="sxs-lookup"><span data-stu-id="0e2e8-250">Property</span></span> | <span data-ttu-id="0e2e8-251">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="0e2e8-251">Permitted values</span></span> | <span data-ttu-id="0e2e8-252">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="0e2e8-252">Default Value</span></span> | <span data-ttu-id="0e2e8-253">Opis</span><span class="sxs-lookup"><span data-stu-id="0e2e8-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0e2e8-254">Współbieżność</span><span class="sxs-lookup"><span data-stu-id="0e2e8-254">concurrency</span></span> |<span data-ttu-id="0e2e8-255">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="0e2e8-255">Integer</span></span> <br/><br/><span data-ttu-id="0e2e8-256">Wartość maksymalna: 10</span><span class="sxs-lookup"><span data-stu-id="0e2e8-256">Max value: 10</span></span> |<span data-ttu-id="0e2e8-257">1</span><span class="sxs-lookup"><span data-stu-id="0e2e8-257">1</span></span> |<span data-ttu-id="0e2e8-258">Liczba równoczesnych wykonaniami hello działania.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-258">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="0e2e8-259">Określa hello Liczba wykonań działania równoległego, które mogą wystąpić na różnych wycinków.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-259">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="0e2e8-260">Na przykład jeśli działanie wymaga toogo za pośrednictwem duży zbiór dostępnych danych o większej wartości współbieżności przyspiesza hello przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-260">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="0e2e8-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="0e2e8-261">executionPriorityOrder</span></span> |<span data-ttu-id="0e2e8-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="0e2e8-262">NewestFirst</span></span><br/><br/><span data-ttu-id="0e2e8-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="0e2e8-263">OldestFirst</span></span> |<span data-ttu-id="0e2e8-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="0e2e8-264">OldestFirst</span></span> |<span data-ttu-id="0e2e8-265">Określa kolejność hello wycinki danych, które są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-265">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="0e2e8-266">Na przykład jeśli masz wycinków 2 (w toku co 4 godziny, a innym godzinie 5), a oba oczekują na wykonanie.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="0e2e8-267">Jeśli ustawisz hello executionPriorityOrder toobe NewestFirst wycinka hello godzinie 5 jest przetwarzana najpierw.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-267">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="0e2e8-268">Podobnie jeśli ustawisz hello executionPriorityORder toobe OldestFIrst wycinka hello godzinie 4 jest przetwarzany.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-268">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="0e2e8-269">retry</span><span class="sxs-lookup"><span data-stu-id="0e2e8-269">retry</span></span> |<span data-ttu-id="0e2e8-270">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="0e2e8-270">Integer</span></span><br/><br/><span data-ttu-id="0e2e8-271">Maksymalna wartość może być 10</span><span class="sxs-lookup"><span data-stu-id="0e2e8-271">Max value can be 10</span></span> |<span data-ttu-id="0e2e8-272">0</span><span class="sxs-lookup"><span data-stu-id="0e2e8-272">0</span></span> |<span data-ttu-id="0e2e8-273">Liczba ponownych prób przed hello przetwarzania danych dla wycinka hello jest oznaczona jako niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-273">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="0e2e8-274">Wykonania działania dla wycinka danych próba zostanie ponowiona się toohello określona liczba ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-274">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="0e2e8-275">Ponów próbę Hello odbywa się jak najszybciej po awarii hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-275">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="0e2e8-276">timeout</span><span class="sxs-lookup"><span data-stu-id="0e2e8-276">timeout</span></span> |<span data-ttu-id="0e2e8-277">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="0e2e8-277">TimeSpan</span></span> |<span data-ttu-id="0e2e8-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="0e2e8-278">00:00:00</span></span> |<span data-ttu-id="0e2e8-279">Limit czasu dla działania hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-279">Timeout for hello activity.</span></span> <span data-ttu-id="0e2e8-280">Przykład: 00:10:00 (oznacza limitu 10 minut)</span><span class="sxs-lookup"><span data-stu-id="0e2e8-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="0e2e8-281">Jeśli wartość nie została określona lub jest równa 0, limit czasu hello jest nieograniczony.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-281">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="0e2e8-282">Jeśli czas przetwarzania danych hello na wycinek przekracza wartość limitu czasu hello, anulowaniu i hello system próbuje tooretry hello przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-282">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="0e2e8-283">Witaj liczby ponownych prób zależy od hello ponawiania właściwości.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-283">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="0e2e8-284">W przypadku przekroczenia limitu czasu hello stan jest ustawiany tooTimedOut.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-284">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="0e2e8-285">Opóźnienie</span><span class="sxs-lookup"><span data-stu-id="0e2e8-285">delay</span></span> |<span data-ttu-id="0e2e8-286">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="0e2e8-286">TimeSpan</span></span> |<span data-ttu-id="0e2e8-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="0e2e8-287">00:00:00</span></span> |<span data-ttu-id="0e2e8-288">Określ opóźnienie hello przed rozpoczęciem przetwarzania danych powoduje uruchomienie wycinek hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-288">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="0e2e8-289">Hello wykonywania działań dotyczących wycinek danych jest uruchamiany po hello opóźnienie jest hello oczekiwany czas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-289">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="0e2e8-290">Przykład: 00:10:00 (oznacza opóźnienia w ciągu 10 minut)</span><span class="sxs-lookup"><span data-stu-id="0e2e8-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="0e2e8-291">Parametr longRetry</span><span class="sxs-lookup"><span data-stu-id="0e2e8-291">longRetry</span></span> |<span data-ttu-id="0e2e8-292">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="0e2e8-292">Integer</span></span><br/><br/><span data-ttu-id="0e2e8-293">Wartość maksymalna: 10</span><span class="sxs-lookup"><span data-stu-id="0e2e8-293">Max value: 10</span></span> |<span data-ttu-id="0e2e8-294">1</span><span class="sxs-lookup"><span data-stu-id="0e2e8-294">1</span></span> |<span data-ttu-id="0e2e8-295">Witaj liczbę długi ponownych prób przed hello wycinek wykonanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-295">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="0e2e8-296">Parametr longRetry prób uzyskają przez longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="0e2e8-297">Dlatego toospecify czas między ponownymi próbami, należy użyć longRetry.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-297">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="0e2e8-298">Jeśli został określony zarówno longRetry, jak i ponów próbę, każdej próbie longRetry zawiera ponownych prób i hello maksymalną liczbę prób ponawiania * longRetry.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="0e2e8-299">Na przykład, jeśli mamy hello następujące ustawienia zasad działania hello:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-299">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="0e2e8-300">Spróbuj ponownie: 3</span><span class="sxs-lookup"><span data-stu-id="0e2e8-300">Retry: 3</span></span><br/><span data-ttu-id="0e2e8-301">Parametr longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="0e2e8-301">longRetry: 2</span></span><br/><span data-ttu-id="0e2e8-302">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="0e2e8-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="0e2e8-303">Załóżmy istnieje tylko jeden wycinek tooexecute (oczekiwanie stanu) i wykonania działania hello zawsze kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-303">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="0e2e8-304">Początkowo może być 3 wykonywanie kolejnych prób.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="0e2e8-305">Po każdej próbie stanu wycinka hello byłoby ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-305">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="0e2e8-306">Po pierwsze 3 prób się za pośrednictwem stanu wycinka hello będą LongRetry.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-306">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="0e2e8-307">Po upływie godziny (to znaczy wartość longRetryInteval w) będzie inny zestaw 3 wykonywanie kolejnych prób.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="0e2e8-308">Po utworzeniu tego stanu wycinka hello będzie można i będą podejmowane próby.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-308">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="0e2e8-309">Dlatego całkowity 6 podejmowano.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="0e2e8-310">Jeśli wykonanie żadnych zakończy się powodzeniem, stan wycinek hello będzie gotowy i są podjęto próby.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-310">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="0e2e8-311">Parametr longRetry mogą być używane w sytuacji, w których danych zależnych dociera deterministyczna razy lub hello ogólnej środowiska jest niestabilnym, w których przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="0e2e8-312">W takich przypadkach podczas ponownych prób po kolei nie mogą pomóc w i w ten sposób po upływie interwału czasu powoduje hello potrzebne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="0e2e8-313">Word Przestroga: nie należy ustawiać wysokiej wartości longRetry lub longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="0e2e8-314">Zazwyczaj wyższej wartości oznacza innych kwestii systemowych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="0e2e8-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="0e2e8-315">longRetryInterval</span></span> |<span data-ttu-id="0e2e8-316">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="0e2e8-316">TimeSpan</span></span> |<span data-ttu-id="0e2e8-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="0e2e8-317">00:00:00</span></span> |<span data-ttu-id="0e2e8-318">Witaj opóźnienie między próbami czas ponów</span><span class="sxs-lookup"><span data-stu-id="0e2e8-318">hello delay between long retry attempts</span></span> |

<span data-ttu-id="0e2e8-319">Aby uzyskać więcej informacji, zobacz [potoki](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="0e2e8-320">Równoległe przetwarzanie wycinków danych</span><span class="sxs-lookup"><span data-stu-id="0e2e8-320">Parallel processing of data slices</span></span>
<span data-ttu-id="0e2e8-321">W przeszłości hello można ustawić hello datę rozpoczęcia dla potoku hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-321">You can set hello start date for hello pipeline in hello past.</span></span> <span data-ttu-id="0e2e8-322">Po wykonaniu tej fabryki danych automatycznie oblicza wszystkie fragmenty danych w przeszłości hello (wypełnienia tyłu) i rozpoczyna przetwarzanie je.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-322">When you do so, Data Factory automatically calculates (back fills) all data slices in hello past and begins processing them.</span></span> <span data-ttu-id="0e2e8-323">Na przykład: Jeśli utworzyć potok z datą rozpoczęcia 2017-04-01 i hello jest data bieżąca 2017-04-10.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-323">For example: if you create a pipeline with start date 2017-04-01 and hello current date is 2017-04-10.</span></span> <span data-ttu-id="0e2e8-324">Jeśli okresach hello z hello produkt wyjściowy zestaw danych jest codziennie, a następnie uruchamia fabryki danych przetwarzania wszystkie fragmenty hello z 2017-04-01 too2017-04-09 natychmiast, ponieważ data rozpoczęcia hello jest w przeszłości hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-324">If hello cadence of hello output dataset is daily, then Data Factory starts processing all hello slices from 2017-04-01 too2017-04-09 immediately because hello start date is in hello past.</span></span> <span data-ttu-id="0e2e8-325">wycinek Hello 2017-04-10 nie został przetworzony jeszcze ponieważ hello wartość właściwości stylu w sekcji dostępności hello jest EndOfInterval domyślnie.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-325">hello slice from 2017-04-10 is not processed yet because hello value of style property in hello availability section is EndOfInterval by default.</span></span> <span data-ttu-id="0e2e8-326">Witaj najstarsze wycinek jest przetwarzany najpierw jako domyślny hello wartość executionPriorityOrder jest OldestFirst.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-326">hello oldest slice is processed first as hello default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="0e2e8-327">Opis właściwości stylu hello, zobacz [dostępności zestawu danych](#dataset-availability) sekcji.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-327">For a description of hello style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="0e2e8-328">Opis sekcji executionPriorityOrder hello, zobacz hello [zasady dotyczące działań](#activity-policies) sekcji.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-328">For a description of hello executionPriorityOrder section, see hello [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="0e2e8-329">Można skonfigurować toobe wycinki danych wypełnione wstecz przetwarzane równolegle przez ustawienie hello **współbieżności** właściwości w hello **zasad** sekcji hello działania w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-329">You can configure back-filled data slices toobe processed in parallel by setting hello **concurrency** property in hello **policy** section of hello activity JSON.</span></span> <span data-ttu-id="0e2e8-330">Ta właściwość określa hello Liczba wykonań działania równoległego, które mogą wystąpić na różnych wycinków.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-330">This property determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="0e2e8-331">Wartość domyślna Hello hello współbieżności właściwości to 1.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-331">hello default value for hello concurrency property is 1.</span></span> <span data-ttu-id="0e2e8-332">W związku z tym jeden wycinek jest przetwarzany w czasie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="0e2e8-333">Witaj, wartość maksymalna wynosi 10.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-333">hello maximum value is 10.</span></span> <span data-ttu-id="0e2e8-334">Gdy potoku potrzebuje toogo za pośrednictwem duży zbiór dostępnych danych o większej wartości współbieżności przyspiesza hello przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-334">When a pipeline needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="0e2e8-335">Uruchom ponownie wycinek danych nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="0e2e8-335">Rerun a failed data slice</span></span>
<span data-ttu-id="0e2e8-336">Gdy wystąpi błąd podczas przetwarzania wycinka danych, można ustalić przyczyny niepowodzenia przetwarzania hello wycinek przy użyciu bloków portalu Azure lub monitora i zarządzania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-336">When an error occurs while processing a data slice, you can find out why hello processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="0e2e8-337">Zobacz [monitorowania i zarządzania nimi przy użyciu bloków portalu Azure potoki](data-factory-monitor-manage-pipelines.md) lub [zarządzania i monitorowania aplikacji](data-factory-monitor-manage-app.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="0e2e8-338">Należy wziąć pod uwagę hello poniższy przykład, który zawiera dwa działania.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-338">Consider hello following example, which shows two activities.</span></span> <span data-ttu-id="0e2e8-339">Działania Activity1 i działania 2.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="0e2e8-340">Działania Activity1 zużywa fragment Dataset1 i tworzy wycinek Dataset2, które jest używane jako dane wejściowe przez tooproduce Activity2 wycinek hello ostatecznego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 tooproduce a slice of hello Final Dataset.</span></span>

![Wycinek nie powiodło się](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="0e2e8-342">Hello diagram wskazuje, że poza trzech ostatnich wycinków, wystąpił wycinek 9 10 AM hello produkujących awarii dla Dataset2.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-342">hello diagram shows that out of three recent slices, there was a failure producing hello 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="0e2e8-343">Fabryka danych automatycznie śledzi zależności zestawu hello czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-343">Data Factory automatically tracks dependency for hello time series dataset.</span></span> <span data-ttu-id="0e2e8-344">W związku z tym nie rozpoczyna działania hello uruchamiania dla wycinka niższego rzędu 9 10 AM hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-344">As a result, it does not start hello activity run for hello 9-10 AM downstream slice.</span></span>

<span data-ttu-id="0e2e8-345">Narzędzia zarządzania i monitorowania fabryki danych pozwala toodrill do dzienników diagnostycznych hello hello wycinka nie powiodło się tooeasily Znajdź hello głównego spowodować hello problemu i rozwiąż problem.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-345">Data Factory monitoring and management tools allow you toodrill into hello diagnostic logs for hello failed slice tooeasily find hello root cause for hello issue and fix it.</span></span> <span data-ttu-id="0e2e8-346">Po hello problem został rozwiązany, można łatwo uruchomić uruchamiania nie powiodło się wycinek hello tooproduce hello działania.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-346">After you have fixed hello issue, you can easily start hello activity run tooproduce hello failed slice.</span></span> <span data-ttu-id="0e2e8-347">Aby uzyskać więcej informacji na temat toorerun i zrozumienie stanu przejścia wycinki danych, zobacz [monitorowania i zarządzania nimi przy użyciu bloków portalu Azure potoki](data-factory-monitor-manage-pipelines.md) lub [zarządzania i monitorowania aplikacji](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-347">For more information on how toorerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="0e2e8-348">Po ponownym uruchomieniu hello 9 10 AM slice dla **Dataset2**, fabryki danych uruchamia hello uruchamiania dla wycinka zależnych 9 10 AM hello na powitania ostatecznego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-348">After you rerun hello 9-10 AM slice for **Dataset2**, Data Factory starts hello run for hello 9-10 AM dependent slice on hello final dataset.</span></span>

![Uruchom ponownie wycinka nie powiodło się](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="0e2e8-350">Wiele działań w potoku</span><span class="sxs-lookup"><span data-stu-id="0e2e8-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="0e2e8-351">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="0e2e8-352">Jeśli masz wiele działań w potoku i hello dane wyjściowe działania nie jest wejściem innego działania, hello działania mogą działać równolegle, jeśli wycinki danych wejściowych dla działań hello jest gotowe.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-352">If you have multiple activities in a pipeline and hello output of an activity is not an input of another activity, hello activities may run in parallel if input data slices for hello activities are ready.</span></span>

<span data-ttu-id="0e2e8-353">Powiązane z dwóch działań (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-353">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="0e2e8-354">działania Hello może znajdować się w hello potoku tego samego lub w innej potoków.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-354">hello activities can be in hello same pipeline or in different pipelines.</span></span> <span data-ttu-id="0e2e8-355">działanie drugi Hello wykonuje tylko wtedy, gdy hello najpierw jeden zakończy działanie pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-355">hello second activity executes only when hello first one finishes successfully.</span></span>

<span data-ttu-id="0e2e8-356">Rozważmy na przykład hello następującego przypadku, gdy potoku ma dwa działania:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-356">For example, consider hello following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="0e2e8-357">A1 działania, który wymaga zewnętrzny zestaw danych wejściowych D1 i tworzy wyjściowy zestaw danych D2.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="0e2e8-358">A2 działania, która wymaga danych wejściowych z zestawu danych D2 i tworzy wyjściowy zestaw danych D3.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="0e2e8-359">W tym scenariuszu działania A1 i A2 są w hello sam potoku.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-359">In this scenario, activities A1 and A2 are in hello same pipeline.</span></span> <span data-ttu-id="0e2e8-360">Witaj działanie, które A1 jest uruchamiany, gdy dane zewnętrzne hello jest dostępny i częstotliwość dostępności hello zaplanowane zostanie osiągnięty.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-360">hello activity A1 runs when hello external data is available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="0e2e8-361">Witaj działania A2 uruchamiane po hello zaplanowane wycinków z D2 staną się dostępne i hello częstotliwość zaplanowana dostępność zostanie osiągnięty.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-361">hello activity A2 runs when hello scheduled slices from D2 become available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="0e2e8-362">W przypadku błędu w jednym z wycinków hello w zestawie danych D2, A2 nie działa dla tego wycinka, dopóki nie będzie dostępny.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-362">If there is an error in one of hello slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="0e2e8-363">Witaj widoku diagramu z obu działaniami w hello się, że tego samego potoku będzie wyglądała powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-363">hello Diagram view with both activities in hello same pipeline would look like hello following diagram:</span></span>

![Tworzenie łańcuchów działań w hello sam potoku](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="0e2e8-365">Jak wspomniano wcześniej, hello działania może być w różnych potoków.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-365">As mentioned earlier, hello activities could be in different pipelines.</span></span> <span data-ttu-id="0e2e8-366">W takiej sytuacji widoku diagramu hello będzie wyglądać powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-366">In such a scenario, hello diagram view would look like hello following diagram:</span></span>

![Tworzenie łańcuchów działań w dwóch potoki](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="0e2e8-368">Zobacz hello [skopiuj sekwencyjnie](#copy-sequentially) sekcji w dodatku hello przykład.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-368">See hello [copy sequentially](#copy-sequentially) section in hello appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="0e2e8-369">Zestawy danych modelu z różnych częstotliwości</span><span class="sxs-lookup"><span data-stu-id="0e2e8-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="0e2e8-370">W próbkach hello zostały hello tej samej częstotliwości hello wejściowych i wyjściowych zestawów danych i hello działania harmonogram okna.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-370">In hello samples, hello frequencies for input and output datasets and hello activity schedule window were hello same.</span></span> <span data-ttu-id="0e2e8-371">W niektórych scenariuszach wymagane hello możliwości tooproduce wyjście z częstotliwością od częstotliwości hello jeden lub więcej składników.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-371">Some scenarios require hello ability tooproduce output at a frequency different than hello frequencies of one or more inputs.</span></span> <span data-ttu-id="0e2e8-372">Fabryka danych obsługuje modelowania tych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="0e2e8-373">Przykład 1: Tworzy codzienne raportu wyjściowego dla danych wejściowych, który jest dostępny co godzinę</span><span class="sxs-lookup"><span data-stu-id="0e2e8-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="0e2e8-374">Rozważmy scenariusz, w którym możesz mieć pomiaru dane wejściowe z czujników dostępne co godzinę w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="0e2e8-375">Chcesz tooproduce codzienne agregacji raport o statystyk, takich jak średnią, minimalną i maksymalną dla dzień hello przy [działania hive fabryki danych](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-375">You want tooproduce a daily aggregate report with statistics such as mean, maximum, and minimum for hello day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="0e2e8-376">Oto, jak można model ten scenariusz przy użyciu fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="0e2e8-377">**Wejściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="0e2e8-377">**Input dataset**</span></span>

<span data-ttu-id="0e2e8-378">Witaj wejściowej co godzinę pliki są usuwane w folderze hello hello danego dnia.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-378">hello hourly input files are dropped in hello folder for hello given day.</span></span> <span data-ttu-id="0e2e8-379">Dostępność dla danych wejściowych jest ustawiona na **godzina** (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="0e2e8-380">**Wyjściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="0e2e8-380">**Output dataset**</span></span>

<span data-ttu-id="0e2e8-381">Jeden plik wyjściowy jest tworzony codziennie w folderze hello dnia.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-381">One output file is created every day in hello day's folder.</span></span> <span data-ttu-id="0e2e8-382">Dostępność danych wyjściowych jest ustawiona na **dzień** (częstotliwość: dzień i interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="0e2e8-383">**Działania: działania w potoku hive**</span><span class="sxs-lookup"><span data-stu-id="0e2e8-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="0e2e8-384">skryptu hive Hello odbiera hello odpowiednie *DateTime* informacji jako parametry, które używają hello **WindowStart** zmiennej, jak pokazano w hello następującego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-384">hello hive script receives hello appropriate *DateTime* information as parameters that use hello **WindowStart** variable as shown in hello following snippet.</span></span> <span data-ttu-id="0e2e8-385">skryptu hive Hello używa tych danych hello tooload zmiennej z hello poprawnego folderu dzień hello i uruchom hello agregacji toogenerate hello w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-385">hello hive script uses this variable tooload hello data from hello correct folder for hello day and run hello aggregation toogenerate hello output.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
            "inputs": [
                {
                    "name": "AzureBlobInput"
                }
            ],
            "outputs": [
                {
                    "name": "AzureBlobOutput"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

<span data-ttu-id="0e2e8-386">Witaj Poniższy diagram przedstawia hello scenariusza z punktu widzenia zależności danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-386">hello following diagram shows hello scenario from a data-dependency point of view.</span></span>

![Zależności danych](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="0e2e8-388">Witaj wycinek danych wyjściowych dla każdego dnia zależy od 24 wycinków co godzinę z zestawem danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-388">hello output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="0e2e8-389">Te zależności automatycznie z nazwami hello wycinki danych wejściowych, które wchodzą w hello oblicza fabryki danych sam okres czasu jako hello wyprodukowanych toobe wycinek danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-389">Data Factory computes these dependencies automatically by figuring out hello input data slices that fall in hello same time period as hello output slice toobe produced.</span></span> <span data-ttu-id="0e2e8-390">Jeśli żadnego hello 24 wycinków wejściowych nie jest dostępna, fabryki danych oczekuje na toobe wejściowych wycinek hello gotowe przed rozpoczęciem hello codziennego uruchamiania działania.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-390">If any of hello 24 input slices is not available, Data Factory waits for hello input slice toobe ready before starting hello daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="0e2e8-391">Przykład 2: Określ zależności z wyrażeń i funkcji usługi fabryka danych</span><span class="sxs-lookup"><span data-stu-id="0e2e8-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="0e2e8-392">Teraz Rozważmy scenariusz, w innym.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-392">Let’s consider another scenario.</span></span> <span data-ttu-id="0e2e8-393">Załóżmy, że masz działania hive, która przetwarza dwóch zestawów danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="0e2e8-394">Jeden z nich ma codziennie nowe dane, ale jeden z nich pobiera nowe dane co tydzień.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="0e2e8-395">Załóżmy, że żądana toodo sprzężenia między hello dwóch parametrów wejściowych i utworzenie danych wyjściowych każdego dnia.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-395">Suppose you wanted toodo a join across hello two inputs and produce an output every day.</span></span>

<span data-ttu-id="0e2e8-396">podejście proste Hello, w którym fabryka danych automatycznie danych liczbowych limit hello dane wejściowe wycinków tooprocess ustawiając wyjściowych toohello okresu nie działa czasowym wycinka danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-396">hello simple approach in which Data Factory automatically figures out hello right input slices tooprocess by aligning toohello output data slice’s time period does not work.</span></span>

<span data-ttu-id="0e2e8-397">Należy określić, że każde działanie Uruchom hello fabryki danych należy używać wycinek danych ostatniego tygodnia dla zestawu danych wejściowych co tydzień hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-397">You must specify that for every activity run, hello Data Factory should use last week’s data slice for hello weekly input dataset.</span></span> <span data-ttu-id="0e2e8-398">Korzystania z funkcji usługi fabryka danych Azure, jak pokazano w powitania po tooimplement fragment to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-398">You use Azure Data Factory functions as shown in hello following snippet tooimplement this behavior.</span></span>

<span data-ttu-id="0e2e8-399">**Input1: Obiektów blob platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="0e2e8-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="0e2e8-400">Witaj pierwsze dane wejściowe, jest hello obiektów blob platformy Azure są aktualizowane codziennie.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-400">hello first input is hello Azure blob being updated daily.</span></span>

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="0e2e8-401">**Input2: Obiektów blob platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="0e2e8-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="0e2e8-402">Input2 jest hello Azure blob aktualizowana co tydzień.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-402">Input2 is hello Azure blob being updated weekly.</span></span>

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

<span data-ttu-id="0e2e8-403">**Dane wyjściowe: Obiektów blob platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="0e2e8-403">**Output: Azure blob**</span></span>

<span data-ttu-id="0e2e8-404">Jeden plik wyjściowy jest tworzony codziennie w folderze hello hello dzień.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-404">One output file is created every day in hello folder for hello day.</span></span> <span data-ttu-id="0e2e8-405">Dostępność danych wyjściowych jest ustawiona zbyt**dzień** (częstotliwość: dzień, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="0e2e8-405">Availability of output is set too**day** (frequency: Day, interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="0e2e8-406">**Działania: działania w potoku hive**</span><span class="sxs-lookup"><span data-stu-id="0e2e8-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="0e2e8-407">działanie hive Hello przyjmuje hello dwóch parametrów wejściowych i tworzy wycinek danych wyjściowych każdego dnia.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-407">hello hive activity takes hello two inputs and produces an output slice every day.</span></span> <span data-ttu-id="0e2e8-408">Można określić toodepend wycinka dane wyjściowe każdego dnia na hello wycinek wejściowych poprzedniego tygodnia dla danych wejściowych co tydzień w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-408">You can specify every day’s output slice toodepend on hello previous week’s input slice for weekly input as follows.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

<span data-ttu-id="0e2e8-409">Zobacz [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md) listę funkcje i zmienne systemu, które obsługuje fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="0e2e8-410">Dodatek</span><span class="sxs-lookup"><span data-stu-id="0e2e8-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="0e2e8-411">Przykład: kopiowanie sekwencyjnie</span><span class="sxs-lookup"><span data-stu-id="0e2e8-411">Example: copy sequentially</span></span>
<span data-ttu-id="0e2e8-412">Jego jest możliwe toorun wiele operacji kopiowania po kolei w sposób sekwencyjnych/uporządkowane.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-412">It is possible toorun multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="0e2e8-413">Na przykład może mieć dwóch kopii działań w potoku (CopyActivity1 i CopyActivity2) z hello następujące dane wejściowe dane wyjściowe zestawy danych:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with hello following input data output datasets:</span></span>   

<span data-ttu-id="0e2e8-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="0e2e8-414">CopyActivity1</span></span>

<span data-ttu-id="0e2e8-415">Dane wejściowe: zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-415">Input: Dataset.</span></span> <span data-ttu-id="0e2e8-416">Dane wyjściowe: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-416">Output: Dataset2.</span></span>

<span data-ttu-id="0e2e8-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="0e2e8-417">CopyActivity2</span></span>

<span data-ttu-id="0e2e8-418">Dane wejściowe: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-418">Input: Dataset2.</span></span>  <span data-ttu-id="0e2e8-419">Dane wyjściowe: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-419">Output: Dataset3.</span></span>

<span data-ttu-id="0e2e8-420">CopyActivity2 może działać tylko wtedy, gdy hello CopyActivity1 zostało uruchomione pomyślnie i Dataset2 jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-420">CopyActivity2 would run only if hello CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="0e2e8-421">Oto kod JSON potoku próbki hello:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-421">Here is hello sample pipeline JSON:</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="0e2e8-422">Zwróć uwagę, że w przykładzie hello hello wyjściowego zestawu danych hello pierwsze działanie kopiowania (Dataset2) został określony jako danych wejściowych dla drugiego działania hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-422">Notice that in hello example, hello output dataset of hello first copy activity (Dataset2) is specified as input for hello second activity.</span></span> <span data-ttu-id="0e2e8-423">W związku z tym hello działania drugi działa tylko wtedy, gdy hello wyjściowy zestaw danych z pierwsze działanie hello jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-423">Therefore, hello second activity runs only when hello output dataset from hello first activity is ready.</span></span>  

<span data-ttu-id="0e2e8-424">Przykład Witaj CopyActivity2 może mieć inne dane, takie jak Dataset3, ale Dataset2 można określić jako tooCopyActivity2 wejściowych, więc nie można uruchomić działanie hello zakończenie CopyActivity1.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-424">In hello example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input tooCopyActivity2, so hello activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="0e2e8-425">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-425">For example:</span></span>

<span data-ttu-id="0e2e8-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="0e2e8-426">CopyActivity1</span></span>

<span data-ttu-id="0e2e8-427">Dane wejściowe: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-427">Input: Dataset1.</span></span> <span data-ttu-id="0e2e8-428">Dane wyjściowe: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-428">Output: Dataset2.</span></span>

<span data-ttu-id="0e2e8-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="0e2e8-429">CopyActivity2</span></span>

<span data-ttu-id="0e2e8-430">Dane wejściowe: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="0e2e8-431">Dane wyjściowe: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-431">Output: Dataset4.</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="0e2e8-432">Zwróć uwagę, że w przykładzie hello dwóch zestawów danych wejściowych są określone dla aktywności kopiowania drugi hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-432">Notice that in hello example, two input datasets are specified for hello second copy activity.</span></span> <span data-ttu-id="0e2e8-433">Jeśli określono wielu danych wejściowych, tylko hello pierwszego wejściowego zestawu danych służy do kopiowania danych, ale inne zestawy danych są używane jako zależności.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-433">When multiple inputs are specified, only hello first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="0e2e8-434">CopyActivity2 zaczyna się dopiero po hello są spełnione następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="0e2e8-434">CopyActivity2 would start only after hello following conditions are met:</span></span>

* <span data-ttu-id="0e2e8-435">Pomyślnie ukończono CopyActivity1 i Dataset2 jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="0e2e8-436">Ten zestaw danych nie jest używany podczas kopiowania tooDataset4 danych.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-436">This dataset is not used when copying data tooDataset4.</span></span> <span data-ttu-id="0e2e8-437">Tylko działa jako zależność planowania dla CopyActivity2.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="0e2e8-438">Dataset3 jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-438">Dataset3 is available.</span></span> <span data-ttu-id="0e2e8-439">Ten zestaw danych reprezentuje dane hello, który jest skopiowany toohello docelowym.</span><span class="sxs-lookup"><span data-stu-id="0e2e8-439">This dataset represents hello data that is copied toohello destination.</span></span> 
