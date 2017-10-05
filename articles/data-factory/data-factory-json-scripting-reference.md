---
title: "Fabryki danych Azure - JSON skryptów odwołania | Dokumentacja firmy Microsoft"
description: "Udostępnia schematów JSON dla jednostek fabryki danych."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 805106c0a5cdbff1f143f22a2ae59f6d2a0bf126
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="38fe0-103">Fabryki danych Azure - JSON skryptów odwołania</span><span class="sxs-lookup"><span data-stu-id="38fe0-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="38fe0-104">Ten artykuł zawiera przykłady i schematów JSON do definiowania jednostek fabryki danych Azure (potoku, działania, zestawu danych i połączonej usługi).</span><span class="sxs-lookup"><span data-stu-id="38fe0-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="38fe0-105">Potok</span><span class="sxs-lookup"><span data-stu-id="38fe0-105">Pipeline</span></span> 
<span data-ttu-id="38fe0-106">Struktura wysokiego poziomu definicji potoku jest następujący:</span><span class="sxs-lookup"><span data-stu-id="38fe0-106">The high-level structure for a pipeline definition is as follows:</span></span> 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="38fe0-107">Poniższa tabela zwiera opis właściwości w potoku definicji JSON:</span><span class="sxs-lookup"><span data-stu-id="38fe0-107">Following table describes the properties within the pipeline JSON definition:</span></span>

| <span data-ttu-id="38fe0-108">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-108">Property</span></span> | <span data-ttu-id="38fe0-109">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-109">Description</span></span> | <span data-ttu-id="38fe0-110">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="38fe0-111">name</span><span class="sxs-lookup"><span data-stu-id="38fe0-111">name</span></span> | <span data-ttu-id="38fe0-112">Nazwa potoku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-112">Name of the pipeline.</span></span> <span data-ttu-id="38fe0-113">Określ nazwę, która reprezentuje akcję że działania lub potoku jest skonfigurowany</span><span class="sxs-lookup"><span data-stu-id="38fe0-113">Specify a name that represents the action that the activity or pipeline is configured to do</span></span><br/><ul><li><span data-ttu-id="38fe0-114">Maksymalna liczba znaków: 260</span><span class="sxs-lookup"><span data-stu-id="38fe0-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="38fe0-115">Musi rozpoczynać się od numeru litery lub znaku podkreślenia (_)</span><span class="sxs-lookup"><span data-stu-id="38fe0-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="38fe0-116">Następujące znaki nie są dozwolone: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</span><span class="sxs-lookup"><span data-stu-id="38fe0-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="38fe0-117">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-117">Yes</span></span> |
| <span data-ttu-id="38fe0-118">Opis elementu</span><span class="sxs-lookup"><span data-stu-id="38fe0-118">description</span></span> |<span data-ttu-id="38fe0-119">Tekst opisujący działania lub potoku do czego służy</span><span class="sxs-lookup"><span data-stu-id="38fe0-119">Text describing what the activity or pipeline is used for</span></span> | <span data-ttu-id="38fe0-120">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-120">No</span></span> |
| <span data-ttu-id="38fe0-121">działania</span><span class="sxs-lookup"><span data-stu-id="38fe0-121">activities</span></span> | <span data-ttu-id="38fe0-122">Zawiera listę działań.</span><span class="sxs-lookup"><span data-stu-id="38fe0-122">Contains a list of activities.</span></span> | <span data-ttu-id="38fe0-123">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-123">Yes</span></span> |
| <span data-ttu-id="38fe0-124">rozpoczynanie</span><span class="sxs-lookup"><span data-stu-id="38fe0-124">start</span></span> |<span data-ttu-id="38fe0-125">Data i godzina rozpoczęcia dla potoku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-125">Start date-time for the pipeline.</span></span> <span data-ttu-id="38fe0-126">Musi być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="38fe0-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="38fe0-127">Na przykład: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="38fe0-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="38fe0-128">Użytkownik może określić czas lokalny, na przykład czas EST.</span><span class="sxs-lookup"><span data-stu-id="38fe0-128">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="38fe0-129">Oto przykład: `2016-02-27T06:00:00**-05:00`, która jest szacowana AM 6</span><span class="sxs-lookup"><span data-stu-id="38fe0-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="38fe0-130">Właściwości początkową i końcową razem Określ aktywny okres potoku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-130">The start and end properties together specify active period for the pipeline.</span></span> <span data-ttu-id="38fe0-131">Wycinki danych wyjściowych tylko są tworzone z aktywny okres.</span><span class="sxs-lookup"><span data-stu-id="38fe0-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="38fe0-132">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-132">No</span></span><br/><br/><span data-ttu-id="38fe0-133">Jeśli określono wartość dla właściwości końca, należy określić wartość dla właściwości rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-133">If you specify a value for the end property, you must specify value for the start property.</span></span><br/><br/><span data-ttu-id="38fe0-134">Godziny rozpoczęcia i zakończenia może jednocześnie być puste, aby utworzyć potok.</span><span class="sxs-lookup"><span data-stu-id="38fe0-134">The start and end times can both be empty to create a pipeline.</span></span> <span data-ttu-id="38fe0-135">Należy określić zarówno wartości można ustawić okresu aktywności w potoku do uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-135">You must specify both values to set an active period for the pipeline to run.</span></span> <span data-ttu-id="38fe0-136">Jeśli nie określono godziny rozpoczęcia i zakończenia podczas tworzenia potoku, można ustawić ich później za pomocą polecenia cmdlet Set-AzureRmDataFactoryPipelineActivePeriod.</span><span class="sxs-lookup"><span data-stu-id="38fe0-136">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="38fe0-137">Koniec</span><span class="sxs-lookup"><span data-stu-id="38fe0-137">end</span></span> |<span data-ttu-id="38fe0-138">Data czas zakończenia dla potoku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-138">End date-time for the pipeline.</span></span> <span data-ttu-id="38fe0-139">Jeśli zostanie określona, musi być w formacie ISO.</span><span class="sxs-lookup"><span data-stu-id="38fe0-139">If specified must be in ISO format.</span></span> <span data-ttu-id="38fe0-140">Na przykład: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="38fe0-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="38fe0-141">Użytkownik może określić czas lokalny, na przykład czas EST.</span><span class="sxs-lookup"><span data-stu-id="38fe0-141">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="38fe0-142">Oto przykład: `2016-02-27T06:00:00**-05:00`, która jest szacowana AM 6</span><span class="sxs-lookup"><span data-stu-id="38fe0-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="38fe0-143">Aby działają przez nieograniczony czas potoku, należy określić 9999-09-09 jako wartość właściwości end.</span><span class="sxs-lookup"><span data-stu-id="38fe0-143">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span></span> |<span data-ttu-id="38fe0-144">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-144">No</span></span> <br/><br/><span data-ttu-id="38fe0-145">Jeśli określono wartość dla właściwości rozpoczęcia, należy określić wartość dla właściwości end.</span><span class="sxs-lookup"><span data-stu-id="38fe0-145">If you specify a value for the start property, you must specify value for the end property.</span></span><br/><br/><span data-ttu-id="38fe0-146">Zobacz uwagi dla **start** właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-146">See notes for the **start** property.</span></span> |
| <span data-ttu-id="38fe0-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="38fe0-147">isPaused</span></span> |<span data-ttu-id="38fe0-148">Jeśli ma wartość true potoku nie działa.</span><span class="sxs-lookup"><span data-stu-id="38fe0-148">If set to true the pipeline does not run.</span></span> <span data-ttu-id="38fe0-149">Wartość domyślna = false.</span><span class="sxs-lookup"><span data-stu-id="38fe0-149">Default value = false.</span></span> <span data-ttu-id="38fe0-150">Ta właściwość umożliwia włączanie lub wyłączanie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-150">You can use this property to enable or disable.</span></span> |<span data-ttu-id="38fe0-151">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-151">No</span></span> |
| <span data-ttu-id="38fe0-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="38fe0-152">pipelineMode</span></span> |<span data-ttu-id="38fe0-153">Metoda planowania działa dla potoku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-153">The method for scheduling runs for the pipeline.</span></span> <span data-ttu-id="38fe0-154">Dozwolone wartości to: (domyślnie), zaplanowane jednorazowe.</span><span class="sxs-lookup"><span data-stu-id="38fe0-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="38fe0-155">"Zaplanowana" wskazuje, że potoku jest uruchamiane w określonych odstępach czasu zgodnie z jego aktywny okres (czas rozpoczęcia i zakończenia).</span><span class="sxs-lookup"><span data-stu-id="38fe0-155">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span></span> <span data-ttu-id="38fe0-156">"Jednorazowe" wskazuje, że potoku jest uruchamiana tylko raz.</span><span class="sxs-lookup"><span data-stu-id="38fe0-156">‘Onetime’ indicates that the pipeline runs only once.</span></span> <span data-ttu-id="38fe0-157">Potoki jednorazowe utworzonej nie może być zmodyfikowany zaktualizowane obecnie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="38fe0-158">Zobacz [potoku Onetime](data-factory-create-pipelines.md#onetime-pipeline) szczegółowe informacje o ustawienie jednorazowe.</span><span class="sxs-lookup"><span data-stu-id="38fe0-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="38fe0-159">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-159">No</span></span> |
| <span data-ttu-id="38fe0-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="38fe0-160">expirationTime</span></span> |<span data-ttu-id="38fe0-161">Czas po utworzeniu, dla którego potoku jest prawidłowy i powinny być zainicjowana.</span><span class="sxs-lookup"><span data-stu-id="38fe0-161">Duration of time after creation for which the pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="38fe0-162">Jeśli nie ma żadnych aktywnych nie powiodło się, lub do czasu działa, potoku zostanie usunięta automatycznie po osiągnięciu czas wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-162">If it does not have any active, failed, or pending runs, the pipeline is deleted automatically once it reaches the expiration time.</span></span> |<span data-ttu-id="38fe0-163">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="38fe0-164">Działanie</span><span class="sxs-lookup"><span data-stu-id="38fe0-164">Activity</span></span> 
<span data-ttu-id="38fe0-165">Struktura wysokiego poziomu do działania w potoku definicji (element działań) jest w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="38fe0-165">The high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

<span data-ttu-id="38fe0-166">Następujące tabeli opisano właściwości wewnątrz działania definicji JSON:</span><span class="sxs-lookup"><span data-stu-id="38fe0-166">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="38fe0-167">Tag</span><span class="sxs-lookup"><span data-stu-id="38fe0-167">Tag</span></span> | <span data-ttu-id="38fe0-168">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-168">Description</span></span> | <span data-ttu-id="38fe0-169">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-170">name</span><span class="sxs-lookup"><span data-stu-id="38fe0-170">name</span></span> |<span data-ttu-id="38fe0-171">Nazwa działania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-171">Name of the activity.</span></span> <span data-ttu-id="38fe0-172">Określ nazwę, która reprezentuje akcję skonfigurowaną działania</span><span class="sxs-lookup"><span data-stu-id="38fe0-172">Specify a name that represents the action that the activity is configured to do</span></span><br/><ul><li><span data-ttu-id="38fe0-173">Maksymalna liczba znaków: 260</span><span class="sxs-lookup"><span data-stu-id="38fe0-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="38fe0-174">Musi rozpoczynać się od numeru litery lub znaku podkreślenia (_)</span><span class="sxs-lookup"><span data-stu-id="38fe0-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="38fe0-175">Następujące znaki nie są dozwolone: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</span><span class="sxs-lookup"><span data-stu-id="38fe0-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="38fe0-176">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-176">Yes</span></span> |
| <span data-ttu-id="38fe0-177">Opis elementu</span><span class="sxs-lookup"><span data-stu-id="38fe0-177">description</span></span> |<span data-ttu-id="38fe0-178">Tekst opisujący działanie do czego służy.</span><span class="sxs-lookup"><span data-stu-id="38fe0-178">Text describing what the activity is used for.</span></span> |<span data-ttu-id="38fe0-179">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-179">Yes</span></span> |
| <span data-ttu-id="38fe0-180">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-180">type</span></span> |<span data-ttu-id="38fe0-181">Określa typ działania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-181">Specifies the type of the activity.</span></span> <span data-ttu-id="38fe0-182">Zobacz [MAGAZYNY danych](#data-stores) i [działań PRZEKSZTAŁCANIA danych](#data-transformation-activities) sekcje dla różnych typów działań.</span><span class="sxs-lookup"><span data-stu-id="38fe0-182">See the [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="38fe0-183">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-183">Yes</span></span> |
| <span data-ttu-id="38fe0-184">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="38fe0-184">inputs</span></span> |<span data-ttu-id="38fe0-185">Tabele wejściowe używane na potrzeby działania</span><span class="sxs-lookup"><span data-stu-id="38fe0-185">Input tables used by the activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="38fe0-186">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-186">Yes</span></span> |
| <span data-ttu-id="38fe0-187">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="38fe0-187">outputs</span></span> |<span data-ttu-id="38fe0-188">Tabele wyjściowe używany przez działanie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-188">Output tables used by the activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="38fe0-189">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-189">Yes</span></span> |
| <span data-ttu-id="38fe0-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="38fe0-190">linkedServiceName</span></span> |<span data-ttu-id="38fe0-191">Nazwa połączonej usługi używana przez działanie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-191">Name of the linked service used by the activity.</span></span> <br/><br/><span data-ttu-id="38fe0-192">Działanie może wymagać określenia połączonej usługi, który stanowi łącze do środowiska obliczeniowego wymagane.</span><span class="sxs-lookup"><span data-stu-id="38fe0-192">An activity may require that you specify the linked service that links to the required compute environment.</span></span> |<span data-ttu-id="38fe0-193">Tak, aby HDInsight działań, działania usługi Azure Machine Learning i działania dotyczącego procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="38fe0-194">Nie dla wszystkich innych</span><span class="sxs-lookup"><span data-stu-id="38fe0-194">No for all others</span></span> |
| <span data-ttu-id="38fe0-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="38fe0-195">typeProperties</span></span> |<span data-ttu-id="38fe0-196">Właściwości w sekcji typeProperties są zależne od typu działania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-196">Properties in the typeProperties section depend on type of the activity.</span></span> |<span data-ttu-id="38fe0-197">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-197">No</span></span> |
| <span data-ttu-id="38fe0-198">Zasady</span><span class="sxs-lookup"><span data-stu-id="38fe0-198">policy</span></span> |<span data-ttu-id="38fe0-199">Zasady, które mają wpływ na zachowanie czasu wykonania działania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-199">Policies that affect the run-time behavior of the activity.</span></span> <span data-ttu-id="38fe0-200">Jeśli nie zostanie określona, używane są zasady domyślne.</span><span class="sxs-lookup"><span data-stu-id="38fe0-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="38fe0-201">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-201">No</span></span> |
| <span data-ttu-id="38fe0-202">Harmonogram</span><span class="sxs-lookup"><span data-stu-id="38fe0-202">scheduler</span></span> |<span data-ttu-id="38fe0-203">Właściwość "harmonogramu" służy do definiowania żądanego planowania dla działania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-203">“scheduler” property is used to define desired scheduling for the activity.</span></span> <span data-ttu-id="38fe0-204">Właściwości podrzędnych są takie same jak te w [właściwości availability w zestawie danych](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="38fe0-204">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="38fe0-205">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="38fe0-206">Zasady</span><span class="sxs-lookup"><span data-stu-id="38fe0-206">Policies</span></span>
<span data-ttu-id="38fe0-207">Zasady wpływają na zachowanie czasu wykonania działania, w szczególności, podczas przetwarzania wycinka tabeli.</span><span class="sxs-lookup"><span data-stu-id="38fe0-207">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="38fe0-208">Poniższa tabela zawiera szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="38fe0-208">The following table provides the details.</span></span>

| <span data-ttu-id="38fe0-209">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-209">Property</span></span> | <span data-ttu-id="38fe0-210">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-210">Permitted values</span></span> | <span data-ttu-id="38fe0-211">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="38fe0-211">Default Value</span></span> | <span data-ttu-id="38fe0-212">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-213">Współbieżność</span><span class="sxs-lookup"><span data-stu-id="38fe0-213">concurrency</span></span> |<span data-ttu-id="38fe0-214">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="38fe0-214">Integer</span></span> <br/><br/><span data-ttu-id="38fe0-215">Wartość maksymalna: 10</span><span class="sxs-lookup"><span data-stu-id="38fe0-215">Max value: 10</span></span> |<span data-ttu-id="38fe0-216">1</span><span class="sxs-lookup"><span data-stu-id="38fe0-216">1</span></span> |<span data-ttu-id="38fe0-217">Liczba równoczesnych wykonania działania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-217">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="38fe0-218">Określa Liczba wykonań działania równoległego, które mogą wystąpić na różnych wycinków.</span><span class="sxs-lookup"><span data-stu-id="38fe0-218">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="38fe0-219">Na przykład jeśli działanie musi przechodzić przez duży zbiór dostępnych danych o większej wartości współbieżności przyspiesza przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-219">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="38fe0-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="38fe0-220">executionPriorityOrder</span></span> |<span data-ttu-id="38fe0-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="38fe0-221">NewestFirst</span></span><br/><br/><span data-ttu-id="38fe0-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="38fe0-222">OldestFirst</span></span> |<span data-ttu-id="38fe0-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="38fe0-223">OldestFirst</span></span> |<span data-ttu-id="38fe0-224">Określa kolejność wycinki danych, które są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="38fe0-224">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="38fe0-225">Na przykład jeśli masz wycinków 2 (w toku co 4 godziny, a innym godzinie 5), a oba oczekują na wykonanie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="38fe0-226">Jeśli ustawisz executionPriorityOrder jako NewestFirst wycinka godzinie 5 jest przetwarzana najpierw.</span><span class="sxs-lookup"><span data-stu-id="38fe0-226">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="38fe0-227">Podobnie jeśli ustawisz executionPriorityORder jako OldestFIrst wycinka godzinie 4 jest przetwarzany.</span><span class="sxs-lookup"><span data-stu-id="38fe0-227">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="38fe0-228">Spróbuj ponownie</span><span class="sxs-lookup"><span data-stu-id="38fe0-228">retry</span></span> |<span data-ttu-id="38fe0-229">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="38fe0-229">Integer</span></span><br/><br/><span data-ttu-id="38fe0-230">Maksymalna wartość może być 10</span><span class="sxs-lookup"><span data-stu-id="38fe0-230">Max value can be 10</span></span> |<span data-ttu-id="38fe0-231">0</span><span class="sxs-lookup"><span data-stu-id="38fe0-231">0</span></span> |<span data-ttu-id="38fe0-232">Liczba ponownych prób przed przetwarzania danych dla wycinka jest oznaczony jako błąd.</span><span class="sxs-lookup"><span data-stu-id="38fe0-232">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="38fe0-233">Do określonego ponownych próba zostanie ponowiona wykonania działania dla wycinka danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-233">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="38fe0-234">Ponów próbę odbywa się jak najszybciej po awarii.</span><span class="sxs-lookup"><span data-stu-id="38fe0-234">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="38fe0-235">Limit czasu</span><span class="sxs-lookup"><span data-stu-id="38fe0-235">timeout</span></span> |<span data-ttu-id="38fe0-236">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="38fe0-236">TimeSpan</span></span> |<span data-ttu-id="38fe0-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="38fe0-237">00:00:00</span></span> |<span data-ttu-id="38fe0-238">Limit czasu działania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-238">Timeout for the activity.</span></span> <span data-ttu-id="38fe0-239">Przykład: 00:10:00 (oznacza limitu 10 minut)</span><span class="sxs-lookup"><span data-stu-id="38fe0-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="38fe0-240">Jeśli wartość nie została określona lub jest równa 0, limit czasu to nieskończoność.</span><span class="sxs-lookup"><span data-stu-id="38fe0-240">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="38fe0-241">Jeśli czas przetwarzania danych na wycinek przekracza wartość limitu czasu, anulowaniu, a system podejmuje próbę przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-241">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="38fe0-242">Liczba ponownych prób zależy od właściwości ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="38fe0-242">The number of retries depends on the retry property.</span></span> <span data-ttu-id="38fe0-243">W przypadku przekroczenia limitu czasu stan jest ustawiony na upłynął limit czasu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-243">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="38fe0-244">Opóźnienie</span><span class="sxs-lookup"><span data-stu-id="38fe0-244">delay</span></span> |<span data-ttu-id="38fe0-245">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="38fe0-245">TimeSpan</span></span> |<span data-ttu-id="38fe0-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="38fe0-246">00:00:00</span></span> |<span data-ttu-id="38fe0-247">Określ opóźnienie przetwarzania danych powoduje uruchomienie wycinka.</span><span class="sxs-lookup"><span data-stu-id="38fe0-247">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="38fe0-248">Wykonanie działań dotyczących wycinek danych jest uruchomiona po opóźnienie oczekiwany czas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-248">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="38fe0-249">Przykład: 00:10:00 (oznacza opóźnienia w ciągu 10 minut)</span><span class="sxs-lookup"><span data-stu-id="38fe0-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="38fe0-250">Parametr longRetry</span><span class="sxs-lookup"><span data-stu-id="38fe0-250">longRetry</span></span> |<span data-ttu-id="38fe0-251">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="38fe0-251">Integer</span></span><br/><br/><span data-ttu-id="38fe0-252">Wartość maksymalna: 10</span><span class="sxs-lookup"><span data-stu-id="38fe0-252">Max value: 10</span></span> |<span data-ttu-id="38fe0-253">1</span><span class="sxs-lookup"><span data-stu-id="38fe0-253">1</span></span> |<span data-ttu-id="38fe0-254">Liczba długa ponownych prób przed wycinek wykonanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="38fe0-254">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="38fe0-255">Parametr longRetry prób uzyskają przez longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="38fe0-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="38fe0-256">Dlatego jeśli trzeba określić czas między ponownymi próbami, użyj longRetry.</span><span class="sxs-lookup"><span data-stu-id="38fe0-256">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="38fe0-257">Jeśli został określony zarówno longRetry, jak i ponów próbę, każdej próbie longRetry zawiera ponownych prób i maksymalną liczbę prób ponawiania * longRetry.</span><span class="sxs-lookup"><span data-stu-id="38fe0-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="38fe0-258">Na przykład, jeśli mamy poniższe ustawienia w zasadach działania:</span><span class="sxs-lookup"><span data-stu-id="38fe0-258">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="38fe0-259">Spróbuj ponownie: 3</span><span class="sxs-lookup"><span data-stu-id="38fe0-259">Retry: 3</span></span><br/><span data-ttu-id="38fe0-260">Parametr longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="38fe0-260">longRetry: 2</span></span><br/><span data-ttu-id="38fe0-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="38fe0-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="38fe0-262">Załóżmy istnieje tylko jeden wycinek do wykonania (oczekiwanie stanu) i wykonania działania zawsze kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="38fe0-262">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="38fe0-263">Początkowo może być 3 wykonywanie kolejnych prób.</span><span class="sxs-lookup"><span data-stu-id="38fe0-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="38fe0-264">Po każdej próbie stanu wycinka byłoby ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="38fe0-264">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="38fe0-265">Po pierwsze 3 prób się za pośrednictwem stanu wycinka będą LongRetry.</span><span class="sxs-lookup"><span data-stu-id="38fe0-265">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="38fe0-266">Po upływie godziny (to znaczy wartość longRetryInteval w) będzie inny zestaw 3 wykonywanie kolejnych prób.</span><span class="sxs-lookup"><span data-stu-id="38fe0-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="38fe0-267">Po wykonaniu tej nie będzie można stanu wycinka i będą podejmowane próby.</span><span class="sxs-lookup"><span data-stu-id="38fe0-267">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="38fe0-268">Dlatego całkowity 6 podejmowano.</span><span class="sxs-lookup"><span data-stu-id="38fe0-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="38fe0-269">Jeśli wykonanie żadnych zakończy się powodzeniem, stan wycinek jest gotowy, a próby są próby.</span><span class="sxs-lookup"><span data-stu-id="38fe0-269">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="38fe0-270">Parametr longRetry mogą być używane w sytuacji, w których danych zależnych dociera deterministyczna razy lub ogólnej środowiska jest niestabilnym, w których przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="38fe0-271">W takich przypadkach to ponownych prób po kolei może nie pomagają i w ten sposób po interwału czasu powoduje żądanego wyniku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="38fe0-272">Word Przestroga: nie należy ustawiać wysokiej wartości longRetry lub longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="38fe0-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="38fe0-273">Zazwyczaj wyższej wartości oznacza innych kwestii systemowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="38fe0-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="38fe0-274">longRetryInterval</span></span> |<span data-ttu-id="38fe0-275">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="38fe0-275">TimeSpan</span></span> |<span data-ttu-id="38fe0-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="38fe0-276">00:00:00</span></span> |<span data-ttu-id="38fe0-277">Opóźnienie między próbami czas ponów</span><span class="sxs-lookup"><span data-stu-id="38fe0-277">The delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="38fe0-278">sekcja typeProperties</span><span class="sxs-lookup"><span data-stu-id="38fe0-278">typeProperties section</span></span>
<span data-ttu-id="38fe0-279">Sekcja typeProperties jest różne dla każdego działania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-279">The typeProperties section is different for each activity.</span></span> <span data-ttu-id="38fe0-280">Transformacja działania mają tylko właściwości typu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-280">Transformation activities have just the type properties.</span></span> <span data-ttu-id="38fe0-281">Zobacz [działań PRZEKSZTAŁCANIA danych](#data-transformation-activities) w tym artykule, aby uzyskać przykłady JSON, które definiują czynności do przekształcenia w potoku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="38fe0-282">**Aktywność kopiowania** ma dwa podpunkty w sekcji typeProperties: **źródła** i **zbiornika**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-282">**Copy activity** has two subsections in the typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="38fe0-283">Zobacz [MAGAZYNY danych](#data-stores) sekcji w niniejszym artykule dla przykłady JSON, które pokazują, jak używać danych przechowywane jako źródła i/lub ujścia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="38fe0-284">Przykład kopii potoku</span><span class="sxs-lookup"><span data-stu-id="38fe0-284">Sample copy pipeline</span></span>
<span data-ttu-id="38fe0-285">W następujących przykładowych potoku, jest jedno działanie typu **kopiowania** w **działania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="38fe0-285">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span></span> <span data-ttu-id="38fe0-286">W tym przykładzie [aktywności kopiowania](data-factory-data-movement-activities.md) kopiuje dane z magazynu obiektów Blob platformy Azure do bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-286">In this sample, the [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="38fe0-287">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="38fe0-287">Note the following points:</span></span>

* <span data-ttu-id="38fe0-288">W sekcji działań jest tylko jedno działanie, którego parametr **type** (typ) został ustawiony na wartość **Copy**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
* <span data-ttu-id="38fe0-289">Dane wejściowe dla działania mają ustawienie **InputDataset**, a dane wyjściowe — **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-289">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span>
* <span data-ttu-id="38fe0-290">W sekcji **typeProperties** parametr **BlobSource** został określony jako typ źródłowy, a parametr **SqlSink** został określony jako typ ujścia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-290">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>

<span data-ttu-id="38fe0-291">Zobacz [MAGAZYNY danych](#data-stores) sekcji w niniejszym artykule dla przykłady JSON, które pokazują, jak używać danych przechowywane jako źródła i/lub ujścia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span>    

<span data-ttu-id="38fe0-292">Aby uzyskać szczegółowy przewodnik tworzenia tego potoku, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob do bazy danych SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="38fe0-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="38fe0-293">Przykładowe przekształcenie potoku</span><span class="sxs-lookup"><span data-stu-id="38fe0-293">Sample transformation pipeline</span></span>
<span data-ttu-id="38fe0-294">W następujących przykładowych potoku, jest jedno działanie typu **HDInsightHive** w **działania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="38fe0-294">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span></span> <span data-ttu-id="38fe0-295">W tym przykładzie [działania HDInsight Hive](data-factory-hive-activity.md) przekształcenia danych z magazynu obiektów Blob platformy Azure, uruchamiając plik skryptu Hive w klastrze usługi Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="38fe0-295">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
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
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="38fe0-296">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="38fe0-296">Note the following points:</span></span> 

* <span data-ttu-id="38fe0-297">W sekcji działania jest tylko jedno działanie którego **typu** ustawiono **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-297">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span></span>
* <span data-ttu-id="38fe0-298">Plik skryptu programu Hive **partitionweblogs.hql** jest przechowywany na koncie usługi Azure Storage (określonym za pomocą elementu scriptLinkedService o nazwie **AzureStorageLinkedService**) oraz w folderze **script** w kontenerze **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-298">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>
* <span data-ttu-id="38fe0-299">**Definiuje** sekcji służy do określania ustawienia środowiska uruchomieniowego, które są przekazywane do skryptu hive jako wartości konfiguracji gałąź (np. `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="38fe0-299">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="38fe0-300">Zobacz [działań PRZEKSZTAŁCANIA danych](#data-transformation-activities) w tym artykule, aby uzyskać przykłady JSON, które definiują czynności do przekształcenia w potoku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="38fe0-301">Aby uzyskać szczegółowy przewodnik tworzenia tego potoku, zobacz [samouczek: tworzenie swój pierwszy potok do przetwarzania danych przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="38fe0-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="38fe0-302">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-302">Linked service</span></span>
<span data-ttu-id="38fe0-303">Struktury wysokiego poziomu dla definicji usługi połączonej następująco:</span><span class="sxs-lookup"><span data-stu-id="38fe0-303">The high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of the linked service>",
    "properties": {
        "type": "<type of the linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="38fe0-304">Następujące tabeli opisano właściwości wewnątrz działania definicji JSON:</span><span class="sxs-lookup"><span data-stu-id="38fe0-304">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="38fe0-305">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-305">Property</span></span> | <span data-ttu-id="38fe0-306">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-306">Description</span></span> | <span data-ttu-id="38fe0-307">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="38fe0-308">name</span><span class="sxs-lookup"><span data-stu-id="38fe0-308">name</span></span> | <span data-ttu-id="38fe0-309">Nazwa połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-309">Name of the linked service.</span></span> | <span data-ttu-id="38fe0-310">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-310">Yes</span></span> | 
| <span data-ttu-id="38fe0-311">właściwości — Typ</span><span class="sxs-lookup"><span data-stu-id="38fe0-311">properties - type</span></span> | <span data-ttu-id="38fe0-312">Typ połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-312">Type of the linked service.</span></span> <span data-ttu-id="38fe0-313">Na przykład: Usługa Azure Storage, baza danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="38fe0-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="38fe0-314">typeProperties</span></span> | <span data-ttu-id="38fe0-315">Sekcja typeProperties zawiera elementy, które są różne dla każdego magazynu danych lub środowiska obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="38fe0-315">The typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="38fe0-316">Zobacz [magazyny danych](#datastores) sekcji dla połączonej usługi przechowywania wszystkich danych i [obliczeniowe środowisk](#compute-environments) dla wszystkich obliczeń połączone usługi</span><span class="sxs-lookup"><span data-stu-id="38fe0-316">See [data stores](#datastores) section for all the data store linked services and [compute environments](#compute-environments) for all the compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="38fe0-317">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-317">Dataset</span></span> 
<span data-ttu-id="38fe0-318">Zestaw danych z fabryki danych Azure jest zdefiniowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="38fe0-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="38fe0-319">W poniższej tabeli opisano właściwości w powyższym JSON:</span><span class="sxs-lookup"><span data-stu-id="38fe0-319">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="38fe0-320">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-320">Property</span></span> | <span data-ttu-id="38fe0-321">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-321">Description</span></span> | <span data-ttu-id="38fe0-322">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-322">Required</span></span> | <span data-ttu-id="38fe0-323">Domyślne</span><span class="sxs-lookup"><span data-stu-id="38fe0-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-324">name</span><span class="sxs-lookup"><span data-stu-id="38fe0-324">name</span></span> | <span data-ttu-id="38fe0-325">Nazwa zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-325">Name of the dataset.</span></span> <span data-ttu-id="38fe0-326">Zobacz [fabryki danych Azure - reguły nazewnictwa](data-factory-naming-rules.md) dla reguły nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="38fe0-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="38fe0-327">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-327">Yes</span></span> |<span data-ttu-id="38fe0-328">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="38fe0-328">NA</span></span> |
| <span data-ttu-id="38fe0-329">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-329">type</span></span> | <span data-ttu-id="38fe0-330">Typ zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-330">Type of the dataset.</span></span> <span data-ttu-id="38fe0-331">Określ jeden z typów obsługiwanych przez usługi fabryka danych Azure (na przykład: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="38fe0-331">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="38fe0-332">Zobacz [MAGAZYNY danych](#data-stores) sekcji dla wszystkich magazynów danych i typy danych obsługiwane przez fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-332">See [DATA STORES](#data-stores) section for all the data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="38fe0-333">Struktura</span><span class="sxs-lookup"><span data-stu-id="38fe0-333">structure</span></span> | <span data-ttu-id="38fe0-334">Schemat zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-334">Schema of the dataset.</span></span> <span data-ttu-id="38fe0-335">Zawiera kolumny, jak ich typy, itp.</span><span class="sxs-lookup"><span data-stu-id="38fe0-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="38fe0-336">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-336">No</span></span> |<span data-ttu-id="38fe0-337">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="38fe0-337">NA</span></span> |
| <span data-ttu-id="38fe0-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="38fe0-338">typeProperties</span></span> | <span data-ttu-id="38fe0-339">Właściwości odpowiadający wybranego typu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-339">Properties corresponding to the selected type.</span></span> <span data-ttu-id="38fe0-340">Zobacz [MAGAZYNY danych](#data-stores) sekcji dla obsługiwanych typów i ich właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="38fe0-341">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-341">Yes</span></span> |<span data-ttu-id="38fe0-342">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="38fe0-342">NA</span></span> |
| <span data-ttu-id="38fe0-343">external</span><span class="sxs-lookup"><span data-stu-id="38fe0-343">external</span></span> | <span data-ttu-id="38fe0-344">Flaga wartości logicznej, aby określić, czy element dataset jawnie jest generowany przez potok fabryki danych, czy nie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-344">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="38fe0-345">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-345">No</span></span> |<span data-ttu-id="38fe0-346">wartość false</span><span class="sxs-lookup"><span data-stu-id="38fe0-346">false</span></span> |
| <span data-ttu-id="38fe0-347">availability</span><span class="sxs-lookup"><span data-stu-id="38fe0-347">availability</span></span> | <span data-ttu-id="38fe0-348">Definiuje okna przetwarzania lub skalowania modelu do produkcji zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-348">Defines the processing window or the slicing model for the dataset production.</span></span> <span data-ttu-id="38fe0-349">Szczegółowe informacje dotyczące tworzenia wycinków modelu zestawu danych, zobacz [planowania i wykonywania](data-factory-scheduling-and-execution.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-349">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="38fe0-350">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-350">Yes</span></span> |<span data-ttu-id="38fe0-351">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="38fe0-351">NA</span></span> |
| <span data-ttu-id="38fe0-352">Zasady</span><span class="sxs-lookup"><span data-stu-id="38fe0-352">policy</span></span> |<span data-ttu-id="38fe0-353">Definiuje kryteria i warunków, które należy spełnić wycinków zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-353">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="38fe0-354">Aby uzyskać więcej informacji, zobacz [zestawie danych zasad](#Policy) sekcji.</span><span class="sxs-lookup"><span data-stu-id="38fe0-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="38fe0-355">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-355">No</span></span> |<span data-ttu-id="38fe0-356">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="38fe0-356">NA</span></span> |

<span data-ttu-id="38fe0-357">Każda kolumna **struktury** sekcja zawiera następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="38fe0-357">Each column in the **structure** section contains the following properties:</span></span>

| <span data-ttu-id="38fe0-358">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-358">Property</span></span> | <span data-ttu-id="38fe0-359">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-359">Description</span></span> | <span data-ttu-id="38fe0-360">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-361">name</span><span class="sxs-lookup"><span data-stu-id="38fe0-361">name</span></span> |<span data-ttu-id="38fe0-362">Nazwa kolumny.</span><span class="sxs-lookup"><span data-stu-id="38fe0-362">Name of the column.</span></span> |<span data-ttu-id="38fe0-363">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-363">Yes</span></span> |
| <span data-ttu-id="38fe0-364">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-364">type</span></span> |<span data-ttu-id="38fe0-365">Typ danych kolumny.</span><span class="sxs-lookup"><span data-stu-id="38fe0-365">Data type of the column.</span></span>  |<span data-ttu-id="38fe0-366">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-366">No</span></span> |
| <span data-ttu-id="38fe0-367">Kultury</span><span class="sxs-lookup"><span data-stu-id="38fe0-367">culture</span></span> |<span data-ttu-id="38fe0-368">.NET na podstawie kultury, który będzie używany podczas typu określono i jest typ architektury .NET `Datetime` lub `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-368">.NET based culture to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="38fe0-369">Domyślnie jest `en-us`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-369">Default is `en-us`.</span></span> |<span data-ttu-id="38fe0-370">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-370">No</span></span> |
| <span data-ttu-id="38fe0-371">Format</span><span class="sxs-lookup"><span data-stu-id="38fe0-371">format</span></span> |<span data-ttu-id="38fe0-372">Ciąg, który będzie używany podczas typu określono i jest typ architektury .NET formatu `Datetime` lub `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-372">Format string to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="38fe0-373">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-373">No</span></span> |

<span data-ttu-id="38fe0-374">W poniższym przykładzie element dataset zawiera trzy kolumny `slicetimestamp`, `projectname`, i `pageviews` i są typu: String, typ String i dziesiętnych odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="38fe0-374">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="38fe0-375">W poniższej tabeli opisano właściwości można używać w **dostępności** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-375">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="38fe0-376">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-376">Property</span></span> | <span data-ttu-id="38fe0-377">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-377">Description</span></span> | <span data-ttu-id="38fe0-378">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-378">Required</span></span> | <span data-ttu-id="38fe0-379">Domyślne</span><span class="sxs-lookup"><span data-stu-id="38fe0-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-380">częstotliwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-380">frequency</span></span> |<span data-ttu-id="38fe0-381">Określa jednostkę czasu dla trybu produkcyjnego wycinek zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-381">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="38fe0-382"><b>Obsługiwana częstotliwość</b>: minuty, godziny, dnia, tygodnia, miesiąca</span><span class="sxs-lookup"><span data-stu-id="38fe0-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="38fe0-383">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-383">Yes</span></span> |<span data-ttu-id="38fe0-384">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="38fe0-384">NA</span></span> |
| <span data-ttu-id="38fe0-385">Interwał</span><span class="sxs-lookup"><span data-stu-id="38fe0-385">interval</span></span> |<span data-ttu-id="38fe0-386">Określa mnożnik częstotliwości</span><span class="sxs-lookup"><span data-stu-id="38fe0-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="38fe0-387">"Interwał częstotliwości x" Określa, jak często jest tworzony wycinek.</span><span class="sxs-lookup"><span data-stu-id="38fe0-387">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="38fe0-388">Zestaw danych, aby zostać podzielona na godzinę, należy ustawić <b>częstotliwość</b> do <b>godzina</b>, i <b>interwał</b> do <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="38fe0-388">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="38fe0-389"><b>Uwaga</b>: Jeśli zostanie określona częstotliwość jako minutę, zaleca się ustawić interwał wynoszący nie mniej niż 15</span><span class="sxs-lookup"><span data-stu-id="38fe0-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="38fe0-390">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-390">Yes</span></span> |<span data-ttu-id="38fe0-391">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="38fe0-391">NA</span></span> |
| <span data-ttu-id="38fe0-392">Styl</span><span class="sxs-lookup"><span data-stu-id="38fe0-392">style</span></span> |<span data-ttu-id="38fe0-393">Określa, czy wycinek będą tworzone na początku/końca zakresu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-393">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="38fe0-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="38fe0-394">StartOfInterval</span></span></li><li><span data-ttu-id="38fe0-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="38fe0-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="38fe0-396">Jeśli częstotliwość ma ustawioną wartość miesiąca i styl ma ustawioną wartość EndOfInterval, wycinek jest realizowane ostatniego dnia miesiąca.</span><span class="sxs-lookup"><span data-stu-id="38fe0-396">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="38fe0-397">Jeżeli styl jest ustawiony na StartOfInterval, wycinek jest generowany na pierwszy dzień miesiąca.</span><span class="sxs-lookup"><span data-stu-id="38fe0-397">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="38fe0-398">Jeśli ustawiono częstotliwość do dnia i styl ma ustawioną wartość EndOfInterval, wycinka jest realizowane w ciągu ostatniej godziny dnia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-398">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="38fe0-399">Jeśli częstotliwość wynosi godzinę i styl ma ustawioną wartość EndOfInterval, wycinek jest generowany na koniec godziny.</span><span class="sxs-lookup"><span data-stu-id="38fe0-399">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="38fe0-400">Na przykład dla wycinka okres 13: 00 – 14: 00, wycinek jest generowany na 14: 00.</span><span class="sxs-lookup"><span data-stu-id="38fe0-400">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="38fe0-401">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-401">No</span></span> |<span data-ttu-id="38fe0-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="38fe0-402">EndOfInterval</span></span> |
| <span data-ttu-id="38fe0-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="38fe0-403">anchorDateTime</span></span> |<span data-ttu-id="38fe0-404">Definiuje położenie bezwzględne w czasie używanych przez harmonogram do obliczenia granice wycinek zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-404">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="38fe0-405"><b>Uwaga</b>: Jeśli AnchorDateTime ma części daty, które są bardziej szczegółowego niż wartość częstotliwości, bardziej szczegółowego części są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="38fe0-405"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="38fe0-406">Na przykład jeśli <b>interwał</b> jest <b>co godzinę</b> (częstotliwość: godzinę i interwał: 1) i <b>AnchorDateTime</b> zawiera <b>minut i sekund</b> , a następnie <b>minut i sekund</b> części AnchorDateTime są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="38fe0-406">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="38fe0-407">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-407">No</span></span> |<span data-ttu-id="38fe0-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="38fe0-408">01/01/0001</span></span> |
| <span data-ttu-id="38fe0-409">Przesunięcie</span><span class="sxs-lookup"><span data-stu-id="38fe0-409">offset</span></span> |<span data-ttu-id="38fe0-410">Zakres czasu za pomocą której zostaną przesunięte początku i końcu wszystkie fragmenty zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-410">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="38fe0-411"><b>Uwaga</b>: Jeśli jest określony zarówno anchorDateTime, jak i przesunięcie wynik jest połączonych shift.</span><span class="sxs-lookup"><span data-stu-id="38fe0-411"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="38fe0-412">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-412">No</span></span> |<span data-ttu-id="38fe0-413">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="38fe0-413">NA</span></span> |

<span data-ttu-id="38fe0-414">W poniższej sekcji dostępności Określa, że wyjściowy zestaw danych jest także co godzinę (albo) danych wejściowych co godzinę zestaw danych jest dostępne:</span><span class="sxs-lookup"><span data-stu-id="38fe0-414">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="38fe0-415">**Zasad** sekcja w definicji zestawu danych definiuje kryteria i warunków, które należy spełnić wycinków zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-415">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

| <span data-ttu-id="38fe0-416">Nazwa zasad</span><span class="sxs-lookup"><span data-stu-id="38fe0-416">Policy Name</span></span> | <span data-ttu-id="38fe0-417">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-417">Description</span></span> | <span data-ttu-id="38fe0-418">Dotyczy</span><span class="sxs-lookup"><span data-stu-id="38fe0-418">Applied To</span></span> | <span data-ttu-id="38fe0-419">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-419">Required</span></span> | <span data-ttu-id="38fe0-420">Domyślne</span><span class="sxs-lookup"><span data-stu-id="38fe0-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="38fe0-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="38fe0-421">minimumSizeMB</span></span> |<span data-ttu-id="38fe0-422">Sprawdza, czy dane w **obiektów blob platformy Azure** spełnia wymagania minimalny rozmiar (w megabajtach).</span><span class="sxs-lookup"><span data-stu-id="38fe0-422">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="38fe0-423">Obiekt bob Azure</span><span class="sxs-lookup"><span data-stu-id="38fe0-423">Azure Blob</span></span> |<span data-ttu-id="38fe0-424">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-424">No</span></span> |<span data-ttu-id="38fe0-425">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="38fe0-425">NA</span></span> |
| <span data-ttu-id="38fe0-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="38fe0-426">minimumRows</span></span> |<span data-ttu-id="38fe0-427">Sprawdza, czy dane w **bazy danych Azure SQL** lub **tabeli platformy Azure** zawiera minimalną liczbę wierszy.</span><span class="sxs-lookup"><span data-stu-id="38fe0-427">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="38fe0-428">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="38fe0-428">Azure SQL Database</span></span></li><li><span data-ttu-id="38fe0-429">Tabeli platformy Azure</span><span class="sxs-lookup"><span data-stu-id="38fe0-429">Azure Table</span></span></li></ul> |<span data-ttu-id="38fe0-430">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-430">No</span></span> |<span data-ttu-id="38fe0-431">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="38fe0-431">NA</span></span> |

<span data-ttu-id="38fe0-432">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="38fe0-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="38fe0-433">Jeśli zestaw danych jest tworzonym przez fabryki danych Azure, powinien być oznaczony jako **zewnętrznych**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="38fe0-434">To ustawienie dotyczy wejść pierwsze działanie w potoku ogólnie rzecz biorąc, chyba że działania lub łańcucha potoku jest używany.</span><span class="sxs-lookup"><span data-stu-id="38fe0-434">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="38fe0-435">Nazwa</span><span class="sxs-lookup"><span data-stu-id="38fe0-435">Name</span></span> | <span data-ttu-id="38fe0-436">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-436">Description</span></span> | <span data-ttu-id="38fe0-437">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-437">Required</span></span> | <span data-ttu-id="38fe0-438">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="38fe0-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="38fe0-439">dataDelay</span></span> |<span data-ttu-id="38fe0-440">Czas opóźnienia sprawdzanie dostępności danych zewnętrznych dla danego wycinka.</span><span class="sxs-lookup"><span data-stu-id="38fe0-440">Time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="38fe0-441">Na przykład jeśli dane są dostępne co godzinę, sprawdź dane zewnętrzne jest dostępna i odpowiednie wycinek jest gotowy można opóźnić przy użyciu dataDelay.</span><span class="sxs-lookup"><span data-stu-id="38fe0-441">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="38fe0-442">Ma zastosowanie tylko do chwili obecnej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-442">Only applies to the present time.</span></span>  <span data-ttu-id="38fe0-443">Na przykład jeśli 1:00 PM od razu i ta wartość to 10 minut, sprawdzanie poprawności rozpoczyna się od 1:22:00.</span><span class="sxs-lookup"><span data-stu-id="38fe0-443">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="38fe0-444">To ustawienie nie wpływa na wycinków w przeszłości (wycinków z godzina zakończenia wycinek + dataDelay < teraz) są przetwarzane bez opóźnień.</span><span class="sxs-lookup"><span data-stu-id="38fe0-444">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="38fe0-445">Czasu większą niż 23:59 godziny należy określić przy użyciu `day.hours:minutes:seconds` format.</span><span class="sxs-lookup"><span data-stu-id="38fe0-445">Time greater than 23:59 hours need to specified using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="38fe0-446">Na przykład aby określić 24 godziny, nie używaj 24:00:00; Zamiast tego należy użyć 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="38fe0-446">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="38fe0-447">Jeśli używasz 24:00:00, będzie traktowane jako 24 dni (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="38fe0-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="38fe0-448">1 dzień i 4 godziny Określ 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="38fe0-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="38fe0-449">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-449">No</span></span> |<span data-ttu-id="38fe0-450">0</span><span class="sxs-lookup"><span data-stu-id="38fe0-450">0</span></span> |
| <span data-ttu-id="38fe0-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="38fe0-451">retryInterval</span></span> |<span data-ttu-id="38fe0-452">Czas oczekiwania między awarii i następnych ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="38fe0-452">The wait time between a failure and the next retry attempt.</span></span> <span data-ttu-id="38fe0-453">W przypadku niepowodzenia spróbuj następnej próbie po retryInterval.</span><span class="sxs-lookup"><span data-stu-id="38fe0-453">If a try fails, the next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="38fe0-454">Jeśli jest 1:00 PM od razu, możemy rozpocząć pierwszej próby.</span><span class="sxs-lookup"><span data-stu-id="38fe0-454">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="38fe0-455">W przypadku czasu oczekiwania na zakończenie pierwszej sprawdzanie poprawności 1 minutę i operacja nie powiodła się, następna ponowna próba wynosi 1:00 1 min (czas trwania) + 1 min (interwału ponawiania prób) = 13:02:00.</span><span class="sxs-lookup"><span data-stu-id="38fe0-455">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="38fe0-456">Wycinki w przeszłości nie ma żadnego opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-456">For slices in the past, there is no delay.</span></span> <span data-ttu-id="38fe0-457">Ponów próbę odbywa się natychmiast.</span><span class="sxs-lookup"><span data-stu-id="38fe0-457">The retry happens immediately.</span></span> |<span data-ttu-id="38fe0-458">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-458">No</span></span> |<span data-ttu-id="38fe0-459">00:01:00 (1 minuta)</span><span class="sxs-lookup"><span data-stu-id="38fe0-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="38fe0-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="38fe0-460">retryTimeout</span></span> |<span data-ttu-id="38fe0-461">Limit czasu dla każdego ponowienia próby.</span><span class="sxs-lookup"><span data-stu-id="38fe0-461">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="38fe0-462">Jeśli ta właściwość jest ustawiona na 10 minut, sprawdzanie poprawności musi być zakończona w ciągu 10 minut.</span><span class="sxs-lookup"><span data-stu-id="38fe0-462">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span></span> <span data-ttu-id="38fe0-463">Jeśli trwa dłużej niż 10 minut, aby wykonać sprawdzanie poprawności, limit czasu próby.</span><span class="sxs-lookup"><span data-stu-id="38fe0-463">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="38fe0-464">Jeśli upłynie limit czasu wszystkie próby zatwierdzenia, wycinek jest oznaczona jako upłynął limit czasu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-464">If all attempts for the validation times out, the slice is marked as TimedOut.</span></span> |<span data-ttu-id="38fe0-465">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-465">No</span></span> |<span data-ttu-id="38fe0-466">00:10:00 (10 minut)</span><span class="sxs-lookup"><span data-stu-id="38fe0-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="38fe0-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="38fe0-467">maximumRetry</span></span> |<span data-ttu-id="38fe0-468">Liczba Sprawdź dostępność danych zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-468">Number of times to check for the availability of the external data.</span></span> <span data-ttu-id="38fe0-469">Wartość maksymalna dozwolonych jest 10.</span><span class="sxs-lookup"><span data-stu-id="38fe0-469">The allowed maximum value is 10.</span></span> |<span data-ttu-id="38fe0-470">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-470">No</span></span> |<span data-ttu-id="38fe0-471">3</span><span class="sxs-lookup"><span data-stu-id="38fe0-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="38fe0-472">MAGAZYNY DANYCH</span><span class="sxs-lookup"><span data-stu-id="38fe0-472">DATA STORES</span></span>
<span data-ttu-id="38fe0-473">[Połączona usługa](#linked-service) opisy sekcji określone elementy JSON, które są wspólne dla wszystkich typów połączonych usług.</span><span class="sxs-lookup"><span data-stu-id="38fe0-473">The [Linked service](#linked-service) section provided descriptions for JSON elements that are common to all types of linked services.</span></span> <span data-ttu-id="38fe0-474">Ta sekcja zawiera szczegółowe informacje o elementach JSON, które są specyficzne dla każdego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-474">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="38fe0-475">[Dataset](#dataset) opisy sekcji określone elementy JSON, które są wspólne dla wszystkich typów zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-475">The [Dataset](#dataset) section provided descriptions for JSON elements that are common to all types of datasets.</span></span> <span data-ttu-id="38fe0-476">Ta sekcja zawiera szczegółowe informacje o elementach JSON, które są specyficzne dla każdego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-476">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="38fe0-477">[Działania](#activity) opisy sekcji określone elementy JSON, które są wspólne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="38fe0-477">The [Activity](#activity) section provided descriptions for JSON elements that are common to all types of activities.</span></span> <span data-ttu-id="38fe0-478">Ta sekcja zawiera szczegółowe informacje o elementach JSON, które są specyficzne dla każdego magazynu danych, gdy jest używany jako źródło/ujście w działaniu kopiowania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-478">This section provides details about JSON elements that are specific to each data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="38fe0-479">Kliknij łącze do magazynu, który chcesz wyświetlić schematów JSON połączonej usługi, zestawu danych i źródło/ujście dla działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-479">Click the link for the store you are interested in to see the JSON schemas for linked service, dataset, and the source/sink for the copy activity.</span></span>

| <span data-ttu-id="38fe0-480">Kategoria</span><span class="sxs-lookup"><span data-stu-id="38fe0-480">Category</span></span> | <span data-ttu-id="38fe0-481">Magazyn danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="38fe0-482">**Azure**</span><span class="sxs-lookup"><span data-stu-id="38fe0-482">**Azure**</span></span> |[<span data-ttu-id="38fe0-483">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="38fe0-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="38fe0-484">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="38fe0-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="38fe0-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="38fe0-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="38fe0-486">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="38fe0-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="38fe0-487">Magazyn danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="38fe0-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="38fe0-488">Azure Search</span><span class="sxs-lookup"><span data-stu-id="38fe0-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="38fe0-489">Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="38fe0-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="38fe0-490">**Bazy danych**</span><span class="sxs-lookup"><span data-stu-id="38fe0-490">**Databases**</span></span> |[<span data-ttu-id="38fe0-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="38fe0-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="38fe0-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="38fe0-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="38fe0-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="38fe0-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="38fe0-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="38fe0-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="38fe0-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="38fe0-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="38fe0-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="38fe0-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="38fe0-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="38fe0-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="38fe0-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="38fe0-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="38fe0-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="38fe0-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="38fe0-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="38fe0-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="38fe0-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="38fe0-501">**NoSQL**</span></span> |[<span data-ttu-id="38fe0-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="38fe0-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="38fe0-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="38fe0-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="38fe0-504">**Plik**</span><span class="sxs-lookup"><span data-stu-id="38fe0-504">**File**</span></span> |[<span data-ttu-id="38fe0-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="38fe0-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="38fe0-506">System plików</span><span class="sxs-lookup"><span data-stu-id="38fe0-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="38fe0-507">FTP</span><span class="sxs-lookup"><span data-stu-id="38fe0-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="38fe0-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="38fe0-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="38fe0-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="38fe0-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="38fe0-510">**Inne**</span><span class="sxs-lookup"><span data-stu-id="38fe0-510">**Others**</span></span> |[<span data-ttu-id="38fe0-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="38fe0-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="38fe0-512">OData</span><span class="sxs-lookup"><span data-stu-id="38fe0-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="38fe0-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="38fe0-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="38fe0-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="38fe0-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="38fe0-515">Tabela sieci Web</span><span class="sxs-lookup"><span data-stu-id="38fe0-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="38fe0-516">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="38fe0-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-517">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-517">Linked service</span></span>
<span data-ttu-id="38fe0-518">Istnieją dwa typy połączonych usług: połączonej usługi magazynu Azure i połączonej usługi magazynu Azure sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="38fe0-519">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="38fe0-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="38fe0-520">Aby połączyć konto magazynu Azure do fabryki danych przy użyciu **klucz konta**, Utwórz połączoną usługą magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-520">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="38fe0-521">Aby zdefiniować usługi Azure Storage połączonej usługi, ustaw **typu** połączonej usługi, aby **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-521">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="38fe0-522">Następnie można określić następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-522">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-523">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-523">Property</span></span> | <span data-ttu-id="38fe0-524">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-524">Description</span></span> | <span data-ttu-id="38fe0-525">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="38fe0-526">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="38fe0-526">connectionString</span></span> |<span data-ttu-id="38fe0-527">Podaj informacje wymagane do połączenia z magazynem platformy Azure dla właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="38fe0-527">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="38fe0-528">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="38fe0-529">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-529">Example</span></span>  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="38fe0-530">Połączonej usługi magazynu Azure SAS</span><span class="sxs-lookup"><span data-stu-id="38fe0-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="38fe0-531">Usługa połączone SAS magazynu Azure umożliwia łączenie konto magazynu Azure do fabryki danych Azure za pomocą udostępnionego podpis dostępu (SAS).</span><span class="sxs-lookup"><span data-stu-id="38fe0-531">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="38fe0-532">Fabryka danych zapewnia ograniczony/czas-powiązane z dostęp do określonego/all zasobów (kontener/obiektów blob) w magazynie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-532">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="38fe0-533">Aby połączyć konto magazynu platformy Azure z fabryki danych przy użyciu sygnatura dostępu współdzielonego, Utwórz SAS magazynu Azure połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-533">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="38fe0-534">Aby zdefiniować SAS magazynu Azure połączonej usługi, ustaw **typu** połączonej usługi, aby **element AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-534">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="38fe0-535">Następnie można określić następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-535">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="38fe0-536">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-536">Property</span></span> | <span data-ttu-id="38fe0-537">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-537">Description</span></span> | <span data-ttu-id="38fe0-538">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="38fe0-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="38fe0-539">sasUri</span></span> |<span data-ttu-id="38fe0-540">Określ udostępniony URI sygnatury dostępu do zasobów usługi Azure Storage, takich jak obiektów blob, kontenera lub tabeli.</span><span class="sxs-lookup"><span data-stu-id="38fe0-540">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="38fe0-541">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="38fe0-542">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-542">Example</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="38fe0-543">Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika usługi Azure Blob Storage](data-factory-azure-blob-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-544">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-544">Dataset</span></span>
<span data-ttu-id="38fe0-545">Aby zdefiniować zestawu danych obiektów Blob platformy Azure, ustaw **typu** zestawu danych do **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-545">To define an Azure Blob dataset, set the **type** of the dataset to **AzureBlob**.</span></span> <span data-ttu-id="38fe0-546">Następnie określ następujące właściwości określonych obiektów Blob platformy Azure w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-546">Then, specify the following Azure Blob specific properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-547">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-547">Property</span></span> | <span data-ttu-id="38fe0-548">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-548">Description</span></span> | <span data-ttu-id="38fe0-549">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="38fe0-550">folderPath</span></span> |<span data-ttu-id="38fe0-551">Ścieżka do kontenera i folderu w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="38fe0-551">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="38fe0-552">Przykład: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="38fe0-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="38fe0-553">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-553">Yes</span></span> |
| <span data-ttu-id="38fe0-554">fileName</span><span class="sxs-lookup"><span data-stu-id="38fe0-554">fileName</span></span> |<span data-ttu-id="38fe0-555">Nazwa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="38fe0-555">Name of the blob.</span></span> <span data-ttu-id="38fe0-556">Nazwa pliku jest opcjonalna i z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="38fe0-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="38fe0-557">Jeśli określono nazwę pliku, działania (w tym kopiowania) działa na konkretnego obiektu Blob.</span><span class="sxs-lookup"><span data-stu-id="38fe0-557">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="38fe0-558">Jeśli nie określono nazwy pliku, kopiowania obejmuje wszystkie obiekty BLOB w ścieżce folderu dla zestawu danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-558">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="38fe0-559">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwę wygenerowanego pliku będzie poniżej tego formatu: danych. <Guid>.txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="38fe0-559">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="38fe0-560">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-560">No</span></span> |
| <span data-ttu-id="38fe0-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="38fe0-561">partitionedBy</span></span> |<span data-ttu-id="38fe0-562">partitionedBy jest opcjonalna właściwość.</span><span class="sxs-lookup"><span data-stu-id="38fe0-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="38fe0-563">Można go określić folderPath dynamiczne i nazwę pliku dla danych w serii. czas.</span><span class="sxs-lookup"><span data-stu-id="38fe0-563">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="38fe0-564">Na przykład folderPath mogą nadać parametry dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="38fe0-565">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-565">No</span></span> |
| <span data-ttu-id="38fe0-566">Format</span><span class="sxs-lookup"><span data-stu-id="38fe0-566">format</span></span> | <span data-ttu-id="38fe0-567">Obsługiwane są następujące typy format: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-567">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="38fe0-568">Ustaw **typu** właściwości w formacie do jednej z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-568">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="38fe0-569">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="38fe0-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="38fe0-570">Jeśli chcesz **skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcji format w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-570">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="38fe0-571">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-571">No</span></span> |
| <span data-ttu-id="38fe0-572">Kompresja</span><span class="sxs-lookup"><span data-stu-id="38fe0-572">compression</span></span> | <span data-ttu-id="38fe0-573">Określ typ i poziom kompresji danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-573">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="38fe0-574">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="38fe0-575">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="38fe0-576">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="38fe0-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="38fe0-577">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-578">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-578">Example</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
 ```


<span data-ttu-id="38fe0-579">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="38fe0-580">BlobSource w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="38fe0-581">Jeśli dane są kopiowane z magazynu obiektów Blob platformy Azure, ustaw **typ źródła** działania kopiowania do **BlobSource**i określ następujące właściwości w ** źródła ** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-581">If you are copying data from an Azure Blob Storage, set the **source type** of the copy activity to **BlobSource**, and specify following properties in the **source **section:</span></span>

| <span data-ttu-id="38fe0-582">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-582">Property</span></span> | <span data-ttu-id="38fe0-583">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-583">Description</span></span> | <span data-ttu-id="38fe0-584">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-584">Allowed values</span></span> | <span data-ttu-id="38fe0-585">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-586">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="38fe0-586">recursive</span></span> |<span data-ttu-id="38fe0-587">Wskazuje, czy dane są odczytywane rekursywnie z folderów sub lub tylko określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-587">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="38fe0-588">TRUE, False (wartość domyślna)</span><span class="sxs-lookup"><span data-stu-id="38fe0-588">True (default value), False</span></span> |<span data-ttu-id="38fe0-589">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="38fe0-590">Przykład: BlobSource **</span><span class="sxs-lookup"><span data-stu-id="38fe0-590">Example: BlobSource**</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="38fe0-591">BlobSink w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="38fe0-592">Jeśli dane są kopiowane do magazynu obiektów Blob Azure, ustaw **typu sink** działania kopiowania do **BlobSink**i określ następujące właściwości w **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-592">If you are copying data to an Azure Blob Storage, set the **sink type** of the copy activity to **BlobSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="38fe0-593">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-593">Property</span></span> | <span data-ttu-id="38fe0-594">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-594">Description</span></span> | <span data-ttu-id="38fe0-595">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-595">Allowed values</span></span> | <span data-ttu-id="38fe0-596">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="38fe0-597">copyBehavior</span></span> |<span data-ttu-id="38fe0-598">Określa zachowanie kopiowania, gdy źródłem jest BlobSource lub systemu plików.</span><span class="sxs-lookup"><span data-stu-id="38fe0-598">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="38fe0-599"><b>PreserveHierarchy</b>: zachowuje hierarchię plików w folderze docelowym.</span><span class="sxs-lookup"><span data-stu-id="38fe0-599"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="38fe0-600">Względna ścieżka pliku źródłowego do folderu źródłowego jest taka sama jak ścieżka względna docelowego pliku do folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-600">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="38fe0-601"><b>FlattenHierarchy</b>: wszystkie pliki z folderu źródłowego znajdują się w pierwszym poziomem folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-601"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="38fe0-602">Pliki docelowe mają automatycznie wygeneruje nazwę.</span><span class="sxs-lookup"><span data-stu-id="38fe0-602">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="38fe0-603"><b>MergeFiles (domyślnie):</b> scala wszystkie pliki z folderu źródłowego do jednego pliku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-603"><b>MergeFiles (default):</b> merges all files from the source folder to one file.</span></span> <span data-ttu-id="38fe0-604">Jeśli zostanie określona nazwa pliku/obiektów Blob, nazwa scalony plik jest określona nazwa; w przeciwnym razie będzie nazwa pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-604">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="38fe0-605">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="38fe0-606">Przykład: BlobSink</span><span class="sxs-lookup"><span data-stu-id="38fe0-606">Example: BlobSink</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-607">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Blob](data-factory-azure-blob-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="38fe0-608">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="38fe0-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-609">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-609">Linked service</span></span>
<span data-ttu-id="38fe0-610">Aby zdefiniować Azure Data Lake Store połączonej usługi, Ustaw typ połączonej usługi, aby **AzureDataLakeStore**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-610">To define an Azure Data Lake Store linked service, set the type of the linked service to **AzureDataLakeStore**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-611">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-611">Property</span></span> | <span data-ttu-id="38fe0-612">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-612">Description</span></span> | <span data-ttu-id="38fe0-613">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="38fe0-614">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-614">type</span></span> | <span data-ttu-id="38fe0-615">Właściwość type musi mieć ustawioną: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="38fe0-615">The type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="38fe0-616">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-616">Yes</span></span> |
| <span data-ttu-id="38fe0-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="38fe0-617">dataLakeStoreUri</span></span> | <span data-ttu-id="38fe0-618">Określ informacje o koncie usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="38fe0-618">Specify information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="38fe0-619">Znajduje się w następującym formacie: `https://[accountname].azuredatalakestore.net/webhdfs/v1` lub `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-619">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="38fe0-620">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-620">Yes</span></span> |
| <span data-ttu-id="38fe0-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="38fe0-621">subscriptionId</span></span> | <span data-ttu-id="38fe0-622">Identyfikator subskrypcji platformy Azure, do której należy usługa Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="38fe0-622">Azure subscription Id to which Data Lake Store belongs.</span></span> | <span data-ttu-id="38fe0-623">Wymagany dla odbiorcy</span><span class="sxs-lookup"><span data-stu-id="38fe0-623">Required for sink</span></span> |
| <span data-ttu-id="38fe0-624">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="38fe0-624">resourceGroupName</span></span> | <span data-ttu-id="38fe0-625">Nazwa grupy zasobów platformy Azure, do której należy usługa Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="38fe0-625">Azure resource group name to which Data Lake Store belongs.</span></span> | <span data-ttu-id="38fe0-626">Wymagany dla odbiorcy</span><span class="sxs-lookup"><span data-stu-id="38fe0-626">Required for sink</span></span> |
| <span data-ttu-id="38fe0-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="38fe0-627">servicePrincipalId</span></span> | <span data-ttu-id="38fe0-628">Określ identyfikator aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="38fe0-628">Specify the application's client ID.</span></span> | <span data-ttu-id="38fe0-629">Tak (dla uwierzytelniania głównej usługi)</span><span class="sxs-lookup"><span data-stu-id="38fe0-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="38fe0-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="38fe0-630">servicePrincipalKey</span></span> | <span data-ttu-id="38fe0-631">Określ klucz aplikacji.</span><span class="sxs-lookup"><span data-stu-id="38fe0-631">Specify the application's key.</span></span> | <span data-ttu-id="38fe0-632">Tak (dla uwierzytelniania głównej usługi)</span><span class="sxs-lookup"><span data-stu-id="38fe0-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="38fe0-633">Dzierżawy</span><span class="sxs-lookup"><span data-stu-id="38fe0-633">tenant</span></span> | <span data-ttu-id="38fe0-634">Określ informacje dzierżawy (identyfikator nazwy lub dzierżawy domeny), w którym znajduje się aplikacja.</span><span class="sxs-lookup"><span data-stu-id="38fe0-634">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="38fe0-635">Można go pobrać, ustawiając kursor myszy w prawym górnym rogu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-635">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="38fe0-636">Tak (dla uwierzytelniania głównej usługi)</span><span class="sxs-lookup"><span data-stu-id="38fe0-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="38fe0-637">Autoryzacji</span><span class="sxs-lookup"><span data-stu-id="38fe0-637">authorization</span></span> | <span data-ttu-id="38fe0-638">Kliknij przycisk **autoryzacji** przycisk **Edytor fabryki danych** , a następnie wprowadź Twoje poświadczenia, który przypisuje adres URL automatycznie generowanej autoryzacji do tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-638">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span></span> | <span data-ttu-id="38fe0-639">Tak (do uwierzytelniania poświadczeń użytkownika)</span><span class="sxs-lookup"><span data-stu-id="38fe0-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="38fe0-640">Identyfikator sesji</span><span class="sxs-lookup"><span data-stu-id="38fe0-640">sessionId</span></span> | <span data-ttu-id="38fe0-641">Identyfikator sesji OAuth z sesji autoryzacji OAuth.</span><span class="sxs-lookup"><span data-stu-id="38fe0-641">OAuth session id from the OAuth authorization session.</span></span> <span data-ttu-id="38fe0-642">Każdy identyfikator sesji jest unikatowy i mogą być użyte tylko raz.</span><span class="sxs-lookup"><span data-stu-id="38fe0-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="38fe0-643">To ustawienie jest generowane automatycznie, gdy używasz Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="38fe0-644">Tak (do uwierzytelniania poświadczeń użytkownika)</span><span class="sxs-lookup"><span data-stu-id="38fe0-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="38fe0-645">Przykład: przy użyciu uwierzytelniania głównej usługi</span><span class="sxs-lookup"><span data-stu-id="38fe0-645">Example: using service principal authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="38fe0-646">Przykład: przy użyciu uwierzytelniania poświadczeń użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-646">Example: using user credential authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

<span data-ttu-id="38fe0-647">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-648">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-648">Dataset</span></span>
<span data-ttu-id="38fe0-649">Aby zdefiniować zestawem danych usługi Azure Data Lake Store, ustaw **typu** zestawu danych do **AzureDataLakeStore**, a następnie określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-649">To define an Azure Data Lake Store dataset, set the **type** of the dataset to **AzureDataLakeStore**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-650">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-650">Property</span></span> | <span data-ttu-id="38fe0-651">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-651">Description</span></span> | <span data-ttu-id="38fe0-652">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="38fe0-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="38fe0-653">folderPath</span></span> |<span data-ttu-id="38fe0-654">Ścieżka do folderu w usłudze Azure Data Lake i kontenera magazynu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-654">Path to the container and folder in the Azure Data Lake store.</span></span> |<span data-ttu-id="38fe0-655">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-655">Yes</span></span> |
| <span data-ttu-id="38fe0-656">fileName</span><span class="sxs-lookup"><span data-stu-id="38fe0-656">fileName</span></span> |<span data-ttu-id="38fe0-657">Nazwa pliku w magazynie usługi Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="38fe0-657">Name of the file in the Azure Data Lake store.</span></span> <span data-ttu-id="38fe0-658">Nazwa pliku jest opcjonalna i z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="38fe0-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="38fe0-659">Określ nazwę pliku, działania (w tym kopiowania) współpracuje w określonym pliku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-659">If you specify a filename, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="38fe0-660">Jeśli nie określono nazwy pliku, kopia zawiera wszystkie pliki w ścieżce folderu dla zestawu danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-660">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="38fe0-661">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwę wygenerowanego pliku będzie poniżej tego formatu: danych. <Guid>.txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="38fe0-661">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="38fe0-662">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-662">No</span></span> |
| <span data-ttu-id="38fe0-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="38fe0-663">partitionedBy</span></span> |<span data-ttu-id="38fe0-664">partitionedBy jest opcjonalna właściwość.</span><span class="sxs-lookup"><span data-stu-id="38fe0-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="38fe0-665">Można go określić folderPath dynamiczne i nazwę pliku dla danych w serii. czas.</span><span class="sxs-lookup"><span data-stu-id="38fe0-665">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="38fe0-666">Na przykład folderPath mogą nadać parametry dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="38fe0-667">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-667">No</span></span> |
| <span data-ttu-id="38fe0-668">Format</span><span class="sxs-lookup"><span data-stu-id="38fe0-668">format</span></span> | <span data-ttu-id="38fe0-669">Obsługiwane są następujące typy format: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-669">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="38fe0-670">Ustaw **typu** właściwości w formacie do jednej z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-670">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="38fe0-671">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="38fe0-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="38fe0-672">Jeśli chcesz **skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcji format w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-672">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="38fe0-673">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-673">No</span></span> |
| <span data-ttu-id="38fe0-674">Kompresja</span><span class="sxs-lookup"><span data-stu-id="38fe0-674">compression</span></span> | <span data-ttu-id="38fe0-675">Określ typ i poziom kompresji danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-675">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="38fe0-676">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="38fe0-677">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="38fe0-678">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="38fe0-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="38fe0-679">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-680">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-680">Example</span></span>
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="38fe0-681">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="38fe0-682">Źródło usługi Azure Data Lake Store w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-683">Jeśli dane są kopiowane z usługi Azure Data Lake Store, ustaw **typ źródła** działania kopiowania do **AzureDataLakeStoreSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-683">If you are copying data from an Azure Data Lake Store, set the **source type** of the copy activity to **AzureDataLakeStoreSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="38fe0-684">**AzureDataLakeStoreSource** obsługuje następujące właściwości **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-684">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="38fe0-685">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-685">Property</span></span> | <span data-ttu-id="38fe0-686">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-686">Description</span></span> | <span data-ttu-id="38fe0-687">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-687">Allowed values</span></span> | <span data-ttu-id="38fe0-688">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-689">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="38fe0-689">recursive</span></span> |<span data-ttu-id="38fe0-690">Wskazuje, czy dane są odczytywane rekursywnie z folderów sub lub tylko określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-690">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="38fe0-691">TRUE, False (wartość domyślna)</span><span class="sxs-lookup"><span data-stu-id="38fe0-691">True (default value), False</span></span> |<span data-ttu-id="38fe0-692">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="38fe0-693">Przykład: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="38fe0-693">Example: AzureDataLakeStoreSource</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-694">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="38fe0-695">Obiekt Sink usługi Azure Data Lake Store w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="38fe0-696">Jeśli dane są kopiowane do usługi Azure Data Lake Store, ustaw **typu sink** działania kopiowania do **AzureDataLakeStoreSink**i określ następujące właściwości w **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-696">If you are copying data to an Azure Data Lake Store, set the **sink type** of the copy activity to **AzureDataLakeStoreSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="38fe0-697">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-697">Property</span></span> | <span data-ttu-id="38fe0-698">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-698">Description</span></span> | <span data-ttu-id="38fe0-699">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-699">Allowed values</span></span> | <span data-ttu-id="38fe0-700">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="38fe0-701">copyBehavior</span></span> |<span data-ttu-id="38fe0-702">Określa zachowanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-702">Specifies the copy behavior.</span></span> |<span data-ttu-id="38fe0-703"><b>PreserveHierarchy</b>: zachowuje hierarchię plików w folderze docelowym.</span><span class="sxs-lookup"><span data-stu-id="38fe0-703"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="38fe0-704">Względna ścieżka pliku źródłowego do folderu źródłowego jest taka sama jak ścieżka względna docelowego pliku do folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-704">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="38fe0-705"><b>FlattenHierarchy</b>: wszystkie pliki z folderu źródłowego są tworzone w pierwszy poziom folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-705"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="38fe0-706">Pliki docelowe są tworzone automatycznie wygeneruje nazwę.</span><span class="sxs-lookup"><span data-stu-id="38fe0-706">The target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="38fe0-707"><b>MergeFiles</b>: scala wszystkie pliki z folderu źródłowego do jednego pliku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-707"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="38fe0-708">Jeśli zostanie określona nazwa pliku/obiektów Blob, nazwa scalony plik jest określona nazwa; w przeciwnym razie będzie nazwa pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-708">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="38fe0-709">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="38fe0-710">Przykład: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="38fe0-710">Example: AzureDataLakeStoreSink</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-711">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="38fe0-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="38fe0-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="38fe0-713">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-713">Linked service</span></span>
<span data-ttu-id="38fe0-714">Aby zdefiniować bazy danych Azure rozwiązania Cosmos połączonej usługi, ustaw **typu** połączonej usługi, aby **DocumentDb**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-714">To define an Azure Cosmos DB linked service, set the **type** of the linked service to **DocumentDb**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-715">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="38fe0-715">**Property**</span></span> | <span data-ttu-id="38fe0-716">**Opis**</span><span class="sxs-lookup"><span data-stu-id="38fe0-716">**Description**</span></span> | <span data-ttu-id="38fe0-717">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="38fe0-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-718">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="38fe0-718">connectionString</span></span> |<span data-ttu-id="38fe0-719">Określ informacje potrzebne do łączenia z bazą danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="38fe0-719">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="38fe0-720">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-721">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-721">Example</span></span>

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
<span data-ttu-id="38fe0-722">Aby uzyskać więcej informacji, zobacz [łącznika Azure DB rozwiązania Cosmos](data-factory-azure-documentdb-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="38fe0-723">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-723">Dataset</span></span>
<span data-ttu-id="38fe0-724">Aby zdefiniować bazy danych Azure rozwiązania Cosmos zestawu danych, ustaw **typu** zestawu danych do **DocumentDbCollection**, a następnie określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-724">To define an Azure Cosmos DB dataset, set the **type** of the dataset to **DocumentDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-725">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="38fe0-725">**Property**</span></span> | <span data-ttu-id="38fe0-726">**Opis**</span><span class="sxs-lookup"><span data-stu-id="38fe0-726">**Description**</span></span> | <span data-ttu-id="38fe0-727">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="38fe0-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-728">CollectionName</span><span class="sxs-lookup"><span data-stu-id="38fe0-728">collectionName</span></span> |<span data-ttu-id="38fe0-729">Nazwa kolekcji bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="38fe0-729">Name of the Azure Cosmos DB collection.</span></span> |<span data-ttu-id="38fe0-730">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-731">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-731">Example</span></span>

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="38fe0-732">Aby uzyskać więcej informacji, zobacz [łącznika Azure DB rozwiązania Cosmos](data-factory-azure-documentdb-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="38fe0-733">Źródło kolekcji Azure rozwiązania Cosmos bazy danych w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-734">Jeśli dane są kopiowane z bazy danych Azure rozwiązania Cosmos, ustaw **typ źródła** działania kopiowania do **DocumentDbCollectionSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-734">If you are copying data from an Azure Cosmos DB, set the **source type** of the copy activity to **DocumentDbCollectionSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="38fe0-735">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="38fe0-735">**Property**</span></span> | <span data-ttu-id="38fe0-736">**Opis**</span><span class="sxs-lookup"><span data-stu-id="38fe0-736">**Description**</span></span> | <span data-ttu-id="38fe0-737">**Dozwolone wartości**</span><span class="sxs-lookup"><span data-stu-id="38fe0-737">**Allowed values**</span></span> | <span data-ttu-id="38fe0-738">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="38fe0-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-739">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-739">query</span></span> |<span data-ttu-id="38fe0-740">Określ zapytanie można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-740">Specify the query to read data.</span></span> |<span data-ttu-id="38fe0-741">Wyślij zapytanie do ciągu obsługuje bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="38fe0-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="38fe0-742">Przykład:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="38fe0-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="38fe0-743">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-743">No</span></span> <br/><br/><span data-ttu-id="38fe0-744">Jeśli nie zostanie określony, która zostanie wykonana instrukcja SQL:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="38fe0-744">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="38fe0-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="38fe0-745">nestingSeparator</span></span> |<span data-ttu-id="38fe0-746">Znaki specjalne w celu wskazania, że dokument jest zagnieżdżony</span><span class="sxs-lookup"><span data-stu-id="38fe0-746">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="38fe0-747">Dowolny znak.</span><span class="sxs-lookup"><span data-stu-id="38fe0-747">Any character.</span></span> <br/><br/><span data-ttu-id="38fe0-748">Azure DB rozwiązania Cosmos jest magazynem NoSQL dla dokumentów JSON, których struktury zagnieżdżone są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="38fe0-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="38fe0-749">Fabryka danych Azure umożliwia użytkownikowi oznaczenia hierarchii za pomocą nestingSeparator, czyli "."</span><span class="sxs-lookup"><span data-stu-id="38fe0-749">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="38fe0-750">w powyższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="38fe0-750">in the above examples.</span></span> <span data-ttu-id="38fe0-751">Z separatorem, działanie kopiowania spowoduje wygenerowanie obiektu "Name" o trzy elementy podrzędne elementy najpierw drugie imię i nazwisko, zgodnie z "Name.First", "Name.Middle" i "Name.Last" w definicji tabeli.</span><span class="sxs-lookup"><span data-stu-id="38fe0-751">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="38fe0-752">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-753">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-753">Example</span></span>

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="38fe0-754">Obiekt Sink kolekcji bazy danych Azure rozwiązania Cosmos w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="38fe0-755">Jeśli dane są kopiowane do bazy danych Azure rozwiązania Cosmos, ustaw **typu sink** działania kopiowania do **DocumentDbCollectionSink**i określ następujące właściwości w **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-755">If you are copying data to Azure Cosmos DB, set the **sink type** of the copy activity to **DocumentDbCollectionSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="38fe0-756">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="38fe0-756">**Property**</span></span> | <span data-ttu-id="38fe0-757">**Opis**</span><span class="sxs-lookup"><span data-stu-id="38fe0-757">**Description**</span></span> | <span data-ttu-id="38fe0-758">**Dozwolone wartości**</span><span class="sxs-lookup"><span data-stu-id="38fe0-758">**Allowed values**</span></span> | <span data-ttu-id="38fe0-759">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="38fe0-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="38fe0-760">nestingSeparator</span></span> |<span data-ttu-id="38fe0-761">Wymagany jest znak specjalny w nazwa kolumny źródłowej, aby wskazać zagnieżdżonych dokumentu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-761">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="38fe0-762">Na przykład powyżej: `Name.First` w danych wyjściowych tabeli tworzy następującą strukturę JSON w dokumencie rozwiązania Cosmos bazy danych:</span><span class="sxs-lookup"><span data-stu-id="38fe0-762">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="38fe0-763">"Nazwa": {</span><span class="sxs-lookup"><span data-stu-id="38fe0-763">"Name": {</span></span><br/>    <span data-ttu-id="38fe0-764">"Pierwszy": "Jan"</span><span class="sxs-lookup"><span data-stu-id="38fe0-764">"First": "John"</span></span><br/><span data-ttu-id="38fe0-765">},</span><span class="sxs-lookup"><span data-stu-id="38fe0-765">},</span></span> |<span data-ttu-id="38fe0-766">Znak używany do rozdzielania poziomów zagnieżdżenia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-766">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="38fe0-767">Wartość domyślna to `.` (kropką).</span><span class="sxs-lookup"><span data-stu-id="38fe0-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="38fe0-768">Znak używany do rozdzielania poziomów zagnieżdżenia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-768">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="38fe0-769">Wartość domyślna to `.` (kropką).</span><span class="sxs-lookup"><span data-stu-id="38fe0-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="38fe0-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="38fe0-770">writeBatchSize</span></span> |<span data-ttu-id="38fe0-771">Liczba równoległych żądań do usługi Azure DB rozwiązania Cosmos w celu utworzenia dokumentów.</span><span class="sxs-lookup"><span data-stu-id="38fe0-771">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="38fe0-772">Aby precyzyjnie zdefiniować wydajność podczas kopiowania danych z bazy danych rozwiązania Cosmos Azure przy użyciu tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-772">You can fine-tune the performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="38fe0-773">Wraz ze zwiększeniem writeBatchSize, ponieważ więcej żądań równoległych do bazy danych Azure rozwiązania Cosmos są wysyłane, może spodziewać się lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="38fe0-773">You can expect a better performance when you increase writeBatchSize because more parallel requests to Azure Cosmos DB are sent.</span></span> <span data-ttu-id="38fe0-774">Jednak należy unikać ograniczania przepustowości, który może zgłaszać komunikat o błędzie: "jest duża szybkość żądania".</span><span class="sxs-lookup"><span data-stu-id="38fe0-774">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="38fe0-775">Ograniczanie zadecyduje o wiele czynników, w tym rozmiar dokumentów, liczbę dokumentów, indeksowania zasady kolekcji docelowej, itd. Dla operacji kopiowania umożliwiają lepsze kolekcji (na przykład S3) ma największą przepływność dostępne (2500 żądań jednostek na sekundę).</span><span class="sxs-lookup"><span data-stu-id="38fe0-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="38fe0-776">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="38fe0-776">Integer</span></span> |<span data-ttu-id="38fe0-777">Nie (domyślne: 5)</span><span class="sxs-lookup"><span data-stu-id="38fe0-777">No (default: 5)</span></span> |
| <span data-ttu-id="38fe0-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="38fe0-778">writeBatchTimeout</span></span> |<span data-ttu-id="38fe0-779">Poczekaj na ukończenie upłynie limit czasu operacji.</span><span class="sxs-lookup"><span data-stu-id="38fe0-779">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="38fe0-780">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="38fe0-780">timespan</span></span><br/><br/> <span data-ttu-id="38fe0-781">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="38fe0-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="38fe0-782">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-783">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-783">Example</span></span>

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

<span data-ttu-id="38fe0-784">Aby uzyskać więcej informacji, zobacz [łącznika Azure DB rozwiązania Cosmos](data-factory-azure-documentdb-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="38fe0-785">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="38fe0-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-786">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-786">Linked service</span></span>
<span data-ttu-id="38fe0-787">Aby zdefiniować bazy danych SQL Azure połączonej usługi, ustaw **typu** połączonej usługi, aby **AzureSqlDatabase**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-787">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-788">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-788">Property</span></span> | <span data-ttu-id="38fe0-789">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-789">Description</span></span> | <span data-ttu-id="38fe0-790">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-791">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="38fe0-791">connectionString</span></span> |<span data-ttu-id="38fe0-792">Podaj informacje wymagane do połączenia z wystąpieniem bazy danych SQL Azure dla właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="38fe0-792">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="38fe0-793">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-794">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-794">Example</span></span>
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="38fe0-795">Aby uzyskać więcej informacji, zobacz [Łącznik usług Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-796">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-796">Dataset</span></span>
<span data-ttu-id="38fe0-797">Aby zdefiniować zestawem danych usługi Azure SQL Database, ustaw **typu** zestawu danych do **AzureSqlTable**, a następnie określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-797">To define an Azure SQL Database dataset, set the **type** of the dataset to **AzureSqlTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-798">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-798">Property</span></span> | <span data-ttu-id="38fe0-799">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-799">Description</span></span> | <span data-ttu-id="38fe0-800">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-801">tableName</span><span class="sxs-lookup"><span data-stu-id="38fe0-801">tableName</span></span> |<span data-ttu-id="38fe0-802">Nazwa tabeli lub widoku w wystąpieniu bazy danych SQL Azure, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-802">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="38fe0-803">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-804">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-804">Example</span></span>

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="38fe0-805">Aby uzyskać więcej informacji, zobacz [Łącznik usług Azure SQL](data-factory-azure-sql-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="38fe0-806">Źródło SQL w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-807">Jeśli dane są kopiowane z bazy danych SQL Azure, ustaw **typ źródła** działania kopiowania do **SqlSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-807">If you are copying data from an Azure SQL Database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="38fe0-808">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-808">Property</span></span> | <span data-ttu-id="38fe0-809">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-809">Description</span></span> | <span data-ttu-id="38fe0-810">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-810">Allowed values</span></span> | <span data-ttu-id="38fe0-811">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-812">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="38fe0-812">sqlReaderQuery</span></span> |<span data-ttu-id="38fe0-813">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-813">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-814">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-814">SQL query string.</span></span> <span data-ttu-id="38fe0-815">Przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="38fe0-816">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-816">No</span></span> |
| <span data-ttu-id="38fe0-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="38fe0-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="38fe0-818">Nazwa procedury przechowywanej, która odczytuje dane z tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-818">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="38fe0-819">Nazwa procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-819">Name of the stored procedure.</span></span> |<span data-ttu-id="38fe0-820">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-820">No</span></span> |
| <span data-ttu-id="38fe0-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="38fe0-821">storedProcedureParameters</span></span> |<span data-ttu-id="38fe0-822">Parametry dla procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-822">Parameters for the stored procedure.</span></span> |<span data-ttu-id="38fe0-823">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="38fe0-823">Name/value pairs.</span></span> <span data-ttu-id="38fe0-824">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, nazwy i wielkość liter w wyrazie parametry procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-824">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="38fe0-825">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-826">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-826">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="38fe0-827">Aby uzyskać więcej informacji, zobacz [Łącznik usług Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="38fe0-828">Obiekt Sink SQL w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="38fe0-829">Jeśli dane są kopiowane do bazy danych SQL Azure, ustaw **typu sink** działania kopiowania do **SqlSink**i określ następujące właściwości w **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-829">If you are copying data to Azure SQL Database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="38fe0-830">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-830">Property</span></span> | <span data-ttu-id="38fe0-831">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-831">Description</span></span> | <span data-ttu-id="38fe0-832">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-832">Allowed values</span></span> | <span data-ttu-id="38fe0-833">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="38fe0-834">writeBatchTimeout</span></span> |<span data-ttu-id="38fe0-835">Czas na ukończenie zanim upłynie limit czasu operacji wstawiania wsadowego oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-835">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="38fe0-836">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="38fe0-836">timespan</span></span><br/><br/> <span data-ttu-id="38fe0-837">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="38fe0-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="38fe0-838">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-838">No</span></span> |
| <span data-ttu-id="38fe0-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="38fe0-839">writeBatchSize</span></span> |<span data-ttu-id="38fe0-840">Wstawia dane do tabeli SQL, gdy writeBatchSize osiągnie rozmiar buforu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-840">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="38fe0-841">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="38fe0-841">Integer (number of rows)</span></span> |<span data-ttu-id="38fe0-842">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="38fe0-842">No (default: 10000)</span></span> |
| <span data-ttu-id="38fe0-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="38fe0-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="38fe0-844">Określ kwerendę dla działania kopiowania do wykonania w taki sposób, że dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="38fe0-844">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="38fe0-845">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-845">A query statement.</span></span> |<span data-ttu-id="38fe0-846">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-846">No</span></span> |
| <span data-ttu-id="38fe0-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="38fe0-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="38fe0-848">Określ nazwę kolumny dla aktywności kopiowania wypełnić automatycznie generowane wycinek identyfikator, który służy do oczyszczania danych określonego wycinek czas ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-848">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="38fe0-849">Nazwa kolumny kolumnę o typie danych binary(32).</span><span class="sxs-lookup"><span data-stu-id="38fe0-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="38fe0-850">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-850">No</span></span> |
| <span data-ttu-id="38fe0-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="38fe0-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="38fe0-852">Nazwa procedury składowanej danych upserts (aktualizacje/INSERT) do tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-852">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="38fe0-853">Nazwa procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-853">Name of the stored procedure.</span></span> |<span data-ttu-id="38fe0-854">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-854">No</span></span> |
| <span data-ttu-id="38fe0-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="38fe0-855">storedProcedureParameters</span></span> |<span data-ttu-id="38fe0-856">Parametry dla procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-856">Parameters for the stored procedure.</span></span> |<span data-ttu-id="38fe0-857">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="38fe0-857">Name/value pairs.</span></span> <span data-ttu-id="38fe0-858">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, nazwy i wielkość liter w wyrazie parametry procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-858">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="38fe0-859">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-859">No</span></span> |
| <span data-ttu-id="38fe0-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="38fe0-860">sqlWriterTableType</span></span> |<span data-ttu-id="38fe0-861">Określ nazwę typu tabeli do użycia w procedurze składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-861">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="38fe0-862">Działanie kopiowania udostępnia dane jest przenoszony w tabeli tymczasowej o tym typie tabeli.</span><span class="sxs-lookup"><span data-stu-id="38fe0-862">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="38fe0-863">Kod procedury składowanej można następnie scalić dane są kopiowane z istniejącymi danymi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-863">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="38fe0-864">Nazwa typu tabeli.</span><span class="sxs-lookup"><span data-stu-id="38fe0-864">A table type name.</span></span> |<span data-ttu-id="38fe0-865">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-866">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-866">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-867">Aby uzyskać więcej informacji, zobacz [Łącznik usług Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="38fe0-868">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="38fe0-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-869">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-869">Linked service</span></span>
<span data-ttu-id="38fe0-870">Aby zdefiniować Azure SQL Data Warehouse połączonej usługi, ustaw **typu** połączonej usługi, aby **AzureSqlDW**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-870">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-871">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-871">Property</span></span> | <span data-ttu-id="38fe0-872">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-872">Description</span></span> | <span data-ttu-id="38fe0-873">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-874">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="38fe0-874">connectionString</span></span> |<span data-ttu-id="38fe0-875">Podaj informacje wymagane do połączenia z wystąpieniem usługi Azure SQL Data Warehouse właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="38fe0-875">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="38fe0-876">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="38fe0-877">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-877">Example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="38fe0-878">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-879">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-879">Dataset</span></span>
<span data-ttu-id="38fe0-880">Aby zdefiniować zestawem danych usługi Azure SQL Data Warehouse, ustaw **typu** zestawu danych do **AzureSqlDWTable**, a następnie określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-880">To define an Azure SQL Data Warehouse dataset, set the **type** of the dataset to **AzureSqlDWTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-881">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-881">Property</span></span> | <span data-ttu-id="38fe0-882">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-882">Description</span></span> | <span data-ttu-id="38fe0-883">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-884">tableName</span><span class="sxs-lookup"><span data-stu-id="38fe0-884">tableName</span></span> |<span data-ttu-id="38fe0-885">Nazwa tabeli lub widoku w bazie danych Azure SQL Data Warehouse, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-885">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="38fe0-886">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-887">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-887">Example</span></span>

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="38fe0-888">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="38fe0-889">Źródła magazynu danych SQL w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-890">Jeśli dane są kopiowane z usługi Azure SQL Data Warehouse, ustaw **typ źródła** działania kopiowania do **SqlDWSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-890">If you are copying data from Azure SQL Data Warehouse, set the **source type** of the copy activity to **SqlDWSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="38fe0-891">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-891">Property</span></span> | <span data-ttu-id="38fe0-892">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-892">Description</span></span> | <span data-ttu-id="38fe0-893">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-893">Allowed values</span></span> | <span data-ttu-id="38fe0-894">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-895">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="38fe0-895">sqlReaderQuery</span></span> |<span data-ttu-id="38fe0-896">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-896">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-897">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-897">SQL query string.</span></span> <span data-ttu-id="38fe0-898">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="38fe0-899">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-899">No</span></span> |
| <span data-ttu-id="38fe0-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="38fe0-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="38fe0-901">Nazwa procedury przechowywanej, która odczytuje dane z tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-901">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="38fe0-902">Nazwa procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-902">Name of the stored procedure.</span></span> |<span data-ttu-id="38fe0-903">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-903">No</span></span> |
| <span data-ttu-id="38fe0-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="38fe0-904">storedProcedureParameters</span></span> |<span data-ttu-id="38fe0-905">Parametry dla procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-905">Parameters for the stored procedure.</span></span> |<span data-ttu-id="38fe0-906">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="38fe0-906">Name/value pairs.</span></span> <span data-ttu-id="38fe0-907">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, nazwy i wielkość liter w wyrazie parametry procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-907">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="38fe0-908">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-909">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-909">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-910">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="38fe0-911">Ujścia magazynu danych SQL w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="38fe0-912">Jeśli dane są kopiowane do usługi Azure SQL Data Warehouse, ustaw **typu sink** działania kopiowania do **SqlDWSink**i określ następujące właściwości w **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-912">If you are copying data to Azure SQL Data Warehouse, set the **sink type** of the copy activity to **SqlDWSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="38fe0-913">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-913">Property</span></span> | <span data-ttu-id="38fe0-914">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-914">Description</span></span> | <span data-ttu-id="38fe0-915">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-915">Allowed values</span></span> | <span data-ttu-id="38fe0-916">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="38fe0-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="38fe0-918">Określ kwerendę dla działania kopiowania do wykonania w taki sposób, że dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="38fe0-918">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="38fe0-919">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-919">A query statement.</span></span> |<span data-ttu-id="38fe0-920">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-920">No</span></span> |
| <span data-ttu-id="38fe0-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="38fe0-921">allowPolyBase</span></span> |<span data-ttu-id="38fe0-922">Wskazuje, czy do użycia zamiast mechanizmu BULKINSERT PolyBase (jeśli jest to wymagane).</span><span class="sxs-lookup"><span data-stu-id="38fe0-922">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="38fe0-923">**Przy użyciu programu PolyBase jest zalecanym sposobem ładowanie danych do usługi SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="38fe0-923">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="38fe0-924">True</span><span class="sxs-lookup"><span data-stu-id="38fe0-924">True</span></span> <br/><span data-ttu-id="38fe0-925">Wartość FAŁSZ (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="38fe0-925">False (default)</span></span> |<span data-ttu-id="38fe0-926">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-926">No</span></span> |
| <span data-ttu-id="38fe0-927">Usługi</span><span class="sxs-lookup"><span data-stu-id="38fe0-927">polyBaseSettings</span></span> |<span data-ttu-id="38fe0-928">Grupy właściwości, które można określić, kiedy **allowPolybase** właściwość jest ustawiona na **true**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-928">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="38fe0-929">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-929">No</span></span> |
| <span data-ttu-id="38fe0-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="38fe0-930">rejectValue</span></span> |<span data-ttu-id="38fe0-931">Określa liczbę lub odsetek wierszy, które można odrzucić przed zapytanie nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="38fe0-931">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="38fe0-932">Dowiedz się więcej o opcjach Odrzuć PolyBase **argumenty** sekcji [Tworzenie tabeli zewnętrznej (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-932">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="38fe0-933">0 (domyślnie), 1, 2...</span><span class="sxs-lookup"><span data-stu-id="38fe0-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="38fe0-934">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-934">No</span></span> |
| <span data-ttu-id="38fe0-935">dla właściwości rejectType</span><span class="sxs-lookup"><span data-stu-id="38fe0-935">rejectType</span></span> |<span data-ttu-id="38fe0-936">Określa, czy opcja rejectValue jest określona jako wartość literału lub wartość procentowa.</span><span class="sxs-lookup"><span data-stu-id="38fe0-936">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="38fe0-937">Wartość (ustawienie domyślne), wartość procentowa</span><span class="sxs-lookup"><span data-stu-id="38fe0-937">Value (default), Percentage</span></span> |<span data-ttu-id="38fe0-938">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-938">No</span></span> |
| <span data-ttu-id="38fe0-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="38fe0-939">rejectSampleValue</span></span> |<span data-ttu-id="38fe0-940">Określa liczbę wierszy do pobrania przed PolyBase ponownie oblicza procent odrzuconych wierszy.</span><span class="sxs-lookup"><span data-stu-id="38fe0-940">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="38fe0-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="38fe0-941">1, 2, …</span></span> |<span data-ttu-id="38fe0-942">Tak, jeśli **dla właściwości rejectType** jest **procent**</span><span class="sxs-lookup"><span data-stu-id="38fe0-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="38fe0-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="38fe0-943">useTypeDefault</span></span> |<span data-ttu-id="38fe0-944">Określa sposób obsługi brakujących wartości w rozdzielane pliki tekstowe, jeśli PolyBase pobiera dane z pliku tekstowego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-944">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="38fe0-945">Dowiedz się więcej o tej właściwości z sekcji argumenty w [utworzyć EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="38fe0-945">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="38fe0-946">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="38fe0-946">True, False (default)</span></span> |<span data-ttu-id="38fe0-947">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-947">No</span></span> |
| <span data-ttu-id="38fe0-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="38fe0-948">writeBatchSize</span></span> |<span data-ttu-id="38fe0-949">Wstawia dane do tabeli SQL, gdy writeBatchSize osiągnie rozmiar buforu</span><span class="sxs-lookup"><span data-stu-id="38fe0-949">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="38fe0-950">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="38fe0-950">Integer (number of rows)</span></span> |<span data-ttu-id="38fe0-951">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="38fe0-951">No (default: 10000)</span></span> |
| <span data-ttu-id="38fe0-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="38fe0-952">writeBatchTimeout</span></span> |<span data-ttu-id="38fe0-953">Czas na ukończenie zanim upłynie limit czasu operacji wstawiania wsadowego oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-953">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="38fe0-954">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="38fe0-954">timespan</span></span><br/><br/> <span data-ttu-id="38fe0-955">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="38fe0-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="38fe0-956">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-957">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-957">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-958">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="38fe0-959">Azure Search</span><span class="sxs-lookup"><span data-stu-id="38fe0-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-960">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-960">Linked service</span></span>
<span data-ttu-id="38fe0-961">Aby zdefiniować usługi Azure Search połączonej usługi, ustaw **typu** połączonej usługi, aby **AzureSearch**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-961">To define an Azure Search linked service, set the **type** of the linked service to **AzureSearch**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-962">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-962">Property</span></span> | <span data-ttu-id="38fe0-963">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-963">Description</span></span> | <span data-ttu-id="38fe0-964">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="38fe0-965">adres URL</span><span class="sxs-lookup"><span data-stu-id="38fe0-965">url</span></span> | <span data-ttu-id="38fe0-966">Adres URL dla usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="38fe0-966">URL for the Azure Search service.</span></span> | <span data-ttu-id="38fe0-967">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-967">Yes</span></span> |
| <span data-ttu-id="38fe0-968">key</span><span class="sxs-lookup"><span data-stu-id="38fe0-968">key</span></span> | <span data-ttu-id="38fe0-969">Klucz administratora dla usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="38fe0-969">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="38fe0-970">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-971">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-971">Example</span></span>

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="38fe0-972">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Search](data-factory-azure-search-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="38fe0-973">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-973">Dataset</span></span>
<span data-ttu-id="38fe0-974">Aby zdefiniować zestawem danych usługi Azure Search, ustaw **typu** zestawu danych do **AzureSearchIndex**, a następnie określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-974">To define an Azure Search dataset, set the **type** of the dataset to **AzureSearchIndex**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-975">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-975">Property</span></span> | <span data-ttu-id="38fe0-976">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-976">Description</span></span> | <span data-ttu-id="38fe0-977">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="38fe0-978">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-978">type</span></span> | <span data-ttu-id="38fe0-979">Właściwość type musi mieć ustawioną **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-979">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="38fe0-980">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-980">Yes</span></span> |
| <span data-ttu-id="38fe0-981">indexName</span><span class="sxs-lookup"><span data-stu-id="38fe0-981">indexName</span></span> | <span data-ttu-id="38fe0-982">Nazwa indeksu usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="38fe0-982">Name of the Azure Search index.</span></span> <span data-ttu-id="38fe0-983">Fabryki danych nie powoduje utworzenia indeksu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-983">Data Factory does not create the index.</span></span> <span data-ttu-id="38fe0-984">Indeks musi istnieć w usłudze Azure Search.</span><span class="sxs-lookup"><span data-stu-id="38fe0-984">The index must exist in Azure Search.</span></span> | <span data-ttu-id="38fe0-985">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-986">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-986">Example</span></span>

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

<span data-ttu-id="38fe0-987">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Search](data-factory-azure-search-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="38fe0-988">Obiekt Sink indeksu usługi Azure Search w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="38fe0-989">Jeśli dane są kopiowane do indeksu usługi Azure Search, ustaw **typu sink** działania kopiowania do **AzureSearchIndexSink**i określ następujące właściwości w **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-989">If you are copying data to an Azure Search index, set the **sink type** of the copy activity to **AzureSearchIndexSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="38fe0-990">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-990">Property</span></span> | <span data-ttu-id="38fe0-991">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-991">Description</span></span> | <span data-ttu-id="38fe0-992">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-992">Allowed values</span></span> | <span data-ttu-id="38fe0-993">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="38fe0-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="38fe0-994">WriteBehavior</span></span> | <span data-ttu-id="38fe0-995">Określa, czy należy scalić lub Zastąp, jeśli istnieje już dokument w indeksie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-995">Specifies whether to merge or replace when a document already exists in the index.</span></span> | <span data-ttu-id="38fe0-996">Merge (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="38fe0-996">Merge (default)</span></span><br/><span data-ttu-id="38fe0-997">Upload</span><span class="sxs-lookup"><span data-stu-id="38fe0-997">Upload</span></span>| <span data-ttu-id="38fe0-998">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-998">No</span></span> |
| <span data-ttu-id="38fe0-999">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="38fe0-999">WriteBatchSize</span></span> | <span data-ttu-id="38fe0-1000">Przekazywanie danych do indeksu usługi Azure Search, gdy writeBatchSize osiągnie rozmiar buforu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1000">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="38fe0-1001">1 do 1000.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1001">1 to 1,000.</span></span> <span data-ttu-id="38fe0-1002">Wartość domyślna to 1000.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1002">Default value is 1000.</span></span> | <span data-ttu-id="38fe0-1003">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1004">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1004">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-1005">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Search](data-factory-azure-search-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="38fe0-1006">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="38fe0-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-1007">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1007">Linked service</span></span>
<span data-ttu-id="38fe0-1008">Istnieją dwa typy połączonych usług: połączonej usługi magazynu Azure i połączonej usługi magazynu Azure sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="38fe0-1009">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="38fe0-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="38fe0-1010">Aby połączyć konto magazynu Azure do fabryki danych przy użyciu **klucz konta**, Utwórz połączoną usługą magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1010">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="38fe0-1011">Aby zdefiniować usługi Azure Storage połączonej usługi, ustaw **typu** połączonej usługi, aby **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1011">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="38fe0-1012">Następnie można określić następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1012">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-1013">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1013">Property</span></span> | <span data-ttu-id="38fe0-1014">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1014">Description</span></span> | <span data-ttu-id="38fe0-1015">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="38fe0-1016">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-1016">type</span></span> |<span data-ttu-id="38fe0-1017">Właściwość type musi mieć ustawioną: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="38fe0-1017">The type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="38fe0-1018">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1018">Yes</span></span> |
| <span data-ttu-id="38fe0-1019">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="38fe0-1019">connectionString</span></span> |<span data-ttu-id="38fe0-1020">Podaj informacje wymagane do połączenia z magazynem platformy Azure dla właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1020">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="38fe0-1021">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1021">Yes</span></span> |

<span data-ttu-id="38fe0-1022">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="38fe0-1022">**Example:**</span></span>  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="38fe0-1023">Połączonej usługi magazynu Azure SAS</span><span class="sxs-lookup"><span data-stu-id="38fe0-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="38fe0-1024">Usługa połączone SAS magazynu Azure umożliwia łączenie konto magazynu Azure do fabryki danych Azure za pomocą udostępnionego podpis dostępu (SAS).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1024">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="38fe0-1025">Fabryka danych zapewnia ograniczony/czas-powiązane z dostęp do określonego/all zasobów (kontener/obiektów blob) w magazynie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1025">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="38fe0-1026">Aby połączyć konto magazynu platformy Azure z fabryki danych przy użyciu sygnatura dostępu współdzielonego, Utwórz SAS magazynu Azure połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1026">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="38fe0-1027">Aby zdefiniować SAS magazynu Azure połączonej usługi, ustaw **typu** połączonej usługi, aby **element AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1027">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="38fe0-1028">Następnie można określić następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1028">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="38fe0-1029">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1029">Property</span></span> | <span data-ttu-id="38fe0-1030">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1030">Description</span></span> | <span data-ttu-id="38fe0-1031">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="38fe0-1032">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-1032">type</span></span> |<span data-ttu-id="38fe0-1033">Właściwość type musi mieć ustawioną: **element AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="38fe0-1033">The type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="38fe0-1034">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1034">Yes</span></span> |
| <span data-ttu-id="38fe0-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="38fe0-1035">sasUri</span></span> |<span data-ttu-id="38fe0-1036">Określ udostępniony URI sygnatury dostępu do zasobów usługi Azure Storage, takich jak obiektów blob, kontenera lub tabeli.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1036">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="38fe0-1037">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1037">Yes</span></span> |

<span data-ttu-id="38fe0-1038">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="38fe0-1038">**Example:**</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="38fe0-1039">Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika Azure Table Storage](data-factory-azure-table-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-1040">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1040">Dataset</span></span>
<span data-ttu-id="38fe0-1041">Aby zdefiniować zestaw tabel Azure, ustaw **typu** zestawu danych do **AzureTable**, a następnie określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1041">To define an Azure Table dataset, set the **type** of the dataset to **AzureTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-1042">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1042">Property</span></span> | <span data-ttu-id="38fe0-1043">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1043">Description</span></span> | <span data-ttu-id="38fe0-1044">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1045">tableName</span></span> |<span data-ttu-id="38fe0-1046">Nazwa tabeli w wystąpieniu bazy danych w tabeli platformy Azure, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1046">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="38fe0-1047">Tak.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1047">Yes.</span></span> <span data-ttu-id="38fe0-1048">W przypadku tableName bez azureTableSourceQuery wszystkie rekordy z tabeli są kopiowane do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1048">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="38fe0-1049">Jeśli określono również azureTableSourceQuery, rekordy z tabeli, która spełnia zapytania są kopiowane do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1049">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1050">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1050">Example</span></span>

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="38fe0-1051">Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika Azure Table Storage](data-factory-azure-table-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="38fe0-1052">Źródło tabeli platformy Azure w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1053">Jeśli dane są kopiowane z magazynu tabel Azure, ustaw **typ źródła** działania kopiowania do **AzureTableSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1053">If you are copying data from Azure Table Storage, set the **source type** of the copy activity to **AzureTableSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-1054">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1054">Property</span></span> | <span data-ttu-id="38fe0-1055">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1055">Description</span></span> | <span data-ttu-id="38fe0-1056">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1056">Allowed values</span></span> | <span data-ttu-id="38fe0-1057">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1058">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="38fe0-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="38fe0-1059">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1059">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-1060">Ciąg zapytania tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1060">Azure table query string.</span></span> <span data-ttu-id="38fe0-1061">Przykłady w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1061">See examples in the next section.</span></span> |<span data-ttu-id="38fe0-1062">Nie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1062">No.</span></span> <span data-ttu-id="38fe0-1063">W przypadku tableName bez azureTableSourceQuery wszystkie rekordy z tabeli są kopiowane do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1063">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="38fe0-1064">Jeśli określono również azureTableSourceQuery, rekordy z tabeli, która spełnia zapytania są kopiowane do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1064">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="38fe0-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="38fe0-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="38fe0-1066">Wskazuje, czy swallow wyjątek tabela nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1066">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="38fe0-1067">WARTOŚĆ TRUE</span><span class="sxs-lookup"><span data-stu-id="38fe0-1067">TRUE</span></span><br/><span data-ttu-id="38fe0-1068">WARTOŚĆ FALSE</span><span class="sxs-lookup"><span data-stu-id="38fe0-1068">FALSE</span></span> |<span data-ttu-id="38fe0-1069">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1070">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1070">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-1071">Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika Azure Table Storage](data-factory-azure-table-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="38fe0-1072">Obiekt Sink tabeli platformy Azure w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="38fe0-1073">Jeśli dane są kopiowane do magazynu tabel Azure, ustaw **typu sink** działania kopiowania do **AzureTableSink**i określ następujące właściwości w **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1073">If you are copying data to Azure Table Storage, set the **sink type** of the copy activity to **AzureTableSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="38fe0-1074">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1074">Property</span></span> | <span data-ttu-id="38fe0-1075">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1075">Description</span></span> | <span data-ttu-id="38fe0-1076">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1076">Allowed values</span></span> | <span data-ttu-id="38fe0-1077">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="38fe0-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="38fe0-1079">Domyślna wartość klucza partycji, które mogą być używane przez obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1079">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="38fe0-1080">Wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1080">A string value.</span></span> |<span data-ttu-id="38fe0-1081">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1081">No</span></span> |
| <span data-ttu-id="38fe0-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="38fe0-1083">Określ nazwę kolumny, których wartości są używane jako klucze partycji.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1083">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="38fe0-1084">Jeśli nie zostanie określony, AzureTableDefaultPartitionKeyValue jest używana jako klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="38fe0-1085">Nazwa kolumny.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1085">A column name.</span></span> |<span data-ttu-id="38fe0-1086">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1086">No</span></span> |
| <span data-ttu-id="38fe0-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="38fe0-1088">Określ nazwę kolumny, których wartości kolumn używanych jako klucz wiersza.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1088">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="38fe0-1089">Jeśli nie zostanie określony, użyj identyfikatora GUID dla każdego wiersza.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="38fe0-1090">Nazwa kolumny.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1090">A column name.</span></span> |<span data-ttu-id="38fe0-1091">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1091">No</span></span> |
| <span data-ttu-id="38fe0-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="38fe0-1092">azureTableInsertType</span></span> |<span data-ttu-id="38fe0-1093">Tryb do wstawiania danych do tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1093">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="38fe0-1094">Ta właściwość określa, czy wartości zastąpienia lub scalić zostać istniejących wierszy w tabeli wyników ze zgodnymi kluczami partycji i wiersza.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1094">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="38fe0-1095">Aby dowiedzieć się więcej na temat działania tych ustawień (scalania i Zastąp), zobacz [wstawienia lub scalania jednostki](https://msdn.microsoft.com/library/azure/hh452241.aspx) i [wstawienia lub Zastąp jednostki](https://msdn.microsoft.com/library/azure/hh452242.aspx) tematów.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1095">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="38fe0-1096">To ustawienie jest stosowane na poziomie wiersza, a nie na poziomie tabeli, a żadna z tych opcji usuwa wiersze w tabeli danych wyjściowych, które nie istnieją w danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1096">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="38fe0-1097">Merge (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1097">merge (default)</span></span><br/><span data-ttu-id="38fe0-1098">Zamień</span><span class="sxs-lookup"><span data-stu-id="38fe0-1098">replace</span></span> |<span data-ttu-id="38fe0-1099">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1099">No</span></span> |
| <span data-ttu-id="38fe0-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="38fe0-1100">writeBatchSize</span></span> |<span data-ttu-id="38fe0-1101">Wstawia dane do tabeli platformy Azure, gdy zostaje trafiony writeBatchSize lub writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1101">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="38fe0-1102">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1102">Integer (number of rows)</span></span> |<span data-ttu-id="38fe0-1103">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="38fe0-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="38fe0-1104">writeBatchTimeout</span></span> |<span data-ttu-id="38fe0-1105">Wstawia dane do tabeli platformy Azure, gdy zostaje trafiony writeBatchSize lub writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="38fe0-1105">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="38fe0-1106">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="38fe0-1106">timespan</span></span><br/><br/><span data-ttu-id="38fe0-1107">Przykład: "00:20:00" (20 minut)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="38fe0-1108">Nie (domyślnie magazynu klienta domyślny limit czasu wartość 90 s)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1108">No (Default to storage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1109">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1109">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="38fe0-1110">Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika Azure Table Storage](data-factory-azure-table-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="38fe0-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="38fe0-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-1112">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1112">Linked service</span></span>
<span data-ttu-id="38fe0-1113">Aby zdefiniować Redshift Amazon połączonej usługi, ustaw **typu** połączonej usługi, aby **AmazonRedshift**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1113">To define an Amazon Redshift linked service, set the **type** of the linked service to **AmazonRedshift**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-1114">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1114">Property</span></span> | <span data-ttu-id="38fe0-1115">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1115">Description</span></span> | <span data-ttu-id="38fe0-1116">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1117">serwer</span><span class="sxs-lookup"><span data-stu-id="38fe0-1117">server</span></span> |<span data-ttu-id="38fe0-1118">IP adres lub nazwę hosta serwera Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1118">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="38fe0-1119">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1119">Yes</span></span> |
| <span data-ttu-id="38fe0-1120">port</span><span class="sxs-lookup"><span data-stu-id="38fe0-1120">port</span></span> |<span data-ttu-id="38fe0-1121">Numer portu TCP używany przez serwer Amazon Redshift do nasłuchiwania dla połączeń klienta.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1121">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="38fe0-1122">Nie, wartość domyślna: 5439</span><span class="sxs-lookup"><span data-stu-id="38fe0-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="38fe0-1123">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1123">database</span></span> |<span data-ttu-id="38fe0-1124">Nazwa bazy danych Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1124">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="38fe0-1125">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1125">Yes</span></span> |
| <span data-ttu-id="38fe0-1126">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-1126">username</span></span> |<span data-ttu-id="38fe0-1127">Nazwa użytkownika, który ma dostęp do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1127">Name of user who has access to the database.</span></span> |<span data-ttu-id="38fe0-1128">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1128">Yes</span></span> |
| <span data-ttu-id="38fe0-1129">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-1129">password</span></span> |<span data-ttu-id="38fe0-1130">Hasło dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1130">Password for the user account.</span></span> |<span data-ttu-id="38fe0-1131">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1132">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1132">Example</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

<span data-ttu-id="38fe0-1133">Aby uzyskać więcej informacji, zobacz [łącznik Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-1134">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1134">Dataset</span></span>
<span data-ttu-id="38fe0-1135">Aby zdefiniować Amazon Redshift zestawu danych, ustaw **typu** zestawu danych do **RelationalTable**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1135">To define an Amazon Redshift dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-1136">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1136">Property</span></span> | <span data-ttu-id="38fe0-1137">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1137">Description</span></span> | <span data-ttu-id="38fe0-1138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1139">tableName</span></span> |<span data-ttu-id="38fe0-1140">Nazwa tabeli w bazie danych Amazon Redshift, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1140">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="38fe0-1141">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="38fe0-1142">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1142">Example</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="38fe0-1143">Aby uzyskać więcej informacji, zobacz [łącznik Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="38fe0-1144">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="38fe0-1145">Jeśli dane są kopiowane z Amazon Redshift, ustaw **typ źródła** działania kopiowania do **RelationalSource**, a następnie określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1145">If you are copying data from Amazon Redshift, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-1146">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1146">Property</span></span> | <span data-ttu-id="38fe0-1147">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1147">Description</span></span> | <span data-ttu-id="38fe0-1148">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1148">Allowed values</span></span> | <span data-ttu-id="38fe0-1149">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1150">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-1150">query</span></span> |<span data-ttu-id="38fe0-1151">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1151">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-1152">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1152">SQL query string.</span></span> <span data-ttu-id="38fe0-1153">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="38fe0-1154">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1155">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1155">Example</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="38fe0-1156">Aby uzyskać więcej informacji, zobacz [łącznik Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="38fe0-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="38fe0-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-1158">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1158">Linked service</span></span>
<span data-ttu-id="38fe0-1159">Aby zdefiniować IBM DB2 połączonej usługi, ustaw **typu** połączonej usługi, aby **OnPremisesDB2**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1159">To define an IBM DB2 linked service, set the **type** of the linked service to **OnPremisesDB2**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-1160">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1160">Property</span></span> | <span data-ttu-id="38fe0-1161">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1161">Description</span></span> | <span data-ttu-id="38fe0-1162">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1163">serwer</span><span class="sxs-lookup"><span data-stu-id="38fe0-1163">server</span></span> |<span data-ttu-id="38fe0-1164">Nazwa serwera bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1164">Name of the DB2 server.</span></span> |<span data-ttu-id="38fe0-1165">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1165">Yes</span></span> |
| <span data-ttu-id="38fe0-1166">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1166">database</span></span> |<span data-ttu-id="38fe0-1167">Nazwa bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1167">Name of the DB2 database.</span></span> |<span data-ttu-id="38fe0-1168">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1168">Yes</span></span> |
| <span data-ttu-id="38fe0-1169">Schemat</span><span class="sxs-lookup"><span data-stu-id="38fe0-1169">schema</span></span> |<span data-ttu-id="38fe0-1170">Nazwa schematu w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1170">Name of the schema in the database.</span></span> <span data-ttu-id="38fe0-1171">Nazwa schematu jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1171">The schema name is case-sensitive.</span></span> |<span data-ttu-id="38fe0-1172">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1172">No</span></span> |
| <span data-ttu-id="38fe0-1173">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-1173">authenticationType</span></span> |<span data-ttu-id="38fe0-1174">Typ uwierzytelniania używany do łączenia z bazą danych DB2.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1174">Type of authentication used to connect to the DB2 database.</span></span> <span data-ttu-id="38fe0-1175">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="38fe0-1176">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1176">Yes</span></span> |
| <span data-ttu-id="38fe0-1177">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-1177">username</span></span> |<span data-ttu-id="38fe0-1178">Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="38fe0-1179">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1179">No</span></span> |
| <span data-ttu-id="38fe0-1180">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-1180">password</span></span> |<span data-ttu-id="38fe0-1181">Określ hasło dla konta użytkownika, określone nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1181">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="38fe0-1182">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1182">No</span></span> |
| <span data-ttu-id="38fe0-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1183">gatewayName</span></span> |<span data-ttu-id="38fe0-1184">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną bazą danych DB2.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1184">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="38fe0-1185">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1186">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1186">Example</span></span>
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="38fe0-1187">Aby uzyskać więcej informacji, zobacz [łącznik IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="38fe0-1188">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1188">Dataset</span></span>
<span data-ttu-id="38fe0-1189">Aby zdefiniować bazy danych DB2 zestawu danych, ustaw **typu** zestawu danych do **RelationalTable**, a następnie określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1189">To define a DB2 dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="38fe0-1190">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1190">Property</span></span> | <span data-ttu-id="38fe0-1191">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1191">Description</span></span> | <span data-ttu-id="38fe0-1192">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1193">tableName</span></span> |<span data-ttu-id="38fe0-1194">Nazwa tabeli w wystąpieniu bazy danych DB2, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1194">Name of the table in the DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="38fe0-1195">Właściwość tableName jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1195">The tableName is case-sensitive.</span></span> |<span data-ttu-id="38fe0-1196">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="38fe0-1197">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1197">Example</span></span>
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="38fe0-1198">Aby uzyskać więcej informacji, zobacz [łącznik IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="38fe0-1199">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1200">Jeśli dane są kopiowane z IBM DB2, ustaw **typ źródła** działania kopiowania do **RelationalSource**, a następnie określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1200">If you are copying data from IBM DB2, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="38fe0-1201">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1201">Property</span></span> | <span data-ttu-id="38fe0-1202">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1202">Description</span></span> | <span data-ttu-id="38fe0-1203">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1203">Allowed values</span></span> | <span data-ttu-id="38fe0-1204">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1205">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-1205">query</span></span> |<span data-ttu-id="38fe0-1206">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1206">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-1207">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1207">SQL query string.</span></span> <span data-ttu-id="38fe0-1208">Na przykład: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="38fe0-1209">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1210">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1210">Example</span></span>
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="38fe0-1211">Aby uzyskać więcej informacji, zobacz [łącznik IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="38fe0-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="38fe0-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-1213">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1213">Linked service</span></span>
<span data-ttu-id="38fe0-1214">Aby zdefiniować MySQL połączonej usługi, ustaw **typu** połączonej usługi, aby **OnPremisesMySql**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1214">To define a MySQL linked service, set the **type** of the linked service to **OnPremisesMySql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-1215">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1215">Property</span></span> | <span data-ttu-id="38fe0-1216">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1216">Description</span></span> | <span data-ttu-id="38fe0-1217">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1218">serwer</span><span class="sxs-lookup"><span data-stu-id="38fe0-1218">server</span></span> |<span data-ttu-id="38fe0-1219">Nazwa serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1219">Name of the MySQL server.</span></span> |<span data-ttu-id="38fe0-1220">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1220">Yes</span></span> |
| <span data-ttu-id="38fe0-1221">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1221">database</span></span> |<span data-ttu-id="38fe0-1222">Nazwa bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1222">Name of the MySQL database.</span></span> |<span data-ttu-id="38fe0-1223">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1223">Yes</span></span> |
| <span data-ttu-id="38fe0-1224">Schemat</span><span class="sxs-lookup"><span data-stu-id="38fe0-1224">schema</span></span> |<span data-ttu-id="38fe0-1225">Nazwa schematu w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1225">Name of the schema in the database.</span></span> |<span data-ttu-id="38fe0-1226">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1226">No</span></span> |
| <span data-ttu-id="38fe0-1227">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-1227">authenticationType</span></span> |<span data-ttu-id="38fe0-1228">Typ uwierzytelniania używany do łączenia z bazą danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1228">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="38fe0-1229">Możliwe wartości to: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="38fe0-1230">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1230">Yes</span></span> |
| <span data-ttu-id="38fe0-1231">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-1231">username</span></span> |<span data-ttu-id="38fe0-1232">Określ nazwę użytkownika do połączenia z bazą danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1232">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="38fe0-1233">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1233">Yes</span></span> |
| <span data-ttu-id="38fe0-1234">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-1234">password</span></span> |<span data-ttu-id="38fe0-1235">Określ hasło dla określonego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1235">Specify password for the user account you specified.</span></span> |<span data-ttu-id="38fe0-1236">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1236">Yes</span></span> |
| <span data-ttu-id="38fe0-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1237">gatewayName</span></span> |<span data-ttu-id="38fe0-1238">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną bazą danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1238">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="38fe0-1239">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1240">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1240">Example</span></span>

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

<span data-ttu-id="38fe0-1241">Aby uzyskać więcej informacji, zobacz [łącznika MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-1242">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1242">Dataset</span></span>
<span data-ttu-id="38fe0-1243">Aby zdefiniować zestawu danych MySQL, ustaw **typu** zestawu danych do **RelationalTable**, a następnie określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1243">To define a MySQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-1244">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1244">Property</span></span> | <span data-ttu-id="38fe0-1245">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1245">Description</span></span> | <span data-ttu-id="38fe0-1246">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1247">tableName</span></span> |<span data-ttu-id="38fe0-1248">Nazwa tabeli w wystąpieniu bazy danych MySQL, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1248">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="38fe0-1249">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1250">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1250">Example</span></span>

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="38fe0-1251">Aby uzyskać więcej informacji, zobacz [łącznika MySQL](data-factory-onprem-mysql-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="38fe0-1252">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1253">Jeśli dane są kopiowane z bazy danych MySQL, ustaw **typ źródła** działania kopiowania do **RelationalSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1253">If you are copying data from a MySQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="38fe0-1254">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1254">Property</span></span> | <span data-ttu-id="38fe0-1255">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1255">Description</span></span> | <span data-ttu-id="38fe0-1256">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1256">Allowed values</span></span> | <span data-ttu-id="38fe0-1257">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1258">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-1258">query</span></span> |<span data-ttu-id="38fe0-1259">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1259">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-1260">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1260">SQL query string.</span></span> <span data-ttu-id="38fe0-1261">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="38fe0-1262">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="38fe0-1263">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1263">Example</span></span>
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="38fe0-1264">Aby uzyskać więcej informacji, zobacz [łącznika MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="38fe0-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="38fe0-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="38fe0-1266">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1266">Linked service</span></span>
<span data-ttu-id="38fe0-1267">Aby zdefiniować Oracle połączonej usługi, ustaw **typu** połączonej usługi, aby **OnPremisesOracle**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1267">To define an Oracle linked service, set the **type** of the linked service to **OnPremisesOracle**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-1268">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1268">Property</span></span> | <span data-ttu-id="38fe0-1269">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1269">Description</span></span> | <span data-ttu-id="38fe0-1270">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="38fe0-1271">driverType</span></span> | <span data-ttu-id="38fe0-1272">Określ sterowniku można skopiować danych z/do bazy danych programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1272">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="38fe0-1273">Dozwolone wartości to **Microsoft** lub **ODP** (ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="38fe0-1274">Zobacz [obsługiwanych wersji i instalacji](#supported-versions-and-installation) sekcji Szczegóły sterownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="38fe0-1275">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1275">No</span></span> |
| <span data-ttu-id="38fe0-1276">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="38fe0-1276">connectionString</span></span> | <span data-ttu-id="38fe0-1277">Podaj informacje wymagane do połączenia z wystąpieniem bazy danych programu Oracle dla właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1277">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="38fe0-1278">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1278">Yes</span></span> |
| <span data-ttu-id="38fe0-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1279">gatewayName</span></span> | <span data-ttu-id="38fe0-1280">Nazwa bramy, czy jest używany do łączenia się z serwerem Oracle lokalnej</span><span class="sxs-lookup"><span data-stu-id="38fe0-1280">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="38fe0-1281">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1282">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1282">Example</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="38fe0-1283">Aby uzyskać więcej informacji, zobacz [łącznika Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="38fe0-1284">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1284">Dataset</span></span>
<span data-ttu-id="38fe0-1285">Aby zdefiniować zestaw danych Oracle, ustaw **typu** zestawu danych do **OracleTable**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1285">To define an Oracle dataset, set the **type** of the dataset to **OracleTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-1286">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1286">Property</span></span> | <span data-ttu-id="38fe0-1287">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1287">Description</span></span> | <span data-ttu-id="38fe0-1288">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1289">tableName</span></span> |<span data-ttu-id="38fe0-1290">Nazwa tabeli w bazie danych programu Oracle, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1290">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="38fe0-1291">Nie (Jeśli **oracleReaderQuery** z **OracleSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1292">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1292">Example</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="38fe0-1293">Aby uzyskać więcej informacji, zobacz [łącznika Oracle](data-factory-onprem-oracle-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="38fe0-1294">Oracle źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1295">Jeśli dane są kopiowane z bazy danych Oracle, ustaw **typ źródła** działania kopiowania do **OracleSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1295">If you are copying data from an Oracle database, set the **source type** of the copy activity to **OracleSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-1296">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1296">Property</span></span> | <span data-ttu-id="38fe0-1297">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1297">Description</span></span> | <span data-ttu-id="38fe0-1298">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1298">Allowed values</span></span> | <span data-ttu-id="38fe0-1299">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="38fe0-1300">oracleReaderQuery</span></span> |<span data-ttu-id="38fe0-1301">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1301">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-1302">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1302">SQL query string.</span></span> <span data-ttu-id="38fe0-1303">Na przykład: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="38fe0-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="38fe0-1304">Jeśli nie zostanie określony, która zostanie wykonana instrukcja SQL:`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="38fe0-1304">If not specified, the SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="38fe0-1305">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1306">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1306">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-1307">Aby uzyskać więcej informacji, zobacz [łącznika Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="38fe0-1308">Obiekt Sink Oracle w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="38fe0-1309">Jeśli dane są kopiowane am bazą danych Oracle, ustaw **typu sink** działania kopiowania do **OracleSink**i określ następujące właściwości w **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1309">If you are copying data to am Oracle database, set the **sink type** of the copy activity to **OracleSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="38fe0-1310">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1310">Property</span></span> | <span data-ttu-id="38fe0-1311">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1311">Description</span></span> | <span data-ttu-id="38fe0-1312">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1312">Allowed values</span></span> | <span data-ttu-id="38fe0-1313">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="38fe0-1314">writeBatchTimeout</span></span> |<span data-ttu-id="38fe0-1315">Czas na ukończenie zanim upłynie limit czasu operacji wstawiania wsadowego oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1315">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="38fe0-1316">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="38fe0-1316">timespan</span></span><br/><br/> <span data-ttu-id="38fe0-1317">Przykład: 00:30:00 (30 minut).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="38fe0-1318">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1318">No</span></span> |
| <span data-ttu-id="38fe0-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="38fe0-1319">writeBatchSize</span></span> |<span data-ttu-id="38fe0-1320">Wstawia dane do tabeli SQL, gdy writeBatchSize osiągnie rozmiar buforu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1320">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="38fe0-1321">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1321">Integer (number of rows)</span></span> |<span data-ttu-id="38fe0-1322">Nie (domyślne: 100)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1322">No (default: 100)</span></span> |
| <span data-ttu-id="38fe0-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="38fe0-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="38fe0-1324">Określ kwerendę dla działania kopiowania do wykonania w taki sposób, że dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1324">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="38fe0-1325">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1325">A query statement.</span></span> |<span data-ttu-id="38fe0-1326">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1326">No</span></span> |
| <span data-ttu-id="38fe0-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="38fe0-1328">Określ nazwę kolumny dla aktywności kopiowania wypełnić automatycznie generowane wycinek identyfikator, który służy do oczyszczania danych określonego wycinek czas ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1328">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="38fe0-1329">Nazwa kolumny kolumnę o typie danych binary(32).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="38fe0-1330">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1331">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1331">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="38fe0-1332">Aby uzyskać więcej informacji, zobacz [łącznika Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="38fe0-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="38fe0-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-1334">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1334">Linked service</span></span>
<span data-ttu-id="38fe0-1335">Aby zdefiniować PostgreSQL połączonej usługi, ustaw **typu** połączonej usługi, aby **OnPremisesPostgreSql**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1335">To define a PostgreSQL linked service, set the **type** of the linked service to **OnPremisesPostgreSql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-1336">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1336">Property</span></span> | <span data-ttu-id="38fe0-1337">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1337">Description</span></span> | <span data-ttu-id="38fe0-1338">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1339">serwer</span><span class="sxs-lookup"><span data-stu-id="38fe0-1339">server</span></span> |<span data-ttu-id="38fe0-1340">Nazwa serwera PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1340">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="38fe0-1341">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1341">Yes</span></span> |
| <span data-ttu-id="38fe0-1342">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1342">database</span></span> |<span data-ttu-id="38fe0-1343">Nazwa bazy danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1343">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="38fe0-1344">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1344">Yes</span></span> |
| <span data-ttu-id="38fe0-1345">Schemat</span><span class="sxs-lookup"><span data-stu-id="38fe0-1345">schema</span></span> |<span data-ttu-id="38fe0-1346">Nazwa schematu w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1346">Name of the schema in the database.</span></span> <span data-ttu-id="38fe0-1347">Nazwa schematu jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1347">The schema name is case-sensitive.</span></span> |<span data-ttu-id="38fe0-1348">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1348">No</span></span> |
| <span data-ttu-id="38fe0-1349">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-1349">authenticationType</span></span> |<span data-ttu-id="38fe0-1350">Typ uwierzytelniania używany do łączenia z bazą danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1350">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="38fe0-1351">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="38fe0-1352">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1352">Yes</span></span> |
| <span data-ttu-id="38fe0-1353">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-1353">username</span></span> |<span data-ttu-id="38fe0-1354">Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="38fe0-1355">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1355">No</span></span> |
| <span data-ttu-id="38fe0-1356">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-1356">password</span></span> |<span data-ttu-id="38fe0-1357">Określ hasło dla konta użytkownika, określone nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1357">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="38fe0-1358">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1358">No</span></span> |
| <span data-ttu-id="38fe0-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1359">gatewayName</span></span> |<span data-ttu-id="38fe0-1360">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną bazą danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1360">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="38fe0-1361">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1362">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1362">Example</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="38fe0-1363">Aby uzyskać więcej informacji, zobacz [łącznik PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="38fe0-1364">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1364">Dataset</span></span>
<span data-ttu-id="38fe0-1365">Aby zdefiniować zestawu danych PostgreSQL, ustaw **typu** zestawu danych do **RelationalTable**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1365">To define a PostgreSQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-1366">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1366">Property</span></span> | <span data-ttu-id="38fe0-1367">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1367">Description</span></span> | <span data-ttu-id="38fe0-1368">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1369">tableName</span></span> |<span data-ttu-id="38fe0-1370">Nazwa tabeli w wystąpieniu bazy danych PostgreSQL, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1370">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="38fe0-1371">Właściwość tableName jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1371">The tableName is case-sensitive.</span></span> |<span data-ttu-id="38fe0-1372">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1373">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1373">Example</span></span>
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="38fe0-1374">Aby uzyskać więcej informacji, zobacz [łącznik PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="38fe0-1375">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1376">Jeśli dane są kopiowane z bazy danych programu PostgreSQL, ustaw **typ źródła** działania kopiowania do **RelationalSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1376">If you are copying data from a PostgreSQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="38fe0-1377">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1377">Property</span></span> | <span data-ttu-id="38fe0-1378">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1378">Description</span></span> | <span data-ttu-id="38fe0-1379">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1379">Allowed values</span></span> | <span data-ttu-id="38fe0-1380">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1381">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-1381">query</span></span> |<span data-ttu-id="38fe0-1382">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1382">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-1383">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1383">SQL query string.</span></span> <span data-ttu-id="38fe0-1384">Na przykład: "zapytania": "Wybierz * z \"MySchema\".\" MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="38fe0-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="38fe0-1385">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1386">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1386">Example</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="38fe0-1387">Aby uzyskać więcej informacji, zobacz [łącznik PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="38fe0-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="38fe0-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="38fe0-1389">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1389">Linked service</span></span>
<span data-ttu-id="38fe0-1390">Aby zdefiniować SAP Business magazynu (BW) połączonej usługi, ustaw **typu** połączonej usługi, aby **SapBw**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1390">To define a SAP Business Warehouse (BW) linked service, set the **type** of the linked service to **SapBw**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="38fe0-1391">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1391">Property</span></span> | <span data-ttu-id="38fe0-1392">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1392">Description</span></span> | <span data-ttu-id="38fe0-1393">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1393">Allowed values</span></span> | <span data-ttu-id="38fe0-1394">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="38fe0-1395">serwer</span><span class="sxs-lookup"><span data-stu-id="38fe0-1395">server</span></span> | <span data-ttu-id="38fe0-1396">Nazwa serwera, na którym znajduje się wystąpienie programu SAP BW.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1396">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="38fe0-1397">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1397">string</span></span> | <span data-ttu-id="38fe0-1398">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1398">Yes</span></span>
<span data-ttu-id="38fe0-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="38fe0-1399">systemNumber</span></span> | <span data-ttu-id="38fe0-1400">Numer systemu systemu SAP BW.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1400">System number of the SAP BW system.</span></span> | <span data-ttu-id="38fe0-1401">Liczba dziesiętna dwucyfrowe reprezentowany jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="38fe0-1402">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1402">Yes</span></span>
<span data-ttu-id="38fe0-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="38fe0-1403">clientId</span></span> | <span data-ttu-id="38fe0-1404">Identyfikator klienta w systemie SAP W klienta.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1404">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="38fe0-1405">Trzycyfrowa liczba dziesiętna reprezentowany jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="38fe0-1406">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1406">Yes</span></span>
<span data-ttu-id="38fe0-1407">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-1407">username</span></span> | <span data-ttu-id="38fe0-1408">Nazwa użytkownika, który ma dostęp do serwera SAP</span><span class="sxs-lookup"><span data-stu-id="38fe0-1408">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="38fe0-1409">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1409">string</span></span> | <span data-ttu-id="38fe0-1410">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1410">Yes</span></span>
<span data-ttu-id="38fe0-1411">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-1411">password</span></span> | <span data-ttu-id="38fe0-1412">Hasło dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1412">Password for the user.</span></span> | <span data-ttu-id="38fe0-1413">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1413">string</span></span> | <span data-ttu-id="38fe0-1414">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1414">Yes</span></span>
<span data-ttu-id="38fe0-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1415">gatewayName</span></span> | <span data-ttu-id="38fe0-1416">Nazwa bramy, która powinna być używana do nawiązania połączenia lokalnego wystąpienia programu SAP BW usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1416">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="38fe0-1417">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1417">string</span></span> | <span data-ttu-id="38fe0-1418">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1418">Yes</span></span>
<span data-ttu-id="38fe0-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="38fe0-1419">encryptedCredential</span></span> | <span data-ttu-id="38fe0-1420">Ciąg zaszyfrowane poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1420">The encrypted credential string.</span></span> | <span data-ttu-id="38fe0-1421">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1421">string</span></span> | <span data-ttu-id="38fe0-1422">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="38fe0-1423">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1423">Example</span></span>

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="38fe0-1424">Aby uzyskać więcej informacji, zobacz [łącznika SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-1425">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1425">Dataset</span></span>
<span data-ttu-id="38fe0-1426">Aby zdefiniować programu SAP BW zestawu danych, ustaw **typu** zestawu danych do **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1426">To define a SAP BW dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="38fe0-1427">Nie ma żadnych właściwości specyficzne dla typu obsługiwane dla zestawu danych SAP BW typu **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1427">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="38fe0-1428">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1428">Example</span></span>

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="38fe0-1429">Aby uzyskać więcej informacji, zobacz [łącznika SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="38fe0-1430">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1431">Jeśli dane są kopiowane z SAP Business Warehouse, ustaw **typ źródła** działania kopiowania do **RelationalSource**, a następnie określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1431">If you are copying data from SAP Business Warehouse, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="38fe0-1432">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1432">Property</span></span> | <span data-ttu-id="38fe0-1433">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1433">Description</span></span> | <span data-ttu-id="38fe0-1434">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1434">Allowed values</span></span> | <span data-ttu-id="38fe0-1435">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1436">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-1436">query</span></span> | <span data-ttu-id="38fe0-1437">Określa zapytanie MDX, które można odczytać danych z wystąpienia programu SAP BW.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1437">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="38fe0-1438">Zapytania MDX.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1438">MDX query.</span></span> | <span data-ttu-id="38fe0-1439">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1440">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1440">Example</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="38fe0-1441">Aby uzyskać więcej informacji, zobacz [łącznika SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="38fe0-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="38fe0-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-1443">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1443">Linked service</span></span>
<span data-ttu-id="38fe0-1444">Aby zdefiniować SAP HANA połączonej usługi, ustaw **typu** połączonej usługi, aby **SapHana**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1444">To define a SAP HANA linked service, set the **type** of the linked service to **SapHana**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="38fe0-1445">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1445">Property</span></span> | <span data-ttu-id="38fe0-1446">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1446">Description</span></span> | <span data-ttu-id="38fe0-1447">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1447">Allowed values</span></span> | <span data-ttu-id="38fe0-1448">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="38fe0-1449">serwer</span><span class="sxs-lookup"><span data-stu-id="38fe0-1449">server</span></span> | <span data-ttu-id="38fe0-1450">Nazwa serwera, na którym znajduje się z wystąpieniem SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1450">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="38fe0-1451">Jeśli serwer używa portu dostosowane, określ `server:port`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="38fe0-1452">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1452">string</span></span> | <span data-ttu-id="38fe0-1453">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1453">Yes</span></span>
<span data-ttu-id="38fe0-1454">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-1454">authenticationType</span></span> | <span data-ttu-id="38fe0-1455">Typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1455">Type of authentication.</span></span> | <span data-ttu-id="38fe0-1456">Ciąg.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1456">string.</span></span> <span data-ttu-id="38fe0-1457">"Basic" lub "Windows"</span><span class="sxs-lookup"><span data-stu-id="38fe0-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="38fe0-1458">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1458">Yes</span></span> 
<span data-ttu-id="38fe0-1459">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-1459">username</span></span> | <span data-ttu-id="38fe0-1460">Nazwa użytkownika, który ma dostęp do serwera SAP</span><span class="sxs-lookup"><span data-stu-id="38fe0-1460">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="38fe0-1461">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1461">string</span></span> | <span data-ttu-id="38fe0-1462">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1462">Yes</span></span>
<span data-ttu-id="38fe0-1463">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-1463">password</span></span> | <span data-ttu-id="38fe0-1464">Hasło dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1464">Password for the user.</span></span> | <span data-ttu-id="38fe0-1465">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1465">string</span></span> | <span data-ttu-id="38fe0-1466">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1466">Yes</span></span>
<span data-ttu-id="38fe0-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1467">gatewayName</span></span> | <span data-ttu-id="38fe0-1468">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązywania połączenia z lokalnym wystąpieniem SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1468">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="38fe0-1469">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1469">string</span></span> | <span data-ttu-id="38fe0-1470">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1470">Yes</span></span>
<span data-ttu-id="38fe0-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="38fe0-1471">encryptedCredential</span></span> | <span data-ttu-id="38fe0-1472">Ciąg zaszyfrowane poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1472">The encrypted credential string.</span></span> | <span data-ttu-id="38fe0-1473">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1473">string</span></span> | <span data-ttu-id="38fe0-1474">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="38fe0-1475">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1475">Example</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
<span data-ttu-id="38fe0-1476">Aby uzyskać więcej informacji, zobacz [łącznika SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="38fe0-1477">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1477">Dataset</span></span>
<span data-ttu-id="38fe0-1478">Aby zdefiniować zestawu danych SAP HANA, ustaw **typu** zestawu danych do **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1478">To define a SAP HANA dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="38fe0-1479">Nie ma żadnych właściwości specyficzne dla typu obsługiwane dla zestawu danych SAP HANA typu **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1479">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="38fe0-1480">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1480">Example</span></span>

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="38fe0-1481">Aby uzyskać więcej informacji, zobacz [łącznika SAP HANA](data-factory-sap-hana-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="38fe0-1482">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1483">Jeśli dane są kopiowane z magazynu danych SAP HANA, ustaw **typ źródła** działania kopiowania do **RelationalSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1483">If you are copying data from a SAP HANA data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-1484">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1484">Property</span></span> | <span data-ttu-id="38fe0-1485">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1485">Description</span></span> | <span data-ttu-id="38fe0-1486">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1486">Allowed values</span></span> | <span data-ttu-id="38fe0-1487">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1488">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-1488">query</span></span> | <span data-ttu-id="38fe0-1489">Określa zapytanie SQL do odczytywania danych z wystąpieniem SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1489">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="38fe0-1490">Zapytanie SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1490">SQL query.</span></span> | <span data-ttu-id="38fe0-1491">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="38fe0-1492">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1492">Example</span></span>


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="38fe0-1493">Aby uzyskać więcej informacji, zobacz [łącznika SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="38fe0-1494">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="38fe0-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-1495">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1495">Linked service</span></span>
<span data-ttu-id="38fe0-1496">Tworzenie połączonej usługi typu **OnPremisesSqlServer** do połączenia z lokalną bazą danych programu SQL Server z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1496">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="38fe0-1497">Poniższa tabela zawiera opis specyficzne dla lokalnej usługi SQL Server połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1497">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="38fe0-1498">Poniższa tabela zawiera opis specyficzne dla usługi SQL Server połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1498">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="38fe0-1499">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1499">Property</span></span> | <span data-ttu-id="38fe0-1500">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1500">Description</span></span> | <span data-ttu-id="38fe0-1501">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1502">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-1502">type</span></span> |<span data-ttu-id="38fe0-1503">Powinien mieć ustawioną właściwość type: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1503">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="38fe0-1504">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1504">Yes</span></span> |
| <span data-ttu-id="38fe0-1505">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="38fe0-1505">connectionString</span></span> |<span data-ttu-id="38fe0-1506">Określ connectionString informacje wymagane do połączenia z lokalną bazą danych programu SQL Server, przy użyciu uwierzytelniania SQL lub uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1506">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="38fe0-1507">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1507">Yes</span></span> |
| <span data-ttu-id="38fe0-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1508">gatewayName</span></span> |<span data-ttu-id="38fe0-1509">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1509">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="38fe0-1510">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1510">Yes</span></span> |
| <span data-ttu-id="38fe0-1511">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-1511">username</span></span> |<span data-ttu-id="38fe0-1512">Określ nazwę użytkownika, jeśli używasz uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="38fe0-1513">Przykład: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="38fe0-1514">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1514">No</span></span> |
| <span data-ttu-id="38fe0-1515">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-1515">password</span></span> |<span data-ttu-id="38fe0-1516">Określ hasło dla konta użytkownika, określone nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1516">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="38fe0-1517">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1517">No</span></span> |

<span data-ttu-id="38fe0-1518">Można szyfrować poświadczeń przy użyciu **AzureRmDataFactoryEncryptValue nowy** polecenia cmdlet i używać ich w parametrach połączenia, jak pokazano w poniższym przykładzie (**EncryptedCredential** właściwość):</span><span class="sxs-lookup"><span data-stu-id="38fe0-1518">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="38fe0-1519">Przykład: JSON dla przy użyciu uwierzytelniania programu SQL</span><span class="sxs-lookup"><span data-stu-id="38fe0-1519">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="38fe0-1520">Przykład: JSON dla przy użyciu uwierzytelniania systemu Windows</span><span class="sxs-lookup"><span data-stu-id="38fe0-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="38fe0-1521">Jeśli podano nazwę użytkownika i hasło, bramy służą one do personifikacja określonego konta użytkownika nawiązać połączenia z lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1521">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="38fe0-1522">W przeciwnym razie brama łączy się z serwerem SQL, bezpośrednio z kontekstem zabezpieczeń bramy (jego konta uruchamiania).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1522">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="38fe0-1523">Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-1524">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1524">Dataset</span></span>
<span data-ttu-id="38fe0-1525">Aby zdefiniować zestawu danych programu SQL Server, ustaw **typu** zestawu danych do **SqlServerTable**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1525">To define a SQL Server dataset, set the **type** of the dataset to **SqlServerTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-1526">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1526">Property</span></span> | <span data-ttu-id="38fe0-1527">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1527">Description</span></span> | <span data-ttu-id="38fe0-1528">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1529">tableName</span></span> |<span data-ttu-id="38fe0-1530">Nazwa tabeli lub widoku w wystąpieniu bazy danych serwera SQL, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1530">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="38fe0-1531">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1532">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1532">Example</span></span>
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="38fe0-1533">Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="38fe0-1534">Źródło SQL w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1535">Jeśli dane są kopiowane z bazy danych programu SQL Server, należy ustawić **typ źródła** działania kopiowania do **SqlSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1535">If you are copying data from a SQL Server database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="38fe0-1536">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1536">Property</span></span> | <span data-ttu-id="38fe0-1537">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1537">Description</span></span> | <span data-ttu-id="38fe0-1538">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1538">Allowed values</span></span> | <span data-ttu-id="38fe0-1539">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1540">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="38fe0-1540">sqlReaderQuery</span></span> |<span data-ttu-id="38fe0-1541">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1541">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-1542">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1542">SQL query string.</span></span> <span data-ttu-id="38fe0-1543">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="38fe0-1544">Może odwoływać się wiele tabel z bazy danych odwołuje się zestaw danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1544">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="38fe0-1545">Jeśli nie zostanie określony, która zostanie wykonana instrukcja SQL: Wybierz z MyTable.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1545">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="38fe0-1546">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1546">No</span></span> |
| <span data-ttu-id="38fe0-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="38fe0-1548">Nazwa procedury przechowywanej, która odczytuje dane z tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1548">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="38fe0-1549">Nazwa procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1549">Name of the stored procedure.</span></span> |<span data-ttu-id="38fe0-1550">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1550">No</span></span> |
| <span data-ttu-id="38fe0-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="38fe0-1551">storedProcedureParameters</span></span> |<span data-ttu-id="38fe0-1552">Parametry dla procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1552">Parameters for the stored procedure.</span></span> |<span data-ttu-id="38fe0-1553">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1553">Name/value pairs.</span></span> <span data-ttu-id="38fe0-1554">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, nazwy i wielkość liter w wyrazie parametry procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1554">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="38fe0-1555">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1555">No</span></span> |

<span data-ttu-id="38fe0-1556">Jeśli **sqlReaderQuery** określono dla SqlSource, odbywa się działanie kopii tego zapytania względem źródła danych programu SQL Server można pobrać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1556">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="38fe0-1557">Można również określić procedury składowanej, podając **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli jest to procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1557">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="38fe0-1558">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName kolumny zdefiniowane w sekcji struktury są używane do tworzenia zapytania select w celu uruchomienia bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="38fe0-1559">Jeśli definicji zestawu danych nie ma on struktury, wszystkie kolumny są wybierane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1559">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="38fe0-1560">Jeśli używasz **sqlReaderStoredProcedureName**, należy określić wartość dla **tableName** właściwość w zestawie danych JSON.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1560">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="38fe0-1561">Nie ma żadnych operacji sprawdzania poprawności, jednak wykonywać na tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="38fe0-1562">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1562">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-1563">W tym przykładzie **sqlReaderQuery** dla SqlSource został określony.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1563">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="38fe0-1564">Działanie kopiowania uruchamia to zapytanie względem źródła danych programu SQL Server można pobrać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1564">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="38fe0-1565">Można również określić procedury składowanej, podając **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli jest to procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1565">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="38fe0-1566">SqlReaderQuery można odwoływać się wiele tabel w bazie danych odwołuje się zestaw danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1566">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="38fe0-1567">Nie jest ograniczona do tabeli, ustawić jako typeProperty tableName zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1567">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="38fe0-1568">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName kolumny zdefiniowane w sekcji struktury są używane do tworzenia zapytania select w celu uruchomienia bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="38fe0-1569">Jeśli definicji zestawu danych nie ma on struktury, wszystkie kolumny są wybierane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1569">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="38fe0-1570">Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="38fe0-1571">Obiekt Sink SQL w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="38fe0-1572">Jeśli dane są kopiowane do bazy danych programu SQL Server, należy ustawić **typu sink** działania kopiowania do **SqlSink**i określ następujące właściwości w **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1572">If you are copying data to a SQL Server database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="38fe0-1573">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1573">Property</span></span> | <span data-ttu-id="38fe0-1574">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1574">Description</span></span> | <span data-ttu-id="38fe0-1575">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1575">Allowed values</span></span> | <span data-ttu-id="38fe0-1576">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="38fe0-1577">writeBatchTimeout</span></span> |<span data-ttu-id="38fe0-1578">Czas na ukończenie zanim upłynie limit czasu operacji wstawiania wsadowego oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1578">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="38fe0-1579">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="38fe0-1579">timespan</span></span><br/><br/> <span data-ttu-id="38fe0-1580">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="38fe0-1581">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1581">No</span></span> |
| <span data-ttu-id="38fe0-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="38fe0-1582">writeBatchSize</span></span> |<span data-ttu-id="38fe0-1583">Wstawia dane do tabeli SQL, gdy writeBatchSize osiągnie rozmiar buforu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1583">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="38fe0-1584">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1584">Integer (number of rows)</span></span> |<span data-ttu-id="38fe0-1585">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="38fe0-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="38fe0-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="38fe0-1587">Określ kwerendę dla działania kopiowania do wykonania w taki sposób, że dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1587">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="38fe0-1588">Aby uzyskać więcej informacji, zobacz [powtarzalności](#repeatability-during-copy) sekcji.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="38fe0-1589">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1589">A query statement.</span></span> |<span data-ttu-id="38fe0-1590">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1590">No</span></span> |
| <span data-ttu-id="38fe0-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="38fe0-1592">Określ nazwę kolumny dla aktywności kopiowania wypełnić automatycznie generowane wycinek identyfikator, który służy do oczyszczania danych określonego wycinek czas ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1592">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="38fe0-1593">Aby uzyskać więcej informacji, zobacz [powtarzalności](#repeatability-during-copy) sekcji.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="38fe0-1594">Nazwa kolumny kolumnę o typie danych binary(32).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="38fe0-1595">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1595">No</span></span> |
| <span data-ttu-id="38fe0-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="38fe0-1597">Nazwa procedury składowanej danych upserts (aktualizacje/INSERT) do tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1597">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="38fe0-1598">Nazwa procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1598">Name of the stored procedure.</span></span> |<span data-ttu-id="38fe0-1599">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1599">No</span></span> |
| <span data-ttu-id="38fe0-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="38fe0-1600">storedProcedureParameters</span></span> |<span data-ttu-id="38fe0-1601">Parametry dla procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1601">Parameters for the stored procedure.</span></span> |<span data-ttu-id="38fe0-1602">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1602">Name/value pairs.</span></span> <span data-ttu-id="38fe0-1603">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, nazwy i wielkość liter w wyrazie parametry procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1603">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="38fe0-1604">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1604">No</span></span> |
| <span data-ttu-id="38fe0-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="38fe0-1605">sqlWriterTableType</span></span> |<span data-ttu-id="38fe0-1606">Należy określić nazwę typu tabeli do użycia w procedurze składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1606">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="38fe0-1607">Działanie kopiowania udostępnia dane jest przenoszony w tabeli tymczasowej o tym typie tabeli.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1607">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="38fe0-1608">Kod procedury składowanej można następnie scalić dane są kopiowane z istniejącymi danymi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1608">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="38fe0-1609">Nazwa typu tabeli.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1609">A table type name.</span></span> |<span data-ttu-id="38fe0-1610">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1611">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1611">Example</span></span>
<span data-ttu-id="38fe0-1612">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania tych zestawów danych wejściowych i wyjściowych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1612">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="38fe0-1613">W definicji JSON potoku **źródła** ustawiono typ **BlobSource** i **zbiornika** ustawiono typ **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1613">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-1614">Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="38fe0-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="38fe0-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-1616">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1616">Linked service</span></span>
<span data-ttu-id="38fe0-1617">Aby zdefiniować Sybase połączonej usługi, ustaw **typu** połączonej usługi, aby **OnPremisesSybase**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1617">To define a Sybase linked service, set the **type** of the linked service to **OnPremisesSybase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-1618">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1618">Property</span></span> | <span data-ttu-id="38fe0-1619">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1619">Description</span></span> | <span data-ttu-id="38fe0-1620">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1621">serwer</span><span class="sxs-lookup"><span data-stu-id="38fe0-1621">server</span></span> |<span data-ttu-id="38fe0-1622">Nazwa serwera programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1622">Name of the Sybase server.</span></span> |<span data-ttu-id="38fe0-1623">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1623">Yes</span></span> |
| <span data-ttu-id="38fe0-1624">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1624">database</span></span> |<span data-ttu-id="38fe0-1625">Nazwa bazy danych programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1625">Name of the Sybase database.</span></span> |<span data-ttu-id="38fe0-1626">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1626">Yes</span></span> |
| <span data-ttu-id="38fe0-1627">Schemat</span><span class="sxs-lookup"><span data-stu-id="38fe0-1627">schema</span></span> |<span data-ttu-id="38fe0-1628">Nazwa schematu w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1628">Name of the schema in the database.</span></span> |<span data-ttu-id="38fe0-1629">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1629">No</span></span> |
| <span data-ttu-id="38fe0-1630">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-1630">authenticationType</span></span> |<span data-ttu-id="38fe0-1631">Typ uwierzytelniania używany do łączenia z bazą danych programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1631">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="38fe0-1632">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="38fe0-1633">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1633">Yes</span></span> |
| <span data-ttu-id="38fe0-1634">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-1634">username</span></span> |<span data-ttu-id="38fe0-1635">Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="38fe0-1636">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1636">No</span></span> |
| <span data-ttu-id="38fe0-1637">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-1637">password</span></span> |<span data-ttu-id="38fe0-1638">Określ hasło dla konta użytkownika, określone nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1638">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="38fe0-1639">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1639">No</span></span> |
| <span data-ttu-id="38fe0-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1640">gatewayName</span></span> |<span data-ttu-id="38fe0-1641">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną bazą danych programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1641">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="38fe0-1642">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1643">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1643">Example</span></span>
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="38fe0-1644">Aby uzyskać więcej informacji, zobacz [łącznika programu Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-1645">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1645">Dataset</span></span>
<span data-ttu-id="38fe0-1646">Aby zdefiniować zestawu danych programu Sybase, ustaw **typu** zestawu danych do **RelationalTable**, a następnie określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1646">To define a Sybase dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-1647">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1647">Property</span></span> | <span data-ttu-id="38fe0-1648">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1648">Description</span></span> | <span data-ttu-id="38fe0-1649">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1650">tableName</span></span> |<span data-ttu-id="38fe0-1651">Nazwa tabeli w wystąpieniu bazy danych programu Sybase, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1651">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="38fe0-1652">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1653">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1653">Example</span></span>

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="38fe0-1654">Aby uzyskać więcej informacji, zobacz [łącznika programu Sybase](data-factory-onprem-sybase-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="38fe0-1655">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1656">Jeśli dane są kopiowane z bazy danych programu Sybase, ustaw **typ źródła** działania kopiowania do **RelationalSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1656">If you are copying data from a Sybase database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="38fe0-1657">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1657">Property</span></span> | <span data-ttu-id="38fe0-1658">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1658">Description</span></span> | <span data-ttu-id="38fe0-1659">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1659">Allowed values</span></span> | <span data-ttu-id="38fe0-1660">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1661">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-1661">query</span></span> |<span data-ttu-id="38fe0-1662">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1662">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-1663">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1663">SQL query string.</span></span> <span data-ttu-id="38fe0-1664">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="38fe0-1665">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1666">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1666">Example</span></span>

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="38fe0-1667">Aby uzyskać więcej informacji, zobacz [łącznika programu Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="38fe0-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="38fe0-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-1669">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1669">Linked service</span></span>
<span data-ttu-id="38fe0-1670">Aby zdefiniować Teradata połączonej usługi, ustaw **typu** połączonej usługi, aby **OnPremisesTeradata**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1670">To define a Teradata linked service, set the **type** of the linked service to **OnPremisesTeradata**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-1671">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1671">Property</span></span> | <span data-ttu-id="38fe0-1672">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1672">Description</span></span> | <span data-ttu-id="38fe0-1673">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1674">serwer</span><span class="sxs-lookup"><span data-stu-id="38fe0-1674">server</span></span> |<span data-ttu-id="38fe0-1675">Nazwa serwera programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1675">Name of the Teradata server.</span></span> |<span data-ttu-id="38fe0-1676">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1676">Yes</span></span> |
| <span data-ttu-id="38fe0-1677">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-1677">authenticationType</span></span> |<span data-ttu-id="38fe0-1678">Typ uwierzytelniania używany do łączenia z bazą danych programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1678">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="38fe0-1679">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="38fe0-1680">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1680">Yes</span></span> |
| <span data-ttu-id="38fe0-1681">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-1681">username</span></span> |<span data-ttu-id="38fe0-1682">Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="38fe0-1683">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1683">No</span></span> |
| <span data-ttu-id="38fe0-1684">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-1684">password</span></span> |<span data-ttu-id="38fe0-1685">Określ hasło dla konta użytkownika, określone nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1685">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="38fe0-1686">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1686">No</span></span> |
| <span data-ttu-id="38fe0-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1687">gatewayName</span></span> |<span data-ttu-id="38fe0-1688">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną bazą danych programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1688">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="38fe0-1689">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1690">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1690">Example</span></span>
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="38fe0-1691">Aby uzyskać więcej informacji, zobacz [łącznika programu Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="38fe0-1692">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1692">Dataset</span></span>
<span data-ttu-id="38fe0-1693">Aby zdefiniować zestawu danych obiektów Teradata Blob, ustaw **typu** zestawu danych do **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1693">To define a Teradata Blob dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="38fe0-1694">Obecnie nie ma żadnych właściwości typu, obsługiwane dla zestawu danych programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1694">Currently, there are no type properties supported for the Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="38fe0-1695">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1695">Example</span></span>
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="38fe0-1696">Aby uzyskać więcej informacji, zobacz [łącznika programu Teradata](data-factory-onprem-teradata-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="38fe0-1697">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1698">Jeśli dane są kopiowane z bazy danych programu Teradata, ustaw **typ źródła** działania kopiowania do **RelationalSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1698">If you are copying data from a Teradata database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-1699">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1699">Property</span></span> | <span data-ttu-id="38fe0-1700">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1700">Description</span></span> | <span data-ttu-id="38fe0-1701">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1701">Allowed values</span></span> | <span data-ttu-id="38fe0-1702">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1703">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-1703">query</span></span> |<span data-ttu-id="38fe0-1704">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1704">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-1705">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1705">SQL query string.</span></span> <span data-ttu-id="38fe0-1706">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="38fe0-1707">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1708">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1708">Example</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="38fe0-1709">Aby uzyskać więcej informacji, zobacz [łącznika programu Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="38fe0-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="38fe0-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="38fe0-1711">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1711">Linked service</span></span>
<span data-ttu-id="38fe0-1712">Aby zdefiniować Cassandra połączone usługi, ustaw **typu** połączonej usługi, aby **OnPremisesCassandra**, a następnie określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1712">To define a Cassandra linked service, set the **type** of the linked service to **OnPremisesCassandra**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-1713">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1713">Property</span></span> | <span data-ttu-id="38fe0-1714">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1714">Description</span></span> | <span data-ttu-id="38fe0-1715">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1716">Host</span><span class="sxs-lookup"><span data-stu-id="38fe0-1716">host</span></span> |<span data-ttu-id="38fe0-1717">Jeden lub więcej adresów IP lub nazw hostów serwerów Cassandra.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="38fe0-1718">Określ rozdzielaną przecinkami listę adresów IP lub nazw hostów, aby nawiązać połączenie wszystkie serwery jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1718">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="38fe0-1719">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1719">Yes</span></span> |
| <span data-ttu-id="38fe0-1720">port</span><span class="sxs-lookup"><span data-stu-id="38fe0-1720">port</span></span> |<span data-ttu-id="38fe0-1721">Port TCP używany przez serwer Cassandra nasłuchiwanie dla połączeń klienta.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1721">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="38fe0-1722">Nie, wartość domyślna: 9042</span><span class="sxs-lookup"><span data-stu-id="38fe0-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="38fe0-1723">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-1723">authenticationType</span></span> |<span data-ttu-id="38fe0-1724">Podstawowa lub anonimowe</span><span class="sxs-lookup"><span data-stu-id="38fe0-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="38fe0-1725">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1725">Yes</span></span> |
| <span data-ttu-id="38fe0-1726">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-1726">username</span></span> |<span data-ttu-id="38fe0-1727">Określ nazwę użytkownika dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1727">Specify user name for the user account.</span></span> |<span data-ttu-id="38fe0-1728">Tak, jeśli authenticationType ustawiany jest podstawowy.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1728">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="38fe0-1729">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-1729">password</span></span> |<span data-ttu-id="38fe0-1730">Określ hasło dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1730">Specify password for the user account.</span></span> |<span data-ttu-id="38fe0-1731">Tak, jeśli authenticationType ustawiany jest podstawowy.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1731">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="38fe0-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1732">gatewayName</span></span> |<span data-ttu-id="38fe0-1733">Nazwa bramy, która służy do łączenia z bazą danych Cassandra lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1733">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="38fe0-1734">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1734">Yes</span></span> |
| <span data-ttu-id="38fe0-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="38fe0-1735">encryptedCredential</span></span> |<span data-ttu-id="38fe0-1736">Poświadczenie szyfrowane przez bramę.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1736">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="38fe0-1737">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1738">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1738">Example</span></span>

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="38fe0-1739">Aby uzyskać więcej informacji, zobacz [łącznik Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-1740">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1740">Dataset</span></span>
<span data-ttu-id="38fe0-1741">Aby zdefiniować Cassandra zestawu danych, ustaw **typu** zestawu danych do **CassandraTable**, a następnie określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1741">To define a Cassandra dataset, set the **type** of the dataset to **CassandraTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-1742">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1742">Property</span></span> | <span data-ttu-id="38fe0-1743">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1743">Description</span></span> | <span data-ttu-id="38fe0-1744">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1745">przestrzeni kluczy</span><span class="sxs-lookup"><span data-stu-id="38fe0-1745">keyspace</span></span> |<span data-ttu-id="38fe0-1746">Nazwa schematu bazy danych Cassandra lub przestrzeni kluczy.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1746">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="38fe0-1747">Tak (Jeśli **zapytania** dla **CassandraSource** nie jest zdefiniowana).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="38fe0-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1748">tableName</span></span> |<span data-ttu-id="38fe0-1749">Nazwa tabeli w bazie danych Cassandra.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1749">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="38fe0-1750">Tak (Jeśli **zapytania** dla **CassandraSource** nie jest zdefiniowana).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1751">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1751">Example</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="38fe0-1752">Aby uzyskać więcej informacji, zobacz [łącznik Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="38fe0-1753">Źródło Cassandra w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1754">Jeśli dane są kopiowane z Cassandra, ustaw **typ źródła** działania kopiowania do **CassandraSource**, a następnie określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1754">If you are copying data from Cassandra, set the **source type** of the copy activity to **CassandraSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-1755">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1755">Property</span></span> | <span data-ttu-id="38fe0-1756">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1756">Description</span></span> | <span data-ttu-id="38fe0-1757">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1757">Allowed values</span></span> | <span data-ttu-id="38fe0-1758">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1759">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-1759">query</span></span> |<span data-ttu-id="38fe0-1760">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1760">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-1761">Zapytania SQL 92 lub CQL zapytania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="38fe0-1762">Zobacz [odwołania CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="38fe0-1763">Korzystając z zapytania SQL, określ **przestrzeni kluczy name.table nazwy** do reprezentowania tabeli ma dotyczyć zapytanie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1763">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="38fe0-1764">Nie (jeśli są zdefiniowane tableName oraz przestrzeni kluczy w zestawie danych).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="38fe0-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="38fe0-1765">consistencyLevel</span></span> |<span data-ttu-id="38fe0-1766">Poziom spójności Określa, jak wiele replik musi odpowiedzieć na żądanie odczytu przed zwróceniem danych do aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1766">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="38fe0-1767">Cassandra sprawdza określonej liczby replik danych do spełnienia żądania odczytu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1767">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="38fe0-1768">JEDNĄ, DWIE, TRZY, KWORUM, WSZYSTKIE, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="38fe0-1769">Zobacz [Konfigurowanie spójność danych](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="38fe0-1770">Nie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1770">No.</span></span> <span data-ttu-id="38fe0-1771">Domyślna wartość to jeden.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1772">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-1773">Aby uzyskać więcej informacji, zobacz [łącznik Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="38fe0-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="38fe0-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-1775">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1775">Linked service</span></span>
<span data-ttu-id="38fe0-1776">Aby zdefiniować bazy danych MongoDB połączonej usługi, ustaw **typu** połączonej usługi, aby **OnPremisesMongoDB**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1776">To define a MongoDB linked service, set the **type** of the linked service to **OnPremisesMongoDB**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-1777">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1777">Property</span></span> | <span data-ttu-id="38fe0-1778">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1778">Description</span></span> | <span data-ttu-id="38fe0-1779">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1780">serwer</span><span class="sxs-lookup"><span data-stu-id="38fe0-1780">server</span></span> |<span data-ttu-id="38fe0-1781">Adres IP lub hosta nazwę serwera bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1781">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="38fe0-1782">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1782">Yes</span></span> |
| <span data-ttu-id="38fe0-1783">port</span><span class="sxs-lookup"><span data-stu-id="38fe0-1783">port</span></span> |<span data-ttu-id="38fe0-1784">Port TCP używany przez serwer bazy danych MongoDB do nasłuchiwania dla połączeń klienta.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1784">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="38fe0-1785">Opcjonalne, wartość domyślna: 27017</span><span class="sxs-lookup"><span data-stu-id="38fe0-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="38fe0-1786">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-1786">authenticationType</span></span> |<span data-ttu-id="38fe0-1787">Podstawowy, lub anonimowe.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="38fe0-1788">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1788">Yes</span></span> |
| <span data-ttu-id="38fe0-1789">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-1789">username</span></span> |<span data-ttu-id="38fe0-1790">Konto użytkownika do bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1790">User account to access MongoDB.</span></span> |<span data-ttu-id="38fe0-1791">Tak (jeśli jest używane uwierzytelnianie podstawowe).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="38fe0-1792">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-1792">password</span></span> |<span data-ttu-id="38fe0-1793">Hasło dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1793">Password for the user.</span></span> |<span data-ttu-id="38fe0-1794">Tak (jeśli jest używane uwierzytelnianie podstawowe).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="38fe0-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="38fe0-1795">authSource</span></span> |<span data-ttu-id="38fe0-1796">Nazwa bazy danych MongoDB, który ma być używany w celu sprawdzenia poświadczeń dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1796">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="38fe0-1797">Opcjonalnie (jeśli jest używane uwierzytelnianie podstawowe).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="38fe0-1798">domyślne: używa konta administratora i baza danych określona za pomocą właściwości databaseName.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1798">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="38fe0-1799">DatabaseName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1799">databaseName</span></span> |<span data-ttu-id="38fe0-1800">Nazwa bazy danych MongoDB, które chcesz uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1800">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="38fe0-1801">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1801">Yes</span></span> |
| <span data-ttu-id="38fe0-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1802">gatewayName</span></span> |<span data-ttu-id="38fe0-1803">Nazwa bramy, która uzyskuje dostęp do magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1803">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="38fe0-1804">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1804">Yes</span></span> |
| <span data-ttu-id="38fe0-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="38fe0-1805">encryptedCredential</span></span> |<span data-ttu-id="38fe0-1806">Poświadczenie szyfrowane przez bramę.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="38fe0-1807">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1808">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="38fe0-1809">Aby uzyskać więcej informacji, zobacz [artykułu łącznika bazy danych MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="38fe0-1810">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1810">Dataset</span></span>
<span data-ttu-id="38fe0-1811">Aby zdefiniować zestawu danych MongoDB, ustaw **typu** zestawu danych do **MongoDbCollection**, a następnie określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1811">To define a MongoDB dataset, set the **type** of the dataset to **MongoDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-1812">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1812">Property</span></span> | <span data-ttu-id="38fe0-1813">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1813">Description</span></span> | <span data-ttu-id="38fe0-1814">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1815">CollectionName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1815">collectionName</span></span> |<span data-ttu-id="38fe0-1816">Nazwa kolekcji w bazie danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1816">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="38fe0-1817">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1818">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1818">Example</span></span>

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="38fe0-1819">Aby uzyskać więcej informacji, zobacz [artykułu łącznika bazy danych MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="38fe0-1820">Źródłowej bazy danych MongoDB w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1821">Jeśli dane są kopiowane z bazy danych MongoDB, ustaw **typ źródła** działania kopiowania do **MongoDbSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1821">If you are copying data from MongoDB, set the **source type** of the copy activity to **MongoDbSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-1822">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1822">Property</span></span> | <span data-ttu-id="38fe0-1823">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1823">Description</span></span> | <span data-ttu-id="38fe0-1824">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1824">Allowed values</span></span> | <span data-ttu-id="38fe0-1825">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1826">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-1826">query</span></span> |<span data-ttu-id="38fe0-1827">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1827">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-1828">Ciąg zapytania SQL 92.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1828">SQL-92 query string.</span></span> <span data-ttu-id="38fe0-1829">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="38fe0-1830">Nie (Jeśli **collectionName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1831">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1831">Example</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="38fe0-1832">Aby uzyskać więcej informacji, zobacz [artykułu łącznika bazy danych MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="38fe0-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="38fe0-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="38fe0-1834">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1834">Linked service</span></span>
<span data-ttu-id="38fe0-1835">Aby zdefiniować Amazon S3 połączonej usługi, ustaw **typu** połączonej usługi, aby **AwsAccessKey**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1835">To define an Amazon S3 linked service, set the **type** of the linked service to **AwsAccessKey**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-1836">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1836">Property</span></span> | <span data-ttu-id="38fe0-1837">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1837">Description</span></span> | <span data-ttu-id="38fe0-1838">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1838">Allowed values</span></span> | <span data-ttu-id="38fe0-1839">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="38fe0-1840">accessKeyID</span></span> |<span data-ttu-id="38fe0-1841">Identyfikator klucza tajnego dostępu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1841">ID of the secret access key.</span></span> |<span data-ttu-id="38fe0-1842">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1842">string</span></span> |<span data-ttu-id="38fe0-1843">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1843">Yes</span></span> |
| <span data-ttu-id="38fe0-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="38fe0-1844">secretAccessKey</span></span> |<span data-ttu-id="38fe0-1845">Samego klucza tajnego dostępu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1845">The secret access key itself.</span></span> |<span data-ttu-id="38fe0-1846">Zaszyfrowanego ciągu tajny</span><span class="sxs-lookup"><span data-stu-id="38fe0-1846">Encrypted secret string</span></span> |<span data-ttu-id="38fe0-1847">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-1848">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1848">Example</span></span>
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

<span data-ttu-id="38fe0-1849">Aby uzyskać więcej informacji, zobacz [Amazon S3 artykułu łącznika](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="38fe0-1850">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1850">Dataset</span></span>
<span data-ttu-id="38fe0-1851">Aby zdefiniować Amazon S3 zestawu danych, ustaw **typu** zestawu danych do **AmazonS3**, a następnie określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1851">To define an Amazon S3 dataset, set the **type** of the dataset to **AmazonS3**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-1852">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1852">Property</span></span> | <span data-ttu-id="38fe0-1853">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1853">Description</span></span> | <span data-ttu-id="38fe0-1854">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1854">Allowed values</span></span> | <span data-ttu-id="38fe0-1855">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1856">bucketName</span></span> |<span data-ttu-id="38fe0-1857">Nazwa pakietu S3.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1857">The S3 bucket name.</span></span> |<span data-ttu-id="38fe0-1858">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1858">String</span></span> |<span data-ttu-id="38fe0-1859">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1859">Yes</span></span> |
| <span data-ttu-id="38fe0-1860">key</span><span class="sxs-lookup"><span data-stu-id="38fe0-1860">key</span></span> |<span data-ttu-id="38fe0-1861">Klucz obiektu S3.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1861">The S3 object key.</span></span> |<span data-ttu-id="38fe0-1862">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1862">String</span></span> |<span data-ttu-id="38fe0-1863">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1863">No</span></span> |
| <span data-ttu-id="38fe0-1864">Prefiks</span><span class="sxs-lookup"><span data-stu-id="38fe0-1864">prefix</span></span> |<span data-ttu-id="38fe0-1865">Prefiks klucza obiektu S3.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1865">Prefix for the S3 object key.</span></span> <span data-ttu-id="38fe0-1866">Wybrano obiektów, w której klucze uruchomienia z tym prefiksem.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="38fe0-1867">Ma zastosowanie tylko wtedy, gdy klucz jest pusty.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="38fe0-1868">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1868">String</span></span> |<span data-ttu-id="38fe0-1869">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1869">No</span></span> |
| <span data-ttu-id="38fe0-1870">Wersja</span><span class="sxs-lookup"><span data-stu-id="38fe0-1870">version</span></span> |<span data-ttu-id="38fe0-1871">Wersja obiektu S3, jeśli włączono S3 przechowywania wersji.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1871">The version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="38fe0-1872">Ciąg</span><span class="sxs-lookup"><span data-stu-id="38fe0-1872">String</span></span> |<span data-ttu-id="38fe0-1873">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1873">No</span></span> |
| <span data-ttu-id="38fe0-1874">Format</span><span class="sxs-lookup"><span data-stu-id="38fe0-1874">format</span></span> | <span data-ttu-id="38fe0-1875">Obsługiwane są następujące typy format: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1875">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="38fe0-1876">Ustaw **typu** właściwości w formacie do jednej z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1876">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="38fe0-1877">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="38fe0-1878">Jeśli chcesz **skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcji format w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1878">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="38fe0-1879">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1879">No</span></span> | |
| <span data-ttu-id="38fe0-1880">Kompresja</span><span class="sxs-lookup"><span data-stu-id="38fe0-1880">compression</span></span> | <span data-ttu-id="38fe0-1881">Określ typ i poziom kompresji danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1881">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="38fe0-1882">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="38fe0-1883">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1883">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="38fe0-1884">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="38fe0-1885">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="38fe0-1886">bucketName + klawisz Określa lokalizację, w którym zasobnika jest nadrzędny kontener dla obiektów S3 i klucz jest pełną ścieżką do obiektu S3 obiektu S3.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1886">bucketName + key specifies the location of the S3 object where bucket is the root container for S3 objects and key is the full path to S3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="38fe0-1887">Przykład: Przykładowego zestawu danych z prefiksem</span><span class="sxs-lookup"><span data-stu-id="38fe0-1887">Example: Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="38fe0-1888">Przykład: Zestaw danych przykładowych (wersją)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1888">Example: Sample data set (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="38fe0-1889">Przykład: Dynamiczne ścieżki S3</span><span class="sxs-lookup"><span data-stu-id="38fe0-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="38fe0-1890">W przykładzie używamy stałej wartości dla właściwości klucza i bucketName w zestawie danych Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1890">In the sample, we use fixed values for key and bucketName properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="38fe0-1891">Program może obliczyć klucza i bucketName dynamicznie w czasie wykonywania za pomocą zmiennych systemowych, takich jak SliceStart fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1891">You can have Data Factory calculate the key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="38fe0-1892">Możesz to zrobić takie same właściwości prefiks Amazon S3 zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1892">You can do the same for the prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="38fe0-1893">Zobacz [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md) listę obsługiwanych funkcjach i zmiennych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="38fe0-1894">Aby uzyskać więcej informacji, zobacz [Amazon S3 artykułu łącznika](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="38fe0-1895">Źródło systemu plików w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1896">Jeśli dane są kopiowane z Amazon S3, ustaw **typ źródła** działania kopiowania do **FileSystemSource**, a następnie określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1896">If you are copying data from Amazon S3, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="38fe0-1897">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1897">Property</span></span> | <span data-ttu-id="38fe0-1898">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1898">Description</span></span> | <span data-ttu-id="38fe0-1899">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1899">Allowed values</span></span> | <span data-ttu-id="38fe0-1900">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1901">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="38fe0-1901">recursive</span></span> |<span data-ttu-id="38fe0-1902">Określa, czy do rekursywnie lista S3 obiektów w katalogu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1902">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="38fe0-1903">wartość true, false</span><span class="sxs-lookup"><span data-stu-id="38fe0-1903">true/false</span></span> |<span data-ttu-id="38fe0-1904">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="38fe0-1905">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1905">Example</span></span>


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

<span data-ttu-id="38fe0-1906">Aby uzyskać więcej informacji, zobacz [Amazon S3 artykułu łącznika](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="38fe0-1907">System plików</span><span class="sxs-lookup"><span data-stu-id="38fe0-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="38fe0-1908">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-1908">Linked service</span></span>
<span data-ttu-id="38fe0-1909">System plików lokalnych można połączyć z fabryki danych Azure z **na lokalnym serwerze plików** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1909">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="38fe0-1910">Poniższa tabela zawiera opisy elementy JSON, które są specyficzne dla usługi z lokalnym serwerem plików połączonych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1910">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="38fe0-1911">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1911">Property</span></span> | <span data-ttu-id="38fe0-1912">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1912">Description</span></span> | <span data-ttu-id="38fe0-1913">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1914">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-1914">type</span></span> |<span data-ttu-id="38fe0-1915">Upewnij się, że właściwość type ma ustawioną **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1915">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="38fe0-1916">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1916">Yes</span></span> |
| <span data-ttu-id="38fe0-1917">Host</span><span class="sxs-lookup"><span data-stu-id="38fe0-1917">host</span></span> |<span data-ttu-id="38fe0-1918">Określa ścieżkę katalogu głównego folderu, który chcesz skopiować.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1918">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="38fe0-1919">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1919">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="38fe0-1920">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="38fe0-1921">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1921">Yes</span></span> |
| <span data-ttu-id="38fe0-1922">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-1922">userid</span></span> |<span data-ttu-id="38fe0-1923">Określ identyfikator użytkownika, który ma dostęp do serwera.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1923">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="38fe0-1924">Nie (Jeśli wybierzesz encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="38fe0-1925">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-1925">password</span></span> |<span data-ttu-id="38fe0-1926">Określ hasło dla użytkownika (nazwa użytkownika).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1926">Specify the password for the user (userid).</span></span> |<span data-ttu-id="38fe0-1927">Nie (Jeśli wybierzesz encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="38fe0-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="38fe0-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="38fe0-1928">encryptedCredential</span></span> |<span data-ttu-id="38fe0-1929">Określ zaszyfrowane poświadczenia, które można uzyskać, uruchamiając polecenie cmdlet New-AzureRmDataFactoryEncryptValue.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1929">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="38fe0-1930">Nie (Jeśli wybierzesz określić identyfikator użytkownika i hasło w postaci zwykłego tekstu)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1930">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="38fe0-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1931">gatewayName</span></span> |<span data-ttu-id="38fe0-1932">Nazwa bramy, która fabryka danych ma używać do łączenia z serwerem plików lokalnych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1932">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="38fe0-1933">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="38fe0-1934">Ścieżka folderu definicje</span><span class="sxs-lookup"><span data-stu-id="38fe0-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="38fe0-1935">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="38fe0-1935">Scenario</span></span> | <span data-ttu-id="38fe0-1936">Host w definicji usługi połączonej</span><span class="sxs-lookup"><span data-stu-id="38fe0-1936">Host in linked service definition</span></span> | <span data-ttu-id="38fe0-1937">folderPath w definicji zestawu danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1938">Folder lokalny na komputerze bramy zarządzania danymi:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="38fe0-1939">Przykłady: D:\\ \* lub D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="38fe0-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="38fe0-1940">D:\\ \\ (dla danych zarządzania bramy 2.0 i nowsze wersje)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="38fe0-1941">localhost (dla starszych niż 2.0 bramy zarządzania danych)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="38fe0-1942">. \\ \\ lub folderu\\\\podfolder (dla danych zarządzania bramy 2.0 i nowsze wersje)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="38fe0-1943">D:\\ \\ lub D:\\\\folderu\\\\podfolder (dla wersji bramy poniżej 2.0)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="38fe0-1944">Zdalny folder udostępniony:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="38fe0-1945">Przykłady: \\ \\MójSerwer\\udostępnianie\\ \* lub \\ \\MójSerwer\\udostępnianie\\folderu\\podfolderu\\*</span><span class="sxs-lookup"><span data-stu-id="38fe0-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="38fe0-1946">\\\\\\\\MójSerwer\\\\udziału</span><span class="sxs-lookup"><span data-stu-id="38fe0-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="38fe0-1947">. \\ \\ lub folderu\\\\podfolderu</span><span class="sxs-lookup"><span data-stu-id="38fe0-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="38fe0-1948">Przykład: Przy użyciu nazwy użytkownika i hasła w postaci zwykłego tekstu</span><span class="sxs-lookup"><span data-stu-id="38fe0-1948">Example: Using username and password in plain text</span></span>

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="38fe0-1949">Przykład: Użycie encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="38fe0-1949">Example: Using encryptedcredential</span></span>

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="38fe0-1950">Aby uzyskać więcej informacji, zobacz [artykułu łącznika systemu plików](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="38fe0-1951">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-1951">Dataset</span></span>
<span data-ttu-id="38fe0-1952">Aby zdefiniować System plików zestawu danych, ustaw **typu** zestawu danych do **FileShare**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1952">To define a File System dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-1953">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1953">Property</span></span> | <span data-ttu-id="38fe0-1954">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1954">Description</span></span> | <span data-ttu-id="38fe0-1955">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="38fe0-1956">folderPath</span></span> |<span data-ttu-id="38fe0-1957">Określa podrzędną do folderu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1957">Specifies the subpath to the folder.</span></span> <span data-ttu-id="38fe0-1958">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1958">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="38fe0-1959">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="38fe0-1960">Możesz łączyć tej właściwości z **partitionBy** do folderu ścieżki oparte na wycinku rozpoczęcia/zakończenia daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1960">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="38fe0-1961">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-1961">Yes</span></span> |
| <span data-ttu-id="38fe0-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="38fe0-1962">fileName</span></span> |<span data-ttu-id="38fe0-1963">Określ nazwę pliku w **folderPath** aby tabela do odwoływania się do określonego pliku w folderze.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1963">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="38fe0-1964">Jeśli nie określono żadnej wartości dla tej właściwości, tabela wskazuje wszystkie pliki w folderze.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1964">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="38fe0-1965">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwę wygenerowanego pliku jest w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1965">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="38fe0-1966">`Data.<Guid>.txt`(Przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="38fe0-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="38fe0-1967">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1967">No</span></span> |
| <span data-ttu-id="38fe0-1968">obiektu fileFilter</span><span class="sxs-lookup"><span data-stu-id="38fe0-1968">fileFilter</span></span> |<span data-ttu-id="38fe0-1969">Określ filtr służący do wybierania podzbioru pliki w ścieżce folderu, a nie wszystkie pliki.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1969">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="38fe0-1970">Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="38fe0-1971">Przykład 1: "obiektu"fileFilter: "* .log"</span><span class="sxs-lookup"><span data-stu-id="38fe0-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="38fe0-1972">Przykład 2: "obiektu"fileFilter: 2016 - 1-?. txt"</span><span class="sxs-lookup"><span data-stu-id="38fe0-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="38fe0-1973">Należy pamiętać, że tego obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="38fe0-1974">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1974">No</span></span> |
| <span data-ttu-id="38fe0-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="38fe0-1975">partitionedBy</span></span> |<span data-ttu-id="38fe0-1976">PartitionedBy służy do określenia dynamiczne folderPath/fileName danych szeregu czasowego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1976">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="38fe0-1977">Przykładem jest folderPath sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="38fe0-1978">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1978">No</span></span> |
| <span data-ttu-id="38fe0-1979">Format</span><span class="sxs-lookup"><span data-stu-id="38fe0-1979">format</span></span> | <span data-ttu-id="38fe0-1980">Obsługiwane są następujące typy format: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1980">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="38fe0-1981">Ustaw **typu** właściwości w formacie do jednej z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1981">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="38fe0-1982">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="38fe0-1983">Jeśli chcesz **skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcji format w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1983">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="38fe0-1984">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1984">No</span></span> |
| <span data-ttu-id="38fe0-1985">Kompresja</span><span class="sxs-lookup"><span data-stu-id="38fe0-1985">compression</span></span> | <span data-ttu-id="38fe0-1986">Określ typ i poziom kompresji danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1986">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="38fe0-1987">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**; i są obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="38fe0-1988">zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="38fe0-1989">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="38fe0-1990">Nie można użyć nazwy pliku i obiektu fileFilter jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="38fe0-1991">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-1991">Example</span></span>

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="38fe0-1992">Aby uzyskać więcej informacji, zobacz [artykułu łącznika systemu plików](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="38fe0-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="38fe0-1993">Źródło systemu plików w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-1994">Jeśli dane są kopiowane z systemu plików, należy ustawić **typ źródła** działania kopiowania do **FileSystemSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-1994">If you are copying data from File System, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-1995">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-1995">Property</span></span> | <span data-ttu-id="38fe0-1996">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-1996">Description</span></span> | <span data-ttu-id="38fe0-1997">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-1997">Allowed values</span></span> | <span data-ttu-id="38fe0-1998">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-1999">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="38fe0-1999">recursive</span></span> |<span data-ttu-id="38fe0-2000">Wskazuje, czy dane są odczytywane rekursywnie z podfoldery lub tylko określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2000">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="38fe0-2001">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2001">True, False (default)</span></span> |<span data-ttu-id="38fe0-2002">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-2003">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2003">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="38fe0-2004">Aby uzyskać więcej informacji, zobacz [artykułu łącznika systemu plików](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="38fe0-2005">W przypadku działania kopiowania obiektu Sink systemu plików</span><span class="sxs-lookup"><span data-stu-id="38fe0-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="38fe0-2006">Jeśli dane są kopiowane do systemu plików, należy ustawić **typu sink** działania kopiowania do **FileSystemSink**i określ następujące właściwości w **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2006">If you are copying data to File System, set the **sink type** of the copy activity to **FileSystemSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="38fe0-2007">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2007">Property</span></span> | <span data-ttu-id="38fe0-2008">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2008">Description</span></span> | <span data-ttu-id="38fe0-2009">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-2009">Allowed values</span></span> | <span data-ttu-id="38fe0-2010">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="38fe0-2011">copyBehavior</span></span> |<span data-ttu-id="38fe0-2012">Określa zachowanie kopiowania, gdy źródłem jest BlobSource lub systemu plików.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2012">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="38fe0-2013">**PreserveHierarchy:** zachowuje hierarchię plików w folderze docelowym.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2013">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="38fe0-2014">Względna ścieżka pliku źródłowego do folderu źródłowego jest taka sama jak ścieżka względna docelowego pliku do folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2014">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="38fe0-2015">**FlattenHierarchy:** wszystkie pliki z folderu źródłowego są tworzone w pierwszy poziom folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2015">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="38fe0-2016">Pliki docelowe są tworzone z automatycznie generowaną nazwą.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2016">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="38fe0-2017">**MergeFiles:** scala wszystkie pliki z folderu źródłowego do jednego pliku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2017">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="38fe0-2018">Jeśli określono nazwę pliku nazwy/obiektów blob, nazwa scalony plik jest określona nazwa.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2018">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="38fe0-2019">W przeciwnym razie jest nazwa pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="38fe0-2020">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2020">No</span></span> |
<span data-ttu-id="38fe0-2021">Auto-</span><span class="sxs-lookup"><span data-stu-id="38fe0-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="38fe0-2022">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2022">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-2023">Aby uzyskać więcej informacji, zobacz [artykułu łącznika systemu plików](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="38fe0-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="38fe0-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-2025">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2025">Linked service</span></span>
<span data-ttu-id="38fe0-2026">Aby zdefiniować FTP połączonej usługi, ustaw **typu** połączonej usługi, aby **SerwerFTP**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2026">To define an FTP linked service, set the **type** of the linked service to **FtpServer**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-2027">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2027">Property</span></span> | <span data-ttu-id="38fe0-2028">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2028">Description</span></span> | <span data-ttu-id="38fe0-2029">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2029">Required</span></span> | <span data-ttu-id="38fe0-2030">Domyślne</span><span class="sxs-lookup"><span data-stu-id="38fe0-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-2031">Host</span><span class="sxs-lookup"><span data-stu-id="38fe0-2031">host</span></span> |<span data-ttu-id="38fe0-2032">Nazwa lub adres IP serwera FTP</span><span class="sxs-lookup"><span data-stu-id="38fe0-2032">Name or IP address of the FTP Server</span></span> |<span data-ttu-id="38fe0-2033">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="38fe0-2034">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-2034">authenticationType</span></span> |<span data-ttu-id="38fe0-2035">Określ typ uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="38fe0-2035">Specify authentication type</span></span> |<span data-ttu-id="38fe0-2036">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2036">Yes</span></span> |<span data-ttu-id="38fe0-2037">Basic anonimowe</span><span class="sxs-lookup"><span data-stu-id="38fe0-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="38fe0-2038">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-2038">username</span></span> |<span data-ttu-id="38fe0-2039">Użytkownik, który ma dostęp do serwera FTP</span><span class="sxs-lookup"><span data-stu-id="38fe0-2039">User who has access to the FTP server</span></span> |<span data-ttu-id="38fe0-2040">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="38fe0-2041">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-2041">password</span></span> |<span data-ttu-id="38fe0-2042">Hasło dla użytkownika (username)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2042">Password for the user (username)</span></span> |<span data-ttu-id="38fe0-2043">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="38fe0-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="38fe0-2044">encryptedCredential</span></span> |<span data-ttu-id="38fe0-2045">Zaszyfrowane poświadczenia dostępu do serwera FTP</span><span class="sxs-lookup"><span data-stu-id="38fe0-2045">Encrypted credential to access the FTP server</span></span> |<span data-ttu-id="38fe0-2046">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="38fe0-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2047">gatewayName</span></span> |<span data-ttu-id="38fe0-2048">Nazwa bramy, brama zarządzania danymi do nawiązania połączenia lokalnego serwera FTP</span><span class="sxs-lookup"><span data-stu-id="38fe0-2048">Name of the Data Management Gateway gateway to connect to an on-premises FTP server</span></span> |<span data-ttu-id="38fe0-2049">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="38fe0-2050">port</span><span class="sxs-lookup"><span data-stu-id="38fe0-2050">port</span></span> |<span data-ttu-id="38fe0-2051">Port, na którym nasłuchuje serwer FTP</span><span class="sxs-lookup"><span data-stu-id="38fe0-2051">Port on which the FTP server is listening</span></span> |<span data-ttu-id="38fe0-2052">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2052">No</span></span> |<span data-ttu-id="38fe0-2053">21</span><span class="sxs-lookup"><span data-stu-id="38fe0-2053">21</span></span> |
| <span data-ttu-id="38fe0-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="38fe0-2054">enableSsl</span></span> |<span data-ttu-id="38fe0-2055">Określ, czy za pomocą FTP za pośrednictwem kanału SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="38fe0-2055">Specify whether to use FTP over SSL/TLS channel</span></span> |<span data-ttu-id="38fe0-2056">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2056">No</span></span> |<span data-ttu-id="38fe0-2057">Wartość true</span><span class="sxs-lookup"><span data-stu-id="38fe0-2057">true</span></span> |
| <span data-ttu-id="38fe0-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="38fe0-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="38fe0-2059">Określ, czy włączyć weryfikacji certyfikatu serwera SSL przy użyciu FTP za pośrednictwem kanału SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="38fe0-2059">Specify whether to enable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="38fe0-2060">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2060">No</span></span> |<span data-ttu-id="38fe0-2061">Wartość true</span><span class="sxs-lookup"><span data-stu-id="38fe0-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="38fe0-2062">Przykład: Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="38fe0-2062">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="38fe0-2063">Przykład: Przy użyciu nazwy użytkownika i hasła w postaci zwykłego tekstu dla uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="38fe0-2063">Example: Using username and password in plain text for basic authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="38fe0-2064">Przykład: Przy użyciu portu, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="38fe0-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="38fe0-2065">Przykład: Użycie encryptedCredential uwierzytelniania i bramy</span><span class="sxs-lookup"><span data-stu-id="38fe0-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

<span data-ttu-id="38fe0-2066">Aby uzyskać więcej informacji, zobacz [łącznik FTP](data-factory-ftp-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="38fe0-2067">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-2067">Dataset</span></span>
<span data-ttu-id="38fe0-2068">Aby zdefiniować zestawem danych usługi FTP, ustaw **typu** zestawu danych do **FileShare**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2068">To define an FTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-2069">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2069">Property</span></span> | <span data-ttu-id="38fe0-2070">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2070">Description</span></span> | <span data-ttu-id="38fe0-2071">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="38fe0-2072">folderPath</span></span> |<span data-ttu-id="38fe0-2073">Sub ścieżkę do folderu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2073">Sub path to the folder.</span></span> <span data-ttu-id="38fe0-2074">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2074">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="38fe0-2075">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="38fe0-2076">Możesz łączyć tej właściwości z **partitionBy** do folderu ścieżki oparte na wycinku rozpoczęcia/zakończenia daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2076">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="38fe0-2077">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2077">Yes</span></span> 
| <span data-ttu-id="38fe0-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2078">fileName</span></span> |<span data-ttu-id="38fe0-2079">Określ nazwę pliku w **folderPath** aby tabela do odwoływania się do określonego pliku w folderze.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2079">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="38fe0-2080">Jeśli nie określono żadnej wartości dla tej właściwości, tabela wskazuje wszystkie pliki w folderze.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2080">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="38fe0-2081">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwę wygenerowanego pliku będzie poniżej tego formatu:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2081">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="38fe0-2082">Dane. <Guid>.txt (przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="38fe0-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="38fe0-2083">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2083">No</span></span> |
| <span data-ttu-id="38fe0-2084">obiektu fileFilter</span><span class="sxs-lookup"><span data-stu-id="38fe0-2084">fileFilter</span></span> |<span data-ttu-id="38fe0-2085">Określ filtr służący do wybierania podzbioru pliki w ścieżce folderu, a nie wszystkie pliki.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2085">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="38fe0-2086">Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="38fe0-2087">Przykład 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="38fe0-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="38fe0-2088">Przykład 2:`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="38fe0-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="38fe0-2089">obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="38fe0-2090">Ta właściwość nie jest obsługiwana z systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="38fe0-2091">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2091">No</span></span> |
| <span data-ttu-id="38fe0-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="38fe0-2092">partitionedBy</span></span> |<span data-ttu-id="38fe0-2093">partitionedBy może służyć do określenia dynamiczne folderPath, nazwę pliku dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2093">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="38fe0-2094">Na przykład folderPath sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="38fe0-2095">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2095">No</span></span> |
| <span data-ttu-id="38fe0-2096">Format</span><span class="sxs-lookup"><span data-stu-id="38fe0-2096">format</span></span> | <span data-ttu-id="38fe0-2097">Obsługiwane są następujące typy format: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2097">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="38fe0-2098">Ustaw **typu** właściwości w formacie do jednej z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2098">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="38fe0-2099">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="38fe0-2100">Jeśli chcesz **skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcji format w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2100">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="38fe0-2101">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2101">No</span></span> |
| <span data-ttu-id="38fe0-2102">Kompresja</span><span class="sxs-lookup"><span data-stu-id="38fe0-2102">compression</span></span> | <span data-ttu-id="38fe0-2103">Określ typ i poziom kompresji danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2103">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="38fe0-2104">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**; i są obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="38fe0-2105">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="38fe0-2106">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2106">No</span></span> |
| <span data-ttu-id="38fe0-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="38fe0-2107">useBinaryTransfer</span></span> |<span data-ttu-id="38fe0-2108">Określ, czy używany tryb transferu binarnego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="38fe0-2109">Wartość true dla trybie binarnym i wartość false ASCII.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="38fe0-2110">Wartość domyślna: wartość True.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2110">Default value: True.</span></span> <span data-ttu-id="38fe0-2111">Ta właściwość jest używana tylko w przypadku typu skojarzonej połączonej usługi typu: SerwerFTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="38fe0-2112">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="38fe0-2113">Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="38fe0-2114">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="38fe0-2115">Aby uzyskać więcej informacji, zobacz [łącznik FTP](data-factory-ftp-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="38fe0-2116">Źródło systemu plików w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-2117">Jeśli dane są kopiowane z serwera FTP, ustaw **typ źródła** działania kopiowania do **FileSystemSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2117">If you are copying data from an FTP server, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-2118">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2118">Property</span></span> | <span data-ttu-id="38fe0-2119">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2119">Description</span></span> | <span data-ttu-id="38fe0-2120">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-2120">Allowed values</span></span> | <span data-ttu-id="38fe0-2121">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-2122">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="38fe0-2122">recursive</span></span> |<span data-ttu-id="38fe0-2123">Wskazuje, czy dane są odczytywane rekursywnie z folderów sub lub tylko określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2123">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="38fe0-2124">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2124">True, False (default)</span></span> |<span data-ttu-id="38fe0-2125">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-2126">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2126">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

<span data-ttu-id="38fe0-2127">Aby uzyskać więcej informacji, zobacz [łącznik FTP](data-factory-ftp-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="38fe0-2128">SYSTEM PLIKÓW HDFS</span><span class="sxs-lookup"><span data-stu-id="38fe0-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-2129">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2129">Linked service</span></span>
<span data-ttu-id="38fe0-2130">Aby zdefiniować HDFS połączonej usługi, ustaw **typu** połączonej usługi, aby **Hdfs**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2130">To define a HDFS linked service, set the **type** of the linked service to **Hdfs**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-2131">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2131">Property</span></span> | <span data-ttu-id="38fe0-2132">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2132">Description</span></span> | <span data-ttu-id="38fe0-2133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2134">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-2134">type</span></span> |<span data-ttu-id="38fe0-2135">Właściwość type musi mieć ustawioną: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="38fe0-2135">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="38fe0-2136">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2136">Yes</span></span> |
| <span data-ttu-id="38fe0-2137">Url</span><span class="sxs-lookup"><span data-stu-id="38fe0-2137">Url</span></span> |<span data-ttu-id="38fe0-2138">Adres URL do systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="38fe0-2138">URL to the HDFS</span></span> |<span data-ttu-id="38fe0-2139">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2139">Yes</span></span> |
| <span data-ttu-id="38fe0-2140">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-2140">authenticationType</span></span> |<span data-ttu-id="38fe0-2141">Anonimowe lub Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="38fe0-2142">Umożliwia **uwierzytelnianie Kerberos** łącznika systemu plików HDFS, można znaleźć w temacie [w tej sekcji](#use-kerberos-authentication-for-hdfs-connector) do odpowiednio skonfigurowane w lokalnym środowisku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2142">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="38fe0-2143">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2143">Yes</span></span> |
| <span data-ttu-id="38fe0-2144">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-2144">userName</span></span> |<span data-ttu-id="38fe0-2145">Uwierzytelnianie nazwy użytkownika dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="38fe0-2146">Tak (w przypadku uwierzytelniania systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="38fe0-2147">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-2147">password</span></span> |<span data-ttu-id="38fe0-2148">Hasło dla uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="38fe0-2149">Tak (w przypadku uwierzytelniania systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="38fe0-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2150">gatewayName</span></span> |<span data-ttu-id="38fe0-2151">Nazwa bramy, która powinna być używana do nawiązania połączenia systemu plików HDFS usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2151">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="38fe0-2152">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2152">Yes</span></span> |
| <span data-ttu-id="38fe0-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="38fe0-2153">encryptedCredential</span></span> |<span data-ttu-id="38fe0-2154">[Nowy AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) poświadczeń dostępu do danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="38fe0-2155">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="38fe0-2156">Przykład: Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="38fe0-2156">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="38fe0-2157">Przykład: Przy użyciu uwierzytelniania systemu Windows</span><span class="sxs-lookup"><span data-stu-id="38fe0-2157">Example: Using Windows authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="38fe0-2158">Aby uzyskać więcej informacji, zobacz [łącznika systemu plików HDFS](#data-factory-hdfs-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-2159">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-2159">Dataset</span></span>
<span data-ttu-id="38fe0-2160">Aby zdefiniować zestawu danych systemu plików HDFS, ustaw **typu** zestawu danych do **FileShare**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2160">To define a HDFS dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-2161">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2161">Property</span></span> | <span data-ttu-id="38fe0-2162">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2162">Description</span></span> | <span data-ttu-id="38fe0-2163">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="38fe0-2164">folderPath</span></span> |<span data-ttu-id="38fe0-2165">Ścieżka do folderu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2165">Path to the folder.</span></span> <span data-ttu-id="38fe0-2166">Przykład:`myfolder`</span><span class="sxs-lookup"><span data-stu-id="38fe0-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="38fe0-2167">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2167">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="38fe0-2168">Na przykład: folder\subfolder, określ folder\\\\podfolderów i dla d:\samplefolder, określ d:\\\\folder_przykładowy.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="38fe0-2169">Możesz łączyć tej właściwości z **partitionBy** do folderu ścieżki oparte na wycinku rozpoczęcia/zakończenia daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2169">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="38fe0-2170">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2170">Yes</span></span> |
| <span data-ttu-id="38fe0-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2171">fileName</span></span> |<span data-ttu-id="38fe0-2172">Określ nazwę pliku w **folderPath** aby tabela do odwoływania się do określonego pliku w folderze.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2172">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="38fe0-2173">Jeśli nie określono żadnej wartości dla tej właściwości, tabela wskazuje wszystkie pliki w folderze.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2173">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="38fe0-2174">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwę wygenerowanego pliku będzie poniżej tego formatu:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2174">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="38fe0-2175">Dane. <Guid>.txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="38fe0-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="38fe0-2176">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2176">No</span></span> |
| <span data-ttu-id="38fe0-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="38fe0-2177">partitionedBy</span></span> |<span data-ttu-id="38fe0-2178">partitionedBy może służyć do określenia dynamiczne folderPath, nazwę pliku dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2178">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="38fe0-2179">Przykład: folderPath sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="38fe0-2180">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2180">No</span></span> |
| <span data-ttu-id="38fe0-2181">Format</span><span class="sxs-lookup"><span data-stu-id="38fe0-2181">format</span></span> | <span data-ttu-id="38fe0-2182">Obsługiwane są następujące typy format: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2182">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="38fe0-2183">Ustaw **typu** właściwości w formacie do jednej z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2183">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="38fe0-2184">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="38fe0-2185">Jeśli chcesz **skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcji format w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2185">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="38fe0-2186">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2186">No</span></span> |
| <span data-ttu-id="38fe0-2187">Kompresja</span><span class="sxs-lookup"><span data-stu-id="38fe0-2187">compression</span></span> | <span data-ttu-id="38fe0-2188">Określ typ i poziom kompresji danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2188">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="38fe0-2189">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="38fe0-2190">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="38fe0-2191">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="38fe0-2192">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="38fe0-2193">Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="38fe0-2194">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2194">Example</span></span>

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="38fe0-2195">Aby uzyskać więcej informacji, zobacz [łącznika systemu plików HDFS](#data-factory-hdfs-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="38fe0-2196">Źródło systemu plików w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-2197">Jeśli dane są kopiowane z systemu plików HDFS, ustaw **typ źródła** działania kopiowania do **FileSystemSource**, a następnie określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2197">If you are copying data from HDFS, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="38fe0-2198">**FileSystemSource** obsługuje następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2198">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="38fe0-2199">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2199">Property</span></span> | <span data-ttu-id="38fe0-2200">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2200">Description</span></span> | <span data-ttu-id="38fe0-2201">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-2201">Allowed values</span></span> | <span data-ttu-id="38fe0-2202">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-2203">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="38fe0-2203">recursive</span></span> |<span data-ttu-id="38fe0-2204">Wskazuje, czy dane są odczytywane rekursywnie z folderów sub lub tylko określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2204">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="38fe0-2205">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2205">True, False (default)</span></span> |<span data-ttu-id="38fe0-2206">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-2207">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2207">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="38fe0-2208">Aby uzyskać więcej informacji, zobacz [łącznika systemu plików HDFS](#data-factory-hdfs-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="38fe0-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="38fe0-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="38fe0-2210">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2210">Linked service</span></span>
<span data-ttu-id="38fe0-2211">Aby zdefiniować SFTP połączonej usługi, ustaw **typu** połączonej usługi, aby **Sftp**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2211">To define an SFTP linked service, set the **type** of the linked service to **Sftp**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-2212">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2212">Property</span></span> | <span data-ttu-id="38fe0-2213">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2213">Description</span></span> | <span data-ttu-id="38fe0-2214">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-2215">Host</span><span class="sxs-lookup"><span data-stu-id="38fe0-2215">host</span></span> | <span data-ttu-id="38fe0-2216">Nazwa lub adres IP serwera SFTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2216">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="38fe0-2217">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2217">Yes</span></span> |
| <span data-ttu-id="38fe0-2218">port</span><span class="sxs-lookup"><span data-stu-id="38fe0-2218">port</span></span> |<span data-ttu-id="38fe0-2219">Port, na którym nasłuchuje serwer SFTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2219">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="38fe0-2220">Wartość domyślna to: 21</span><span class="sxs-lookup"><span data-stu-id="38fe0-2220">The default value is: 21</span></span> |<span data-ttu-id="38fe0-2221">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2221">No</span></span> |
| <span data-ttu-id="38fe0-2222">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-2222">authenticationType</span></span> |<span data-ttu-id="38fe0-2223">Określ typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2223">Specify authentication type.</span></span> <span data-ttu-id="38fe0-2224">Dozwolone wartości: **podstawowe**, **parametry SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="38fe0-2225">Zapoznaj się [uwierzytelnianie podstawowe Using](#using-basic-authentication) i [przy użyciu publicznego klucza uwierzytelniania SSH](#using-ssh-public-key-authentication) odpowiednio sekcje więcej właściwości i przykłady JSON.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2225">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="38fe0-2226">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2226">Yes</span></span> |
| <span data-ttu-id="38fe0-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="38fe0-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="38fe0-2228">Określ, czy pominąć sprawdzanie poprawności klucza hosta.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2228">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="38fe0-2229">Nie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2229">No.</span></span> <span data-ttu-id="38fe0-2230">Wartość domyślna: false</span><span class="sxs-lookup"><span data-stu-id="38fe0-2230">The default value: false</span></span> |
| <span data-ttu-id="38fe0-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="38fe0-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="38fe0-2232">Podaj odcisk palca klucza hosta.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2232">Specify the finger print of the host key.</span></span> | <span data-ttu-id="38fe0-2233">Tak, jeśli `skipHostKeyValidation` ma wartość false.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2233">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="38fe0-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2234">gatewayName</span></span> |<span data-ttu-id="38fe0-2235">Nazwa bramy zarządzania danymi do nawiązywania połączenia z serwerem lokalnym SFTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2235">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="38fe0-2236">Tak, jeśli kopiowanie danych z lokalnego serwera SFTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="38fe0-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="38fe0-2237">encryptedCredential</span></span> | <span data-ttu-id="38fe0-2238">Zaszyfrowane poświadczenia dostępu do serwera SFTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2238">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="38fe0-2239">Wygenerowany automatycznie po określeniu w kreatorze kopiowania lub w oknie podręcznym ClickOnce uwierzytelnianie podstawowe (nazwy użytkownika i hasła) lub uwierzytelniania parametry SshPublicKey (nazwy użytkownika i ścieżki do klucza prywatnego lub zawartości).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="38fe0-2240">Nie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2240">No.</span></span> <span data-ttu-id="38fe0-2241">Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera SFTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="38fe0-2242">Przykład: Przy użyciu uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="38fe0-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="38fe0-2243">Aby uwierzytelnianie podstawowe, należy ustawić `authenticationType` jako `Basic`i określ następujące właściwości poza łącznika SFTP ogólnego z nich wprowadzone w ostatniej sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2243">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="38fe0-2244">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2244">Property</span></span> | <span data-ttu-id="38fe0-2245">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2245">Description</span></span> | <span data-ttu-id="38fe0-2246">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-2247">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-2247">username</span></span> | <span data-ttu-id="38fe0-2248">Użytkownik, który ma dostęp do serwera SFTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2248">User who has access to the SFTP server.</span></span> |<span data-ttu-id="38fe0-2249">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2249">Yes</span></span> |
| <span data-ttu-id="38fe0-2250">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-2250">password</span></span> | <span data-ttu-id="38fe0-2251">Hasło dla użytkownika (username).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2251">Password for the user (username).</span></span> | <span data-ttu-id="38fe0-2252">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2252">Yes</span></span> |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="38fe0-2253">Przykład: Uwierzytelnianie podstawowe z zaszyfrowanych poświadczeń **</span><span class="sxs-lookup"><span data-stu-id="38fe0-2253">Example: Basic authentication with encrypted credential**</span></span>

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="38fe0-2254">Przy użyciu uwierzytelniania klucza publicznego SSH: **</span><span class="sxs-lookup"><span data-stu-id="38fe0-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="38fe0-2255">Aby uwierzytelnianie podstawowe, należy ustawić `authenticationType` jako `SshPublicKey`i określ następujące właściwości poza łącznika SFTP ogólnego z nich wprowadzone w ostatniej sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2255">To use basic authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="38fe0-2256">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2256">Property</span></span> | <span data-ttu-id="38fe0-2257">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2257">Description</span></span> | <span data-ttu-id="38fe0-2258">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-2259">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-2259">username</span></span> |<span data-ttu-id="38fe0-2260">Użytkownik, który ma dostęp do serwera SFTP</span><span class="sxs-lookup"><span data-stu-id="38fe0-2260">User who has access to the SFTP server</span></span> |<span data-ttu-id="38fe0-2261">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2261">Yes</span></span> |
| <span data-ttu-id="38fe0-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="38fe0-2262">privateKeyPath</span></span> | <span data-ttu-id="38fe0-2263">Określ ścieżka bezwzględna do pliku klucza prywatnego może dostęp do tej bramy.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2263">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="38fe0-2264">Określ `privateKeyPath` lub `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2264">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="38fe0-2265">Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera SFTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="38fe0-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="38fe0-2266">privateKeyContent</span></span> | <span data-ttu-id="38fe0-2267">Ciąg serializacji zawartość klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2267">A serialized string of the private key content.</span></span> <span data-ttu-id="38fe0-2268">Kreator kopiowania można odczytać pliku klucza prywatnego i Wyodrębnij zawartość klucza prywatnego automatycznie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2268">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="38fe0-2269">Jeśli używane są wszystkie inne narzędzie/pakiet SDK, należy użyć właściwości privateKeyPath.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2269">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="38fe0-2270">Określ `privateKeyPath` lub `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2270">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="38fe0-2271">Hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-2271">passPhrase</span></span> | <span data-ttu-id="38fe0-2272">Określ przebiegu frazy/hasło do odszyfrowania klucza prywatnego, jeśli plik klucza jest chroniony przez hasło.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2272">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="38fe0-2273">Tak, jeśli hasło jest chroniony plik klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2273">Yes if the private key file is protected by a pass phrase.</span></span> |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="38fe0-2274">Przykład: Parametry SshPublicKey uwierzytelniania za pomocą prywatnego klucza zawartości **</span><span class="sxs-lookup"><span data-stu-id="38fe0-2274">Example: SshPublicKey authentication using private key content**</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="38fe0-2275">Aby uzyskać więcej informacji, zobacz [łącznika SFTP](data-factory-sftp-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-2276">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-2276">Dataset</span></span>
<span data-ttu-id="38fe0-2277">Aby zdefiniować SFTP zestawu danych, ustaw **typu** zestawu danych do **FileShare**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2277">To define an SFTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-2278">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2278">Property</span></span> | <span data-ttu-id="38fe0-2279">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2279">Description</span></span> | <span data-ttu-id="38fe0-2280">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="38fe0-2281">folderPath</span></span> |<span data-ttu-id="38fe0-2282">Sub ścieżkę do folderu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2282">Sub path to the folder.</span></span> <span data-ttu-id="38fe0-2283">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2283">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="38fe0-2284">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="38fe0-2285">Możesz łączyć tej właściwości z **partitionBy** do folderu ścieżki oparte na wycinku rozpoczęcia/zakończenia daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2285">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="38fe0-2286">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2286">Yes</span></span> |
| <span data-ttu-id="38fe0-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2287">fileName</span></span> |<span data-ttu-id="38fe0-2288">Określ nazwę pliku w **folderPath** aby tabela do odwoływania się do określonego pliku w folderze.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2288">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="38fe0-2289">Jeśli nie określono żadnej wartości dla tej właściwości, tabela wskazuje wszystkie pliki w folderze.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2289">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="38fe0-2290">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwę wygenerowanego pliku będzie poniżej tego formatu:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2290">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="38fe0-2291">Dane. <Guid>.txt (przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="38fe0-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="38fe0-2292">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2292">No</span></span> |
| <span data-ttu-id="38fe0-2293">obiektu fileFilter</span><span class="sxs-lookup"><span data-stu-id="38fe0-2293">fileFilter</span></span> |<span data-ttu-id="38fe0-2294">Określ filtr służący do wybierania podzbioru pliki w ścieżce folderu, a nie wszystkie pliki.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2294">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="38fe0-2295">Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="38fe0-2296">Przykład 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="38fe0-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="38fe0-2297">Przykład 2:`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="38fe0-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="38fe0-2298">obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="38fe0-2299">Ta właściwość nie jest obsługiwana z systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="38fe0-2300">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2300">No</span></span> |
| <span data-ttu-id="38fe0-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="38fe0-2301">partitionedBy</span></span> |<span data-ttu-id="38fe0-2302">partitionedBy może służyć do określenia dynamiczne folderPath, nazwę pliku dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2302">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="38fe0-2303">Na przykład folderPath sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="38fe0-2304">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2304">No</span></span> |
| <span data-ttu-id="38fe0-2305">Format</span><span class="sxs-lookup"><span data-stu-id="38fe0-2305">format</span></span> | <span data-ttu-id="38fe0-2306">Obsługiwane są następujące typy format: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2306">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="38fe0-2307">Ustaw **typu** właściwości w formacie do jednej z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2307">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="38fe0-2308">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="38fe0-2309">Jeśli chcesz **skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcji format w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2309">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="38fe0-2310">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2310">No</span></span> |
| <span data-ttu-id="38fe0-2311">Kompresja</span><span class="sxs-lookup"><span data-stu-id="38fe0-2311">compression</span></span> | <span data-ttu-id="38fe0-2312">Określ typ i poziom kompresji danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2312">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="38fe0-2313">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="38fe0-2314">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="38fe0-2315">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="38fe0-2316">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2316">No</span></span> |
| <span data-ttu-id="38fe0-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="38fe0-2317">useBinaryTransfer</span></span> |<span data-ttu-id="38fe0-2318">Określ, czy używany tryb transferu binarnego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="38fe0-2319">Wartość true dla trybie binarnym i wartość false ASCII.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="38fe0-2320">Wartość domyślna: wartość True.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2320">Default value: True.</span></span> <span data-ttu-id="38fe0-2321">Ta właściwość jest używana tylko w przypadku typu skojarzonej połączonej usługi typu: SerwerFTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="38fe0-2322">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="38fe0-2323">Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="38fe0-2324">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="38fe0-2325">Aby uzyskać więcej informacji, zobacz [łącznika SFTP](data-factory-sftp-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="38fe0-2326">Źródło systemu plików w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-2327">Jeśli dane są kopiowane z użyciem protokołu SFTP źródła, ustaw **typ źródła** działania kopiowania do **FileSystemSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2327">If you are copying data from an SFTP source, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-2328">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2328">Property</span></span> | <span data-ttu-id="38fe0-2329">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2329">Description</span></span> | <span data-ttu-id="38fe0-2330">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-2330">Allowed values</span></span> | <span data-ttu-id="38fe0-2331">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-2332">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="38fe0-2332">recursive</span></span> |<span data-ttu-id="38fe0-2333">Wskazuje, czy dane są odczytywane rekursywnie z folderów sub lub tylko określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2333">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="38fe0-2334">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2334">True, False (default)</span></span> |<span data-ttu-id="38fe0-2335">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="38fe0-2336">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2336">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

<span data-ttu-id="38fe0-2337">Aby uzyskać więcej informacji, zobacz [łącznika SFTP](data-factory-sftp-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="38fe0-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="38fe0-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-2339">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2339">Linked service</span></span>
<span data-ttu-id="38fe0-2340">Aby zdefiniować HTTP połączonej usługi, ustaw **typu** połączonej usługi, aby **Http**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2340">To define a HTTP linked service, set the **type** of the linked service to **Http**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-2341">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2341">Property</span></span> | <span data-ttu-id="38fe0-2342">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2342">Description</span></span> | <span data-ttu-id="38fe0-2343">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2344">adres URL</span><span class="sxs-lookup"><span data-stu-id="38fe0-2344">url</span></span> | <span data-ttu-id="38fe0-2345">Podstawowy adres URL do serwera sieci Web</span><span class="sxs-lookup"><span data-stu-id="38fe0-2345">Base URL to the Web Server</span></span> | <span data-ttu-id="38fe0-2346">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2346">Yes</span></span> |
| <span data-ttu-id="38fe0-2347">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-2347">authenticationType</span></span> | <span data-ttu-id="38fe0-2348">Określa typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2348">Specifies the authentication type.</span></span> <span data-ttu-id="38fe0-2349">Dozwolone wartości to: **anonimowe**, **podstawowe**, **szyfrowanego**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="38fe0-2350">Odpowiednio można znaleźć w sekcjach poniżej tej tabeli na więcej właściwości i przykłady JSON dla tych typów uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2350">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="38fe0-2351">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2351">Yes</span></span> |
| <span data-ttu-id="38fe0-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="38fe0-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="38fe0-2353">Określ, czy włączyć weryfikacji certyfikatu serwera SSL, jeśli źródło jest serwer sieci Web protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="38fe0-2353">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="38fe0-2354">Nie, domyślna to true</span><span class="sxs-lookup"><span data-stu-id="38fe0-2354">No, default is true</span></span> |
| <span data-ttu-id="38fe0-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2355">gatewayName</span></span> | <span data-ttu-id="38fe0-2356">Nazwa bramy zarządzania danymi do łączenia się z lokalnym źródłem HTTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2356">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="38fe0-2357">Tak, jeśli kopiowanie danych z lokalnego źródła HTTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="38fe0-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="38fe0-2358">encryptedCredential</span></span> | <span data-ttu-id="38fe0-2359">Zaszyfrowane poświadczenia można uzyskać dostępu do punktu końcowego HTTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2359">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="38fe0-2360">Wygenerowany automatycznie podczas konfigurowania informacji o uwierzytelnianiu w kreatorze kopiowania lub w oknie podręcznym ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2360">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="38fe0-2361">Nie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2361">No.</span></span> <span data-ttu-id="38fe0-2362">Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera HTTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="38fe0-2363">Przykład: Uwierzytelnianie podstawowe, szyfrowane lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="38fe0-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="38fe0-2364">Ustaw `authenticationType` jako `Basic`, `Digest`, lub `Windows`i określ następujące właściwości poza łącznika HTTP ogólnego z nich wprowadzono powyżej:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="38fe0-2365">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2365">Property</span></span> | <span data-ttu-id="38fe0-2366">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2366">Description</span></span> | <span data-ttu-id="38fe0-2367">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2368">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-2368">username</span></span> | <span data-ttu-id="38fe0-2369">Nazwa użytkownika do uzyskania dostępu punkt końcowy HTTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2369">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="38fe0-2370">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2370">Yes</span></span> |
| <span data-ttu-id="38fe0-2371">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-2371">password</span></span> | <span data-ttu-id="38fe0-2372">Hasło dla użytkownika (username).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2372">Password for the user (username).</span></span> | <span data-ttu-id="38fe0-2373">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2373">Yes</span></span> |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="38fe0-2374">Przykład: Przy użyciu uwierzytelniania ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="38fe0-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="38fe0-2375">Aby uwierzytelnianie podstawowe, należy ustawić `authenticationType` jako `ClientCertificate`i określ następujące właściwości poza łącznika HTTP ogólnego z nich wprowadzono powyżej:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2375">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="38fe0-2376">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2376">Property</span></span> | <span data-ttu-id="38fe0-2377">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2377">Description</span></span> | <span data-ttu-id="38fe0-2378">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="38fe0-2379">embeddedCertData</span></span> | <span data-ttu-id="38fe0-2380">Zawartość algorytmem Base64 danych binarnych z pliku wymiany informacji osobistych (PFX).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2380">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="38fe0-2381">Określ `embeddedCertData` lub `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2381">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="38fe0-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="38fe0-2382">certThumbprint</span></span> | <span data-ttu-id="38fe0-2383">Odcisk palca certyfikatu, który został zainstalowany na komputerze bramy magazynu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2383">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="38fe0-2384">Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego źródła HTTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="38fe0-2385">Określ `embeddedCertData` lub `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2385">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="38fe0-2386">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-2386">password</span></span> | <span data-ttu-id="38fe0-2387">Hasło skojarzone z certyfikatem.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2387">Password associated with the certificate.</span></span> | <span data-ttu-id="38fe0-2388">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2388">No</span></span> |

<span data-ttu-id="38fe0-2389">Jeśli używasz `certThumbprint` dla uwierzytelniania i certyfikat jest zainstalowany w magazynie osobistym komputera lokalnego, należy udzielić uprawnień do odczytu do usługi bramy:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2389">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="38fe0-2390">Uruchom program Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="38fe0-2391">Dodaj **certyfikaty** przystawki przeznaczonego **komputera lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2391">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="38fe0-2392">Rozwiń węzeł **certyfikaty**, **osobistych**i kliknij przycisk **certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="38fe0-2393">Kliknij prawym przyciskiem myszy certyfikat z magazynu osobistego i wybierz **wszystkie zadania**->**Zarządzaj kluczami prywatnymi...**</span><span class="sxs-lookup"><span data-stu-id="38fe0-2393">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="38fe0-2394">Na **zabezpieczeń** , Dodaj konto użytkownika, pod którą jest uruchomiona usługa hosta bramy zarządzania danymi z dostępem do odczytu do certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2394">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

<span data-ttu-id="38fe0-2395">**Przykład: przy użyciu certyfikatu klienta:** to połączone usługi łączy fabrykę danych z lokalnego serwera sieci web HTTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2395">**Example: using client certificate:** This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="38fe0-2396">Używa certyfikatu klienta, który jest instalowany na komputerze z zainstalowana brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2396">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="38fe0-2397">Przykład: przy użyciu certyfikatu klienta w pliku</span><span class="sxs-lookup"><span data-stu-id="38fe0-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="38fe0-2398">Łącza usługi to połączone fabrykę danych z lokalnego serwera sieci web HTTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2398">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="38fe0-2399">Za pomocą pliku certyfikatu klienta na komputer i zainstalowana brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2399">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

<span data-ttu-id="38fe0-2400">Aby uzyskać więcej informacji, zobacz [łącznika HTTP](data-factory-http-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="38fe0-2401">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-2401">Dataset</span></span>
<span data-ttu-id="38fe0-2402">Aby zdefiniować zestawu danych HTTP, ustaw **typu** zestawu danych do **Http**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2402">To define a HTTP dataset, set the **type** of the dataset to **Http**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-2403">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2403">Property</span></span> | <span data-ttu-id="38fe0-2404">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2404">Description</span></span> | <span data-ttu-id="38fe0-2405">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="38fe0-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="38fe0-2406">relativeUrl</span></span> | <span data-ttu-id="38fe0-2407">Względny adres URL do zasobu, który zawiera dane.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2407">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="38fe0-2408">Jeśli ścieżka nie jest określona, używana jest tylko adres URL określony w definicji połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2408">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="38fe0-2409">Aby utworzyć dynamicznego adresu URL, można użyć [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md), przykład: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2409">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="38fe0-2410">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2410">No</span></span> |
| <span data-ttu-id="38fe0-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="38fe0-2411">requestMethod</span></span> | <span data-ttu-id="38fe0-2412">Metoda HTTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2412">Http method.</span></span> <span data-ttu-id="38fe0-2413">Dozwolone wartości to **UZYSKAĆ** lub **POST**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="38fe0-2414">Nie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2414">No.</span></span> <span data-ttu-id="38fe0-2415">Domyślnie jest `GET`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="38fe0-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="38fe0-2416">additionalHeaders</span></span> | <span data-ttu-id="38fe0-2417">Dodatkowych nagłówków żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="38fe0-2418">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2418">No</span></span> |
| <span data-ttu-id="38fe0-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="38fe0-2419">requestBody</span></span> | <span data-ttu-id="38fe0-2420">Treść żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2420">Body for HTTP request.</span></span> | <span data-ttu-id="38fe0-2421">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2421">No</span></span> |
| <span data-ttu-id="38fe0-2422">Format</span><span class="sxs-lookup"><span data-stu-id="38fe0-2422">format</span></span> | <span data-ttu-id="38fe0-2423">Jeśli chcesz po prostu **pobierają dane z punktu końcowego HTTP jako — jest** bez podczas analizowania, Pomiń ten ustawienia formatu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2423">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="38fe0-2424">Jeśli chcesz przeanalizować zawartości odpowiedzi HTTP podczas kopiowania, obsługiwane są następujące typy format: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2424">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="38fe0-2425">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="38fe0-2426">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2426">No</span></span> |
| <span data-ttu-id="38fe0-2427">Kompresja</span><span class="sxs-lookup"><span data-stu-id="38fe0-2427">compression</span></span> | <span data-ttu-id="38fe0-2428">Określ typ i poziom kompresji danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2428">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="38fe0-2429">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="38fe0-2430">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="38fe0-2431">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="38fe0-2432">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2432">No</span></span> |

#### <a name="example-using-the-get-default-method"></a><span data-ttu-id="38fe0-2433">Przykład: używających metody GET (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2433">Example: using the GET (default) method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-the-post-method"></a><span data-ttu-id="38fe0-2434">Przykład: przy użyciu metody POST</span><span class="sxs-lookup"><span data-stu-id="38fe0-2434">Example: using the POST method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="38fe0-2435">Aby uzyskać więcej informacji, zobacz [łącznika HTTP](data-factory-http-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="38fe0-2436">Źródła HTTP w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-2437">Jeśli dane są kopiowane ze źródła HTTP, ustaw **typ źródła** działania kopiowania do **HttpSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2437">If you are copying data from a HTTP source, set the **source type** of the copy activity to **HttpSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-2438">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2438">Property</span></span> | <span data-ttu-id="38fe0-2439">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2439">Description</span></span> | <span data-ttu-id="38fe0-2440">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="38fe0-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="38fe0-2441">httpRequestTimeout</span></span> | <span data-ttu-id="38fe0-2442">Limit czasu (TimeSpan) dla żądania HTTP można uzyskać odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2442">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="38fe0-2443">Limit czasu jest uzyskanie odpowiedzi nie limitu czasu można odczytać danych odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2443">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="38fe0-2444">Nie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2444">No.</span></span> <span data-ttu-id="38fe0-2445">Wartość domyślna: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="38fe0-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="38fe0-2446">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-2447">Aby uzyskać więcej informacji, zobacz [łącznika HTTP](data-factory-http-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="38fe0-2448">OData</span><span class="sxs-lookup"><span data-stu-id="38fe0-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-2449">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2449">Linked service</span></span>
<span data-ttu-id="38fe0-2450">Aby zdefiniować OData połączonej usługi, ustaw **typu** połączonej usługi, aby **OData**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2450">To define an OData linked service, set the **type** of the linked service to **OData**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-2451">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2451">Property</span></span> | <span data-ttu-id="38fe0-2452">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2452">Description</span></span> | <span data-ttu-id="38fe0-2453">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2454">adres URL</span><span class="sxs-lookup"><span data-stu-id="38fe0-2454">url</span></span> |<span data-ttu-id="38fe0-2455">Adres URL usługi OData.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2455">Url of the OData service.</span></span> |<span data-ttu-id="38fe0-2456">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2456">Yes</span></span> |
| <span data-ttu-id="38fe0-2457">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-2457">authenticationType</span></span> |<span data-ttu-id="38fe0-2458">Typ uwierzytelniania używany do nawiązania połączenia źródła OData.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2458">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="38fe0-2459">Chmury OData możliwe wartości to anonimowe, podstawowe i OAuth (Uwaga obecnie tylko pomocy technicznej usługi fabryka danych Azure OAuth opartej na usłudze Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="38fe0-2460">Dla protokołu OData lokalnymi możliwe wartości to anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="38fe0-2461">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2461">Yes</span></span> |
| <span data-ttu-id="38fe0-2462">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-2462">username</span></span> |<span data-ttu-id="38fe0-2463">Określ nazwę użytkownika, jeśli używasz uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="38fe0-2464">Tak (tylko wtedy, gdy używasz uwierzytelniania podstawowego)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="38fe0-2465">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-2465">password</span></span> |<span data-ttu-id="38fe0-2466">Określ hasło dla konta użytkownika, określone nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2466">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="38fe0-2467">Tak (tylko wtedy, gdy używasz uwierzytelniania podstawowego)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="38fe0-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="38fe0-2468">authorizedCredential</span></span> |<span data-ttu-id="38fe0-2469">Jeśli używasz uwierzytelniania OAuth, kliknij przycisk **autoryzacji** przycisku w kreatorze kopiowania fabryki danych lub edytorze, a następnie wprowadź Twoje poświadczenia wartość tej właściwości będzie wygenerowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2469">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="38fe0-2470">Tak (tylko wtedy, gdy używasz uwierzytelniania OAuth)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="38fe0-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2471">gatewayName</span></span> |<span data-ttu-id="38fe0-2472">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną usługą OData.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2472">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="38fe0-2473">Określ tylko, jeśli dane są kopiowane z lokalnego źródła OData.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="38fe0-2474">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="38fe0-2475">Przykład — przy użyciu uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="38fe0-2475">Example - Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="38fe0-2476">Przykład — przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="38fe0-2476">Example - Using Anonymous authentication</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="38fe0-2477">Przykład — Windows przy użyciu uwierzytelniania dostępu do lokalnego źródła OData</span><span class="sxs-lookup"><span data-stu-id="38fe0-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="38fe0-2478">Przykład — przy użyciu uwierzytelniania OAuth, uzyskiwanie dostępu do chmury źródło OData</span><span class="sxs-lookup"><span data-stu-id="38fe0-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="38fe0-2479">Aby uzyskać więcej informacji, zobacz [łącznika OData](data-factory-odata-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="38fe0-2480">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-2480">Dataset</span></span>
<span data-ttu-id="38fe0-2481">Aby zdefiniować zestaw danych OData, ustaw **typu** zestawu danych do **ODataResource**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2481">To define an OData dataset, set the **type** of the dataset to **ODataResource**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-2482">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2482">Property</span></span> | <span data-ttu-id="38fe0-2483">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2483">Description</span></span> | <span data-ttu-id="38fe0-2484">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2485">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="38fe0-2485">path</span></span> |<span data-ttu-id="38fe0-2486">Ścieżka do zasobu OData</span><span class="sxs-lookup"><span data-stu-id="38fe0-2486">Path to the OData resource</span></span> |<span data-ttu-id="38fe0-2487">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-2488">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2488">Example</span></span>

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

<span data-ttu-id="38fe0-2489">Aby uzyskać więcej informacji, zobacz [łącznika OData](data-factory-odata-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="38fe0-2490">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-2491">Jeśli dane są kopiowane ze źródła danych OData, ustaw **typ źródła** działania kopiowania do **RelationalSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2491">If you are copying data from an OData source, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-2492">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2492">Property</span></span> | <span data-ttu-id="38fe0-2493">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2493">Description</span></span> | <span data-ttu-id="38fe0-2494">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2494">Example</span></span> | <span data-ttu-id="38fe0-2495">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-2496">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-2496">query</span></span> |<span data-ttu-id="38fe0-2497">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2497">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-2498">"? $select = nazwa, opis i $top = 5"</span><span class="sxs-lookup"><span data-stu-id="38fe0-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="38fe0-2499">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-2500">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2500">Example</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

<span data-ttu-id="38fe0-2501">Aby uzyskać więcej informacji, zobacz [łącznika OData](data-factory-odata-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="38fe0-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="38fe0-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="38fe0-2503">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2503">Linked service</span></span>
<span data-ttu-id="38fe0-2504">Aby zdefiniować ODBC połączonej usługi, ustaw **typu** połączonej usługi, aby **OnPremisesOdbc**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2504">To define an ODBC linked service, set the **type** of the linked service to **OnPremisesOdbc**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-2505">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2505">Property</span></span> | <span data-ttu-id="38fe0-2506">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2506">Description</span></span> | <span data-ttu-id="38fe0-2507">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2508">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="38fe0-2508">connectionString</span></span> |<span data-ttu-id="38fe0-2509">Poświadczenie dostępu z systemem innym niż część ciąg połączenia i opcjonalnie zaszyfrowane poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2509">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="38fe0-2510">Przykłady w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2510">See examples in the following sections.</span></span> |<span data-ttu-id="38fe0-2511">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2511">Yes</span></span> |
| <span data-ttu-id="38fe0-2512">poświadczenia</span><span class="sxs-lookup"><span data-stu-id="38fe0-2512">credential</span></span> |<span data-ttu-id="38fe0-2513">Dostęp do poświadczeń część ciągu połączenia określonego w formacie wartości właściwości sterownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2513">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="38fe0-2514">Przykład: "Uid =<user ID>; Pwd =<password>; RefreshToken =<secret refresh token>; ".</span><span class="sxs-lookup"><span data-stu-id="38fe0-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="38fe0-2515">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2515">No</span></span> |
| <span data-ttu-id="38fe0-2516">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-2516">authenticationType</span></span> |<span data-ttu-id="38fe0-2517">Typ uwierzytelniania używany do łączenia się z magazynem danych ODBC.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2517">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="38fe0-2518">Możliwe wartości to: anonimowych, jak i podstawowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="38fe0-2519">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2519">Yes</span></span> |
| <span data-ttu-id="38fe0-2520">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-2520">username</span></span> |<span data-ttu-id="38fe0-2521">Określ nazwę użytkownika, jeśli używasz uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="38fe0-2522">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2522">No</span></span> |
| <span data-ttu-id="38fe0-2523">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-2523">password</span></span> |<span data-ttu-id="38fe0-2524">Określ hasło dla konta użytkownika, określone nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2524">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="38fe0-2525">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2525">No</span></span> |
| <span data-ttu-id="38fe0-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2526">gatewayName</span></span> |<span data-ttu-id="38fe0-2527">Nazwa bramy, która powinna być używana przez usługi fabryka danych do połączenia z magazynem danych ODBC.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2527">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="38fe0-2528">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="38fe0-2529">Przykład — przy użyciu uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="38fe0-2529">Example - Using Basic authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="38fe0-2530">Przykład — użyciu zaszyfrowane poświadczenia uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="38fe0-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="38fe0-2531">Można szyfrować poświadczeń przy użyciu [AzureRMDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/mt603802.aspx) polecenia cmdlet (w wersji 1.0 programu Azure PowerShell) lub [AzureDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 lub starszej wersji programu Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2531">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="38fe0-2532">Przykład: Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="38fe0-2532">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="38fe0-2533">Aby uzyskać więcej informacji, zobacz [łącznika ODBC](data-factory-odbc-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-2534">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-2534">Dataset</span></span>
<span data-ttu-id="38fe0-2535">Aby zdefiniować zestaw danych ODBC, ustaw **typu** zestawu danych do **RelationalTable**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2535">To define an ODBC dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-2536">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2536">Property</span></span> | <span data-ttu-id="38fe0-2537">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2537">Description</span></span> | <span data-ttu-id="38fe0-2538">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2539">tableName</span></span> |<span data-ttu-id="38fe0-2540">Nazwa tabeli w magazynie danych ODBC.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2540">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="38fe0-2541">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="38fe0-2542">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2542">Example</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="38fe0-2543">Aby uzyskać więcej informacji, zobacz [łącznika ODBC](data-factory-odbc-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="38fe0-2544">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-2545">Jeśli dane są kopiowane z magazynu danych ODBC, ustaw **typ źródła** działania kopiowania do **RelationalSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2545">If you are copying data from an ODBC data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-2546">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2546">Property</span></span> | <span data-ttu-id="38fe0-2547">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2547">Description</span></span> | <span data-ttu-id="38fe0-2548">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-2548">Allowed values</span></span> | <span data-ttu-id="38fe0-2549">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-2550">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-2550">query</span></span> |<span data-ttu-id="38fe0-2551">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2551">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-2552">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2552">SQL query string.</span></span> <span data-ttu-id="38fe0-2553">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="38fe0-2554">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-2555">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2555">Example</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

<span data-ttu-id="38fe0-2556">Aby uzyskać więcej informacji, zobacz [łącznika ODBC](data-factory-odbc-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="38fe0-2557">SalesForce</span><span class="sxs-lookup"><span data-stu-id="38fe0-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="38fe0-2558">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2558">Linked service</span></span>
<span data-ttu-id="38fe0-2559">Aby zdefiniować Salesforce połączonej usługi, ustaw **typu** połączonej usługi, aby **Salesforce**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2559">To define a Salesforce linked service, set the **type** of the linked service to **Salesforce**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-2560">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2560">Property</span></span> | <span data-ttu-id="38fe0-2561">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2561">Description</span></span> | <span data-ttu-id="38fe0-2562">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="38fe0-2563">environmentUrl</span></span> | <span data-ttu-id="38fe0-2564">Określ wystąpienie adres URL usługi Salesforce.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2564">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="38fe0-2565">-Domyślna to "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="38fe0-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="38fe0-2566">-Aby skopiować dane z piaskownicy, określ "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="38fe0-2566">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="38fe0-2567">-Aby skopiować dane z domeny niestandardowej, określ, na przykład "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="38fe0-2567">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="38fe0-2568">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2568">No</span></span> |
| <span data-ttu-id="38fe0-2569">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-2569">username</span></span> |<span data-ttu-id="38fe0-2570">Określ nazwę użytkownika dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2570">Specify a user name for the user account.</span></span> |<span data-ttu-id="38fe0-2571">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2571">Yes</span></span> |
| <span data-ttu-id="38fe0-2572">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-2572">password</span></span> |<span data-ttu-id="38fe0-2573">Określ hasło dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2573">Specify a password for the user account.</span></span> |<span data-ttu-id="38fe0-2574">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2574">Yes</span></span> |
| <span data-ttu-id="38fe0-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="38fe0-2575">securityToken</span></span> |<span data-ttu-id="38fe0-2576">Określ tokenu zabezpieczającego dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2576">Specify a security token for the user account.</span></span> <span data-ttu-id="38fe0-2577">Zobacz [uzyskać token zabezpieczeń](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) instrukcje dotyczące resetowania/Get tokenu zabezpieczającego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="38fe0-2578">Aby dowiedzieć się więcej o tokeny zabezpieczające ogólnie rzecz biorąc, zobacz [zabezpieczeń i interfejsu API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2578">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="38fe0-2579">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-2580">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2580">Example</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

<span data-ttu-id="38fe0-2581">Aby uzyskać więcej informacji, zobacz [łącznika usług Salesforce](data-factory-salesforce-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-2582">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-2582">Dataset</span></span>
<span data-ttu-id="38fe0-2583">Aby zdefiniować Salesforce zestawu danych, ustaw **typu** zestawu danych do **RelationalTable**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2583">To define a Salesforce dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-2584">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2584">Property</span></span> | <span data-ttu-id="38fe0-2585">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2585">Description</span></span> | <span data-ttu-id="38fe0-2586">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2587">tableName</span></span> |<span data-ttu-id="38fe0-2588">Nazwa tabeli w usłudze Salesforce.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2588">Name of the table in Salesforce.</span></span> |<span data-ttu-id="38fe0-2589">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-2590">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2590">Example</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="38fe0-2591">Aby uzyskać więcej informacji, zobacz [łącznika usług Salesforce](data-factory-salesforce-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="38fe0-2592">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-2593">Jeśli dane są kopiowane z usług Salesforce, ustaw **typ źródła** działania kopiowania do **RelationalSource**i określ następujące właściwości w **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2593">If you are copying data from Salesforce, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="38fe0-2594">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2594">Property</span></span> | <span data-ttu-id="38fe0-2595">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2595">Description</span></span> | <span data-ttu-id="38fe0-2596">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="38fe0-2596">Allowed values</span></span> | <span data-ttu-id="38fe0-2597">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38fe0-2598">query</span><span class="sxs-lookup"><span data-stu-id="38fe0-2598">query</span></span> |<span data-ttu-id="38fe0-2599">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2599">Use the custom query to read data.</span></span> |<span data-ttu-id="38fe0-2600">Zapytania SQL 92 lub [Salesforce obiektu Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) zapytania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="38fe0-2601">Przykład: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="38fe0-2602">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2602">No (if the **tableName** of the **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-2603">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="38fe0-2604">Część "__c" Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2604">The "__c" part of the API Name is needed for any custom object.</span></span>

<span data-ttu-id="38fe0-2605">Aby uzyskać więcej informacji, zobacz [łącznika usług Salesforce](data-factory-salesforce-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="38fe0-2606">Dane sieci Web</span><span class="sxs-lookup"><span data-stu-id="38fe0-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="38fe0-2607">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2607">Linked service</span></span>
<span data-ttu-id="38fe0-2608">Aby zdefiniować sieci Web połączonej usługi, ustaw **typu** połączonej usługi, aby **sieci Web**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2608">To define a Web linked service, set the **type** of the linked service to **Web**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-2609">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2609">Property</span></span> | <span data-ttu-id="38fe0-2610">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2610">Description</span></span> | <span data-ttu-id="38fe0-2611">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2612">Url</span><span class="sxs-lookup"><span data-stu-id="38fe0-2612">Url</span></span> |<span data-ttu-id="38fe0-2613">Adres URL źródła w sieci Web</span><span class="sxs-lookup"><span data-stu-id="38fe0-2613">URL to the Web source</span></span> |<span data-ttu-id="38fe0-2614">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2614">Yes</span></span> |
| <span data-ttu-id="38fe0-2615">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="38fe0-2615">authenticationType</span></span> |<span data-ttu-id="38fe0-2616">Anonimowe.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2616">Anonymous.</span></span> |<span data-ttu-id="38fe0-2617">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="38fe0-2618">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2618">Example</span></span>


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="38fe0-2619">Aby uzyskać więcej informacji, zobacz [łącznika tabeli Web](data-factory-web-table-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="38fe0-2620">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-2620">Dataset</span></span>
<span data-ttu-id="38fe0-2621">Aby zdefiniować zestawu danych w sieci Web, ustaw **typu** zestawu danych do **tabeli WebTable**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2621">To define a Web dataset, set the **type** of the dataset to **WebTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="38fe0-2622">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2622">Property</span></span> | <span data-ttu-id="38fe0-2623">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2623">Description</span></span> | <span data-ttu-id="38fe0-2624">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="38fe0-2625">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-2625">type</span></span> |<span data-ttu-id="38fe0-2626">Typ zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2626">type of the dataset.</span></span> <span data-ttu-id="38fe0-2627">należy wybrać opcję **tabeli WebTable**</span><span class="sxs-lookup"><span data-stu-id="38fe0-2627">must be set to **WebTable**</span></span> |<span data-ttu-id="38fe0-2628">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2628">Yes</span></span> |
| <span data-ttu-id="38fe0-2629">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="38fe0-2629">path</span></span> |<span data-ttu-id="38fe0-2630">Względny adres URL do zasobu, który zawiera tabelę.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2630">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="38fe0-2631">Nie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2631">No.</span></span> <span data-ttu-id="38fe0-2632">Jeśli ścieżka nie jest określona, używana jest tylko adres URL określony w definicji połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2632">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="38fe0-2633">Indeks</span><span class="sxs-lookup"><span data-stu-id="38fe0-2633">index</span></span> |<span data-ttu-id="38fe0-2634">Indeks tabeli w zasobie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2634">The index of the table in the resource.</span></span> <span data-ttu-id="38fe0-2635">Zobacz [Get indeksu tabeli na stronie HTML](#get-index-of-a-table-in-an-html-page) sekcji, aby instrukcje dotyczące pobierania indeksu tabeli na stronie HTML.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="38fe0-2636">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="38fe0-2637">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2637">Example</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="38fe0-2638">Aby uzyskać więcej informacji, zobacz [łącznika tabeli Web](data-factory-web-table-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="38fe0-2639">Źródło w sieci Web w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="38fe0-2640">Jeśli dane są kopiowane z tabeli sieci web, należy ustawić **typ źródła** działania kopiowania do **WebSource**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2640">If you are copying data from a web table, set the **source type** of the copy activity to **WebSource**.</span></span> <span data-ttu-id="38fe0-2641">Obecnie, gdy źródła w przypadku działania kopiowania jest typu **WebSource**, są obsługiwane żadne dodatkowe właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2641">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="38fe0-2642">Przykład</span><span class="sxs-lookup"><span data-stu-id="38fe0-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="38fe0-2643">Aby uzyskać więcej informacji, zobacz [łącznika tabeli Web](data-factory-web-table-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="38fe0-2644">ŚRODOWISKA OBLICZENIOWE</span><span class="sxs-lookup"><span data-stu-id="38fe0-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="38fe0-2645">W poniższej tabeli wymieniono środowiska obliczeniowe obsługiwane przez fabryki danych i działań przekształcania, które można uruchomić na nich.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2645">The following table lists the compute environments supported by Data Factory and the transformation activities that can run on them.</span></span> <span data-ttu-id="38fe0-2646">Kliknij łącze do obliczeń, który chcesz wyświetlić schematów JSON połączonej usługi połączyć je z fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2646">Click the link for the compute you are interested in to see the JSON schemas for linked service to link it to a data factory.</span></span> 

| <span data-ttu-id="38fe0-2647">Środowisko obliczeniowe</span><span class="sxs-lookup"><span data-stu-id="38fe0-2647">Compute environment</span></span> | <span data-ttu-id="38fe0-2648">Działania</span><span class="sxs-lookup"><span data-stu-id="38fe0-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="38fe0-2649">[Klaster usługi HDInsight na żądanie](#on-demand-azure-hdinsight-cluster) lub [klastrem usługi HDInsight](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="38fe0-2650">[Działania niestandardowego .NET](#net-custom-activity), [Hive działania](#hdinsight-hive-activity), [wieprzowa działania] (#hdinsight-pig działania [działania MapReduce](#hdinsight-mapreduce-activity), [przesyłanie strumieniowe działania Hadoop](#hdinsight-streaming-activityd), [Spark działania](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="38fe0-2651">Partia zadań Azure</span><span class="sxs-lookup"><span data-stu-id="38fe0-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="38fe0-2652">Niestandardowe działanie platformy .NET</span><span class="sxs-lookup"><span data-stu-id="38fe0-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="38fe0-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="38fe0-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="38fe0-2654">[Działanie wykonywania wsadowego uczenia maszynowego](#machine-learning-batch-execution-activity), [działanie aktualizacji zasobu uczenia maszynowego](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="38fe0-2655">Usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="38fe0-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="38fe0-2656">Język U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="38fe0-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="38fe0-2657">[Baza danych Azure SQL](#azure-sql-database-1), [magazyn danych Azure SQL](#azure-sql-data-warehouse-1), [programu SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="38fe0-2658">Procedura składowana</span><span class="sxs-lookup"><span data-stu-id="38fe0-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="38fe0-2659">Klaster Azure HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="38fe0-2660">Usługi fabryka danych Azure może automatycznie tworzyć opartych na systemie Windows/Linux klastra usługi HDInsight na żądanie do przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2660">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span></span> <span data-ttu-id="38fe0-2661">Klaster jest tworzony w tym samym regionie co skojarzone z klastrem konta magazynu (właściwość linkedServiceName w formacie JSON).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2661">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span></span> <span data-ttu-id="38fe0-2662">Można uruchamiać następujących działań transformacji na tej połączonej usługi: [działania niestandardowego .NET](#net-custom-activity), [Hive działania](#hdinsight-hive-activity), [wieprzowa działania] (#hdinsight-pig działania [działania MapReduce](#hdinsight-mapreduce-activity), [przesyłanie strumieniowe działania Hadoop](#hdinsight-streaming-activityd), [Spark działania](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2662">You can run the following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="38fe0-2663">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2663">Linked service</span></span> 
<span data-ttu-id="38fe0-2664">Poniższa tabela zawiera opisy właściwości używane w definicji Azure JSON usługi HDInsight połączony na żądanie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2664">The following table provides descriptions for the properties used in the Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="38fe0-2665">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2665">Property</span></span> | <span data-ttu-id="38fe0-2666">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2666">Description</span></span> | <span data-ttu-id="38fe0-2667">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2668">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-2668">type</span></span> |<span data-ttu-id="38fe0-2669">Powinien mieć ustawioną właściwość type **HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2669">The type property should be set to **HDInsightOnDemand**.</span></span> |<span data-ttu-id="38fe0-2670">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2670">Yes</span></span> |
| <span data-ttu-id="38fe0-2671">Wartość ClusterSize</span><span class="sxs-lookup"><span data-stu-id="38fe0-2671">clusterSize</span></span> |<span data-ttu-id="38fe0-2672">Liczba węzłów procesu roboczego/danych w klastrze.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2672">Number of worker/data nodes in the cluster.</span></span> <span data-ttu-id="38fe0-2673">Klaster usługi HDInsight jest tworzony z głównymi węzłami 2 wraz z liczbą węzłów procesu roboczego, które określisz dla tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2673">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span></span> <span data-ttu-id="38fe0-2674">Węzły mają rozmiar Standard_D3, który ma 4 rdzenie, więc klastra z węzłem procesu roboczego 4 przyjmuje 24 rdzenie (4\*4 = 16 rdzenie dla węzłów procesu roboczego, a także 2\*rdzenie 4 = 8 dla węzłów głównych).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2674">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="38fe0-2675">Zobacz [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) szczegółowe informacje na temat warstwy Standard_D3.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span></span> |<span data-ttu-id="38fe0-2676">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2676">Yes</span></span> |
| <span data-ttu-id="38fe0-2677">wartość TimeToLive</span><span class="sxs-lookup"><span data-stu-id="38fe0-2677">timetolive</span></span> |<span data-ttu-id="38fe0-2678">Limit czasu bezczynności klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2678">The allowed idle time for the on-demand HDInsight cluster.</span></span> <span data-ttu-id="38fe0-2679">Określa, jak długo klastra usługi HDInsight na żądanie pozostaje aktywne po zakończeniu działania uruchamiania, jeśli w klastrze nie ma żadnych aktywnych działań.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2679">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span></span><br/><br/><span data-ttu-id="38fe0-2680">Na przykład jeśli uruchomienia działania trwa 6 minut i timetolive jest ustawiony na 5 minut, klaster pozostanie aktywności 5 minut po uruchomieniu 6 minut przetwarzania działania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2680">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span></span> <span data-ttu-id="38fe0-2681">Jeśli inny uruchamiania działania jest wykonywane z okna 6 minut, jednak jest przetwarzany przez tego samego klastra.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2681">If another activity run is executed with the 6 minutes window, it is processed by the same cluster.</span></span><br/><br/><span data-ttu-id="38fe0-2682">Tworzenie klastra usługi HDInsight na żądanie jest kosztowna operacja (może to potrwać pewien czas), użyj tak, to ustawienie jako potrzebne do zwiększenia wydajności fabryki danych przez ponowne użycie klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="38fe0-2683">Jeśli wartość timetolive jest ustawiona na 0, klastra jest usuwany natychmiast uruchomić działanie w przetworzonej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2683">If you set timetolive value to 0, the cluster is deleted as soon as the activity run in processed.</span></span> <span data-ttu-id="38fe0-2684">Z drugiej strony Jeśli ustawisz wysokiej wartości klastra może pozostać bezczynny, co niepotrzebnie wysokich kosztów.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2684">On the other hand, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="38fe0-2685">Dlatego jest ważne, aby ustawić odpowiednią wartość, na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2685">Therefore, it is important that you set the appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="38fe0-2686">Wiele potoki mogą współużytkować tego samego wystąpienia klastra usługi HDInsight na żądanie w przypadku skonfigurowana wartość timetolive właściwości</span><span class="sxs-lookup"><span data-stu-id="38fe0-2686">Multiple pipelines can share the same instance of the on-demand HDInsight cluster if the timetolive property value is appropriately set</span></span> |<span data-ttu-id="38fe0-2687">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2687">Yes</span></span> |
| <span data-ttu-id="38fe0-2688">Wersja</span><span class="sxs-lookup"><span data-stu-id="38fe0-2688">version</span></span> |<span data-ttu-id="38fe0-2689">Wersja klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2689">Version of the HDInsight cluster.</span></span> <span data-ttu-id="38fe0-2690">Aby uzyskać więcej informacji, zobacz [obsługiwane wersje usługi HDInsight w fabryce danych Azure](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="38fe0-2691">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2691">No</span></span> |
| <span data-ttu-id="38fe0-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2692">linkedServiceName</span></span> |<span data-ttu-id="38fe0-2693">Azure połączonej usługi magazynu do użycia przez klaster na żądanie do przechowywania i przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2693">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="38fe0-2694">Obecnie nie można utworzyć klastra usługi HDInsight na żądanie, która używa usługi Azure Data Lake Store jako magazynu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span></span> <span data-ttu-id="38fe0-2695">Jeśli chcesz przechowywać dane wynikowe z HDInsight przetwarzania w usłudze Azure Data Lake Store, umożliwia działanie kopiowania skopiować dane z magazynu obiektów Blob Azure do usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2695">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="38fe0-2696">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2696">Yes</span></span> |
| <span data-ttu-id="38fe0-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="38fe0-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="38fe0-2698">Określa, że dodatkowe konta magazynu dla usługi HDInsight połączonej usługi, dzięki czemu usługi fabryka danych można zarejestrować je w Twoim imieniu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2698">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="38fe0-2699">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2699">No</span></span> |
| <span data-ttu-id="38fe0-2700">osType</span><span class="sxs-lookup"><span data-stu-id="38fe0-2700">osType</span></span> |<span data-ttu-id="38fe0-2701">Typ systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2701">Type of operating system.</span></span> <span data-ttu-id="38fe0-2702">Dozwolone wartości to: (domyślnie) systemu Windows i Linux</span><span class="sxs-lookup"><span data-stu-id="38fe0-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="38fe0-2703">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2703">No</span></span> |
| <span data-ttu-id="38fe0-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="38fe0-2705">Nazwa programu Azure SQL połączonej usługi, które HCatalog bazy danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2705">The name of Azure SQL linked service that point to the HCatalog database.</span></span> <span data-ttu-id="38fe0-2706">Klaster usługi HDInsight na żądanie jest tworzona przy użyciu bazy danych Azure SQL jako potrzeby magazynu metadanych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2706">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span></span> |<span data-ttu-id="38fe0-2707">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="38fe0-2708">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-2708">JSON example</span></span>
<span data-ttu-id="38fe0-2709">Następujące JSON definiuje opartych na systemie Linux usługi HDInsight połączony na żądanie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2709">The following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="38fe0-2710">Usługi fabryka danych automatycznie tworzy **opartych na systemie Linux** klastra usługi HDInsight podczas przetwarzania wycinka danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2710">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

<span data-ttu-id="38fe0-2711">Aby uzyskać więcej informacji, zobacz [obliczeniowe połączonych usług](data-factory-compute-linked-services.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="38fe0-2712">Istniejący klaster Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="38fe0-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="38fe0-2713">Można utworzyć usługi Azure HDInsight połączony do zarejestrowania klastrem usługi HDInsight przy użyciu fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2713">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="38fe0-2714">Można wykonać następujące działania przekształcania danych na tej połączonej usługi: [działania niestandardowego .NET](#net-custom-activity), [Hive działania](#hdinsight-hive-activity), [wieprzowa działania] (#hdinsight-pig działania [działania MapReduce](#hdinsight-mapreduce-activity), [przesyłanie strumieniowe działania Hadoop](#hdinsight-streaming-activityd), [Spark działania](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2714">You can run the following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="38fe0-2715">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2715">Linked service</span></span>
<span data-ttu-id="38fe0-2716">Poniższa tabela zawiera opisy właściwości używane w definicji Azure JSON usługi Azure HDInsight połączone.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2716">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="38fe0-2717">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2717">Property</span></span> | <span data-ttu-id="38fe0-2718">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2718">Description</span></span> | <span data-ttu-id="38fe0-2719">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2720">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-2720">type</span></span> |<span data-ttu-id="38fe0-2721">Powinien mieć ustawioną właściwość type **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2721">The type property should be set to **HDInsight**.</span></span> |<span data-ttu-id="38fe0-2722">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2722">Yes</span></span> |
| <span data-ttu-id="38fe0-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="38fe0-2723">clusterUri</span></span> |<span data-ttu-id="38fe0-2724">Identyfikator URI klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2724">The URI of the HDInsight cluster.</span></span> |<span data-ttu-id="38fe0-2725">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2725">Yes</span></span> |
| <span data-ttu-id="38fe0-2726">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-2726">username</span></span> |<span data-ttu-id="38fe0-2727">Określ nazwę użytkownika, który ma być używany do nawiązania połączenia z istniejącym klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2727">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span></span> |<span data-ttu-id="38fe0-2728">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2728">Yes</span></span> |
| <span data-ttu-id="38fe0-2729">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-2729">password</span></span> |<span data-ttu-id="38fe0-2730">Określ hasło dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2730">Specify password for the user account.</span></span> |<span data-ttu-id="38fe0-2731">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2731">Yes</span></span> |
| <span data-ttu-id="38fe0-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2732">linkedServiceName</span></span> | <span data-ttu-id="38fe0-2733">Nazwa usługi Azure Storage połączone usługi, która odwołuje się do magazynu obiektów blob platformy Azure, używane przez klaster usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2733">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span></span> <p><span data-ttu-id="38fe0-2734">Obecnie nie można określić, czy usługa Azure Data Lake Store połączonej usługi dla tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="38fe0-2735">Jeśli klaster usługi HDInsight ma dostęp do usługi Data Lake Store może dostęp do danych w usłudze Azure Data Lake Store ze skryptów gałęzi/Pig.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2735">You may access data in the Azure Data Lake Store from Hive/Pig scripts if the HDInsight cluster has access to the Data Lake Store.</span></span> </p>  |<span data-ttu-id="38fe0-2736">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2736">Yes</span></span> |

<span data-ttu-id="38fe0-2737">Dla wersji obsługiwane klastrów usługi HDInsight, zobacz [obsługiwane wersje HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="38fe0-2738">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-2738">JSON example</span></span>

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a><span data-ttu-id="38fe0-2739">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="38fe0-2739">Azure Batch</span></span>
<span data-ttu-id="38fe0-2740">Usługa partii zadań Azure połączony do zarejestrowania puli partii maszynach wirtualnych (VM) można utworzyć przy użyciu fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2740">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="38fe0-2741">Możesz uruchomić niestandardowych działań platformy .NET przy użyciu partii zadań Azure lub usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="38fe0-2742">Można uruchomić [działania niestandardowego .NET](#net-custom-activity) na tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="38fe0-2743">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2743">Linked service</span></span>
<span data-ttu-id="38fe0-2744">Poniższa tabela zawiera opisy właściwości używane w definicji Azure JSON usługi partia zadań Azure połączone.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2744">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="38fe0-2745">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2745">Property</span></span> | <span data-ttu-id="38fe0-2746">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2746">Description</span></span> | <span data-ttu-id="38fe0-2747">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2748">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-2748">type</span></span> |<span data-ttu-id="38fe0-2749">Powinien mieć ustawioną właściwość type **AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2749">The type property should be set to **AzureBatch**.</span></span> |<span data-ttu-id="38fe0-2750">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2750">Yes</span></span> |
| <span data-ttu-id="38fe0-2751">Nazwa konta</span><span class="sxs-lookup"><span data-stu-id="38fe0-2751">accountName</span></span> |<span data-ttu-id="38fe0-2752">Nazwa konta partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2752">Name of the Azure Batch account.</span></span> |<span data-ttu-id="38fe0-2753">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2753">Yes</span></span> |
| <span data-ttu-id="38fe0-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="38fe0-2754">accessKey</span></span> |<span data-ttu-id="38fe0-2755">Klucz dostępu dla konta usługi partia zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2755">Access key for the Azure Batch account.</span></span> |<span data-ttu-id="38fe0-2756">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2756">Yes</span></span> |
| <span data-ttu-id="38fe0-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2757">poolName</span></span> |<span data-ttu-id="38fe0-2758">Nazwa puli maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2758">Name of the pool of virtual machines.</span></span> |<span data-ttu-id="38fe0-2759">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2759">Yes</span></span> |
| <span data-ttu-id="38fe0-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2760">linkedServiceName</span></span> |<span data-ttu-id="38fe0-2761">Nazwa usługi Azure Storage połączonej usługi skojarzone z tą usługą partii zadań Azure połączone.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2761">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="38fe0-2762">Tej połączonej usługi jest używany dla tymczasowych plików wymaganych do uruchomienia działania i przechowywanie dzienniki wykonywania działania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2762">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span></span> |<span data-ttu-id="38fe0-2763">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="38fe0-2764">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-2764">JSON example</span></span>

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a><span data-ttu-id="38fe0-2765">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="38fe0-2765">Azure Machine Learning</span></span>
<span data-ttu-id="38fe0-2766">Można utworzyć usługi Azure Machine Learning, połączone można zarejestrować punktu końcowego z fabryką danych oceniania partii uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2766">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="38fe0-2767">Dwa przekształcania działań, które można uruchomić na tym połączonej usługi: [działanie wykonywania wsadowego przez Machine Learning](#machine-learning-batch-execution-activity), [Machine Learning aktualizacji zasobów działania](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="38fe0-2768">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2768">Linked service</span></span>
<span data-ttu-id="38fe0-2769">Poniższa tabela zawiera opisy właściwości używane w definicji Azure JSON usługi Azure Machine Learning połączone.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2769">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="38fe0-2770">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2770">Property</span></span> | <span data-ttu-id="38fe0-2771">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2771">Description</span></span> | <span data-ttu-id="38fe0-2772">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2773">Typ</span><span class="sxs-lookup"><span data-stu-id="38fe0-2773">Type</span></span> |<span data-ttu-id="38fe0-2774">Powinien mieć ustawioną właściwość type: **uczenie maszynowe Azure**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2774">The type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="38fe0-2775">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2775">Yes</span></span> |
| <span data-ttu-id="38fe0-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="38fe0-2776">mlEndpoint</span></span> |<span data-ttu-id="38fe0-2777">Adres URL wsadowego oceniania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2777">The batch scoring URL.</span></span> |<span data-ttu-id="38fe0-2778">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2778">Yes</span></span> |
| <span data-ttu-id="38fe0-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="38fe0-2779">apiKey</span></span> |<span data-ttu-id="38fe0-2780">Interfejs API modelu opublikowanych obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2780">The published workspace model’s API.</span></span> |<span data-ttu-id="38fe0-2781">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="38fe0-2782">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-2782">JSON example</span></span>

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="38fe0-2783">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="38fe0-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="38fe0-2784">Możesz utworzyć **Azure Data Lake Analytics** połączonej usługi, aby połączyć z usługą Azure Data Lake Analytics obliczeniowe usługi fabryka danych Azure, przed użyciem [działanie U-SQL w programie Data Lake Analytics](data-factory-usql-activity.md) w potoku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2784">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory before using the [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="38fe0-2785">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2785">Linked service</span></span>

<span data-ttu-id="38fe0-2786">Poniższa tabela zawiera opisy właściwości używane w definicji JSON usługi Azure Data Lake Analytics połączone.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2786">The following table provides descriptions for the properties used in the JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="38fe0-2787">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2787">Property</span></span> | <span data-ttu-id="38fe0-2788">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2788">Description</span></span> | <span data-ttu-id="38fe0-2789">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2790">Typ</span><span class="sxs-lookup"><span data-stu-id="38fe0-2790">Type</span></span> |<span data-ttu-id="38fe0-2791">Powinien mieć ustawioną właściwość type: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2791">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="38fe0-2792">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2792">Yes</span></span> |
| <span data-ttu-id="38fe0-2793">Nazwa konta</span><span class="sxs-lookup"><span data-stu-id="38fe0-2793">accountName</span></span> |<span data-ttu-id="38fe0-2794">Nazwa konta usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="38fe0-2795">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2795">Yes</span></span> |
| <span data-ttu-id="38fe0-2796">Element dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="38fe0-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="38fe0-2797">Identyfikator URI, usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="38fe0-2798">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2798">No</span></span> |
| <span data-ttu-id="38fe0-2799">Autoryzacji</span><span class="sxs-lookup"><span data-stu-id="38fe0-2799">authorization</span></span> |<span data-ttu-id="38fe0-2800">Kod autoryzacji jest automatycznie pobierany po kliknięciu przycisku **autoryzacji** przycisk Edytor fabryki danych i ukończeniu operacji logowania OAuth.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2800">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span></span> |<span data-ttu-id="38fe0-2801">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2801">Yes</span></span> |
| <span data-ttu-id="38fe0-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="38fe0-2802">subscriptionId</span></span> |<span data-ttu-id="38fe0-2803">Identyfikator subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="38fe0-2803">Azure subscription id</span></span> |<span data-ttu-id="38fe0-2804">Nie (Jeśli nie zostanie określony, używany subskrypcji fabryki danych).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2804">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="38fe0-2805">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2805">resourceGroupName</span></span> |<span data-ttu-id="38fe0-2806">Nazwa grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="38fe0-2806">Azure resource group name</span></span> |<span data-ttu-id="38fe0-2807">Nie (Jeśli nie zostanie określony, używana grupa zasobów z fabryką danych).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2807">No (If not specified, resource group of the data factory is used).</span></span> |
| <span data-ttu-id="38fe0-2808">Identyfikator sesji</span><span class="sxs-lookup"><span data-stu-id="38fe0-2808">sessionId</span></span> |<span data-ttu-id="38fe0-2809">Identyfikator sesji z sesji autoryzacji OAuth.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2809">session id from the OAuth authorization session.</span></span> <span data-ttu-id="38fe0-2810">Każdy identyfikator sesji jest unikatowy i mogą być użyte tylko raz.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="38fe0-2811">Gdy używasz Edytor fabryki danych, ten identyfikator jest generowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2811">When you use the Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="38fe0-2812">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="38fe0-2813">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-2813">JSON example</span></span>
<span data-ttu-id="38fe0-2814">W poniższym przykładzie przedstawiono definicję JSON dla usługi Azure Data Lake Analytics połączone.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2814">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a><span data-ttu-id="38fe0-2815">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="38fe0-2815">Azure SQL Database</span></span>
<span data-ttu-id="38fe0-2816">Tworzenie Azure połączoną usługą SQL i użyj go przy użyciu [działania dotyczącego procedury składowanej](#stored-procedure-activity) aby wywołać procedurę składowaną z potoku fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2816">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](#stored-procedure-activity) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="38fe0-2817">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2817">Linked service</span></span>
<span data-ttu-id="38fe0-2818">Aby zdefiniować bazy danych SQL Azure połączonej usługi, ustaw **typu** połączonej usługi, aby **AzureSqlDatabase**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2818">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-2819">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2819">Property</span></span> | <span data-ttu-id="38fe0-2820">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2820">Description</span></span> | <span data-ttu-id="38fe0-2821">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2822">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="38fe0-2822">connectionString</span></span> |<span data-ttu-id="38fe0-2823">Podaj informacje wymagane do połączenia z wystąpieniem bazy danych SQL Azure dla właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2823">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="38fe0-2824">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="38fe0-2825">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-2825">JSON example</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="38fe0-2826">Zobacz [Łącznik usług SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) artykułu, aby uzyskać szczegółowe informacje o tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="38fe0-2827">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="38fe0-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="38fe0-2828">Tworzenie usługi Azure SQL Data Warehouse połączone i używać go z [działania dotyczącego procedury składowanej](data-factory-stored-proc-activity.md) aby wywołać procedurę składowaną z potoku fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2828">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="38fe0-2829">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2829">Linked service</span></span>
<span data-ttu-id="38fe0-2830">Aby zdefiniować Azure SQL Data Warehouse połączonej usługi, ustaw **typu** połączonej usługi, aby **AzureSqlDW**i określ następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2830">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="38fe0-2831">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2831">Property</span></span> | <span data-ttu-id="38fe0-2832">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2832">Description</span></span> | <span data-ttu-id="38fe0-2833">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2834">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="38fe0-2834">connectionString</span></span> |<span data-ttu-id="38fe0-2835">Podaj informacje wymagane do połączenia z wystąpieniem usługi Azure SQL Data Warehouse właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2835">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="38fe0-2836">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="38fe0-2837">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-2837">JSON example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="38fe0-2838">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="38fe0-2839">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="38fe0-2839">SQL Server</span></span> 
<span data-ttu-id="38fe0-2840">Tworzenie usługi SQL Server połączone i używać go z [działania dotyczącego procedury składowanej](data-factory-stored-proc-activity.md) aby wywołać procedurę składowaną z potoku fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2840">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="38fe0-2841">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="38fe0-2841">Linked service</span></span>
<span data-ttu-id="38fe0-2842">Tworzenie połączonej usługi typu **OnPremisesSqlServer** do połączenia z lokalną bazą danych programu SQL Server z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2842">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="38fe0-2843">Poniższa tabela zawiera opis specyficzne dla lokalnej usługi SQL Server połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2843">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="38fe0-2844">Poniższa tabela zawiera opis specyficzne dla usługi SQL Server połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2844">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="38fe0-2845">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2845">Property</span></span> | <span data-ttu-id="38fe0-2846">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2846">Description</span></span> | <span data-ttu-id="38fe0-2847">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2848">type</span><span class="sxs-lookup"><span data-stu-id="38fe0-2848">type</span></span> |<span data-ttu-id="38fe0-2849">Powinien mieć ustawioną właściwość type: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2849">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="38fe0-2850">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2850">Yes</span></span> |
| <span data-ttu-id="38fe0-2851">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="38fe0-2851">connectionString</span></span> |<span data-ttu-id="38fe0-2852">Określ connectionString informacje wymagane do połączenia z lokalną bazą danych programu SQL Server, przy użyciu uwierzytelniania SQL lub uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2852">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="38fe0-2853">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2853">Yes</span></span> |
| <span data-ttu-id="38fe0-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38fe0-2854">gatewayName</span></span> |<span data-ttu-id="38fe0-2855">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2855">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="38fe0-2856">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2856">Yes</span></span> |
| <span data-ttu-id="38fe0-2857">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="38fe0-2857">username</span></span> |<span data-ttu-id="38fe0-2858">Określ nazwę użytkownika, jeśli używasz uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="38fe0-2859">Przykład: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="38fe0-2860">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2860">No</span></span> |
| <span data-ttu-id="38fe0-2861">hasło</span><span class="sxs-lookup"><span data-stu-id="38fe0-2861">password</span></span> |<span data-ttu-id="38fe0-2862">Określ hasło dla konta użytkownika, określone nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2862">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="38fe0-2863">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2863">No</span></span> |

<span data-ttu-id="38fe0-2864">Można szyfrować poświadczeń przy użyciu **AzureRmDataFactoryEncryptValue nowy** polecenia cmdlet i używać ich w parametrach połączenia, jak pokazano w poniższym przykładzie (**EncryptedCredential** właściwość):</span><span class="sxs-lookup"><span data-stu-id="38fe0-2864">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="38fe0-2865">Przykład: JSON dla przy użyciu uwierzytelniania programu SQL</span><span class="sxs-lookup"><span data-stu-id="38fe0-2865">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="38fe0-2866">Przykład: JSON dla przy użyciu uwierzytelniania systemu Windows</span><span class="sxs-lookup"><span data-stu-id="38fe0-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="38fe0-2867">Jeśli podano nazwę użytkownika i hasło, bramy służą one do personifikacja określonego konta użytkownika nawiązać połączenia z lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2867">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="38fe0-2868">W przeciwnym razie brama łączy się z serwerem SQL, bezpośrednio z kontekstem zabezpieczeń bramy (jego konta uruchamiania).</span><span class="sxs-lookup"><span data-stu-id="38fe0-2868">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="38fe0-2869">Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="38fe0-2870">DZIAŁANIA PRZEKSZTAŁCENIA DANYCH</span><span class="sxs-lookup"><span data-stu-id="38fe0-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="38fe0-2871">Działanie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2871">Activity</span></span> | <span data-ttu-id="38fe0-2872">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="38fe0-2873">Działanie HDInsight Hive</span><span class="sxs-lookup"><span data-stu-id="38fe0-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="38fe0-2874">HDInsight Hive działania w potoku fabryki danych wykonuje zapytań programu Hive samodzielnie lub w klastrze systemu Windows/Linux-based HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2874">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="38fe0-2875">Działanie HDInsight Pig</span><span class="sxs-lookup"><span data-stu-id="38fe0-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="38fe0-2876">HDInsight Pig działania w potoku fabryki danych wykonuje zapytania Pig samodzielnie lub klastra systemu Windows/Linux-based HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2876">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="38fe0-2877">Działania technologii MapReduce w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="38fe0-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="38fe0-2878">HDInsight MapReduce działania w potoku fabryki danych wykonuje programy MapReduce samodzielnie lub klastra systemu Windows/Linux-based HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2878">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="38fe0-2879">Działania przesyłania strumieniowego usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="38fe0-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="38fe0-2880">HDInsight działaniu przesyłania strumieniowego w potoku fabryki danych wykonuje przesyłania strumieniowego usługi Hadoop programy samodzielnie lub klastra systemu Windows/Linux-based HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2880">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="38fe0-2881">Działania platformy Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="38fe0-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="38fe0-2882">HDInsight Spark działania w potoku fabryki danych wykonuje programy Spark w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2882">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="38fe0-2883">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="38fe0-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="38fe0-2884">Fabryka danych Azure umożliwia łatwe tworzenie potoków korzystających z opublikowanych usługi sieci web Azure Machine Learning analizy predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2884">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="38fe0-2885">Przy użyciu działanie wykonywania wsadowego w potoku fabryki danych Azure, można wywołać usługi sieci web usługi Machine Learning w celu tworzenia prognoz danych w partii.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2885">Using the Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span></span> 
[<span data-ttu-id="38fe0-2886">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="38fe0-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="38fe0-2887">Wraz z upływem czasu modeli predykcyjnych w uczeniu maszynowym oceniania eksperymenty konieczne retrained, przy użyciu nowych baz danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2887">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="38fe0-2888">Po wykonaniu ponownego trenowania chcesz zaktualizować usługę sieci web oceniania retrained modelu uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2888">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span></span> <span data-ttu-id="38fe0-2889">Działanie aktualizacji zasobu służy do aktualizowania usługi sieci web z nowo trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2889">You can use the Update Resource Activity to update the web service with the newly trained model.</span></span>
[<span data-ttu-id="38fe0-2890">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="38fe0-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="38fe0-2891">Działania procedury składowanej w potoku fabryki danych służy do wywołania procedury przechowywanej w jednym z następujących magazynów danych: baza danych SQL Azure, Magazyn danych SQL Azure, bazy danych serwera SQL w przedsiębiorstwie lub maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2891">You can use the Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="38fe0-2892">Data Lake Analytics U-SQL działania</span><span class="sxs-lookup"><span data-stu-id="38fe0-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="38fe0-2893">Data Lake Analytics U-SQL działanie uruchamia skrypt U-SQL w klastrze usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="38fe0-2894">Niestandardowe działanie platformy .NET</span><span class="sxs-lookup"><span data-stu-id="38fe0-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="38fe0-2895">Do przekształcania danych w taki sposób, który nie jest obsługiwany przez fabrykę danych należy można tworzyć niestandardowe działania na własną logikę przetwarzania danych i użyj działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2895">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span></span> <span data-ttu-id="38fe0-2896">Można skonfigurować niestandardowe działania .NET przy użyciu usługi partia zadań Azure lub klaster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2896">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="38fe0-2897">Działania technologii Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="38fe0-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="38fe0-2898">Można określić następujące właściwości w definicji Hive JSON działania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2898">You can specify the following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="38fe0-2899">Właściwość typu działania musi być: **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2899">The type property for the activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="38fe0-2900">Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę jej jako wartości dla **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2900">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="38fe0-2901">Następujące właściwości są obsługiwane w **typeProperties** sekcji, gdy wartość typu działania HDInsightHive:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2901">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightHive:</span></span>

| <span data-ttu-id="38fe0-2902">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2902">Property</span></span> | <span data-ttu-id="38fe0-2903">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2903">Description</span></span> | <span data-ttu-id="38fe0-2904">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2905">Skrypt</span><span class="sxs-lookup"><span data-stu-id="38fe0-2905">script</span></span> |<span data-ttu-id="38fe0-2906">Określ wbudowanego skryptu Hive</span><span class="sxs-lookup"><span data-stu-id="38fe0-2906">Specify the Hive script inline</span></span> |<span data-ttu-id="38fe0-2907">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2907">No</span></span> |
| <span data-ttu-id="38fe0-2908">Ścieżka skryptu</span><span class="sxs-lookup"><span data-stu-id="38fe0-2908">script path</span></span> |<span data-ttu-id="38fe0-2909">Przechowywanie skryptu Hive w magazynie obiektów blob platformy Azure i podaj ścieżkę do pliku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2909">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="38fe0-2910">Użyj właściwości 'script' lub "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="38fe0-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="38fe0-2911">Nie można używać razem.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2911">Both cannot be used together.</span></span> <span data-ttu-id="38fe0-2912">Nazwa pliku jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2912">The file name is case-sensitive.</span></span> |<span data-ttu-id="38fe0-2913">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2913">No</span></span> |
| <span data-ttu-id="38fe0-2914">Definiuje</span><span class="sxs-lookup"><span data-stu-id="38fe0-2914">defines</span></span> |<span data-ttu-id="38fe0-2915">Określ parametry jako pary klucz wartość dla odwołania do skryptu Hive za pomocą "hiveconf"</span><span class="sxs-lookup"><span data-stu-id="38fe0-2915">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="38fe0-2916">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2916">No</span></span> |

<span data-ttu-id="38fe0-2917">Te właściwości typu są specyficzne dla działania Hive.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2917">These type properties are specific to the Hive Activity.</span></span> <span data-ttu-id="38fe0-2918">Inne właściwości (poza sekcji typeProperties) są obsługiwane dla wszystkich działań.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2918">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="38fe0-2919">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-2919">JSON example</span></span>
<span data-ttu-id="38fe0-2920">Następujące JSON definiuje działania HDInsight Hive w potoku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2920">The following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

<span data-ttu-id="38fe0-2921">Aby uzyskać więcej informacji, zobacz [Hive działania](data-factory-hive-activity.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="38fe0-2922">Działania technologii Pig w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="38fe0-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="38fe0-2923">Można określić następujące właściwości w definicji Pig działania w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2923">You can specify the following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="38fe0-2924">Właściwość typu działania musi być: **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2924">The type property for the activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="38fe0-2925">Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę jej jako wartości dla **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2925">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="38fe0-2926">Następujące właściwości są obsługiwane w **typeProperties** sekcji, gdy wartość typu działania HDInsightPig:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2926">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightPig:</span></span> 

| <span data-ttu-id="38fe0-2927">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2927">Property</span></span> | <span data-ttu-id="38fe0-2928">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2928">Description</span></span> | <span data-ttu-id="38fe0-2929">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2930">Skrypt</span><span class="sxs-lookup"><span data-stu-id="38fe0-2930">script</span></span> |<span data-ttu-id="38fe0-2931">Określ wbudowanego skryptu Pig</span><span class="sxs-lookup"><span data-stu-id="38fe0-2931">Specify the Pig script inline</span></span> |<span data-ttu-id="38fe0-2932">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2932">No</span></span> |
| <span data-ttu-id="38fe0-2933">Ścieżka skryptu</span><span class="sxs-lookup"><span data-stu-id="38fe0-2933">script path</span></span> |<span data-ttu-id="38fe0-2934">Umieść skrypt programu Pig w magazynie obiektów blob platformy Azure, a następnie podaj ścieżkę do pliku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2934">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="38fe0-2935">Użyj właściwości 'script' lub "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="38fe0-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="38fe0-2936">Nie można używać razem.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2936">Both cannot be used together.</span></span> <span data-ttu-id="38fe0-2937">Nazwa pliku jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2937">The file name is case-sensitive.</span></span> |<span data-ttu-id="38fe0-2938">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2938">No</span></span> |
| <span data-ttu-id="38fe0-2939">Definiuje</span><span class="sxs-lookup"><span data-stu-id="38fe0-2939">defines</span></span> |<span data-ttu-id="38fe0-2940">Określ parametry jako pary klucz wartość dla odwołania do skryptu Pig</span><span class="sxs-lookup"><span data-stu-id="38fe0-2940">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="38fe0-2941">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2941">No</span></span> |

<span data-ttu-id="38fe0-2942">Te właściwości typu są specyficzne dla działania Pig.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2942">These type properties are specific to the Pig Activity.</span></span> <span data-ttu-id="38fe0-2943">Inne właściwości (poza sekcji typeProperties) są obsługiwane dla wszystkich działań.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2943">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="38fe0-2944">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-2944">JSON example</span></span>

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

<span data-ttu-id="38fe0-2945">Aby uzyskać więcej informacji, zobacz [działania Pig](#data-factory-pig-activity.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="38fe0-2946">Działania technologii MapReduce w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="38fe0-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="38fe0-2947">Można określić następujące właściwości w definicji JSON działania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2947">You can specify the following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="38fe0-2948">Właściwość typu działania musi być: **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2948">The type property for the activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="38fe0-2949">Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę jej jako wartości dla **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2949">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="38fe0-2950">Następujące właściwości są obsługiwane w **typeProperties** sekcji, gdy wartość typu działania HDInsightMapReduce:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2950">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightMapReduce:</span></span> 

| <span data-ttu-id="38fe0-2951">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2951">Property</span></span> | <span data-ttu-id="38fe0-2952">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2952">Description</span></span> | <span data-ttu-id="38fe0-2953">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="38fe0-2954">jarLinkedService</span></span> | <span data-ttu-id="38fe0-2955">Nazwa połączonej usługi dla usługi Azure Storage, który zawiera plik JAR.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2955">Name of the linked service for the Azure Storage that contains the JAR file.</span></span> | <span data-ttu-id="38fe0-2956">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2956">Yes</span></span> |
| <span data-ttu-id="38fe0-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="38fe0-2957">jarFilePath</span></span> | <span data-ttu-id="38fe0-2958">Ścieżka do pliku JAR w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2958">Path to the JAR file in the Azure Storage.</span></span> | <span data-ttu-id="38fe0-2959">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2959">Yes</span></span> | 
| <span data-ttu-id="38fe0-2960">className</span><span class="sxs-lookup"><span data-stu-id="38fe0-2960">className</span></span> | <span data-ttu-id="38fe0-2961">Nazwa klasy głównym w pliku JAR.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2961">Name of the main class in the JAR file.</span></span> | <span data-ttu-id="38fe0-2962">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-2962">Yes</span></span> | 
| <span data-ttu-id="38fe0-2963">Argumenty</span><span class="sxs-lookup"><span data-stu-id="38fe0-2963">arguments</span></span> | <span data-ttu-id="38fe0-2964">Lista argumentów rozdzielonych przecinkami programu MapReduce.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2964">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="38fe0-2965">W czasie wykonywania, zobacz kilka dodatkowych argumentów (na przykład: mapreduce.job.tags) z platformy MapReduce.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="38fe0-2966">Rozróżnianie argumentów z argumentami MapReduce, należy rozważyć użycie zarówno opcji i wartości jako argumenty, jak pokazano w poniższym przykładzie (- s, — dane wejściowe,--itp., dane wyjściowe są opcje bezpośrednio następuje ich wartości)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2966">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="38fe0-2967">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="38fe0-2968">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix to determine the similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce to generate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="38fe0-2969">Aby uzyskać więcej informacji, zobacz [działania MapReduce](data-factory-map-reduce.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="38fe0-2970">Działania przesyłania strumieniowego usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="38fe0-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="38fe0-2971">Można określić następujące właściwości w definicji działania przesyłania strumieniowego usługi Hadoop w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2971">You can specify the following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="38fe0-2972">Właściwość typu działania musi być: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2972">The type property for the activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="38fe0-2973">Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę jej jako wartości dla **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2973">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="38fe0-2974">Następujące właściwości są obsługiwane w **typeProperties** sekcji, gdy wartość typu działania HDInsightStreaming:</span><span class="sxs-lookup"><span data-stu-id="38fe0-2974">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightStreaming:</span></span> 

| <span data-ttu-id="38fe0-2975">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-2975">Property</span></span> | <span data-ttu-id="38fe0-2976">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="38fe0-2977">mapowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-2977">mapper</span></span> | <span data-ttu-id="38fe0-2978">Nazwa pliku wykonywalnego mapowania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2978">Name of the mapper executable.</span></span> <span data-ttu-id="38fe0-2979">W tym przykładzie cat.exe jest mapowania pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2979">In the example, cat.exe is the mapper executable.</span></span>| 
| <span data-ttu-id="38fe0-2980">Reduktor</span><span class="sxs-lookup"><span data-stu-id="38fe0-2980">reducer</span></span> | <span data-ttu-id="38fe0-2981">Nazwa pliku wykonywalnego reduktor.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2981">Name of the reducer executable.</span></span> <span data-ttu-id="38fe0-2982">W tym przykładzie wc.exe jest reduktor pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2982">In the example, wc.exe is the reducer executable.</span></span> | 
| <span data-ttu-id="38fe0-2983">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="38fe0-2983">input</span></span> | <span data-ttu-id="38fe0-2984">Plik wejściowy (w tym miejscu) dla mapowania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2984">Input file (including location) for the mapper.</span></span> <span data-ttu-id="38fe0-2985">W tym przykładzie: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample jest kontenera obiektów blob, przykład/data/Gutenberg jest folder i davinci.txt jest obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2985">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span> |
| <span data-ttu-id="38fe0-2986">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="38fe0-2986">output</span></span> | <span data-ttu-id="38fe0-2987">Plik wyjściowy (w tym miejscu) dla reduktor.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2987">Output file (including location) for the reducer.</span></span> <span data-ttu-id="38fe0-2988">Dane wyjściowe zadania przesyłania strumieniowego usługi Hadoop jest zapisany w lokalizacji określonej dla tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2988">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span> |
| <span data-ttu-id="38fe0-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="38fe0-2989">filePaths</span></span> | <span data-ttu-id="38fe0-2990">Ścieżki do plików wykonywalnych mapowania i reduktor.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2990">Paths for the mapper and reducer executables.</span></span> <span data-ttu-id="38fe0-2991">W tym przykładzie: "adfsample/example/apps/wc.exe" adfsample jest kontenera obiektów blob, przykład/aplikacji jest folder i wc.exe jest plikiem wykonywalnym.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2991">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span> | 
| <span data-ttu-id="38fe0-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="38fe0-2992">fileLinkedService</span></span> | <span data-ttu-id="38fe0-2993">Usługa Azure Storage połączone usługi, która reprezentuje magazynu Azure, który zawiera pliki określone w sekcji filePaths.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2993">Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span> | 
| <span data-ttu-id="38fe0-2994">Argumenty</span><span class="sxs-lookup"><span data-stu-id="38fe0-2994">arguments</span></span> | <span data-ttu-id="38fe0-2995">Lista argumentów rozdzielonych przecinkami programu MapReduce.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2995">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="38fe0-2996">W czasie wykonywania, zobacz kilka dodatkowych argumentów (na przykład: mapreduce.job.tags) z platformy MapReduce.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="38fe0-2997">Rozróżnianie argumentów z argumentami MapReduce, należy rozważyć użycie zarówno opcji i wartości jako argumenty, jak pokazano w poniższym przykładzie (- s, — dane wejściowe,--itp., dane wyjściowe są opcje bezpośrednio następuje ich wartości)</span><span class="sxs-lookup"><span data-stu-id="38fe0-2997">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="38fe0-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="38fe0-2998">getDebugInfo</span></span> | <span data-ttu-id="38fe0-2999">Element opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="38fe0-2999">An optional element.</span></span> <span data-ttu-id="38fe0-3000">Jeśli ustawiono awarii, dzienniki są pobierane tylko w przypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3000">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="38fe0-3001">Jeśli je skonfigurowano do wszystkich, dzienniki są zawsze pobierane niezależnie od stanu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3001">When it is set to All, logs are always downloaded irrespective of the execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="38fe0-3002">Należy określić wyjściowy zestaw danych działania przesyłania strumieniowego usługi Hadoop dla **generuje** właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3002">You must specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="38fe0-3003">Ten zestaw danych można tylko fikcyjny zestawu danych, który jest wymagany do kierowania harmonogram potoku (co godzinę, codziennie, itp.).</span><span class="sxs-lookup"><span data-stu-id="38fe0-3003">This dataset can be just a dummy dataset that is required to drive the pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="38fe0-3004">Jeśli działanie nie przyjmuje dane wejściowe, można pominąć, określając zestawem danych wejściowych dla działania dla **dane wejściowe** właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3004">If the activity doesn't take an input, you can skip specifying an input dataset for the activity for the **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="38fe0-3005">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-3005">JSON example</span></span>

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

<span data-ttu-id="38fe0-3006">Aby uzyskać więcej informacji, zobacz [działaniu przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="38fe0-3007">Działania platformy Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="38fe0-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="38fe0-3008">Można określić następujące właściwości w definicji Spark działania w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3008">You can specify the following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="38fe0-3009">Właściwość typu działania musi być: **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3009">The type property for the activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="38fe0-3010">Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę jej jako wartości dla **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3010">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="38fe0-3011">Następujące właściwości są obsługiwane w **typeProperties** sekcji, gdy wartość typu działania HDInsightSpark:</span><span class="sxs-lookup"><span data-stu-id="38fe0-3011">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightSpark:</span></span> 

| <span data-ttu-id="38fe0-3012">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-3012">Property</span></span> | <span data-ttu-id="38fe0-3013">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-3013">Description</span></span> | <span data-ttu-id="38fe0-3014">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="38fe0-3015">Właściwość rootPath</span><span class="sxs-lookup"><span data-stu-id="38fe0-3015">rootPath</span></span> | <span data-ttu-id="38fe0-3016">Kontener obiektów Blob platformy Azure i folder zawierający plik Spark.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3016">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="38fe0-3017">Nazwa pliku jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3017">The file name is case-sensitive.</span></span> | <span data-ttu-id="38fe0-3018">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-3018">Yes</span></span> |
| <span data-ttu-id="38fe0-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="38fe0-3019">entryFilePath</span></span> | <span data-ttu-id="38fe0-3020">Ścieżka względna do folderu głównego Spark kodu/pakietu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3020">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="38fe0-3021">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-3021">Yes</span></span> |
| <span data-ttu-id="38fe0-3022">className</span><span class="sxs-lookup"><span data-stu-id="38fe0-3022">className</span></span> | <span data-ttu-id="38fe0-3023">Klasy głównym aplikacji Java/Spark</span><span class="sxs-lookup"><span data-stu-id="38fe0-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="38fe0-3024">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-3024">No</span></span> | 
| <span data-ttu-id="38fe0-3025">Argumenty</span><span class="sxs-lookup"><span data-stu-id="38fe0-3025">arguments</span></span> | <span data-ttu-id="38fe0-3026">Lista argumentów wiersza polecenia do programu Spark.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3026">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="38fe0-3027">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-3027">No</span></span> | 
| <span data-ttu-id="38fe0-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="38fe0-3028">proxyUser</span></span> | <span data-ttu-id="38fe0-3029">Konto użytkownika do personifikacji do wykonania programu Spark</span><span class="sxs-lookup"><span data-stu-id="38fe0-3029">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="38fe0-3030">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-3030">No</span></span> | 
| <span data-ttu-id="38fe0-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="38fe0-3031">sparkConfig</span></span> | <span data-ttu-id="38fe0-3032">Właściwości konfiguracji platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3032">Spark configuration properties.</span></span> | <span data-ttu-id="38fe0-3033">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-3033">No</span></span> | 
| <span data-ttu-id="38fe0-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="38fe0-3034">getDebugInfo</span></span> | <span data-ttu-id="38fe0-3035">Określa, kiedy Spark pliki dziennika są kopiowane do magazynu Azure używanego przez klaster usługi HDInsight (lub) został określony przez sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3035">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="38fe0-3036">Dozwolone wartości: None, zawsze lub niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="38fe0-3037">Wartość domyślna: Brak.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3037">Default value: None.</span></span> | <span data-ttu-id="38fe0-3038">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-3038">No</span></span> | 
| <span data-ttu-id="38fe0-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="38fe0-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="38fe0-3040">Magazyn Azure połączone usługi, która ma Spark plik zadania, zależności i dzienniki.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3040">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="38fe0-3041">Jeśli nie określisz wartości dla tej właściwości, Magazyn skojarzony z klastrem usługi HDInsight jest używany.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3041">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="38fe0-3042">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="38fe0-3043">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-3043">JSON example</span></span>

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
<span data-ttu-id="38fe0-3044">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="38fe0-3044">Note the following points:</span></span> 

- <span data-ttu-id="38fe0-3045">**Typu** właściwość jest ustawiona na **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3045">The **type** property is set to **HDInsightSpark**.</span></span>
- <span data-ttu-id="38fe0-3046">**Właściwość rootPath** ustawiono **adfspark\\pyFiles** gdzie adfspark jest kontenera obiektów Blob platformy Azure i pyFiles jest poprawnie folder, w tym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3046">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="38fe0-3047">W tym przykładzie magazynu obiektów Blob Azure jest skojarzony z klastrem Spark.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3047">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="38fe0-3048">Można przekazać pliku do innego magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3048">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="38fe0-3049">Jeśli tak zrobisz, Utwórz połączoną usługą magazynu Azure, aby połączyć konto magazynu z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3049">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="38fe0-3050">Następnie określ jako wartość dla nazwy połączonej usługi **sparkJobLinkedService** właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3050">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="38fe0-3051">Zobacz [właściwości działania Spark](#spark-activity-properties) szczegóły dotyczące tej właściwości oraz inne właściwości obsługiwane przez działanie Spark.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>
- <span data-ttu-id="38fe0-3052">**EntryFilePath** ustawiono **test.py**, czyli plik python.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3052">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span> 
- <span data-ttu-id="38fe0-3053">**GetDebugInfo** właściwość jest ustawiona na **zawsze**, co oznacza, że pliki dziennika są zawsze generowany (powodzenie lub niepowodzenie).</span><span class="sxs-lookup"><span data-stu-id="38fe0-3053">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="38fe0-3054">Zaleca się, że nie zostały ustawione ta właściwość zawsze w środowisku produkcyjnym, chyba że są Rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3054">We recommend that you do not set this property to Always in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="38fe0-3055">**Generuje** sekcja ma jeden wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3055">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="38fe0-3056">Należy określić wyjściowy zestaw danych, nawet jeśli spark program nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3056">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="38fe0-3057">Wyjściowy zestaw danych dysków harmonogramu dla potoku (co godzinę, codziennie, itp.).</span><span class="sxs-lookup"><span data-stu-id="38fe0-3057">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="38fe0-3058">Aby uzyskać więcej informacji na temat działania, zobacz [działania Spark](data-factory-spark.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3058">For more information about the activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="38fe0-3059">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="38fe0-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="38fe0-3060">W definicji usługi Azure ML wsadowe wykonywanie działania JSON można określić następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3060">You can specify the following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="38fe0-3061">Właściwość typu działania musi być: **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3061">The type property for the activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="38fe0-3062">Musisz utworzyć maszyny platformy Azure, najpierw uczenia połączonej usługi i określ nazwę go jako wartość **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3062">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="38fe0-3063">Następujące właściwości są obsługiwane w **typeProperties** sekcji, gdy wartość typu działania AzureMLBatchExecution:</span><span class="sxs-lookup"><span data-stu-id="38fe0-3063">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLBatchExecution:</span></span>

<span data-ttu-id="38fe0-3064">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-3064">Property</span></span> | <span data-ttu-id="38fe0-3065">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-3065">Description</span></span> | <span data-ttu-id="38fe0-3066">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="38fe0-3067">WebServiceInputActivity</span><span class="sxs-lookup"><span data-stu-id="38fe0-3067">webServiceInput</span></span> | <span data-ttu-id="38fe0-3068">Zestaw danych do przekazania jako dane wejściowe dla usługi sieci web uczenie Maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3068">The dataset to be passed as an input for the Azure ML web service.</span></span> <span data-ttu-id="38fe0-3069">Ten zestaw danych, również musi być uwzględniona w danych wejściowych dla działania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3069">This dataset must also be included in the inputs for the activity.</span></span> |<span data-ttu-id="38fe0-3070">Użyj WebServiceInputActivity lub webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="38fe0-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="38fe0-3071">webServiceInputs</span></span> | <span data-ttu-id="38fe0-3072">Określ zestawy danych można przekazać jako dane wejściowe dla usługi sieci web uczenie Maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3072">Specify datasets to be passed as inputs for the Azure ML web service.</span></span> <span data-ttu-id="38fe0-3073">Jeśli usługa sieci web wymaga wielu danych wejściowych, użyj właściwości webServiceInputs zamiast właściwości WebServiceInputActivity.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3073">If the web service takes multiple inputs, use the webServiceInputs property instead of using the webServiceInput property.</span></span> <span data-ttu-id="38fe0-3074">Zestawy danych, które odwołują się **webServiceInputs** muszą także być ujęte w działaniu **dane wejściowe**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3074">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span> | <span data-ttu-id="38fe0-3075">Użyj WebServiceInputActivity lub webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="38fe0-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="38fe0-3076">webServiceOutputs</span></span> | <span data-ttu-id="38fe0-3077">Zestawy danych, które są przypisane jako dane wyjściowe dla usługi sieci web uczenie Maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3077">The datasets that are assigned as outputs for the Azure ML web service.</span></span> <span data-ttu-id="38fe0-3078">Usługa sieci web zwraca dane wyjściowe w tym zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3078">The web service returns output data in this dataset.</span></span> | <span data-ttu-id="38fe0-3079">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-3079">Yes</span></span> | 
<span data-ttu-id="38fe0-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="38fe0-3080">globalParameters</span></span> | <span data-ttu-id="38fe0-3081">Określ wartości dla parametrów usługi sieci web w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3081">Specify values for the web service parameters in this section.</span></span> | <span data-ttu-id="38fe0-3082">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="38fe0-3083">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-3083">JSON example</span></span>
<span data-ttu-id="38fe0-3084">W tym przykładzie działanie ma zestaw danych **MLSqlInput** jako dane wejściowe i **MLSqlOutput** jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3084">In this example, the activity has the dataset **MLSqlInput** as input and **MLSqlOutput** as the output.</span></span> <span data-ttu-id="38fe0-3085">**MLSqlInput** przekazany jako dane wejściowe z usługą sieci web przez przy użyciu **WebServiceInputActivity** właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3085">The **MLSqlInput** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="38fe0-3086">**MLSqlOutput** jest przekazywany jako dane wyjściowe z usługą sieci Web przez przy użyciu **webServiceOutputs** właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3086">The **MLSqlOutput** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span> 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

<span data-ttu-id="38fe0-3087">W przykładzie JSON wdrożonej usługi sieci Web Azure Machine Learning używa czytnika i modułu zapisywania danych bazy danych SQL Azure z/do odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3087">In the JSON example, the deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="38fe0-3088">Ta usługa sieci Web udostępnia następujące cztery parametry: Nazwa serwera, nazwa bazy danych, nazwę konta użytkownika serwera i hasło konta użytkownika serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3088">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="38fe0-3089">Tylko danych wejściowych i wyjściowych działania AzureMLBatchExecution mogą być przekazywane jako parametry z usługą sieci Web.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3089">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="38fe0-3090">Na przykład w powyższym fragment kodu JSON MLSqlInput jest wartością wejściową działania AzureMLBatchExecution, który jest przekazywany jako dane wejściowe do usługi sieci Web za pomocą parametru WebServiceInputActivity.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3090">For example, in the above JSON snippet, MLSqlInput is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="38fe0-3091">Działanie aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="38fe0-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="38fe0-3092">W definicji usługi Azure ML aktualizacji zasobów działania JSON można określić następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3092">You can specify the following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="38fe0-3093">Właściwość typu działania musi być: **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3093">The type property for the activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="38fe0-3094">Musisz utworzyć maszyny platformy Azure, najpierw uczenia połączonej usługi i określ nazwę go jako wartość **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3094">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="38fe0-3095">Następujące właściwości są obsługiwane w **typeProperties** sekcji, gdy wartość typu działania AzureMLUpdateResource:</span><span class="sxs-lookup"><span data-stu-id="38fe0-3095">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLUpdateResource:</span></span>

<span data-ttu-id="38fe0-3096">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-3096">Property</span></span> | <span data-ttu-id="38fe0-3097">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-3097">Description</span></span> | <span data-ttu-id="38fe0-3098">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="38fe0-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="38fe0-3099">trainedModelName</span></span> | <span data-ttu-id="38fe0-3100">Nazwa modelu retrained.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3100">Name of the retrained model.</span></span> | <span data-ttu-id="38fe0-3101">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-3101">Yes</span></span> |  
<span data-ttu-id="38fe0-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="38fe0-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="38fe0-3103">Zestaw danych, wskazując plik iLearner zwrócony przez operację ponownego trenowania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3103">Dataset pointing to the iLearner file returned by the retraining operation.</span></span> | <span data-ttu-id="38fe0-3104">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="38fe0-3105">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-3105">JSON example</span></span>
<span data-ttu-id="38fe0-3106">Potok zawiera dwa działania: **AzureMLBatchExecution** i **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3106">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="38fe0-3107">Działanie wykonywania wsadowego usługi uczenie Maszynowe Azure przyjmuje jako dane wejściowe dane szkoleniowe i tworzy plik iLearner jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3107">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="38fe0-3108">Działanie wywołuje usługę sieci web szkolenia (eksperyment uczenia udostępniony jako usługa sieci web) przy użyciu danych wejściowych szkolenia i odbiera plik ilearner z usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3108">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="38fe0-3109">PlaceholderBlob jest tylko fikcyjny wyjściowego zestawu danych, który jest wymagany przez usługi fabryka danych Azure do uruchamiania potoku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3109">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="38fe0-3110">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="38fe0-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="38fe0-3111">Można określić następujące właściwości w definicji JSON działanie U-SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3111">You can specify the following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="38fe0-3112">Właściwość typu działania musi być: **DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3112">The type property for the activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="38fe0-3113">Musisz utworzyć usługi Azure Data Lake Analytics połączone i określ nazwę go jako wartość **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3113">You must create an Azure Data Lake Analytics linked service and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="38fe0-3114">Następujące właściwości są obsługiwane w **typeProperties** sekcji, gdy wartość typu działania DataLakeAnalyticsU SQL:</span><span class="sxs-lookup"><span data-stu-id="38fe0-3114">The following properties are supported in the **typeProperties** section when you set the type of activity to DataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="38fe0-3115">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-3115">Property</span></span> | <span data-ttu-id="38fe0-3116">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-3116">Description</span></span> | <span data-ttu-id="38fe0-3117">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="38fe0-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="38fe0-3118">scriptPath</span></span> |<span data-ttu-id="38fe0-3119">Ścieżka do folderu, który zawiera skrypt U-SQL.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3119">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="38fe0-3120">Nazwa pliku jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3120">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="38fe0-3121">Nie (Jeśli używasz skryptu)</span><span class="sxs-lookup"><span data-stu-id="38fe0-3121">No (if you use script)</span></span> |
| <span data-ttu-id="38fe0-3122">Element scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="38fe0-3122">scriptLinkedService</span></span> |<span data-ttu-id="38fe0-3123">Połączonej usługi, która łączy magazynu, który zawiera skrypt do fabryki danych</span><span class="sxs-lookup"><span data-stu-id="38fe0-3123">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="38fe0-3124">Nie (Jeśli używasz skryptu)</span><span class="sxs-lookup"><span data-stu-id="38fe0-3124">No (if you use script)</span></span> |
| <span data-ttu-id="38fe0-3125">Skrypt</span><span class="sxs-lookup"><span data-stu-id="38fe0-3125">script</span></span> |<span data-ttu-id="38fe0-3126">Określ skrypt wbudowany zamiast określania scriptPath i scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="38fe0-3127">Na przykład: "skrypt": "Test Utwórz bazę danych".</span><span class="sxs-lookup"><span data-stu-id="38fe0-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="38fe0-3128">Nie (Jeśli używasz scriptPath i scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="38fe0-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="38fe0-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="38fe0-3129">degreeOfParallelism</span></span> |<span data-ttu-id="38fe0-3130">Maksymalna liczba węzłów jednocześnie użyta do uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3130">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="38fe0-3131">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-3131">No</span></span> |
| <span data-ttu-id="38fe0-3132">Priorytet</span><span class="sxs-lookup"><span data-stu-id="38fe0-3132">priority</span></span> |<span data-ttu-id="38fe0-3133">Określa, które spośród wszystkich znajdujących się w kolejce zadań należy wybrać ma być uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3133">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="38fe0-3134">Im niższy numer, tym wyższy priorytet.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3134">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="38fe0-3135">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-3135">No</span></span> |
| <span data-ttu-id="38fe0-3136">Parametry</span><span class="sxs-lookup"><span data-stu-id="38fe0-3136">parameters</span></span> |<span data-ttu-id="38fe0-3137">Parametry skryptu U-SQL</span><span class="sxs-lookup"><span data-stu-id="38fe0-3137">Parameters for the U-SQL script</span></span> |<span data-ttu-id="38fe0-3138">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="38fe0-3139">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-3139">JSON example</span></span>

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="38fe0-3140">Aby uzyskać więcej informacji, zobacz [Data Lake Analytics U-SQL działania](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="38fe0-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="38fe0-3141">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="38fe0-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="38fe0-3142">W definicji przechowywane procedury działania JSON można określić następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3142">You can specify the following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="38fe0-3143">Właściwość typu działania musi być: **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3143">The type property for the activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="38fe0-3144">Należy utworzyć następujące połączone usługi i określ nazwę połączonej usługi jako wartość **linkedServiceName** właściwości:</span><span class="sxs-lookup"><span data-stu-id="38fe0-3144">You must create an one of the following linked services and specify the name of the linked service as a value for the **linkedServiceName** property:</span></span>

- <span data-ttu-id="38fe0-3145">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="38fe0-3145">SQL Server</span></span> 
- <span data-ttu-id="38fe0-3146">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="38fe0-3146">Azure SQL Database</span></span>
- <span data-ttu-id="38fe0-3147">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="38fe0-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="38fe0-3148">Następujące właściwości są obsługiwane w **typeProperties** sekcji, gdy wartość typu działania SqlServerStoredProcedure:</span><span class="sxs-lookup"><span data-stu-id="38fe0-3148">The following properties are supported in the **typeProperties** section when you set the type of activity to SqlServerStoredProcedure:</span></span>

| <span data-ttu-id="38fe0-3149">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-3149">Property</span></span> | <span data-ttu-id="38fe0-3150">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-3150">Description</span></span> | <span data-ttu-id="38fe0-3151">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38fe0-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="38fe0-3152">storedProcedureName</span></span> |<span data-ttu-id="38fe0-3153">Określ nazwę procedury składowanej w bazie danych Azure SQL lub usługi Azure SQL Data Warehouse jest reprezentowana przez połączonej usługi, która używa tabeli wyników.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3153">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="38fe0-3154">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-3154">Yes</span></span> |
| <span data-ttu-id="38fe0-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="38fe0-3155">storedProcedureParameters</span></span> |<span data-ttu-id="38fe0-3156">Określ wartości dla parametrów procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="38fe0-3157">Jeśli chcesz przekazać wartości null dla parametru należy użyć składni: "param1": wartość null (małe litery).</span><span class="sxs-lookup"><span data-stu-id="38fe0-3157">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="38fe0-3158">Zobacz poniższy przykład, aby dowiedzieć się więcej o korzystaniu z tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3158">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="38fe0-3159">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-3159">No</span></span> |

<span data-ttu-id="38fe0-3160">Jeśli określisz wejściowy zestaw danych, musi być dostępny (w stanie "Gotowe") dla działania procedury składowanej do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="38fe0-3161">Wejściowy zestaw danych nie mogą być używane w procedurze składowanej jako parametr.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3161">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="38fe0-3162">Tylko służy do sprawdzania zależności przed rozpoczęciem działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3162">It is only used to check the dependency before starting the stored procedure activity.</span></span> <span data-ttu-id="38fe0-3163">Należy określić zestaw danych wyjściowych dla działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="38fe0-3164">Określa wyjściowy zestaw danych **harmonogram** działania procedury składowanej (co godzinę, co tydzień, co miesiąc, itp.).</span><span class="sxs-lookup"><span data-stu-id="38fe0-3164">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="38fe0-3165">Wyjściowy zestaw danych musi używać **połączona usługa** odwołujący się do bazy danych SQL Azure lub usługi Azure SQL Data Warehouse lub bazy danych programu SQL Server w której ma zostać procedurę składowaną, aby uruchomić.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3165">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="38fe0-3166">Wyjściowy zestaw danych może stanowić sposób przekazać wyników procedury składowanej dla kolejnych przetwarzania przez inne działanie ([łańcucha działania](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) w potoku.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3166">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in the pipeline.</span></span> <span data-ttu-id="38fe0-3167">Jednak fabryki danych nie automatycznie zapisuje dane wyjściowe procedury składowanej do tego elementu dataset.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3167">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="38fe0-3168">Jest procedury przechowywanej, która zapisuje do tabeli SQL, która wskazuje wyjściowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3168">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="38fe0-3169">W niektórych przypadkach może być wyjściowy zestaw danych **fikcyjny zestawu danych**, które służą tylko do określ harmonogram uruchamiania działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3169">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="38fe0-3170">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-3170">JSON example</span></span>

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="38fe0-3171">Aby uzyskać więcej informacji, zobacz [działania dotyczącego procedury składowanej](data-factory-stored-proc-activity.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="38fe0-3172">Niestandardowe działanie platformy .NET</span><span class="sxs-lookup"><span data-stu-id="38fe0-3172">.NET custom activity</span></span>
<span data-ttu-id="38fe0-3173">Można określić następujące właściwości w .NET działań niestandardowych definicji JSON.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3173">You can specify the following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="38fe0-3174">Właściwość typu działania musi być: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3174">The type property for the activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="38fe0-3175">Należy utworzyć usługi Azure HDInsight połączone lub partii zadań Azure połączone usługi i określ nazwę połączonej usługi jako wartość **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify the name of the linked service as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="38fe0-3176">Następujące właściwości są obsługiwane w **typeProperties** sekcji, gdy wartość typu działania DotNetActivity:</span><span class="sxs-lookup"><span data-stu-id="38fe0-3176">The following properties are supported in the **typeProperties** section when you set the type of activity to DotNetActivity:</span></span>
 
| <span data-ttu-id="38fe0-3177">Właściwość</span><span class="sxs-lookup"><span data-stu-id="38fe0-3177">Property</span></span> | <span data-ttu-id="38fe0-3178">Opis</span><span class="sxs-lookup"><span data-stu-id="38fe0-3178">Description</span></span> | <span data-ttu-id="38fe0-3179">Wymagane</span><span class="sxs-lookup"><span data-stu-id="38fe0-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="38fe0-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="38fe0-3180">AssemblyName</span></span> | <span data-ttu-id="38fe0-3181">Nazwa zestawu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3181">Name of the assembly.</span></span> <span data-ttu-id="38fe0-3182">W tym przykładzie jest: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3182">In the example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="38fe0-3183">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-3183">Yes</span></span> |
| <span data-ttu-id="38fe0-3184">Punkt wejścia</span><span class="sxs-lookup"><span data-stu-id="38fe0-3184">EntryPoint</span></span> |<span data-ttu-id="38fe0-3185">Nazwa klasy, która implementuje interfejs IDotNetActivity.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3185">Name of the class that implements the IDotNetActivity interface.</span></span> <span data-ttu-id="38fe0-3186">W tym przykładzie jest: **MyDotNetActivityNS.MyDotNetActivity** gdzie przestrzeni nazw jest MyDotNetActivityNS i MyDotNetActivity jest klasą.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3186">In the example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is the namespace and MyDotNetActivity is the class.</span></span>  | <span data-ttu-id="38fe0-3187">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-3187">Yes</span></span> | 
| <span data-ttu-id="38fe0-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="38fe0-3188">PackageLinkedService</span></span> | <span data-ttu-id="38fe0-3189">Nazwa połączoną usługą magazynu Azure wskazujące do magazynu obiektów blob, który zawiera plik zip działania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3189">Name of the Azure Storage linked service that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="38fe0-3190">W tym przykładzie jest: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3190">In the example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="38fe0-3191">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-3191">Yes</span></span> |
| <span data-ttu-id="38fe0-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="38fe0-3192">PackageFile</span></span> | <span data-ttu-id="38fe0-3193">Nazwa pliku zip.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3193">Name of the zip file.</span></span> <span data-ttu-id="38fe0-3194">W tym przykładzie jest: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3194">In the example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="38fe0-3195">Tak</span><span class="sxs-lookup"><span data-stu-id="38fe0-3195">Yes</span></span> |
| <span data-ttu-id="38fe0-3196">właściwości rozszerzone</span><span class="sxs-lookup"><span data-stu-id="38fe0-3196">extendedProperties</span></span> | <span data-ttu-id="38fe0-3197">Rozszerzone właściwości, które można definiować i przekazać kodu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3197">Extended properties that you can define and pass on to the .NET code.</span></span> <span data-ttu-id="38fe0-3198">W tym przykładzie **SliceStart** zmienna jest ustawiona wartość opartą na SliceStart zmiennej systemowej.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3198">In this example, the **SliceStart** variable is set to a value based on the SliceStart system variable.</span></span> | <span data-ttu-id="38fe0-3199">Nie</span><span class="sxs-lookup"><span data-stu-id="38fe0-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="38fe0-3200">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="38fe0-3200">JSON example</span></span>

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

<span data-ttu-id="38fe0-3201">Aby uzyskać szczegółowe informacje, zobacz [skorzystać z działań niestandardowych w fabryce danych](data-factory-use-custom-activities.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="38fe0-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="38fe0-3202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="38fe0-3202">Next Steps</span></span>
<span data-ttu-id="38fe0-3203">Zobacz następujące samouczki:</span><span class="sxs-lookup"><span data-stu-id="38fe0-3203">See the following tutorials:</span></span> 

- [<span data-ttu-id="38fe0-3204">Samouczek: tworzenie potoku z działanie kopiowania</span><span class="sxs-lookup"><span data-stu-id="38fe0-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="38fe0-3205">Samouczek: tworzenie potoku z działaniem gałęzi</span><span class="sxs-lookup"><span data-stu-id="38fe0-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)