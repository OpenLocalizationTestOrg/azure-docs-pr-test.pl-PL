---
title: "aaaAzure fabryki danych - odwołanie skryptów JSON | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="d6179-103">Fabryki danych Azure - JSON skryptów odwołania</span><span class="sxs-lookup"><span data-stu-id="d6179-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="d6179-104">Ten artykuł zawiera przykłady i schematów JSON do definiowania jednostek fabryki danych Azure (potoku, działania, zestawu danych i połączonej usługi).</span><span class="sxs-lookup"><span data-stu-id="d6179-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="d6179-105">Potok</span><span class="sxs-lookup"><span data-stu-id="d6179-105">Pipeline</span></span> 
<span data-ttu-id="d6179-106">Struktura wysokiego poziomu Hello definicji potoku jest następujący:</span><span class="sxs-lookup"><span data-stu-id="d6179-106">hello high-level structure for a pipeline definition is as follows:</span></span> 

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

<span data-ttu-id="d6179-107">Poniższa tabela zawiera opis właściwości hello w potoku hello definicji JSON:</span><span class="sxs-lookup"><span data-stu-id="d6179-107">Following table describes hello properties within hello pipeline JSON definition:</span></span>

| <span data-ttu-id="d6179-108">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-108">Property</span></span> | <span data-ttu-id="d6179-109">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-109">Description</span></span> | <span data-ttu-id="d6179-110">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="d6179-111">name</span><span class="sxs-lookup"><span data-stu-id="d6179-111">name</span></span> | <span data-ttu-id="d6179-112">Nazwa potoku hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-112">Name of hello pipeline.</span></span> <span data-ttu-id="d6179-113">Określ nazwę, która reprezentuje akcję hello hello działania lub potoku jest skonfigurowany toodo</span><span class="sxs-lookup"><span data-stu-id="d6179-113">Specify a name that represents hello action that hello activity or pipeline is configured toodo</span></span><br/><ul><li><span data-ttu-id="d6179-114">Maksymalna liczba znaków: 260</span><span class="sxs-lookup"><span data-stu-id="d6179-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="d6179-115">Musi rozpoczynać się literą, cyfrą lub podkreśleniem (_)</span><span class="sxs-lookup"><span data-stu-id="d6179-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="d6179-116">Następujące znaki nie są dozwolone: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</span><span class="sxs-lookup"><span data-stu-id="d6179-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="d6179-117">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-117">Yes</span></span> |
| <span data-ttu-id="d6179-118">description</span><span class="sxs-lookup"><span data-stu-id="d6179-118">description</span></span> |<span data-ttu-id="d6179-119">Tekst opisujący, jakie działania hello lub potoku jest używana</span><span class="sxs-lookup"><span data-stu-id="d6179-119">Text describing what hello activity or pipeline is used for</span></span> | <span data-ttu-id="d6179-120">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-120">No</span></span> |
| <span data-ttu-id="d6179-121">activities</span><span class="sxs-lookup"><span data-stu-id="d6179-121">activities</span></span> | <span data-ttu-id="d6179-122">Zawiera listę działań.</span><span class="sxs-lookup"><span data-stu-id="d6179-122">Contains a list of activities.</span></span> | <span data-ttu-id="d6179-123">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-123">Yes</span></span> |
| <span data-ttu-id="d6179-124">rozpoczynanie</span><span class="sxs-lookup"><span data-stu-id="d6179-124">start</span></span> |<span data-ttu-id="d6179-125">Data i godzina rozpoczęcia dla potoku hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-125">Start date-time for hello pipeline.</span></span> <span data-ttu-id="d6179-126">Musi być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="d6179-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="d6179-127">Na przykład: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="d6179-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="d6179-128">Jest możliwe toospecify czasu lokalnego, na przykład czas EST.</span><span class="sxs-lookup"><span data-stu-id="d6179-128">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="d6179-129">Oto przykład: `2016-02-27T06:00:00**-05:00`, która jest szacowana AM 6</span><span class="sxs-lookup"><span data-stu-id="d6179-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="d6179-130">Witaj właściwości początkową i końcową razem Określ okres aktywności potoku hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-130">hello start and end properties together specify active period for hello pipeline.</span></span> <span data-ttu-id="d6179-131">Wycinki danych wyjściowych tylko są tworzone z aktywny okres.</span><span class="sxs-lookup"><span data-stu-id="d6179-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="d6179-132">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-132">No</span></span><br/><br/><span data-ttu-id="d6179-133">Jeśli określono wartość dla właściwości końca hello, musisz określić wartość dla właściwości rozpoczęcia hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-133">If you specify a value for hello end property, you must specify value for hello start property.</span></span><br/><br/><span data-ttu-id="d6179-134">Witaj godziny rozpoczęcia i zakończenia zarówno można pusty toocreate potoku.</span><span class="sxs-lookup"><span data-stu-id="d6179-134">hello start and end times can both be empty toocreate a pipeline.</span></span> <span data-ttu-id="d6179-135">Należy określić zarówno wartości tooset jako aktywny okres hello toorun potoku.</span><span class="sxs-lookup"><span data-stu-id="d6179-135">You must specify both values tooset an active period for hello pipeline toorun.</span></span> <span data-ttu-id="d6179-136">Jeśli nie określono godziny rozpoczęcia i zakończenia podczas tworzenia potoku, można ustawić ich później za pomocą polecenia cmdlet hello AzureRmDataFactoryPipelineActivePeriod zestawu.</span><span class="sxs-lookup"><span data-stu-id="d6179-136">If you do not specify start and end times when creating a pipeline, you can set them using hello Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="d6179-137">Koniec</span><span class="sxs-lookup"><span data-stu-id="d6179-137">end</span></span> |<span data-ttu-id="d6179-138">Data czas zakończenia dla potoku hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-138">End date-time for hello pipeline.</span></span> <span data-ttu-id="d6179-139">Jeśli zostanie określona, musi być w formacie ISO.</span><span class="sxs-lookup"><span data-stu-id="d6179-139">If specified must be in ISO format.</span></span> <span data-ttu-id="d6179-140">Na przykład: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="d6179-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="d6179-141">Jest możliwe toospecify czasu lokalnego, na przykład czas EST.</span><span class="sxs-lookup"><span data-stu-id="d6179-141">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="d6179-142">Oto przykład: `2016-02-27T06:00:00**-05:00`, która jest szacowana AM 6</span><span class="sxs-lookup"><span data-stu-id="d6179-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="d6179-143">potok hello toorun przez czas nieokreślony, określ 9999-09-09 jako wartość właściwości końca hello hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-143">toorun hello pipeline indefinitely, specify 9999-09-09 as hello value for hello end property.</span></span> |<span data-ttu-id="d6179-144">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-144">No</span></span> <br/><br/><span data-ttu-id="d6179-145">Jeśli określono wartość dla właściwości rozpoczęcia hello, musisz określić wartość dla właściwości końca hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-145">If you specify a value for hello start property, you must specify value for hello end property.</span></span><br/><br/><span data-ttu-id="d6179-146">Zobacz uwagi dla hello **start** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-146">See notes for hello **start** property.</span></span> |
| <span data-ttu-id="d6179-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="d6179-147">isPaused</span></span> |<span data-ttu-id="d6179-148">Jeśli zestaw tootrue hello potoku nie działa.</span><span class="sxs-lookup"><span data-stu-id="d6179-148">If set tootrue hello pipeline does not run.</span></span> <span data-ttu-id="d6179-149">Wartość domyślna = false.</span><span class="sxs-lookup"><span data-stu-id="d6179-149">Default value = false.</span></span> <span data-ttu-id="d6179-150">Można użyć tej właściwości tooenable lub wyłączyć.</span><span class="sxs-lookup"><span data-stu-id="d6179-150">You can use this property tooenable or disable.</span></span> |<span data-ttu-id="d6179-151">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-151">No</span></span> |
| <span data-ttu-id="d6179-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="d6179-152">pipelineMode</span></span> |<span data-ttu-id="d6179-153">Metoda Hello planowania trwający hello potoku.</span><span class="sxs-lookup"><span data-stu-id="d6179-153">hello method for scheduling runs for hello pipeline.</span></span> <span data-ttu-id="d6179-154">Dozwolone wartości to: (domyślnie), zaplanowane jednorazowe.</span><span class="sxs-lookup"><span data-stu-id="d6179-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="d6179-155">"Zaplanowana" oznacza, że tego potoku hello jest uruchamiane w określonych odstępach czasu zgodnie z tooits aktywny okres (czas rozpoczęcia i zakończenia).</span><span class="sxs-lookup"><span data-stu-id="d6179-155">‘Scheduled’ indicates that hello pipeline runs at a specified time interval according tooits active period (start and end time).</span></span> <span data-ttu-id="d6179-156">"Jednorazowe" oznacza, że tego potoku hello jest wykonywane tylko raz.</span><span class="sxs-lookup"><span data-stu-id="d6179-156">‘Onetime’ indicates that hello pipeline runs only once.</span></span> <span data-ttu-id="d6179-157">Potoki jednorazowe utworzonej nie może być zmodyfikowany zaktualizowane obecnie.</span><span class="sxs-lookup"><span data-stu-id="d6179-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="d6179-158">Zobacz [potoku Onetime](data-factory-create-pipelines.md#onetime-pipeline) szczegółowe informacje o ustawienie jednorazowe.</span><span class="sxs-lookup"><span data-stu-id="d6179-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="d6179-159">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-159">No</span></span> |
| <span data-ttu-id="d6179-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="d6179-160">expirationTime</span></span> |<span data-ttu-id="d6179-161">Czas po utworzeniu, dla których hello potoku jest prawidłowa i powinny być zainicjowana.</span><span class="sxs-lookup"><span data-stu-id="d6179-161">Duration of time after creation for which hello pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="d6179-162">Jeśli nie ma żadnych aktywnych nie powiodło się, lub oczekujące działa, potoku hello zostanie usunięta automatycznie po osiągnięciu hello czas wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="d6179-162">If it does not have any active, failed, or pending runs, hello pipeline is deleted automatically once it reaches hello expiration time.</span></span> |<span data-ttu-id="d6179-163">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="d6179-164">Działanie</span><span class="sxs-lookup"><span data-stu-id="d6179-164">Activity</span></span> 
<span data-ttu-id="d6179-165">Hello struktury wysokiego poziomu do działania w potoku definicji (element działania), jest następujący:</span><span class="sxs-lookup"><span data-stu-id="d6179-165">hello high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

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

<span data-ttu-id="d6179-166">Następujące tabeli opisano właściwości hello w ramach działania hello definicji JSON:</span><span class="sxs-lookup"><span data-stu-id="d6179-166">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="d6179-167">Tag</span><span class="sxs-lookup"><span data-stu-id="d6179-167">Tag</span></span> | <span data-ttu-id="d6179-168">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-168">Description</span></span> | <span data-ttu-id="d6179-169">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-170">name</span><span class="sxs-lookup"><span data-stu-id="d6179-170">name</span></span> |<span data-ttu-id="d6179-171">Nazwa działania hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-171">Name of hello activity.</span></span> <span data-ttu-id="d6179-172">Określ nazwę, która reprezentuje hello akcję, która jest działanie hello skonfigurować toodo</span><span class="sxs-lookup"><span data-stu-id="d6179-172">Specify a name that represents hello action that hello activity is configured toodo</span></span><br/><ul><li><span data-ttu-id="d6179-173">Maksymalna liczba znaków: 260</span><span class="sxs-lookup"><span data-stu-id="d6179-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="d6179-174">Musi rozpoczynać się literą, cyfrą lub podkreśleniem (_)</span><span class="sxs-lookup"><span data-stu-id="d6179-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="d6179-175">Następujące znaki nie są dozwolone: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</span><span class="sxs-lookup"><span data-stu-id="d6179-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="d6179-176">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-176">Yes</span></span> |
| <span data-ttu-id="d6179-177">description</span><span class="sxs-lookup"><span data-stu-id="d6179-177">description</span></span> |<span data-ttu-id="d6179-178">Tekst opisujący, jakie działanie hello jest używany dla.</span><span class="sxs-lookup"><span data-stu-id="d6179-178">Text describing what hello activity is used for.</span></span> |<span data-ttu-id="d6179-179">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-179">Yes</span></span> |
| <span data-ttu-id="d6179-180">type</span><span class="sxs-lookup"><span data-stu-id="d6179-180">type</span></span> |<span data-ttu-id="d6179-181">Określa typ hello hello działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-181">Specifies hello type of hello activity.</span></span> <span data-ttu-id="d6179-182">Zobacz hello [MAGAZYNY danych](#data-stores) i [działań PRZEKSZTAŁCANIA danych](#data-transformation-activities) sekcje dla różnych typów działań.</span><span class="sxs-lookup"><span data-stu-id="d6179-182">See hello [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="d6179-183">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-183">Yes</span></span> |
| <span data-ttu-id="d6179-184">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="d6179-184">inputs</span></span> |<span data-ttu-id="d6179-185">Tabele wejściowe używane przez działanie hello</span><span class="sxs-lookup"><span data-stu-id="d6179-185">Input tables used by hello activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="d6179-186">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-186">Yes</span></span> |
| <span data-ttu-id="d6179-187">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="d6179-187">outputs</span></span> |<span data-ttu-id="d6179-188">Tabele wyjściowe używany w działaniu hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-188">Output tables used by hello activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="d6179-189">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-189">Yes</span></span> |
| <span data-ttu-id="d6179-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d6179-190">linkedServiceName</span></span> |<span data-ttu-id="d6179-191">Nazwa hello połączonej usługi używana na powitania działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-191">Name of hello linked service used by hello activity.</span></span> <br/><br/><span data-ttu-id="d6179-192">Działanie może wymagać określenia hello połączone usługi, która łączy toohello środowiska obliczeniowego wymagane.</span><span class="sxs-lookup"><span data-stu-id="d6179-192">An activity may require that you specify hello linked service that links toohello required compute environment.</span></span> |<span data-ttu-id="d6179-193">Tak, aby HDInsight działań, działania usługi Azure Machine Learning i działania dotyczącego procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="d6179-194">Nie dla wszystkich innych</span><span class="sxs-lookup"><span data-stu-id="d6179-194">No for all others</span></span> |
| <span data-ttu-id="d6179-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="d6179-195">typeProperties</span></span> |<span data-ttu-id="d6179-196">Właściwości w sekcji typeProperties hello są zależne od typu hello działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-196">Properties in hello typeProperties section depend on type of hello activity.</span></span> |<span data-ttu-id="d6179-197">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-197">No</span></span> |
| <span data-ttu-id="d6179-198">policy</span><span class="sxs-lookup"><span data-stu-id="d6179-198">policy</span></span> |<span data-ttu-id="d6179-199">Zasady, które mają wpływ na zachowanie środowiska wykonawczego hello hello działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-199">Policies that affect hello run-time behavior of hello activity.</span></span> <span data-ttu-id="d6179-200">Jeśli nie zostanie określona, używane są zasady domyślne.</span><span class="sxs-lookup"><span data-stu-id="d6179-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="d6179-201">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-201">No</span></span> |
| <span data-ttu-id="d6179-202">Harmonogram</span><span class="sxs-lookup"><span data-stu-id="d6179-202">scheduler</span></span> |<span data-ttu-id="d6179-203">Właściwość "harmonogramu" jest używana toodefine potrzeby planowania dla działania hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-203">“scheduler” property is used toodefine desired scheduling for hello activity.</span></span> <span data-ttu-id="d6179-204">Właściwości podrzędnych są takie same jak te w hello hello hello [właściwości availability w zestawie danych](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="d6179-204">Its subproperties are hello same as hello ones in hello [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="d6179-205">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="d6179-206">Zasady</span><span class="sxs-lookup"><span data-stu-id="d6179-206">Policies</span></span>
<span data-ttu-id="d6179-207">Zasady wpływają na zachowanie środowiska wykonawczego hello działania, w szczególności, podczas przetwarzania wycinka hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="d6179-207">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="d6179-208">w poniższej tabeli Hello zawiera szczegóły hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-208">hello following table provides hello details.</span></span>

| <span data-ttu-id="d6179-209">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-209">Property</span></span> | <span data-ttu-id="d6179-210">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-210">Permitted values</span></span> | <span data-ttu-id="d6179-211">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="d6179-211">Default Value</span></span> | <span data-ttu-id="d6179-212">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-213">Współbieżność</span><span class="sxs-lookup"><span data-stu-id="d6179-213">concurrency</span></span> |<span data-ttu-id="d6179-214">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="d6179-214">Integer</span></span> <br/><br/><span data-ttu-id="d6179-215">Wartość maksymalna: 10</span><span class="sxs-lookup"><span data-stu-id="d6179-215">Max value: 10</span></span> |<span data-ttu-id="d6179-216">1</span><span class="sxs-lookup"><span data-stu-id="d6179-216">1</span></span> |<span data-ttu-id="d6179-217">Liczba równoczesnych wykonaniami hello działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-217">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="d6179-218">Określa hello Liczba wykonań działania równoległego, które mogą wystąpić na różnych wycinków.</span><span class="sxs-lookup"><span data-stu-id="d6179-218">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="d6179-219">Na przykład jeśli działanie wymaga toogo za pośrednictwem duży zbiór dostępnych danych o większej wartości współbieżności przyspiesza hello przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-219">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="d6179-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="d6179-220">executionPriorityOrder</span></span> |<span data-ttu-id="d6179-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="d6179-221">NewestFirst</span></span><br/><br/><span data-ttu-id="d6179-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="d6179-222">OldestFirst</span></span> |<span data-ttu-id="d6179-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="d6179-223">OldestFirst</span></span> |<span data-ttu-id="d6179-224">Określa kolejność hello wycinki danych, które są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="d6179-224">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="d6179-225">Na przykład jeśli masz wycinków 2 (w toku co 4 godziny, a innym godzinie 5), a oba oczekują na wykonanie.</span><span class="sxs-lookup"><span data-stu-id="d6179-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="d6179-226">Jeśli ustawisz hello executionPriorityOrder toobe NewestFirst wycinka hello godzinie 5 jest przetwarzana najpierw.</span><span class="sxs-lookup"><span data-stu-id="d6179-226">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="d6179-227">Podobnie jeśli ustawisz hello executionPriorityORder toobe OldestFIrst wycinka hello godzinie 4 jest przetwarzany.</span><span class="sxs-lookup"><span data-stu-id="d6179-227">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="d6179-228">retry</span><span class="sxs-lookup"><span data-stu-id="d6179-228">retry</span></span> |<span data-ttu-id="d6179-229">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="d6179-229">Integer</span></span><br/><br/><span data-ttu-id="d6179-230">Maksymalna wartość może być 10</span><span class="sxs-lookup"><span data-stu-id="d6179-230">Max value can be 10</span></span> |<span data-ttu-id="d6179-231">0</span><span class="sxs-lookup"><span data-stu-id="d6179-231">0</span></span> |<span data-ttu-id="d6179-232">Liczba ponownych prób przed hello przetwarzania danych dla wycinka hello jest oznaczona jako niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="d6179-232">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="d6179-233">Wykonania działania dla wycinka danych próba zostanie ponowiona się toohello określona liczba ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="d6179-233">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="d6179-234">Ponów próbę Hello odbywa się jak najszybciej po awarii hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-234">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="d6179-235">timeout</span><span class="sxs-lookup"><span data-stu-id="d6179-235">timeout</span></span> |<span data-ttu-id="d6179-236">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="d6179-236">TimeSpan</span></span> |<span data-ttu-id="d6179-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="d6179-237">00:00:00</span></span> |<span data-ttu-id="d6179-238">Limit czasu dla działania hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-238">Timeout for hello activity.</span></span> <span data-ttu-id="d6179-239">Przykład: 00:10:00 (oznacza limitu 10 minut)</span><span class="sxs-lookup"><span data-stu-id="d6179-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="d6179-240">Jeśli wartość nie została określona lub jest równa 0, limit czasu hello jest nieograniczony.</span><span class="sxs-lookup"><span data-stu-id="d6179-240">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="d6179-241">Jeśli czas przetwarzania danych hello na wycinek przekracza wartość limitu czasu hello, anulowaniu i hello system próbuje tooretry hello przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="d6179-241">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="d6179-242">Witaj liczby ponownych prób zależy od hello ponawiania właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-242">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="d6179-243">W przypadku przekroczenia limitu czasu hello stan jest ustawiany tooTimedOut.</span><span class="sxs-lookup"><span data-stu-id="d6179-243">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="d6179-244">Opóźnienie</span><span class="sxs-lookup"><span data-stu-id="d6179-244">delay</span></span> |<span data-ttu-id="d6179-245">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="d6179-245">TimeSpan</span></span> |<span data-ttu-id="d6179-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="d6179-246">00:00:00</span></span> |<span data-ttu-id="d6179-247">Określ opóźnienie hello przed rozpoczęciem przetwarzania danych powoduje uruchomienie wycinek hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-247">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="d6179-248">Hello wykonywania działań dotyczących wycinek danych jest uruchamiany po hello opóźnienie jest hello oczekiwany czas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d6179-248">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="d6179-249">Przykład: 00:10:00 (oznacza opóźnienia w ciągu 10 minut)</span><span class="sxs-lookup"><span data-stu-id="d6179-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="d6179-250">Parametr longRetry</span><span class="sxs-lookup"><span data-stu-id="d6179-250">longRetry</span></span> |<span data-ttu-id="d6179-251">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="d6179-251">Integer</span></span><br/><br/><span data-ttu-id="d6179-252">Wartość maksymalna: 10</span><span class="sxs-lookup"><span data-stu-id="d6179-252">Max value: 10</span></span> |<span data-ttu-id="d6179-253">1</span><span class="sxs-lookup"><span data-stu-id="d6179-253">1</span></span> |<span data-ttu-id="d6179-254">Witaj liczbę długi ponownych prób przed hello wycinek wykonanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="d6179-254">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="d6179-255">Parametr longRetry prób uzyskają przez longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="d6179-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="d6179-256">Dlatego toospecify czas między ponownymi próbami, należy użyć longRetry.</span><span class="sxs-lookup"><span data-stu-id="d6179-256">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="d6179-257">Jeśli został określony zarówno longRetry, jak i ponów próbę, każdej próbie longRetry zawiera ponownych prób i hello maksymalną liczbę prób ponawiania * longRetry.</span><span class="sxs-lookup"><span data-stu-id="d6179-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="d6179-258">Na przykład, jeśli mamy hello następujące ustawienia zasad działania hello:</span><span class="sxs-lookup"><span data-stu-id="d6179-258">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="d6179-259">Spróbuj ponownie: 3</span><span class="sxs-lookup"><span data-stu-id="d6179-259">Retry: 3</span></span><br/><span data-ttu-id="d6179-260">Parametr longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="d6179-260">longRetry: 2</span></span><br/><span data-ttu-id="d6179-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="d6179-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="d6179-262">Załóżmy istnieje tylko jeden wycinek tooexecute (oczekiwanie stanu) i wykonania działania hello zawsze kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="d6179-262">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="d6179-263">Początkowo może być 3 wykonywanie kolejnych prób.</span><span class="sxs-lookup"><span data-stu-id="d6179-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="d6179-264">Po każdej próbie stanu wycinka hello byłoby ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="d6179-264">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="d6179-265">Po pierwsze 3 prób się za pośrednictwem stanu wycinka hello będą LongRetry.</span><span class="sxs-lookup"><span data-stu-id="d6179-265">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="d6179-266">Po upływie godziny (to znaczy wartość longRetryInteval w) będzie inny zestaw 3 wykonywanie kolejnych prób.</span><span class="sxs-lookup"><span data-stu-id="d6179-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="d6179-267">Po utworzeniu tego stanu wycinka hello będzie można i będą podejmowane próby.</span><span class="sxs-lookup"><span data-stu-id="d6179-267">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="d6179-268">Dlatego całkowity 6 podejmowano.</span><span class="sxs-lookup"><span data-stu-id="d6179-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="d6179-269">Jeśli wykonanie żadnych zakończy się powodzeniem, stan wycinek hello będzie gotowy i są podjęto próby.</span><span class="sxs-lookup"><span data-stu-id="d6179-269">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="d6179-270">Parametr longRetry mogą być używane w sytuacji, w których danych zależnych dociera deterministyczna razy lub hello ogólnej środowiska jest niestabilnym, w których przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="d6179-271">W takich przypadkach podczas ponownych prób po kolei nie mogą pomóc w i w ten sposób po upływie interwału czasu powoduje hello potrzebne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="d6179-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="d6179-272">Word Przestroga: nie należy ustawiać wysokiej wartości longRetry lub longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="d6179-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="d6179-273">Zazwyczaj wyższej wartości oznacza innych kwestii systemowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="d6179-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="d6179-274">longRetryInterval</span></span> |<span data-ttu-id="d6179-275">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="d6179-275">TimeSpan</span></span> |<span data-ttu-id="d6179-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="d6179-276">00:00:00</span></span> |<span data-ttu-id="d6179-277">Witaj opóźnienie między próbami czas ponów</span><span class="sxs-lookup"><span data-stu-id="d6179-277">hello delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="d6179-278">sekcja typeProperties</span><span class="sxs-lookup"><span data-stu-id="d6179-278">typeProperties section</span></span>
<span data-ttu-id="d6179-279">sekcja typeProperties Hello jest różne dla każdego działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-279">hello typeProperties section is different for each activity.</span></span> <span data-ttu-id="d6179-280">Transformacja działania mają tylko hello typu właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-280">Transformation activities have just hello type properties.</span></span> <span data-ttu-id="d6179-281">Zobacz [działań PRZEKSZTAŁCANIA danych](#data-transformation-activities) w tym artykule, aby uzyskać przykłady JSON, które definiują czynności do przekształcenia w potoku.</span><span class="sxs-lookup"><span data-stu-id="d6179-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="d6179-282">**Aktywność kopiowania** zawiera dwa podpunkty w sekcji typeProperties hello: **źródła** i **zbiornika**.</span><span class="sxs-lookup"><span data-stu-id="d6179-282">**Copy activity** has two subsections in hello typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="d6179-283">Zobacz [MAGAZYNY danych](#data-stores) sekcji w niniejszym artykule dla JSON przykłady przedstawiające sposób przechowywania toouse danych jako źródła i/lub ujścia.</span><span class="sxs-lookup"><span data-stu-id="d6179-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="d6179-284">Przykładowy potok kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-284">Sample copy pipeline</span></span>
<span data-ttu-id="d6179-285">Następujące przykładowe potoku hello, ma jedno działanie typu **kopiowania** w hello **działania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6179-285">In hello following sample pipeline, there is one activity of type **Copy** in hello **activities** section.</span></span> <span data-ttu-id="d6179-286">W tym przykładzie hello [aktywności kopiowania](data-factory-data-movement-activities.md) kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-286">In this sample, hello [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage tooan Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
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

<span data-ttu-id="d6179-287">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="d6179-287">Note hello following points:</span></span>

* <span data-ttu-id="d6179-288">W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="d6179-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span>
* <span data-ttu-id="d6179-289">Dane wejściowe dla działania hello jest ustawiony za**InputDataset** i danych wyjściowych dla działania hello jest ustawiony za**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="d6179-289">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span>
* <span data-ttu-id="d6179-290">W hello **typeProperties** sekcji **BlobSource** jest określony jako typ źródła hello i **SqlSink** jest określony jako typ ujścia hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-290">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span>

<span data-ttu-id="d6179-291">Zobacz [MAGAZYNY danych](#data-stores) sekcji w niniejszym artykule dla JSON przykłady przedstawiające sposób przechowywania toouse danych jako źródła i/lub ujścia.</span><span class="sxs-lookup"><span data-stu-id="d6179-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span>    

<span data-ttu-id="d6179-292">Aby uzyskać szczegółowy przewodnik tworzenia tego potoku, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d6179-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="d6179-293">Przykładowy potok przekształcania</span><span class="sxs-lookup"><span data-stu-id="d6179-293">Sample transformation pipeline</span></span>
<span data-ttu-id="d6179-294">Następujące przykładowe potoku hello, ma jedno działanie typu **HDInsightHive** w hello **działania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6179-294">In hello following sample pipeline, there is one activity of type **HDInsightHive** in hello **activities** section.</span></span> <span data-ttu-id="d6179-295">W tym przykładzie hello [działania HDInsight Hive](data-factory-hive-activity.md) przekształcenia danych z magazynu obiektów Blob platformy Azure, uruchamiając plik skryptu Hive w klastrze usługi Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d6179-295">In this sample, hello [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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

<span data-ttu-id="d6179-296">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="d6179-296">Note hello following points:</span></span> 

* <span data-ttu-id="d6179-297">W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="d6179-297">In hello activities section, there is only one activity whose **type** is set too**HDInsightHive**.</span></span>
* <span data-ttu-id="d6179-298">plik skryptu Hive Hello, **partitionweblogs.hql**, są przechowywane w hello kontem magazynu platformy Azure (określonego przez element scriptLinkedService hello, nazywany **AzureStorageLinkedService**) i w  **skrypt** folderu w kontenerze hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="d6179-298">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>
* <span data-ttu-id="d6179-299">Witaj **definiuje** sekcja jest używane toospecify hello środowiska uruchomieniowego ustawień, które są przekazywane skryptu hive toohello jako wartości konfiguracji gałąź (np. `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="d6179-299">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="d6179-300">Zobacz [działań PRZEKSZTAŁCANIA danych](#data-transformation-activities) w tym artykule, aby uzyskać przykłady JSON, które definiują czynności do przekształcenia w potoku.</span><span class="sxs-lookup"><span data-stu-id="d6179-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="d6179-301">Aby uzyskać szczegółowy przewodnik tworzenia tego potoku, zobacz [samouczek: Tworzenie pierwszego potoku dane tooprocess przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="d6179-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline tooprocess data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="d6179-302">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-302">Linked service</span></span>
<span data-ttu-id="d6179-303">Hello struktury wysokiego poziomu dla definicji usługi połączonej następująco:</span><span class="sxs-lookup"><span data-stu-id="d6179-303">hello high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="d6179-304">Następujące tabeli opisano właściwości hello w ramach działania hello definicji JSON:</span><span class="sxs-lookup"><span data-stu-id="d6179-304">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="d6179-305">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-305">Property</span></span> | <span data-ttu-id="d6179-306">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-306">Description</span></span> | <span data-ttu-id="d6179-307">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="d6179-308">name</span><span class="sxs-lookup"><span data-stu-id="d6179-308">name</span></span> | <span data-ttu-id="d6179-309">Nazwa hello połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="d6179-309">Name of hello linked service.</span></span> | <span data-ttu-id="d6179-310">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-310">Yes</span></span> | 
| <span data-ttu-id="d6179-311">właściwości — Typ</span><span class="sxs-lookup"><span data-stu-id="d6179-311">properties - type</span></span> | <span data-ttu-id="d6179-312">Typ hello połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="d6179-312">Type of hello linked service.</span></span> <span data-ttu-id="d6179-313">Na przykład: Usługa Azure Storage, baza danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="d6179-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="d6179-314">typeProperties</span></span> | <span data-ttu-id="d6179-315">sekcja typeProperties Hello zawiera elementy, które są różne dla każdego magazynu danych lub środowiska obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="d6179-315">hello typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="d6179-316">Zobacz [magazyny danych](#datastores) sekcji przypadku wszystkie dane hello sklepu usług połączonych i [obliczeniowe środowisk](#compute-environments) dla wszystkich hello obliczeniowe połączone usługi</span><span class="sxs-lookup"><span data-stu-id="d6179-316">See [data stores](#datastores) section for all hello data store linked services and [compute environments](#compute-environments) for all hello compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="d6179-317">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-317">Dataset</span></span> 
<span data-ttu-id="d6179-318">Zestaw danych z fabryki danych Azure jest zdefiniowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d6179-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="d6179-319">Witaj w poniższej tabeli opisano właściwości w hello powyżej JSON:</span><span class="sxs-lookup"><span data-stu-id="d6179-319">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="d6179-320">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-320">Property</span></span> | <span data-ttu-id="d6179-321">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-321">Description</span></span> | <span data-ttu-id="d6179-322">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-322">Required</span></span> | <span data-ttu-id="d6179-323">Domyślne</span><span class="sxs-lookup"><span data-stu-id="d6179-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-324">name</span><span class="sxs-lookup"><span data-stu-id="d6179-324">name</span></span> | <span data-ttu-id="d6179-325">Nazwa zestawu danych hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-325">Name of hello dataset.</span></span> <span data-ttu-id="d6179-326">Zobacz [fabryki danych Azure - reguły nazewnictwa](data-factory-naming-rules.md) dla reguły nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="d6179-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="d6179-327">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-327">Yes</span></span> |<span data-ttu-id="d6179-328">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d6179-328">NA</span></span> |
| <span data-ttu-id="d6179-329">type</span><span class="sxs-lookup"><span data-stu-id="d6179-329">type</span></span> | <span data-ttu-id="d6179-330">Typ hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-330">Type of hello dataset.</span></span> <span data-ttu-id="d6179-331">Określ jeden z typów hello obsługiwane przez usługi fabryka danych Azure (na przykład: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="d6179-331">Specify one of hello types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="d6179-332">Zobacz [MAGAZYNY danych](#data-stores) sekcji dla wszystkich hello magazynów danych i typy danych obsługiwane przez fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-332">See [DATA STORES](#data-stores) section for all hello data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="d6179-333">Struktura</span><span class="sxs-lookup"><span data-stu-id="d6179-333">structure</span></span> | <span data-ttu-id="d6179-334">Schemat hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-334">Schema of hello dataset.</span></span> <span data-ttu-id="d6179-335">Zawiera kolumny, jak ich typy, itp.</span><span class="sxs-lookup"><span data-stu-id="d6179-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="d6179-336">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-336">No</span></span> |<span data-ttu-id="d6179-337">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d6179-337">NA</span></span> |
| <span data-ttu-id="d6179-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="d6179-338">typeProperties</span></span> | <span data-ttu-id="d6179-339">Właściwości odpowiadającego toohello wybranego typu.</span><span class="sxs-lookup"><span data-stu-id="d6179-339">Properties corresponding toohello selected type.</span></span> <span data-ttu-id="d6179-340">Zobacz [MAGAZYNY danych](#data-stores) sekcji dla obsługiwanych typów i ich właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="d6179-341">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-341">Yes</span></span> |<span data-ttu-id="d6179-342">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d6179-342">NA</span></span> |
| <span data-ttu-id="d6179-343">external</span><span class="sxs-lookup"><span data-stu-id="d6179-343">external</span></span> | <span data-ttu-id="d6179-344">Wartość logiczna Flaga toospecify, czy zestaw danych jawnie jest generowany przez potok fabryki danych lub nie.</span><span class="sxs-lookup"><span data-stu-id="d6179-344">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="d6179-345">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-345">No</span></span> |<span data-ttu-id="d6179-346">wartość false</span><span class="sxs-lookup"><span data-stu-id="d6179-346">false</span></span> |
| <span data-ttu-id="d6179-347">availability</span><span class="sxs-lookup"><span data-stu-id="d6179-347">availability</span></span> | <span data-ttu-id="d6179-348">Definiuje hello przetwarzania okna lub hello fragmentowania modelu hello zestawu danych produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="d6179-348">Defines hello processing window or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="d6179-349">Aby uzyskać szczegółowe informacje w zestawie danych hello fragmentowania modelu, zobacz [planowania i wykonywania](data-factory-scheduling-and-execution.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-349">For details on hello dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="d6179-350">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-350">Yes</span></span> |<span data-ttu-id="d6179-351">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d6179-351">NA</span></span> |
| <span data-ttu-id="d6179-352">policy</span><span class="sxs-lookup"><span data-stu-id="d6179-352">policy</span></span> |<span data-ttu-id="d6179-353">Definiuje kryteria hello lub hello warunek, który należy spełnić hello wycinków zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-353">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="d6179-354">Aby uzyskać więcej informacji, zobacz [zestawie danych zasad](#Policy) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6179-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="d6179-355">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-355">No</span></span> |<span data-ttu-id="d6179-356">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d6179-356">NA</span></span> |

<span data-ttu-id="d6179-357">Każda kolumna hello **struktury** sekcja zawiera hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="d6179-357">Each column in hello **structure** section contains hello following properties:</span></span>

| <span data-ttu-id="d6179-358">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-358">Property</span></span> | <span data-ttu-id="d6179-359">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-359">Description</span></span> | <span data-ttu-id="d6179-360">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-361">name</span><span class="sxs-lookup"><span data-stu-id="d6179-361">name</span></span> |<span data-ttu-id="d6179-362">Nazwa kolumny hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-362">Name of hello column.</span></span> |<span data-ttu-id="d6179-363">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-363">Yes</span></span> |
| <span data-ttu-id="d6179-364">type</span><span class="sxs-lookup"><span data-stu-id="d6179-364">type</span></span> |<span data-ttu-id="d6179-365">Typ danych kolumny hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-365">Data type of hello column.</span></span>  |<span data-ttu-id="d6179-366">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-366">No</span></span> |
| <span data-ttu-id="d6179-367">Kultury</span><span class="sxs-lookup"><span data-stu-id="d6179-367">culture</span></span> |<span data-ttu-id="d6179-368">.NET na podstawie toobe kultura używana, gdy typ jest określona i jest typ architektury .NET `Datetime` lub `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="d6179-368">.NET based culture toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="d6179-369">Domyślnie jest `en-us`.</span><span class="sxs-lookup"><span data-stu-id="d6179-369">Default is `en-us`.</span></span> |<span data-ttu-id="d6179-370">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-370">No</span></span> |
| <span data-ttu-id="d6179-371">Format</span><span class="sxs-lookup"><span data-stu-id="d6179-371">format</span></span> |<span data-ttu-id="d6179-372">Format ciągu toobe używany, gdy typ jest określona i jest typ architektury .NET `Datetime` lub `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="d6179-372">Format string toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="d6179-373">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-373">No</span></span> |

<span data-ttu-id="d6179-374">W hello poniższy przykład, hello dataset zawiera trzy kolumny `slicetimestamp`, `projectname`, i `pageviews` i są typu: String, typ String i dziesiętnych odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="d6179-374">In hello following example, hello dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="d6179-375">Witaj poniższej tabeli opisano właściwości można używać w hello **dostępności** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-375">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="d6179-376">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-376">Property</span></span> | <span data-ttu-id="d6179-377">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-377">Description</span></span> | <span data-ttu-id="d6179-378">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-378">Required</span></span> | <span data-ttu-id="d6179-379">Domyślne</span><span class="sxs-lookup"><span data-stu-id="d6179-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-380">frequency</span><span class="sxs-lookup"><span data-stu-id="d6179-380">frequency</span></span> |<span data-ttu-id="d6179-381">Określa jednostkę czasu hello w środowisku produkcyjnym wycinek zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-381">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="d6179-382"><b>Obsługiwana częstotliwość</b>: minuty, godziny, dnia, tygodnia, miesiąca</span><span class="sxs-lookup"><span data-stu-id="d6179-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="d6179-383">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-383">Yes</span></span> |<span data-ttu-id="d6179-384">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d6179-384">NA</span></span> |
| <span data-ttu-id="d6179-385">interval</span><span class="sxs-lookup"><span data-stu-id="d6179-385">interval</span></span> |<span data-ttu-id="d6179-386">Określa mnożnik częstotliwości</span><span class="sxs-lookup"><span data-stu-id="d6179-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="d6179-387">"Interwał częstotliwości x" Określa, jak często hello wycinek jest generowany.</span><span class="sxs-lookup"><span data-stu-id="d6179-387">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="d6179-388">Należy hello podzielona na godzinę toobe zestawu danych, należy ustawić <b>częstotliwość</b> za<b>godzina</b>, i <b>interwał</b> za<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="d6179-388">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="d6179-389"><b>Uwaga</b>: Jeśli określisz częstotliwość co minutę, firma Microsoft zaleca ustawienie hello interwał toono mniej niż 15</span><span class="sxs-lookup"><span data-stu-id="d6179-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="d6179-390">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-390">Yes</span></span> |<span data-ttu-id="d6179-391">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d6179-391">NA</span></span> |
| <span data-ttu-id="d6179-392">Styl</span><span class="sxs-lookup"><span data-stu-id="d6179-392">style</span></span> |<span data-ttu-id="d6179-393">Określa, czy wycinek hello powinien zostać utworzony w hello rozpoczęcia/zakończenia hello interwału.</span><span class="sxs-lookup"><span data-stu-id="d6179-393">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="d6179-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="d6179-394">StartOfInterval</span></span></li><li><span data-ttu-id="d6179-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="d6179-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="d6179-396">Jeśli częstotliwość ustawiono tooMonth i styl jest ustawiony tooEndOfInterval, wycinek hello jest realizowane na powitania ostatni dzień miesiąca.</span><span class="sxs-lookup"><span data-stu-id="d6179-396">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="d6179-397">Jeśli hello styl jest ustawiony tooStartOfInterval, wycinek hello jest realizowane na powitania pierwszego dnia miesiąca.</span><span class="sxs-lookup"><span data-stu-id="d6179-397">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="d6179-398">Jeśli częstotliwość ustawiono tooDay i styl jest ustawiony tooEndOfInterval, wycinek hello jest tworzona w hello ostatniej godziny hello dnia.</span><span class="sxs-lookup"><span data-stu-id="d6179-398">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="d6179-399">Jeśli częstotliwość ustawiono tooHour i styl jest ustawiony tooEndOfInterval, wycinek hello jest generowany na końcu hello hello godzinę.</span><span class="sxs-lookup"><span data-stu-id="d6179-399">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="d6179-400">Na przykład dla wycinka okres 13: 00 – 14: 00, wycinek hello jest generowany na 14: 00.</span><span class="sxs-lookup"><span data-stu-id="d6179-400">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="d6179-401">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-401">No</span></span> |<span data-ttu-id="d6179-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="d6179-402">EndOfInterval</span></span> |
| <span data-ttu-id="d6179-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="d6179-403">anchorDateTime</span></span> |<span data-ttu-id="d6179-404">Definiuje położenie bezwzględne hello w czasie używana przez granice wycinek dataset toocompute harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="d6179-404">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="d6179-405"><b>Uwaga</b>: hello AnchorDateTime ma części daty, które są bardziej szczegółowego niż częstotliwość hello następnie hello części bardziej szczegółowego są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="d6179-405"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="d6179-406">Na przykład, jeśli hello <b>interwał</b> jest <b>co godzinę</b> (częstotliwość: godzinę i interwał: 1) i hello <b>AnchorDateTime</b> zawiera <b>minut i sekund</b>następnie hello <b>minut i sekund</b> części hello AnchorDateTime są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="d6179-406">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="d6179-407">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-407">No</span></span> |<span data-ttu-id="d6179-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="d6179-408">01/01/0001</span></span> |
| <span data-ttu-id="d6179-409">Przesunięcie</span><span class="sxs-lookup"><span data-stu-id="d6179-409">offset</span></span> |<span data-ttu-id="d6179-410">Zakres czasu, przez który hello przesunięte początku i końcu wszystkie fragmenty zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-410">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="d6179-411"><b>Uwaga</b>: Jeśli jest określony zarówno anchorDateTime, jak i przesunięcie wynik hello jest shift hello połączone.</span><span class="sxs-lookup"><span data-stu-id="d6179-411"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="d6179-412">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-412">No</span></span> |<span data-ttu-id="d6179-413">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d6179-413">NA</span></span> |

<span data-ttu-id="d6179-414">Określa powitania po sekcji dostępności tego zestawu danych wyjściowych hello jest utworzonych co godzinę (lub) danych wejściowych co godzinę zestaw danych jest dostępne:</span><span class="sxs-lookup"><span data-stu-id="d6179-414">hello following availability section specifies that hello output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="d6179-415">Witaj **zasad** sekcja w definicji zestawu danych definiuje kryteria hello lub konieczne jest spełnienie warunku hello hello wycinków zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-415">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

| <span data-ttu-id="d6179-416">Nazwa zasad</span><span class="sxs-lookup"><span data-stu-id="d6179-416">Policy Name</span></span> | <span data-ttu-id="d6179-417">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-417">Description</span></span> | <span data-ttu-id="d6179-418">Stosowane za</span><span class="sxs-lookup"><span data-stu-id="d6179-418">Applied too</span></span>| <span data-ttu-id="d6179-419">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-419">Required</span></span> | <span data-ttu-id="d6179-420">Domyślne</span><span class="sxs-lookup"><span data-stu-id="d6179-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d6179-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="d6179-421">minimumSizeMB</span></span> |<span data-ttu-id="d6179-422">Sprawdza poprawność danych hello w **obiektów blob platformy Azure** spełnia hello wymagań minimalny rozmiar (w MB).</span><span class="sxs-lookup"><span data-stu-id="d6179-422">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="d6179-423">Obiekt bob Azure</span><span class="sxs-lookup"><span data-stu-id="d6179-423">Azure Blob</span></span> |<span data-ttu-id="d6179-424">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-424">No</span></span> |<span data-ttu-id="d6179-425">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d6179-425">NA</span></span> |
| <span data-ttu-id="d6179-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="d6179-426">minimumRows</span></span> |<span data-ttu-id="d6179-427">Sprawdza poprawność danych hello w **bazy danych Azure SQL** lub **tabeli platformy Azure** zawiera hello minimalną liczbę wierszy.</span><span class="sxs-lookup"><span data-stu-id="d6179-427">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="d6179-428">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d6179-428">Azure SQL Database</span></span></li><li><span data-ttu-id="d6179-429">Tabeli platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d6179-429">Azure Table</span></span></li></ul> |<span data-ttu-id="d6179-430">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-430">No</span></span> |<span data-ttu-id="d6179-431">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d6179-431">NA</span></span> |

<span data-ttu-id="d6179-432">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="d6179-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="d6179-433">Jeśli zestaw danych jest tworzonym przez fabryki danych Azure, powinien być oznaczony jako **zewnętrznych**.</span><span class="sxs-lookup"><span data-stu-id="d6179-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="d6179-434">To ustawienie dotyczy wejść toohello pierwszy aktywności w potoku, chyba że działania lub łańcucha potoku jest używany.</span><span class="sxs-lookup"><span data-stu-id="d6179-434">This setting generally applies toohello inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="d6179-435">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d6179-435">Name</span></span> | <span data-ttu-id="d6179-436">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-436">Description</span></span> | <span data-ttu-id="d6179-437">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-437">Required</span></span> | <span data-ttu-id="d6179-438">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="d6179-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="d6179-439">dataDelay</span></span> |<span data-ttu-id="d6179-440">Sprawdzenie hello toodelay czasu dostępności hello hello danych zewnętrznych dla hello podane wycinka.</span><span class="sxs-lookup"><span data-stu-id="d6179-440">Time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="d6179-441">Na przykład jeśli hello są dostępne dane co godzinę, dane zewnętrzne hello toosee wyboru hello jest dostępny i hello odpowiedniego wycinek jest gotowy można opóźnić przy użyciu dataDelay.</span><span class="sxs-lookup"><span data-stu-id="d6179-441">For example, if hello data is available hourly, hello check toosee hello external data is available and hello corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="d6179-442">Ma zastosowanie tylko toohello obecny czas.</span><span class="sxs-lookup"><span data-stu-id="d6179-442">Only applies toohello present time.</span></span>  <span data-ttu-id="d6179-443">Na przykład jeśli 1:00 PM od razu i ta wartość to 10 minut, weryfikacji hello rozpoczyna się od 1:22:00.</span><span class="sxs-lookup"><span data-stu-id="d6179-443">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="d6179-444">To ustawienie nie ma wpływu na wycinki hello ostatnich (wycinków z godzina zakończenia wycinek + dataDelay < teraz) są przetwarzane bez opóźnień.</span><span class="sxs-lookup"><span data-stu-id="d6179-444">This setting does not affect slices in hello past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="d6179-445">Czasu większą niż 23:59 godziny wymagają toospecified przy użyciu hello `day.hours:minutes:seconds` format.</span><span class="sxs-lookup"><span data-stu-id="d6179-445">Time greater than 23:59 hours need toospecified using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="d6179-446">Na przykład toospecify 24 godziny, nie używaj 24:00:00; Zamiast tego należy użyć 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="d6179-446">For example, toospecify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="d6179-447">Jeśli używasz 24:00:00, będzie traktowane jako 24 dni (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="d6179-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="d6179-448">1 dzień i 4 godziny Określ 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="d6179-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="d6179-449">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-449">No</span></span> |<span data-ttu-id="d6179-450">0</span><span class="sxs-lookup"><span data-stu-id="d6179-450">0</span></span> |
| <span data-ttu-id="d6179-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="d6179-451">retryInterval</span></span> |<span data-ttu-id="d6179-452">czas oczekiwania Hello między błędu i hello dalej ponowienia próby.</span><span class="sxs-lookup"><span data-stu-id="d6179-452">hello wait time between a failure and hello next retry attempt.</span></span> <span data-ttu-id="d6179-453">W przypadku niepowodzenia spróbuj następnej próbie hello jest po retryInterval.</span><span class="sxs-lookup"><span data-stu-id="d6179-453">If a try fails, hello next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="d6179-454">Jeśli jest 1:00 PM od razu, możemy rozpocząć hello pierwszej próby.</span><span class="sxs-lookup"><span data-stu-id="d6179-454">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="d6179-455">W przypadku 1 minutę i nie można wykonać operacji hello hello czas trwania toocomplete hello pierwsze sprawdzanie poprawności hello Następna ponowna próba nastąpi na 1:00 1 min (czas trwania) + 1 min (interwał ponawiania) = 13:02:00.</span><span class="sxs-lookup"><span data-stu-id="d6179-455">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="d6179-456">Wycinki w przeszłości hello nie ma żadnego opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="d6179-456">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="d6179-457">Ponów próbę Hello odbywa się natychmiast.</span><span class="sxs-lookup"><span data-stu-id="d6179-457">hello retry happens immediately.</span></span> |<span data-ttu-id="d6179-458">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-458">No</span></span> |<span data-ttu-id="d6179-459">00:01:00 (1 minuta)</span><span class="sxs-lookup"><span data-stu-id="d6179-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="d6179-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="d6179-460">retryTimeout</span></span> |<span data-ttu-id="d6179-461">Witaj limitu czasu dla każdego ponowienia próby.</span><span class="sxs-lookup"><span data-stu-id="d6179-461">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="d6179-462">Jeśli ta właściwość jest ustawiona minut too10 hello toobe potrzeb Weryfikacja zakończona w ciągu 10 minut.</span><span class="sxs-lookup"><span data-stu-id="d6179-462">If this property is set too10 minutes, hello validation needs toobe completed within 10 minutes.</span></span> <span data-ttu-id="d6179-463">Jeśli trwa dłużej niż 10 minut tooperform hello weryfikacji, hello ponów limit.</span><span class="sxs-lookup"><span data-stu-id="d6179-463">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="d6179-464">Jeśli upłynie limit czasu wszystkie próby dla weryfikacji hello, wycinek hello jest oznaczona jako upłynął limit czasu.</span><span class="sxs-lookup"><span data-stu-id="d6179-464">If all attempts for hello validation times out, hello slice is marked as TimedOut.</span></span> |<span data-ttu-id="d6179-465">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-465">No</span></span> |<span data-ttu-id="d6179-466">00:10:00 (10 minut)</span><span class="sxs-lookup"><span data-stu-id="d6179-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="d6179-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="d6179-467">maximumRetry</span></span> |<span data-ttu-id="d6179-468">Liczba toocheck dostępności hello hello danych zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="d6179-468">Number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="d6179-469">Witaj dozwolone, wartość maksymalna to 10.</span><span class="sxs-lookup"><span data-stu-id="d6179-469">hello allowed maximum value is 10.</span></span> |<span data-ttu-id="d6179-470">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-470">No</span></span> |<span data-ttu-id="d6179-471">3</span><span class="sxs-lookup"><span data-stu-id="d6179-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="d6179-472">MAGAZYNY DANYCH</span><span class="sxs-lookup"><span data-stu-id="d6179-472">DATA STORES</span></span>
<span data-ttu-id="d6179-473">Witaj [połączona usługa](#linked-service) opisy sekcji określone dla elementów JSON, które są typowe tooall typów połączonych usług.</span><span class="sxs-lookup"><span data-stu-id="d6179-473">hello [Linked service](#linked-service) section provided descriptions for JSON elements that are common tooall types of linked services.</span></span> <span data-ttu-id="d6179-474">Ta sekcja zawiera szczegółowe informacje o elementach JSON, które są określone tooeach magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-474">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="d6179-475">Witaj [Dataset](#dataset) opisy sekcji określone dla elementów JSON, które są najczęściej spotykane typy tooall zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-475">hello [Dataset](#dataset) section provided descriptions for JSON elements that are common tooall types of datasets.</span></span> <span data-ttu-id="d6179-476">Ta sekcja zawiera szczegółowe informacje o elementach JSON, które są określone tooeach magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-476">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="d6179-477">Witaj [działania](#activity) opisy sekcji określone dla elementów JSON, które są tooall typowych działań.</span><span class="sxs-lookup"><span data-stu-id="d6179-477">hello [Activity](#activity) section provided descriptions for JSON elements that are common tooall types of activities.</span></span> <span data-ttu-id="d6179-478">Ta sekcja zawiera szczegółowe informacje o elementach JSON, które są określone tooeach magazynu danych, gdy jest używany jako źródło/ujście w działaniu kopiowania.</span><span class="sxs-lookup"><span data-stu-id="d6179-478">This section provides details about JSON elements that are specific tooeach data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="d6179-479">Kliknij łącze hello magazynu hello interesuje schematów JSON hello toosee dla połączonej usługi, zestaw danych i hello źródło/ujście dla aktywności kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-479">Click hello link for hello store you are interested in toosee hello JSON schemas for linked service, dataset, and hello source/sink for hello copy activity.</span></span>

| <span data-ttu-id="d6179-480">Kategoria</span><span class="sxs-lookup"><span data-stu-id="d6179-480">Category</span></span> | <span data-ttu-id="d6179-481">Magazyn danych</span><span class="sxs-lookup"><span data-stu-id="d6179-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="d6179-482">**Azure**</span><span class="sxs-lookup"><span data-stu-id="d6179-482">**Azure**</span></span> |[<span data-ttu-id="d6179-483">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="d6179-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="d6179-484">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d6179-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="d6179-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d6179-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="d6179-486">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d6179-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="d6179-487">Magazyn danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="d6179-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="d6179-488">Azure Search</span><span class="sxs-lookup"><span data-stu-id="d6179-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="d6179-489">Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="d6179-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="d6179-490">**Bazy danych**</span><span class="sxs-lookup"><span data-stu-id="d6179-490">**Databases**</span></span> |[<span data-ttu-id="d6179-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="d6179-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="d6179-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="d6179-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="d6179-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="d6179-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="d6179-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="d6179-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="d6179-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d6179-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="d6179-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="d6179-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="d6179-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="d6179-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="d6179-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="d6179-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="d6179-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="d6179-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="d6179-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="d6179-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="d6179-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="d6179-501">**NoSQL**</span></span> |[<span data-ttu-id="d6179-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="d6179-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="d6179-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="d6179-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="d6179-504">**Plik**</span><span class="sxs-lookup"><span data-stu-id="d6179-504">**File**</span></span> |[<span data-ttu-id="d6179-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="d6179-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="d6179-506">System plików</span><span class="sxs-lookup"><span data-stu-id="d6179-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="d6179-507">FTP</span><span class="sxs-lookup"><span data-stu-id="d6179-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="d6179-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="d6179-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="d6179-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="d6179-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="d6179-510">**Inne**</span><span class="sxs-lookup"><span data-stu-id="d6179-510">**Others**</span></span> |[<span data-ttu-id="d6179-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="d6179-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="d6179-512">OData</span><span class="sxs-lookup"><span data-stu-id="d6179-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="d6179-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="d6179-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="d6179-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="d6179-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="d6179-515">Tabela sieci Web</span><span class="sxs-lookup"><span data-stu-id="d6179-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="d6179-516">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="d6179-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-517">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-517">Linked service</span></span>
<span data-ttu-id="d6179-518">Istnieją dwa typy połączonych usług: połączonej usługi magazynu Azure i połączonej usługi magazynu Azure sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="d6179-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="d6179-519">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d6179-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="d6179-520">toolink fabrykę danych tooa konta magazynu platformy Azure przy użyciu hello **klucz konta**, Utwórz połączoną usługą magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-520">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="d6179-521">toodefine usługi Azure Storage połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="d6179-521">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="d6179-522">Następnie można określić następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-522">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-523">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-523">Property</span></span> | <span data-ttu-id="d6179-524">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-524">Description</span></span> | <span data-ttu-id="d6179-525">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d6179-526">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="d6179-526">connectionString</span></span> |<span data-ttu-id="d6179-527">Określ informacje niezbędne tooconnect tooAzure magazynu dla właściwości connectionString hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-527">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="d6179-528">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="d6179-529">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-529">Example</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="d6179-530">Połączonej usługi magazynu Azure SAS</span><span class="sxs-lookup"><span data-stu-id="d6179-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="d6179-531">Hello SAS magazynu Azure połączone usługi umożliwia toolink fabryki danych Azure tooan konta magazynu Azure za pomocą udostępnionego podpis dostępu (SAS).</span><span class="sxs-lookup"><span data-stu-id="d6179-531">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="d6179-532">Zapewnia fabryki danych hello dostęp ograniczony/czas-powiązane z określonego/tooall zasobów (kontener/obiektów blob) w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-532">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="d6179-533">toolink fabrykę danych tooa konta magazynu platformy Azure przy użyciu sygnatura dostępu współdzielonego, Utwórz usługę połączone SAS magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-533">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="d6179-534">toodefine SAS magazynu Azure połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**element AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="d6179-534">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="d6179-535">Następnie można określić następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-535">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="d6179-536">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-536">Property</span></span> | <span data-ttu-id="d6179-537">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-537">Description</span></span> | <span data-ttu-id="d6179-538">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d6179-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="d6179-539">sasUri</span></span> |<span data-ttu-id="d6179-540">Określ zasoby usługi Azure Storage toohello udostępnionych URI sygnatury dostępu obiektu blob, kontenera lub tabeli.</span><span class="sxs-lookup"><span data-stu-id="d6179-540">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="d6179-541">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="d6179-542">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-542">Example</span></span>

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

<span data-ttu-id="d6179-543">Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika usługi Azure Blob Storage](data-factory-azure-blob-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-544">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-544">Dataset</span></span>
<span data-ttu-id="d6179-545">toodefine zestawu danych obiektów Blob platformy Azure, zestawu hello **typu** hello DataSet za**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="d6179-545">toodefine an Azure Blob dataset, set hello **type** of hello dataset too**AzureBlob**.</span></span> <span data-ttu-id="d6179-546">Następnie określ następujące właściwości specyficzne dla obiektów Blob platformy Azure w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-546">Then, specify hello following Azure Blob specific properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-547">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-547">Property</span></span> | <span data-ttu-id="d6179-548">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-548">Description</span></span> | <span data-ttu-id="d6179-549">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="d6179-550">folderPath</span></span> |<span data-ttu-id="d6179-551">Ścieżka toohello kontenera i folderu w magazynie obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-551">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="d6179-552">Przykład: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="d6179-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="d6179-553">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-553">Yes</span></span> |
| <span data-ttu-id="d6179-554">fileName</span><span class="sxs-lookup"><span data-stu-id="d6179-554">fileName</span></span> |<span data-ttu-id="d6179-555">Nazwa obiektu blob hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-555">Name of hello blob.</span></span> <span data-ttu-id="d6179-556">Nazwa pliku jest opcjonalna i z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="d6179-557">Jeśli określono nazwę pliku, hello działania (takie jak kopiowanie) działa na hello konkretnego obiektu Blob.</span><span class="sxs-lookup"><span data-stu-id="d6179-557">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="d6179-558">Jeśli nie określono nazwy pliku, kopiowania obejmuje wszystkie obiekty BLOB w hello folderPath dla zestawu danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-558">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="d6179-559">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu: danych. <Guid>.txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="d6179-559">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="d6179-560">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-560">No</span></span> |
| <span data-ttu-id="d6179-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="d6179-561">partitionedBy</span></span> |<span data-ttu-id="d6179-562">partitionedBy jest opcjonalna właściwość.</span><span class="sxs-lookup"><span data-stu-id="d6179-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="d6179-563">Umożliwia toospecify folderPath dynamiczne i nazwę pliku dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-563">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="d6179-564">Na przykład folderPath mogą nadać parametry dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="d6179-565">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-565">No</span></span> |
| <span data-ttu-id="d6179-566">Format</span><span class="sxs-lookup"><span data-stu-id="d6179-566">format</span></span> | <span data-ttu-id="d6179-567">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d6179-567">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d6179-568">Zestaw hello **typu** właściwości w formacie tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d6179-568">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d6179-569">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="d6179-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d6179-570">Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-570">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d6179-571">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-571">No</span></span> |
| <span data-ttu-id="d6179-572">Kompresja</span><span class="sxs-lookup"><span data-stu-id="d6179-572">compression</span></span> | <span data-ttu-id="d6179-573">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-573">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d6179-574">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d6179-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="d6179-575">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="d6179-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d6179-576">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d6179-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d6179-577">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-578">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-578">Example</span></span>

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


<span data-ttu-id="d6179-579">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="d6179-580">BlobSource w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="d6179-581">Jeśli dane są kopiowane z magazynu obiektów Blob platformy Azure, należy ustawić hello **typ źródła** hello skopiować działania zbyt**BlobSource**i określ następujące właściwości w hello ** źródła ** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-581">If you are copying data from an Azure Blob Storage, set hello **source type** of hello copy activity too**BlobSource**, and specify following properties in hello **source **section:</span></span>

| <span data-ttu-id="d6179-582">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-582">Property</span></span> | <span data-ttu-id="d6179-583">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-583">Description</span></span> | <span data-ttu-id="d6179-584">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-584">Allowed values</span></span> | <span data-ttu-id="d6179-585">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-586">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="d6179-586">recursive</span></span> |<span data-ttu-id="d6179-587">Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="d6179-587">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="d6179-588">TRUE, False (wartość domyślna)</span><span class="sxs-lookup"><span data-stu-id="d6179-588">True (default value), False</span></span> |<span data-ttu-id="d6179-589">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="d6179-590">Przykład: BlobSource **</span><span class="sxs-lookup"><span data-stu-id="d6179-590">Example: BlobSource**</span></span>
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
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="d6179-591">BlobSink w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="d6179-592">Jeśli kopiujesz tooan danych magazynu obiektów Blob Azure, należy ustawić hello **typu sink** hello skopiować działania za**BlobSink**i określ następujące właściwości w hello **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-592">If you are copying data tooan Azure Blob Storage, set hello **sink type** of hello copy activity too**BlobSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="d6179-593">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-593">Property</span></span> | <span data-ttu-id="d6179-594">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-594">Description</span></span> | <span data-ttu-id="d6179-595">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-595">Allowed values</span></span> | <span data-ttu-id="d6179-596">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="d6179-597">copyBehavior</span></span> |<span data-ttu-id="d6179-598">Definiuje zachowanie kopii hello, gdy źródłem hello jest BlobSource lub systemu plików.</span><span class="sxs-lookup"><span data-stu-id="d6179-598">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="d6179-599"><b>PreserveHierarchy</b>: zachowuje hello hierarchii plików w folderze docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-599"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="d6179-600">Ścieżka względna Hello folderu toosource pliku źródłowego jest identyczne toohello względnej ścieżki folderu tootarget pliku docelowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-600">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="d6179-601"><b>FlattenHierarchy</b>: wszystkie pliki z folderu źródłowego hello znajdują się w hello najpierw poziomu folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-601"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="d6179-602">pliki docelowe Hello ma automatycznie wygeneruje nazwę.</span><span class="sxs-lookup"><span data-stu-id="d6179-602">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="d6179-603"><b>MergeFiles (domyślnie):</b> scala wszystkie pliki z pliku tooone folderu źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-603"><b>MergeFiles (default):</b> merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="d6179-604">Jeśli określono hello nazwa pliku/obiektu Blob, nazwa pliku scalonych hello będzie hello określoną nazwą; w przeciwnym razie będzie nazwa pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d6179-604">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="d6179-605">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="d6179-606">Przykład: BlobSink</span><span class="sxs-lookup"><span data-stu-id="d6179-606">Example: BlobSink</span></span>

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

<span data-ttu-id="d6179-607">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Blob](data-factory-azure-blob-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="d6179-608">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d6179-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-609">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-609">Linked service</span></span>
<span data-ttu-id="d6179-610">toodefine usługi Azure Data Lake Store połączony zestaw typu hello hello połączona usługa zbyt**AzureDataLakeStore**, a następnie określ następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-610">toodefine an Azure Data Lake Store linked service, set hello type of hello linked service too**AzureDataLakeStore**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-611">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-611">Property</span></span> | <span data-ttu-id="d6179-612">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-612">Description</span></span> | <span data-ttu-id="d6179-613">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d6179-614">type</span><span class="sxs-lookup"><span data-stu-id="d6179-614">type</span></span> | <span data-ttu-id="d6179-615">musi mieć ustawioną właściwość type Hello: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="d6179-615">hello type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="d6179-616">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-616">Yes</span></span> |
| <span data-ttu-id="d6179-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="d6179-617">dataLakeStoreUri</span></span> | <span data-ttu-id="d6179-618">Określ informacje o hello konta usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d6179-618">Specify information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="d6179-619">Jest on zgodny z formatem hello: `https://[accountname].azuredatalakestore.net/webhdfs/v1` lub `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="d6179-619">It is in hello following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="d6179-620">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-620">Yes</span></span> |
| <span data-ttu-id="d6179-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="d6179-621">subscriptionId</span></span> | <span data-ttu-id="d6179-622">Należy subskrypcji platformy Azure toowhich identyfikator usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d6179-622">Azure subscription Id toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="d6179-623">Wymagany dla odbiorcy</span><span class="sxs-lookup"><span data-stu-id="d6179-623">Required for sink</span></span> |
| <span data-ttu-id="d6179-624">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="d6179-624">resourceGroupName</span></span> | <span data-ttu-id="d6179-625">Należy toowhich Nazwa grupy zasobów platformy Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d6179-625">Azure resource group name toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="d6179-626">Wymagany dla odbiorcy</span><span class="sxs-lookup"><span data-stu-id="d6179-626">Required for sink</span></span> |
| <span data-ttu-id="d6179-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="d6179-627">servicePrincipalId</span></span> | <span data-ttu-id="d6179-628">Określ identyfikator aplikacji hello klienta.</span><span class="sxs-lookup"><span data-stu-id="d6179-628">Specify hello application's client ID.</span></span> | <span data-ttu-id="d6179-629">Tak (dla uwierzytelniania głównej usługi)</span><span class="sxs-lookup"><span data-stu-id="d6179-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="d6179-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="d6179-630">servicePrincipalKey</span></span> | <span data-ttu-id="d6179-631">Określ klucz aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-631">Specify hello application's key.</span></span> | <span data-ttu-id="d6179-632">Tak (dla uwierzytelniania głównej usługi)</span><span class="sxs-lookup"><span data-stu-id="d6179-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="d6179-633">Dzierżawy</span><span class="sxs-lookup"><span data-stu-id="d6179-633">tenant</span></span> | <span data-ttu-id="d6179-634">Określ informacje dzierżawy hello (identyfikator nazwy lub dzierżawy domeny), w którym znajduje się aplikacja.</span><span class="sxs-lookup"><span data-stu-id="d6179-634">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="d6179-635">Można go pobrać aktywowania myszy hello w hello prawym górnym rogu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-635">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure portal.</span></span> | <span data-ttu-id="d6179-636">Tak (dla uwierzytelniania głównej usługi)</span><span class="sxs-lookup"><span data-stu-id="d6179-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="d6179-637">Autoryzacji</span><span class="sxs-lookup"><span data-stu-id="d6179-637">authorization</span></span> | <span data-ttu-id="d6179-638">Kliknij przycisk **autoryzacji** przycisku na powitania **Edytor fabryki danych** , a następnie wprowadź Twoje poświadczenia przypisującej hello automatycznie generowanej autoryzacji adresu URL toothis właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-638">Click **Authorize** button in hello **Data Factory Editor** and enter your credential that assigns hello auto-generated authorization URL toothis property.</span></span> | <span data-ttu-id="d6179-639">Tak (do uwierzytelniania poświadczeń użytkownika)</span><span class="sxs-lookup"><span data-stu-id="d6179-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="d6179-640">Identyfikator sesji</span><span class="sxs-lookup"><span data-stu-id="d6179-640">sessionId</span></span> | <span data-ttu-id="d6179-641">Identyfikator sesji OAuth z sesji autoryzacji OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-641">OAuth session id from hello OAuth authorization session.</span></span> <span data-ttu-id="d6179-642">Każdy identyfikator sesji jest unikatowy i mogą być użyte tylko raz.</span><span class="sxs-lookup"><span data-stu-id="d6179-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="d6179-643">To ustawienie jest generowane automatycznie, gdy używasz Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="d6179-644">Tak (do uwierzytelniania poświadczeń użytkownika)</span><span class="sxs-lookup"><span data-stu-id="d6179-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="d6179-645">Przykład: przy użyciu uwierzytelniania głównej usługi</span><span class="sxs-lookup"><span data-stu-id="d6179-645">Example: using service principal authentication</span></span>
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

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="d6179-646">Przykład: przy użyciu uwierzytelniania poświadczeń użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-646">Example: using user credential authentication</span></span>
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

<span data-ttu-id="d6179-647">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-648">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-648">Dataset</span></span>
<span data-ttu-id="d6179-649">toodefine zestawem danych usługi Azure Data Lake Store hello zestaw **typu** hello DataSet za**AzureDataLakeStore**i określ następujące właściwości w hello hello **typeProperties**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-649">toodefine an Azure Data Lake Store dataset, set hello **type** of hello dataset too**AzureDataLakeStore**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-650">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-650">Property</span></span> | <span data-ttu-id="d6179-651">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-651">Description</span></span> | <span data-ttu-id="d6179-652">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d6179-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="d6179-653">folderPath</span></span> |<span data-ttu-id="d6179-654">Ścieżka toohello kontenera i folderu w hello Azure Data Lake magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6179-654">Path toohello container and folder in hello Azure Data Lake store.</span></span> |<span data-ttu-id="d6179-655">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-655">Yes</span></span> |
| <span data-ttu-id="d6179-656">fileName</span><span class="sxs-lookup"><span data-stu-id="d6179-656">fileName</span></span> |<span data-ttu-id="d6179-657">Nazwa pliku hello w hello Azure Data Lake store.</span><span class="sxs-lookup"><span data-stu-id="d6179-657">Name of hello file in hello Azure Data Lake store.</span></span> <span data-ttu-id="d6179-658">Nazwa pliku jest opcjonalna i z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="d6179-659">Jeśli określono nazwę pliku, hello działania (w tym kopiowania) działa na powitania określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="d6179-659">If you specify a filename, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="d6179-660">Jeśli nie określono nazwy pliku, kopia zawiera wszystkie pliki w hello folderPath dla zestawu danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-660">When fileName is not specified, Copy includes all files in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="d6179-661">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu: danych. <Guid>.txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="d6179-661">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="d6179-662">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-662">No</span></span> |
| <span data-ttu-id="d6179-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="d6179-663">partitionedBy</span></span> |<span data-ttu-id="d6179-664">partitionedBy jest opcjonalna właściwość.</span><span class="sxs-lookup"><span data-stu-id="d6179-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="d6179-665">Umożliwia toospecify folderPath dynamiczne i nazwę pliku dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-665">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="d6179-666">Na przykład folderPath mogą nadać parametry dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="d6179-667">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-667">No</span></span> |
| <span data-ttu-id="d6179-668">Format</span><span class="sxs-lookup"><span data-stu-id="d6179-668">format</span></span> | <span data-ttu-id="d6179-669">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d6179-669">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d6179-670">Zestaw hello **typu** właściwości w formacie tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d6179-670">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d6179-671">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="d6179-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d6179-672">Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-672">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d6179-673">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-673">No</span></span> |
| <span data-ttu-id="d6179-674">Kompresja</span><span class="sxs-lookup"><span data-stu-id="d6179-674">compression</span></span> | <span data-ttu-id="d6179-675">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-675">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d6179-676">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d6179-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="d6179-677">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="d6179-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d6179-678">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d6179-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d6179-679">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-680">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-680">Example</span></span>
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

<span data-ttu-id="d6179-681">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="d6179-682">Źródło usługi Azure Data Lake Store w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="d6179-683">Jeśli dane są kopiowane z usługi Azure Data Lake Store, ustaw hello **typ źródła** hello skopiować działania zbyt**AzureDataLakeStoreSource**i określ następujące właściwości w hello **źródła**  sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-683">If you are copying data from an Azure Data Lake Store, set hello **source type** of hello copy activity too**AzureDataLakeStoreSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="d6179-684">**AzureDataLakeStoreSource** obsługuje następujące właściwości hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-684">**AzureDataLakeStoreSource** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="d6179-685">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-685">Property</span></span> | <span data-ttu-id="d6179-686">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-686">Description</span></span> | <span data-ttu-id="d6179-687">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-687">Allowed values</span></span> | <span data-ttu-id="d6179-688">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-689">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="d6179-689">recursive</span></span> |<span data-ttu-id="d6179-690">Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="d6179-690">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="d6179-691">TRUE, False (wartość domyślna)</span><span class="sxs-lookup"><span data-stu-id="d6179-691">True (default value), False</span></span> |<span data-ttu-id="d6179-692">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="d6179-693">Przykład: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="d6179-693">Example: AzureDataLakeStoreSource</span></span>

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

<span data-ttu-id="d6179-694">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="d6179-695">Obiekt Sink usługi Azure Data Lake Store w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="d6179-696">Kopiowania danych tooan Azure Data Lake Store, ustaw hello **typu sink** hello skopiować działania zbyt**AzureDataLakeStoreSink**i określ następujące właściwości w hello **zbiornika**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-696">If you are copying data tooan Azure Data Lake Store, set hello **sink type** of hello copy activity too**AzureDataLakeStoreSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="d6179-697">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-697">Property</span></span> | <span data-ttu-id="d6179-698">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-698">Description</span></span> | <span data-ttu-id="d6179-699">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-699">Allowed values</span></span> | <span data-ttu-id="d6179-700">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="d6179-701">copyBehavior</span></span> |<span data-ttu-id="d6179-702">Określa zachowanie kopii hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-702">Specifies hello copy behavior.</span></span> |<span data-ttu-id="d6179-703"><b>PreserveHierarchy</b>: zachowuje hello hierarchii plików w folderze docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-703"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="d6179-704">Ścieżka względna Hello folderu toosource pliku źródłowego jest identyczne toohello względnej ścieżki folderu tootarget pliku docelowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-704">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="d6179-705"><b>FlattenHierarchy</b>: wszystkie pliki z folderu źródłowego hello są tworzone w hello pierwszy poziom folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-705"><b>FlattenHierarchy</b>: all files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="d6179-706">pliki docelowe Hello są tworzone z nazwą automatycznie generowane.</span><span class="sxs-lookup"><span data-stu-id="d6179-706">hello target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="d6179-707"><b>MergeFiles</b>: scala wszystkie pliki z pliku tooone folderu źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-707"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="d6179-708">Jeśli określono hello nazwa pliku/obiektu Blob, nazwa pliku scalonych hello będzie hello określoną nazwą; w przeciwnym razie będzie nazwa pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d6179-708">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="d6179-709">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="d6179-710">Przykład: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="d6179-710">Example: AzureDataLakeStoreSink</span></span>
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

<span data-ttu-id="d6179-711">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="d6179-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d6179-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="d6179-713">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-713">Linked service</span></span>
<span data-ttu-id="d6179-714">toodefine bazy danych Azure rozwiązania Cosmos połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**DocumentDb**i określ następujące właściwości w hello **typeProperties** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-714">toodefine an Azure Cosmos DB linked service, set hello **type** of hello linked service too**DocumentDb**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-715">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="d6179-715">**Property**</span></span> | <span data-ttu-id="d6179-716">**Opis**</span><span class="sxs-lookup"><span data-stu-id="d6179-716">**Description**</span></span> | <span data-ttu-id="d6179-717">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="d6179-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-718">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="d6179-718">connectionString</span></span> |<span data-ttu-id="d6179-719">Określ informacje niezbędne tooconnect tooAzure DB rozwiązania Cosmos w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-719">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="d6179-720">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-721">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-721">Example</span></span>

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
<span data-ttu-id="d6179-722">Aby uzyskać więcej informacji, zobacz [łącznika Azure DB rozwiązania Cosmos](data-factory-azure-documentdb-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="d6179-723">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-723">Dataset</span></span>
<span data-ttu-id="d6179-724">toodefine zestawem danych bazy danych Azure rozwiązania Cosmos hello zestaw **typu** hello DataSet za**DocumentDbCollection**i określ następujące właściwości w hello hello **typeProperties** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-724">toodefine an Azure Cosmos DB dataset, set hello **type** of hello dataset too**DocumentDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-725">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="d6179-725">**Property**</span></span> | <span data-ttu-id="d6179-726">**Opis**</span><span class="sxs-lookup"><span data-stu-id="d6179-726">**Description**</span></span> | <span data-ttu-id="d6179-727">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="d6179-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-728">CollectionName</span><span class="sxs-lookup"><span data-stu-id="d6179-728">collectionName</span></span> |<span data-ttu-id="d6179-729">Nazwa hello Azure DB rozwiązania Cosmos kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d6179-729">Name of hello Azure Cosmos DB collection.</span></span> |<span data-ttu-id="d6179-730">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-731">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-731">Example</span></span>

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
<span data-ttu-id="d6179-732">Aby uzyskać więcej informacji, zobacz [łącznika Azure DB rozwiązania Cosmos](data-factory-azure-documentdb-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="d6179-733">Źródło kolekcji Azure rozwiązania Cosmos bazy danych w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="d6179-734">Jeśli dane są kopiowane z bazy danych Azure rozwiązania Cosmos, ustaw hello **typ źródła** hello skopiować działania zbyt**DocumentDbCollectionSource**i określ następujące właściwości w hello **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-734">If you are copying data from an Azure Cosmos DB, set hello **source type** of hello copy activity too**DocumentDbCollectionSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="d6179-735">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="d6179-735">**Property**</span></span> | <span data-ttu-id="d6179-736">**Opis**</span><span class="sxs-lookup"><span data-stu-id="d6179-736">**Description**</span></span> | <span data-ttu-id="d6179-737">**Dozwolone wartości**</span><span class="sxs-lookup"><span data-stu-id="d6179-737">**Allowed values**</span></span> | <span data-ttu-id="d6179-738">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="d6179-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-739">query</span><span class="sxs-lookup"><span data-stu-id="d6179-739">query</span></span> |<span data-ttu-id="d6179-740">Określ hello zapytania tooread dane.</span><span class="sxs-lookup"><span data-stu-id="d6179-740">Specify hello query tooread data.</span></span> |<span data-ttu-id="d6179-741">Wyślij zapytanie do ciągu obsługuje bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d6179-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="d6179-742">Przykład:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="d6179-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="d6179-743">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-743">No</span></span> <br/><br/><span data-ttu-id="d6179-744">Jeśli nie zostanie określony, hello instrukcji SQL, która jest wykonywana:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="d6179-744">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="d6179-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="d6179-745">nestingSeparator</span></span> |<span data-ttu-id="d6179-746">Tooindicate znak specjalny, który hello dokumentu jest zagnieżdżony.</span><span class="sxs-lookup"><span data-stu-id="d6179-746">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="d6179-747">Dowolny znak.</span><span class="sxs-lookup"><span data-stu-id="d6179-747">Any character.</span></span> <br/><br/><span data-ttu-id="d6179-748">Azure DB rozwiązania Cosmos jest magazynem NoSQL dla dokumentów JSON, których struktury zagnieżdżone są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="d6179-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="d6179-749">Fabryka danych Azure umożliwia hierarchii toodenote użytkownika za pośrednictwem nestingSeparator, czyli "."</span><span class="sxs-lookup"><span data-stu-id="d6179-749">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="d6179-750">w hello powyżej przykłady.</span><span class="sxs-lookup"><span data-stu-id="d6179-750">in hello above examples.</span></span> <span data-ttu-id="d6179-751">Z separatorem hello działanie kopiowania hello wygeneruje obiektu "Name" hello z trzech elementów podrzędnych elementów pierwszy, środkowy i ostatnich, zgodnie z too"Name.First", "Name.Middle" i "Name.Last" w hello definicja tabeli.</span><span class="sxs-lookup"><span data-stu-id="d6179-751">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="d6179-752">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-753">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-753">Example</span></span>

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

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="d6179-754">Obiekt Sink kolekcji bazy danych Azure rozwiązania Cosmos w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="d6179-755">Jeśli kopiujesz tooAzure danych DB rozwiązania Cosmos ustawić hello **typu sink** hello skopiować działania zbyt**DocumentDbCollectionSink**i określ następujące właściwości w hello **zbiornika**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-755">If you are copying data tooAzure Cosmos DB, set hello **sink type** of hello copy activity too**DocumentDbCollectionSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="d6179-756">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="d6179-756">**Property**</span></span> | <span data-ttu-id="d6179-757">**Opis**</span><span class="sxs-lookup"><span data-stu-id="d6179-757">**Description**</span></span> | <span data-ttu-id="d6179-758">**Dozwolone wartości**</span><span class="sxs-lookup"><span data-stu-id="d6179-758">**Allowed values**</span></span> | <span data-ttu-id="d6179-759">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="d6179-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="d6179-760">nestingSeparator</span></span> |<span data-ttu-id="d6179-761">Wymagany jest znak specjalny w tooindicate nazwa kolumny źródła hello, który zagnieżdżone dokumentu.</span><span class="sxs-lookup"><span data-stu-id="d6179-761">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="d6179-762">Na przykład powyżej: `Name.First` w danych wyjściowych hello tabeli tworzy hello następującej strukturze JSON w dokumencie DB rozwiązania Cosmos hello:</span><span class="sxs-lookup"><span data-stu-id="d6179-762">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="d6179-763">"Nazwa": {</span><span class="sxs-lookup"><span data-stu-id="d6179-763">"Name": {</span></span><br/>    <span data-ttu-id="d6179-764">"Pierwszy": "Jan"</span><span class="sxs-lookup"><span data-stu-id="d6179-764">"First": "John"</span></span><br/><span data-ttu-id="d6179-765">},</span><span class="sxs-lookup"><span data-stu-id="d6179-765">},</span></span> |<span data-ttu-id="d6179-766">Znak, który jest używany tooseparate poziomów zagnieżdżenia.</span><span class="sxs-lookup"><span data-stu-id="d6179-766">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="d6179-767">Wartość domyślna to `.` (kropką).</span><span class="sxs-lookup"><span data-stu-id="d6179-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="d6179-768">Znak, który jest używany tooseparate poziomów zagnieżdżenia.</span><span class="sxs-lookup"><span data-stu-id="d6179-768">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="d6179-769">Wartość domyślna to `.` (kropką).</span><span class="sxs-lookup"><span data-stu-id="d6179-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="d6179-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d6179-770">writeBatchSize</span></span> |<span data-ttu-id="d6179-771">Liczba równoległe żądań tooAzure DB rozwiązania Cosmos usługi toocreate dokumentów.</span><span class="sxs-lookup"><span data-stu-id="d6179-771">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="d6179-772">Aby precyzyjnie zdefiniować hello wydajności podczas kopiowania danych z bazy danych rozwiązania Cosmos Azure przy użyciu tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-772">You can fine-tune hello performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="d6179-773">Wraz ze zwiększeniem writeBatchSize, ponieważ więcej żądań równoległych tooAzure rozwiązania Cosmos bazy danych są wysyłane, może spodziewać się lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="d6179-773">You can expect a better performance when you increase writeBatchSize because more parallel requests tooAzure Cosmos DB are sent.</span></span> <span data-ttu-id="d6179-774">Jednak potrzebny tooavoid ograniczania przepustowości, który może zgłaszać komunikat o błędzie hello: "jest duża szybkość żądania".</span><span class="sxs-lookup"><span data-stu-id="d6179-774">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="d6179-775">Ograniczanie zadecyduje o wiele czynników, w tym rozmiar dokumentów, liczbę dokumentów, indeksowania zasady kolekcji docelowej, itd. Operacje kopiowania, można użyć lepsze hello toohave kolekcji (na przykład S3) większości dostępna przepustowość (2500 żądań jednostek na sekundę).</span><span class="sxs-lookup"><span data-stu-id="d6179-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="d6179-776">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="d6179-776">Integer</span></span> |<span data-ttu-id="d6179-777">Nie (domyślne: 5)</span><span class="sxs-lookup"><span data-stu-id="d6179-777">No (default: 5)</span></span> |
| <span data-ttu-id="d6179-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="d6179-778">writeBatchTimeout</span></span> |<span data-ttu-id="d6179-779">Czas toocomplete operacji hello oczekiwania, zanim upłynie limit czasu.</span><span class="sxs-lookup"><span data-stu-id="d6179-779">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="d6179-780">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="d6179-780">timespan</span></span><br/><br/> <span data-ttu-id="d6179-781">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="d6179-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="d6179-782">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-783">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-783">Example</span></span>

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
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
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

<span data-ttu-id="d6179-784">Aby uzyskać więcej informacji, zobacz [łącznika Azure DB rozwiązania Cosmos](data-factory-azure-documentdb-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="d6179-785">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d6179-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-786">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-786">Linked service</span></span>
<span data-ttu-id="d6179-787">toodefine bazy danych SQL Azure połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureSqlDatabase**i określ następujące właściwości w hello **typeProperties**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-787">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-788">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-788">Property</span></span> | <span data-ttu-id="d6179-789">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-789">Description</span></span> | <span data-ttu-id="d6179-790">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-791">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="d6179-791">connectionString</span></span> |<span data-ttu-id="d6179-792">Określ informacje niezbędne wystąpienie bazy danych SQL Azure toohello tooconnect hello właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="d6179-792">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="d6179-793">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-794">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-794">Example</span></span>
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

<span data-ttu-id="d6179-795">Aby uzyskać więcej informacji, zobacz [Łącznik usług Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-796">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-796">Dataset</span></span>
<span data-ttu-id="d6179-797">toodefine zestawem danych usługi Azure SQL Database hello zestaw **typu** hello DataSet za**AzureSqlTable**i określ następujące właściwości w hello hello **typeProperties** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-797">toodefine an Azure SQL Database dataset, set hello **type** of hello dataset too**AzureSqlTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-798">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-798">Property</span></span> | <span data-ttu-id="d6179-799">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-799">Description</span></span> | <span data-ttu-id="d6179-800">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-801">tableName</span><span class="sxs-lookup"><span data-stu-id="d6179-801">tableName</span></span> |<span data-ttu-id="d6179-802">Nazwa hello tabeli lub widoku w wystąpieniu bazy danych SQL Azure hello, która jest połączona usługa odnosi się do.</span><span class="sxs-lookup"><span data-stu-id="d6179-802">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="d6179-803">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-804">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-804">Example</span></span>

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
<span data-ttu-id="d6179-805">Aby uzyskać więcej informacji, zobacz [Łącznik usług Azure SQL](data-factory-azure-sql-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="d6179-806">Źródło SQL w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="d6179-807">Jeśli dane są kopiowane z bazy danych SQL Azure, należy ustawić hello **typ źródła** hello skopiować działania zbyt**SqlSource**i określ następujące właściwości w hello **źródła** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-807">If you are copying data from an Azure SQL Database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="d6179-808">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-808">Property</span></span> | <span data-ttu-id="d6179-809">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-809">Description</span></span> | <span data-ttu-id="d6179-810">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-810">Allowed values</span></span> | <span data-ttu-id="d6179-811">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-812">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="d6179-812">sqlReaderQuery</span></span> |<span data-ttu-id="d6179-813">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-813">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-814">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-814">SQL query string.</span></span> <span data-ttu-id="d6179-815">Przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="d6179-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="d6179-816">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-816">No</span></span> |
| <span data-ttu-id="d6179-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="d6179-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="d6179-818">Nazwa hello przechowywane procedury, która odczytuje dane z hello tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="d6179-818">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="d6179-819">Nazwa hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-819">Name of hello stored procedure.</span></span> |<span data-ttu-id="d6179-820">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-820">No</span></span> |
| <span data-ttu-id="d6179-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="d6179-821">storedProcedureParameters</span></span> |<span data-ttu-id="d6179-822">Parametry hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-822">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="d6179-823">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="d6179-823">Name/value pairs.</span></span> <span data-ttu-id="d6179-824">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-824">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="d6179-825">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-826">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-826">Example</span></span>

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
<span data-ttu-id="d6179-827">Aby uzyskać więcej informacji, zobacz [Łącznik usług Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="d6179-828">Obiekt Sink SQL w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="d6179-829">Jeśli kopiujesz tooAzure danych bazy danych SQL, ustaw hello **typu sink** hello skopiować działania zbyt**SqlSink**i określ następujące właściwości w hello **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-829">If you are copying data tooAzure SQL Database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="d6179-830">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-830">Property</span></span> | <span data-ttu-id="d6179-831">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-831">Description</span></span> | <span data-ttu-id="d6179-832">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-832">Allowed values</span></span> | <span data-ttu-id="d6179-833">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="d6179-834">writeBatchTimeout</span></span> |<span data-ttu-id="d6179-835">Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu.</span><span class="sxs-lookup"><span data-stu-id="d6179-835">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="d6179-836">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="d6179-836">timespan</span></span><br/><br/> <span data-ttu-id="d6179-837">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="d6179-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="d6179-838">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-838">No</span></span> |
| <span data-ttu-id="d6179-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d6179-839">writeBatchSize</span></span> |<span data-ttu-id="d6179-840">Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="d6179-840">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="d6179-841">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="d6179-841">Integer (number of rows)</span></span> |<span data-ttu-id="d6179-842">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="d6179-842">No (default: 10000)</span></span> |
| <span data-ttu-id="d6179-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="d6179-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="d6179-844">Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="d6179-844">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="d6179-845">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="d6179-845">A query statement.</span></span> |<span data-ttu-id="d6179-846">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-846">No</span></span> |
| <span data-ttu-id="d6179-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="d6179-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="d6179-848">Określ nazwę kolumny dla działania kopiowania toofill o identyfikatorze wycinek automatycznie generowane, która jest używana tooclean zapasowych określonych wycinek czas ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="d6179-848">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="d6179-849">Nazwa kolumny kolumnę o typie danych binary(32).</span><span class="sxs-lookup"><span data-stu-id="d6179-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="d6179-850">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-850">No</span></span> |
| <span data-ttu-id="d6179-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="d6179-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="d6179-852">Nazwa hello procedury składowanej danych upserts (aktualizacje/INSERT) do tabeli docelowej hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-852">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="d6179-853">Nazwa hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-853">Name of hello stored procedure.</span></span> |<span data-ttu-id="d6179-854">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-854">No</span></span> |
| <span data-ttu-id="d6179-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="d6179-855">storedProcedureParameters</span></span> |<span data-ttu-id="d6179-856">Parametry hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-856">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="d6179-857">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="d6179-857">Name/value pairs.</span></span> <span data-ttu-id="d6179-858">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-858">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="d6179-859">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-859">No</span></span> |
| <span data-ttu-id="d6179-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="d6179-860">sqlWriterTableType</span></span> |<span data-ttu-id="d6179-861">Określ toobe nazwy typu tabeli używany w procedurze hello przechowywane.</span><span class="sxs-lookup"><span data-stu-id="d6179-861">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="d6179-862">Działanie kopiowania udostępnia dane hello przenoszone w tabeli tymczasowej o tym typie tabeli.</span><span class="sxs-lookup"><span data-stu-id="d6179-862">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="d6179-863">Procedura składowana kod następnie można scalać dane hello kopiowane z istniejącymi danymi.</span><span class="sxs-lookup"><span data-stu-id="d6179-863">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="d6179-864">Nazwa typu tabeli.</span><span class="sxs-lookup"><span data-stu-id="d6179-864">A table type name.</span></span> |<span data-ttu-id="d6179-865">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-866">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-866">Example</span></span>

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

<span data-ttu-id="d6179-867">Aby uzyskać więcej informacji, zobacz [Łącznik usług Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="d6179-868">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d6179-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-869">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-869">Linked service</span></span>
<span data-ttu-id="d6179-870">toodefine Azure SQL Data Warehouse połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureSqlDW**i określ następujące właściwości w hello **typeProperties**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-870">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-871">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-871">Property</span></span> | <span data-ttu-id="d6179-872">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-872">Description</span></span> | <span data-ttu-id="d6179-873">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-874">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="d6179-874">connectionString</span></span> |<span data-ttu-id="d6179-875">Określ informacje potrzebne wystąpienia usługi Azure SQL Data Warehouse toohello tooconnect hello właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="d6179-875">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="d6179-876">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="d6179-877">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-877">Example</span></span>

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

<span data-ttu-id="d6179-878">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-879">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-879">Dataset</span></span>
<span data-ttu-id="d6179-880">toodefine zestawem danych usługi Azure SQL Data Warehouse hello zestaw **typu** hello DataSet za**AzureSqlDWTable**i określ następujące właściwości w hello hello **typeProperties**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-880">toodefine an Azure SQL Data Warehouse dataset, set hello **type** of hello dataset too**AzureSqlDWTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-881">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-881">Property</span></span> | <span data-ttu-id="d6179-882">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-882">Description</span></span> | <span data-ttu-id="d6179-883">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-884">tableName</span><span class="sxs-lookup"><span data-stu-id="d6179-884">tableName</span></span> |<span data-ttu-id="d6179-885">Nazwa hello tabeli lub widoku w bazie danych Azure SQL Data Warehouse hello, który hello połączonej usługi odwołuje się do.</span><span class="sxs-lookup"><span data-stu-id="d6179-885">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="d6179-886">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-887">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-887">Example</span></span>

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

<span data-ttu-id="d6179-888">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="d6179-889">Źródła magazynu danych SQL w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="d6179-890">Jeśli dane są kopiowane z magazynu danych SQL Azure, należy ustawić hello **typ źródła** hello skopiować działania zbyt**SqlDWSource**i określ następujące właściwości w hello **źródła**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-890">If you are copying data from Azure SQL Data Warehouse, set hello **source type** of hello copy activity too**SqlDWSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="d6179-891">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-891">Property</span></span> | <span data-ttu-id="d6179-892">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-892">Description</span></span> | <span data-ttu-id="d6179-893">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-893">Allowed values</span></span> | <span data-ttu-id="d6179-894">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-895">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="d6179-895">sqlReaderQuery</span></span> |<span data-ttu-id="d6179-896">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-896">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-897">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-897">SQL query string.</span></span> <span data-ttu-id="d6179-898">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="d6179-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="d6179-899">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-899">No</span></span> |
| <span data-ttu-id="d6179-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="d6179-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="d6179-901">Nazwa hello przechowywane procedury, która odczytuje dane z hello tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="d6179-901">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="d6179-902">Nazwa hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-902">Name of hello stored procedure.</span></span> |<span data-ttu-id="d6179-903">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-903">No</span></span> |
| <span data-ttu-id="d6179-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="d6179-904">storedProcedureParameters</span></span> |<span data-ttu-id="d6179-905">Parametry hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-905">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="d6179-906">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="d6179-906">Name/value pairs.</span></span> <span data-ttu-id="d6179-907">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-907">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="d6179-908">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-909">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-909">Example</span></span>

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

<span data-ttu-id="d6179-910">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="d6179-911">Ujścia magazynu danych SQL w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="d6179-912">Jeśli kopiujesz tooAzure danych magazynu danych SQL, ustaw hello **typu sink** hello skopiować działania zbyt**SqlDWSink**i określ następujące właściwości w hello **ujścia** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-912">If you are copying data tooAzure SQL Data Warehouse, set hello **sink type** of hello copy activity too**SqlDWSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="d6179-913">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-913">Property</span></span> | <span data-ttu-id="d6179-914">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-914">Description</span></span> | <span data-ttu-id="d6179-915">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-915">Allowed values</span></span> | <span data-ttu-id="d6179-916">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="d6179-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="d6179-918">Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="d6179-918">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="d6179-919">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="d6179-919">A query statement.</span></span> |<span data-ttu-id="d6179-920">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-920">No</span></span> |
| <span data-ttu-id="d6179-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="d6179-921">allowPolyBase</span></span> |<span data-ttu-id="d6179-922">Wskazuje, czy toouse PolyBase (jeśli jest to wymagane) zamiast BULKINSERT mechanizmu.</span><span class="sxs-lookup"><span data-stu-id="d6179-922">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="d6179-923">**Przy użyciu programu PolyBase jest hello zalecany sposób tooload danych do usługi SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="d6179-923">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="d6179-924">True</span><span class="sxs-lookup"><span data-stu-id="d6179-924">True</span></span> <br/><span data-ttu-id="d6179-925">Wartość FAŁSZ (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="d6179-925">False (default)</span></span> |<span data-ttu-id="d6179-926">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-926">No</span></span> |
| <span data-ttu-id="d6179-927">Usługi</span><span class="sxs-lookup"><span data-stu-id="d6179-927">polyBaseSettings</span></span> |<span data-ttu-id="d6179-928">Grupa właściwości, które można określić podczas hello **allowPolybase** właściwość jest ustawiona zbyt**true**.</span><span class="sxs-lookup"><span data-stu-id="d6179-928">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="d6179-929">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-929">No</span></span> |
| <span data-ttu-id="d6179-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="d6179-930">rejectValue</span></span> |<span data-ttu-id="d6179-931">Określa numer hello lub procent wierszy, które można odrzucić przed hello działanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="d6179-931">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="d6179-932">Dowiedz się więcej na temat hello PolyBase Odrzuć opcje w hello **argumenty** sekcji [Tworzenie tabeli zewnętrznej (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="d6179-932">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="d6179-933">0 (domyślnie), 1, 2...</span><span class="sxs-lookup"><span data-stu-id="d6179-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="d6179-934">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-934">No</span></span> |
| <span data-ttu-id="d6179-935">dla właściwości rejectType</span><span class="sxs-lookup"><span data-stu-id="d6179-935">rejectType</span></span> |<span data-ttu-id="d6179-936">Określa, czy opcja rejectValue hello jest określona jako wartość literału lub wartość procentowa.</span><span class="sxs-lookup"><span data-stu-id="d6179-936">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="d6179-937">Wartość (ustawienie domyślne), wartość procentowa</span><span class="sxs-lookup"><span data-stu-id="d6179-937">Value (default), Percentage</span></span> |<span data-ttu-id="d6179-938">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-938">No</span></span> |
| <span data-ttu-id="d6179-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="d6179-939">rejectSampleValue</span></span> |<span data-ttu-id="d6179-940">Określa liczbę hello tooretrieve wierszy przed hello PolyBase ponownie oblicza hello procent odrzuconych wierszy.</span><span class="sxs-lookup"><span data-stu-id="d6179-940">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="d6179-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="d6179-941">1, 2, …</span></span> |<span data-ttu-id="d6179-942">Tak, jeśli **dla właściwości rejectType** jest **procent**</span><span class="sxs-lookup"><span data-stu-id="d6179-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="d6179-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="d6179-943">useTypeDefault</span></span> |<span data-ttu-id="d6179-944">Określa, jak toohandle brakujących wartości w rozdzielane pliki tekstowe po programie PolyBase pobiera dane z pliku tekstowego hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-944">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="d6179-945">Dowiedz się więcej o tej właściwości z sekcji argumenty hello w [utworzyć EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6179-945">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="d6179-946">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="d6179-946">True, False (default)</span></span> |<span data-ttu-id="d6179-947">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-947">No</span></span> |
| <span data-ttu-id="d6179-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d6179-948">writeBatchSize</span></span> |<span data-ttu-id="d6179-949">Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d6179-949">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="d6179-950">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="d6179-950">Integer (number of rows)</span></span> |<span data-ttu-id="d6179-951">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="d6179-951">No (default: 10000)</span></span> |
| <span data-ttu-id="d6179-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="d6179-952">writeBatchTimeout</span></span> |<span data-ttu-id="d6179-953">Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu.</span><span class="sxs-lookup"><span data-stu-id="d6179-953">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="d6179-954">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="d6179-954">timespan</span></span><br/><br/> <span data-ttu-id="d6179-955">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="d6179-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="d6179-956">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-957">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-957">Example</span></span>

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

<span data-ttu-id="d6179-958">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="d6179-959">Azure Search</span><span class="sxs-lookup"><span data-stu-id="d6179-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-960">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-960">Linked service</span></span>
<span data-ttu-id="d6179-961">toodefine usługi Azure Search połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureSearch**i określ następujące właściwości w hello **typeProperties** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-961">toodefine an Azure Search linked service, set hello **type** of hello linked service too**AzureSearch**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-962">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-962">Property</span></span> | <span data-ttu-id="d6179-963">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-963">Description</span></span> | <span data-ttu-id="d6179-964">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="d6179-965">adres URL</span><span class="sxs-lookup"><span data-stu-id="d6179-965">url</span></span> | <span data-ttu-id="d6179-966">Adres URL hello usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="d6179-966">URL for hello Azure Search service.</span></span> | <span data-ttu-id="d6179-967">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-967">Yes</span></span> |
| <span data-ttu-id="d6179-968">key</span><span class="sxs-lookup"><span data-stu-id="d6179-968">key</span></span> | <span data-ttu-id="d6179-969">Klucz administratora dla hello usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="d6179-969">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="d6179-970">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-971">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-971">Example</span></span>

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

<span data-ttu-id="d6179-972">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Search](data-factory-azure-search-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="d6179-973">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-973">Dataset</span></span>
<span data-ttu-id="d6179-974">toodefine zestawem danych usługi Azure Search hello zestaw **typu** hello DataSet za**AzureSearchIndex**i określ następujące właściwości w hello hello **typeProperties** sekcji :</span><span class="sxs-lookup"><span data-stu-id="d6179-974">toodefine an Azure Search dataset, set hello **type** of hello dataset too**AzureSearchIndex**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-975">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-975">Property</span></span> | <span data-ttu-id="d6179-976">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-976">Description</span></span> | <span data-ttu-id="d6179-977">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="d6179-978">type</span><span class="sxs-lookup"><span data-stu-id="d6179-978">type</span></span> | <span data-ttu-id="d6179-979">zbyt należy ustawić właściwość typu Hello**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="d6179-979">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="d6179-980">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-980">Yes</span></span> |
| <span data-ttu-id="d6179-981">indexName</span><span class="sxs-lookup"><span data-stu-id="d6179-981">indexName</span></span> | <span data-ttu-id="d6179-982">Nazwa indeksu usługi Azure Search hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-982">Name of hello Azure Search index.</span></span> <span data-ttu-id="d6179-983">Fabryki danych nie powoduje utworzenia hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="d6179-983">Data Factory does not create hello index.</span></span> <span data-ttu-id="d6179-984">Indeks Hello musi istnieć w usłudze Azure Search.</span><span class="sxs-lookup"><span data-stu-id="d6179-984">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="d6179-985">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-986">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-986">Example</span></span>

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

<span data-ttu-id="d6179-987">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Search](data-factory-azure-search-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="d6179-988">Obiekt Sink indeksu usługi Azure Search w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="d6179-989">Jeśli kopiujesz indeksu usługi Azure Search tooan danych, ustaw hello **typu sink** hello skopiować działania zbyt**AzureSearchIndexSink**i określ następujące właściwości w hello **zbiornika**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-989">If you are copying data tooan Azure Search index, set hello **sink type** of hello copy activity too**AzureSearchIndexSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="d6179-990">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-990">Property</span></span> | <span data-ttu-id="d6179-991">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-991">Description</span></span> | <span data-ttu-id="d6179-992">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-992">Allowed values</span></span> | <span data-ttu-id="d6179-993">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="d6179-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="d6179-994">WriteBehavior</span></span> | <span data-ttu-id="d6179-995">Określa, czy toomerge lub Zastąp, gdy dokument już istnieje w indeksie hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-995">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> | <span data-ttu-id="d6179-996">Merge (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="d6179-996">Merge (default)</span></span><br/><span data-ttu-id="d6179-997">Upload</span><span class="sxs-lookup"><span data-stu-id="d6179-997">Upload</span></span>| <span data-ttu-id="d6179-998">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-998">No</span></span> |
| <span data-ttu-id="d6179-999">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d6179-999">WriteBatchSize</span></span> | <span data-ttu-id="d6179-1000">Przekazywanie danych do indeksu usługi Azure Search hello, gdy osiągnie rozmiar buforu hello writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="d6179-1000">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="d6179-1001">1 too1 000.</span><span class="sxs-lookup"><span data-stu-id="d6179-1001">1 too1,000.</span></span> <span data-ttu-id="d6179-1002">Wartość domyślna to 1000.</span><span class="sxs-lookup"><span data-stu-id="d6179-1002">Default value is 1000.</span></span> | <span data-ttu-id="d6179-1003">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1004">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1004">Example</span></span>

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

<span data-ttu-id="d6179-1005">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure Search](data-factory-azure-search-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="d6179-1006">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="d6179-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-1007">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1007">Linked service</span></span>
<span data-ttu-id="d6179-1008">Istnieją dwa typy połączonych usług: połączonej usługi magazynu Azure i połączonej usługi magazynu Azure sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="d6179-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="d6179-1009">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d6179-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="d6179-1010">toolink fabrykę danych tooa konta magazynu platformy Azure przy użyciu hello **klucz konta**, Utwórz połączoną usługą magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-1010">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="d6179-1011">toodefine usługi Azure Storage połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1011">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="d6179-1012">Następnie można określić następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1012">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-1013">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1013">Property</span></span> | <span data-ttu-id="d6179-1014">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1014">Description</span></span> | <span data-ttu-id="d6179-1015">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d6179-1016">type</span><span class="sxs-lookup"><span data-stu-id="d6179-1016">type</span></span> |<span data-ttu-id="d6179-1017">musi mieć ustawioną właściwość type Hello: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="d6179-1017">hello type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="d6179-1018">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1018">Yes</span></span> |
| <span data-ttu-id="d6179-1019">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="d6179-1019">connectionString</span></span> |<span data-ttu-id="d6179-1020">Określ informacje niezbędne tooconnect tooAzure magazynu dla właściwości connectionString hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1020">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="d6179-1021">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1021">Yes</span></span> |

<span data-ttu-id="d6179-1022">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="d6179-1022">**Example:**</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="d6179-1023">Połączonej usługi magazynu Azure SAS</span><span class="sxs-lookup"><span data-stu-id="d6179-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="d6179-1024">Hello SAS magazynu Azure połączone usługi umożliwia toolink fabryki danych Azure tooan konta magazynu Azure za pomocą udostępnionego podpis dostępu (SAS).</span><span class="sxs-lookup"><span data-stu-id="d6179-1024">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="d6179-1025">Zapewnia fabryki danych hello dostęp ograniczony/czas-powiązane z określonego/tooall zasobów (kontener/obiektów blob) w magazynie hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1025">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="d6179-1026">toolink fabrykę danych tooa konta magazynu platformy Azure przy użyciu sygnatura dostępu współdzielonego, Utwórz usługę połączone SAS magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-1026">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="d6179-1027">toodefine SAS magazynu Azure połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**element AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1027">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="d6179-1028">Następnie można określić następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1028">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="d6179-1029">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1029">Property</span></span> | <span data-ttu-id="d6179-1030">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1030">Description</span></span> | <span data-ttu-id="d6179-1031">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d6179-1032">type</span><span class="sxs-lookup"><span data-stu-id="d6179-1032">type</span></span> |<span data-ttu-id="d6179-1033">musi mieć ustawioną właściwość type Hello: **element AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="d6179-1033">hello type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="d6179-1034">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1034">Yes</span></span> |
| <span data-ttu-id="d6179-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="d6179-1035">sasUri</span></span> |<span data-ttu-id="d6179-1036">Określ zasoby usługi Azure Storage toohello udostępnionych URI sygnatury dostępu obiektu blob, kontenera lub tabeli.</span><span class="sxs-lookup"><span data-stu-id="d6179-1036">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="d6179-1037">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1037">Yes</span></span> |

<span data-ttu-id="d6179-1038">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="d6179-1038">**Example:**</span></span>

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

<span data-ttu-id="d6179-1039">Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika Azure Table Storage](data-factory-azure-table-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-1040">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1040">Dataset</span></span>
<span data-ttu-id="d6179-1041">toodefine zestaw tabel Azure hello zestaw **typu** hello DataSet za**AzureTable**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1041">toodefine an Azure Table dataset, set hello **type** of hello dataset too**AzureTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-1042">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1042">Property</span></span> | <span data-ttu-id="d6179-1043">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1043">Description</span></span> | <span data-ttu-id="d6179-1044">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="d6179-1045">tableName</span></span> |<span data-ttu-id="d6179-1046">Nazwa tabeli hello w wystąpieniu bazy danych tabeli Azure hello, która jest połączona usługa odnosi się do.</span><span class="sxs-lookup"><span data-stu-id="d6179-1046">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="d6179-1047">Tak.</span><span class="sxs-lookup"><span data-stu-id="d6179-1047">Yes.</span></span> <span data-ttu-id="d6179-1048">TableName jest określona bez azureTableSourceQuery, wszystkie rekordy z tabeli hello są skopiowanych toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-1048">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="d6179-1049">Jeśli określono również azureTableSourceQuery, rekordy z tabeli hello, która spełnia hello zapytania są skopiowanych toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-1049">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1050">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1050">Example</span></span>

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

<span data-ttu-id="d6179-1051">Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika Azure Table Storage](data-factory-azure-table-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="d6179-1052">Źródło tabeli platformy Azure w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1053">Jeśli dane są kopiowane z magazynu tabel Azure, należy ustawić hello **typ źródła** hello skopiować działania zbyt**AzureTableSource**i określ następujące właściwości w hello **źródła**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1053">If you are copying data from Azure Table Storage, set hello **source type** of hello copy activity too**AzureTableSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-1054">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1054">Property</span></span> | <span data-ttu-id="d6179-1055">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1055">Description</span></span> | <span data-ttu-id="d6179-1056">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1056">Allowed values</span></span> | <span data-ttu-id="d6179-1057">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1058">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="d6179-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="d6179-1059">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1059">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-1060">Ciąg zapytania tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-1060">Azure table query string.</span></span> <span data-ttu-id="d6179-1061">Przykłady w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1061">See examples in hello next section.</span></span> |<span data-ttu-id="d6179-1062">Nie.</span><span class="sxs-lookup"><span data-stu-id="d6179-1062">No.</span></span> <span data-ttu-id="d6179-1063">TableName jest określona bez azureTableSourceQuery, wszystkie rekordy z tabeli hello są skopiowanych toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-1063">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="d6179-1064">Jeśli określono również azureTableSourceQuery, rekordy z tabeli hello, która spełnia hello zapytania są skopiowanych toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-1064">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="d6179-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="d6179-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="d6179-1066">Wskazuje, czy wyjątek hello swallow tabeli nie istnieją.</span><span class="sxs-lookup"><span data-stu-id="d6179-1066">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="d6179-1067">WARTOŚĆ TRUE</span><span class="sxs-lookup"><span data-stu-id="d6179-1067">TRUE</span></span><br/><span data-ttu-id="d6179-1068">WARTOŚĆ FALSE</span><span class="sxs-lookup"><span data-stu-id="d6179-1068">FALSE</span></span> |<span data-ttu-id="d6179-1069">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1070">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1070">Example</span></span>

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

<span data-ttu-id="d6179-1071">Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika Azure Table Storage](data-factory-azure-table-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="d6179-1072">Obiekt Sink tabeli platformy Azure w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="d6179-1073">Jeśli kopiujesz tooAzure danych magazynu tabel, ustaw hello **typu sink** hello skopiować działania zbyt**AzureTableSink**i określ następujące właściwości w hello **ujścia** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-1073">If you are copying data tooAzure Table Storage, set hello **sink type** of hello copy activity too**AzureTableSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="d6179-1074">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1074">Property</span></span> | <span data-ttu-id="d6179-1075">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1075">Description</span></span> | <span data-ttu-id="d6179-1076">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1076">Allowed values</span></span> | <span data-ttu-id="d6179-1077">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="d6179-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="d6179-1079">Domyślna wartość klucza partycji, które mogą być używane przez obiekt sink hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1079">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="d6179-1080">Wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1080">A string value.</span></span> |<span data-ttu-id="d6179-1081">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1081">No</span></span> |
| <span data-ttu-id="d6179-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="d6179-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="d6179-1083">Określ nazwę kolumny hello, których wartości są używane jako klucze partycji.</span><span class="sxs-lookup"><span data-stu-id="d6179-1083">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="d6179-1084">Jeśli nie zostanie określony, AzureTableDefaultPartitionKeyValue jest używana jako klucza partycji hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="d6179-1085">Nazwa kolumny.</span><span class="sxs-lookup"><span data-stu-id="d6179-1085">A column name.</span></span> |<span data-ttu-id="d6179-1086">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1086">No</span></span> |
| <span data-ttu-id="d6179-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="d6179-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="d6179-1088">Określ nazwę kolumny hello, w których wartości kolumn używanych jako klucz wiersza.</span><span class="sxs-lookup"><span data-stu-id="d6179-1088">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="d6179-1089">Jeśli nie zostanie określony, użyj identyfikatora GUID dla każdego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d6179-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="d6179-1090">Nazwa kolumny.</span><span class="sxs-lookup"><span data-stu-id="d6179-1090">A column name.</span></span> |<span data-ttu-id="d6179-1091">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1091">No</span></span> |
| <span data-ttu-id="d6179-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="d6179-1092">azureTableInsertType</span></span> |<span data-ttu-id="d6179-1093">Tryb Hello tooinsert dane w tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-1093">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="d6179-1094">Ta właściwość określa, czy wartości zastąpienia lub scalić zostać istniejących wierszy w tabeli wyników hello ze zgodnymi kluczami partycji i wiersza.</span><span class="sxs-lookup"><span data-stu-id="d6179-1094">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="d6179-1095">toolearn informacji na temat tych ustawień (scalania i Zastąp) działania, zobacz [wstawienia lub scalania jednostki](https://msdn.microsoft.com/library/azure/hh452241.aspx) i [wstawienia lub Zastąp jednostki](https://msdn.microsoft.com/library/azure/hh452242.aspx) tematów.</span><span class="sxs-lookup"><span data-stu-id="d6179-1095">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="d6179-1096">To ustawienie jest stosowane na poziomie wiersza hello, nie poziomu tabeli hello i żadna z tych opcji usuwa wiersze w tabeli wyników hello, które nie istnieją w danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1096">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="d6179-1097">Merge (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="d6179-1097">merge (default)</span></span><br/><span data-ttu-id="d6179-1098">Zamień</span><span class="sxs-lookup"><span data-stu-id="d6179-1098">replace</span></span> |<span data-ttu-id="d6179-1099">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1099">No</span></span> |
| <span data-ttu-id="d6179-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d6179-1100">writeBatchSize</span></span> |<span data-ttu-id="d6179-1101">Wstawia dane do hello tabeli platformy Azure, gdy zostaje trafiony hello writeBatchSize lub writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="d6179-1101">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="d6179-1102">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="d6179-1102">Integer (number of rows)</span></span> |<span data-ttu-id="d6179-1103">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="d6179-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="d6179-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="d6179-1104">writeBatchTimeout</span></span> |<span data-ttu-id="d6179-1105">Wstawia dane do hello tabeli platformy Azure, gdy zostaje trafiony hello writeBatchSize lub writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="d6179-1105">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="d6179-1106">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="d6179-1106">timespan</span></span><br/><br/><span data-ttu-id="d6179-1107">Przykład: "00:20:00" (20 minut)</span><span class="sxs-lookup"><span data-stu-id="d6179-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="d6179-1108">Nie (domyślna toostorage klienta domyślny limit czasu operacji wartość 90 s)</span><span class="sxs-lookup"><span data-stu-id="d6179-1108">No (Default toostorage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1109">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1109">Example</span></span>

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
<span data-ttu-id="d6179-1110">Aby uzyskać więcej informacji na temat następujące połączone usługi, zobacz [łącznika Azure Table Storage](data-factory-azure-table-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="d6179-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="d6179-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-1112">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1112">Linked service</span></span>
<span data-ttu-id="d6179-1113">toodefine Redshift Amazon połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AmazonRedshift**i określ następujące właściwości w hello **typeProperties**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1113">toodefine an Amazon Redshift linked service, set hello **type** of hello linked service too**AmazonRedshift**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-1114">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1114">Property</span></span> | <span data-ttu-id="d6179-1115">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1115">Description</span></span> | <span data-ttu-id="d6179-1116">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1117">serwer</span><span class="sxs-lookup"><span data-stu-id="d6179-1117">server</span></span> |<span data-ttu-id="d6179-1118">Adres IP lub hosta nazwę hello Amazon Redshift serwera.</span><span class="sxs-lookup"><span data-stu-id="d6179-1118">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="d6179-1119">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1119">Yes</span></span> |
| <span data-ttu-id="d6179-1120">port</span><span class="sxs-lookup"><span data-stu-id="d6179-1120">port</span></span> |<span data-ttu-id="d6179-1121">Witaj liczbę hello port TCP, którego hello Amazon Redshift serwer używa toolisten dla połączeń klienta.</span><span class="sxs-lookup"><span data-stu-id="d6179-1121">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="d6179-1122">Nie, wartość domyślna: 5439</span><span class="sxs-lookup"><span data-stu-id="d6179-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="d6179-1123">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1123">database</span></span> |<span data-ttu-id="d6179-1124">Nazwa bazy danych usługi Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1124">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="d6179-1125">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1125">Yes</span></span> |
| <span data-ttu-id="d6179-1126">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-1126">username</span></span> |<span data-ttu-id="d6179-1127">Nazwa użytkownika, który ma toohello dostępu do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1127">Name of user who has access toohello database.</span></span> |<span data-ttu-id="d6179-1128">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1128">Yes</span></span> |
| <span data-ttu-id="d6179-1129">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-1129">password</span></span> |<span data-ttu-id="d6179-1130">Hasło dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1130">Password for hello user account.</span></span> |<span data-ttu-id="d6179-1131">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1132">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1132">Example</span></span>

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

<span data-ttu-id="d6179-1133">Aby uzyskać więcej informacji, zobacz [łącznik Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-1134">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1134">Dataset</span></span>
<span data-ttu-id="d6179-1135">toodefine zestawem danych usługi Amazon Redshift hello zestaw **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-1135">toodefine an Amazon Redshift dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-1136">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1136">Property</span></span> | <span data-ttu-id="d6179-1137">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1137">Description</span></span> | <span data-ttu-id="d6179-1138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="d6179-1139">tableName</span></span> |<span data-ttu-id="d6179-1140">Nazwa tabeli hello w bazie danych usługi Amazon Redshift hello, których połączonej usługi odwołuje się do.</span><span class="sxs-lookup"><span data-stu-id="d6179-1140">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="d6179-1141">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="d6179-1142">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1142">Example</span></span>

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
<span data-ttu-id="d6179-1143">Aby uzyskać więcej informacji, zobacz [łącznik Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="d6179-1144">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="d6179-1145">Jeśli dane są kopiowane z Amazon Redshift, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-1145">If you are copying data from Amazon Redshift, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-1146">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1146">Property</span></span> | <span data-ttu-id="d6179-1147">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1147">Description</span></span> | <span data-ttu-id="d6179-1148">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1148">Allowed values</span></span> | <span data-ttu-id="d6179-1149">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1150">query</span><span class="sxs-lookup"><span data-stu-id="d6179-1150">query</span></span> |<span data-ttu-id="d6179-1151">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1151">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-1152">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-1152">SQL query string.</span></span> <span data-ttu-id="d6179-1153">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="d6179-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="d6179-1154">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1155">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1155">Example</span></span>

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
<span data-ttu-id="d6179-1156">Aby uzyskać więcej informacji, zobacz [łącznik Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="d6179-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="d6179-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-1158">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1158">Linked service</span></span>
<span data-ttu-id="d6179-1159">toodefine IBM DB2 połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesDB2**i określ następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1159">toodefine an IBM DB2 linked service, set hello **type** of hello linked service too**OnPremisesDB2**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-1160">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1160">Property</span></span> | <span data-ttu-id="d6179-1161">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1161">Description</span></span> | <span data-ttu-id="d6179-1162">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1163">serwer</span><span class="sxs-lookup"><span data-stu-id="d6179-1163">server</span></span> |<span data-ttu-id="d6179-1164">Nazwa serwera hello bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="d6179-1164">Name of hello DB2 server.</span></span> |<span data-ttu-id="d6179-1165">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1165">Yes</span></span> |
| <span data-ttu-id="d6179-1166">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1166">database</span></span> |<span data-ttu-id="d6179-1167">Nazwa bazy danych hello DB2.</span><span class="sxs-lookup"><span data-stu-id="d6179-1167">Name of hello DB2 database.</span></span> |<span data-ttu-id="d6179-1168">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1168">Yes</span></span> |
| <span data-ttu-id="d6179-1169">Schemat</span><span class="sxs-lookup"><span data-stu-id="d6179-1169">schema</span></span> |<span data-ttu-id="d6179-1170">Nazwa schematu hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1170">Name of hello schema in hello database.</span></span> <span data-ttu-id="d6179-1171">Nazwa schematu Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-1171">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="d6179-1172">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1172">No</span></span> |
| <span data-ttu-id="d6179-1173">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-1173">authenticationType</span></span> |<span data-ttu-id="d6179-1174">Typ uwierzytelniania używany toohello tooconnect bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="d6179-1174">Type of authentication used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="d6179-1175">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="d6179-1176">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1176">Yes</span></span> |
| <span data-ttu-id="d6179-1177">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-1177">username</span></span> |<span data-ttu-id="d6179-1178">Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="d6179-1179">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1179">No</span></span> |
| <span data-ttu-id="d6179-1180">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-1180">password</span></span> |<span data-ttu-id="d6179-1181">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d6179-1181">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="d6179-1182">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1182">No</span></span> |
| <span data-ttu-id="d6179-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-1183">gatewayName</span></span> |<span data-ttu-id="d6179-1184">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych DB2.</span><span class="sxs-lookup"><span data-stu-id="d6179-1184">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="d6179-1185">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1186">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1186">Example</span></span>
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
<span data-ttu-id="d6179-1187">Aby uzyskać więcej informacji, zobacz [łącznik IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="d6179-1188">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1188">Dataset</span></span>
<span data-ttu-id="d6179-1189">toodefine bazy danych DB2 zestawu danych, ustaw hello **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1189">toodefine a DB2 dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="d6179-1190">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1190">Property</span></span> | <span data-ttu-id="d6179-1191">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1191">Description</span></span> | <span data-ttu-id="d6179-1192">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="d6179-1193">tableName</span></span> |<span data-ttu-id="d6179-1194">Nazwa tabeli hello w wystąpieniu bazy danych DB2 hello, która jest połączona usługa odnosi się do.</span><span class="sxs-lookup"><span data-stu-id="d6179-1194">Name of hello table in hello DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="d6179-1195">Witaj tableName jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-1195">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="d6179-1196">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="d6179-1197">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1197">Example</span></span>
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

<span data-ttu-id="d6179-1198">Aby uzyskać więcej informacji, zobacz [łącznik IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="d6179-1199">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1200">Jeśli dane są kopiowane z IBM DB2, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1200">If you are copying data from IBM DB2, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="d6179-1201">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1201">Property</span></span> | <span data-ttu-id="d6179-1202">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1202">Description</span></span> | <span data-ttu-id="d6179-1203">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1203">Allowed values</span></span> | <span data-ttu-id="d6179-1204">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1205">query</span><span class="sxs-lookup"><span data-stu-id="d6179-1205">query</span></span> |<span data-ttu-id="d6179-1206">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1206">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-1207">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-1207">SQL query string.</span></span> <span data-ttu-id="d6179-1208">Na przykład: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="d6179-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="d6179-1209">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1210">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1210">Example</span></span>
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
<span data-ttu-id="d6179-1211">Aby uzyskać więcej informacji, zobacz [łącznik IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="d6179-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="d6179-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-1213">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1213">Linked service</span></span>
<span data-ttu-id="d6179-1214">toodefine MySQL połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesMySql**i określ następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1214">toodefine a MySQL linked service, set hello **type** of hello linked service too**OnPremisesMySql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-1215">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1215">Property</span></span> | <span data-ttu-id="d6179-1216">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1216">Description</span></span> | <span data-ttu-id="d6179-1217">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1218">serwer</span><span class="sxs-lookup"><span data-stu-id="d6179-1218">server</span></span> |<span data-ttu-id="d6179-1219">Nazwa serwera MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1219">Name of hello MySQL server.</span></span> |<span data-ttu-id="d6179-1220">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1220">Yes</span></span> |
| <span data-ttu-id="d6179-1221">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1221">database</span></span> |<span data-ttu-id="d6179-1222">Nazwa bazy danych MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1222">Name of hello MySQL database.</span></span> |<span data-ttu-id="d6179-1223">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1223">Yes</span></span> |
| <span data-ttu-id="d6179-1224">Schemat</span><span class="sxs-lookup"><span data-stu-id="d6179-1224">schema</span></span> |<span data-ttu-id="d6179-1225">Nazwa schematu hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1225">Name of hello schema in hello database.</span></span> |<span data-ttu-id="d6179-1226">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1226">No</span></span> |
| <span data-ttu-id="d6179-1227">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-1227">authenticationType</span></span> |<span data-ttu-id="d6179-1228">Typ uwierzytelniania używany toohello tooconnect baza danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-1228">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="d6179-1229">Możliwe wartości to: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="d6179-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="d6179-1230">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1230">Yes</span></span> |
| <span data-ttu-id="d6179-1231">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-1231">username</span></span> |<span data-ttu-id="d6179-1232">Określ bazy danych MySQL toohello tooconnect nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d6179-1232">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="d6179-1233">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1233">Yes</span></span> |
| <span data-ttu-id="d6179-1234">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-1234">password</span></span> |<span data-ttu-id="d6179-1235">Określ hasło dla konta użytkownika hello określona.</span><span class="sxs-lookup"><span data-stu-id="d6179-1235">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="d6179-1236">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1236">Yes</span></span> |
| <span data-ttu-id="d6179-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-1237">gatewayName</span></span> |<span data-ttu-id="d6179-1238">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-1238">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="d6179-1239">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1240">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1240">Example</span></span>

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

<span data-ttu-id="d6179-1241">Aby uzyskać więcej informacji, zobacz [łącznika MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-1242">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1242">Dataset</span></span>
<span data-ttu-id="d6179-1243">toodefine zestawu danych MySQL, zestaw hello **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1243">toodefine a MySQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-1244">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1244">Property</span></span> | <span data-ttu-id="d6179-1245">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1245">Description</span></span> | <span data-ttu-id="d6179-1246">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="d6179-1247">tableName</span></span> |<span data-ttu-id="d6179-1248">Nazwa tabeli hello w hello wystąpienie bazy danych MySQL, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="d6179-1248">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="d6179-1249">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1250">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1250">Example</span></span>

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
<span data-ttu-id="d6179-1251">Aby uzyskać więcej informacji, zobacz [łącznika MySQL](data-factory-onprem-mysql-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="d6179-1252">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1253">Jeśli dane są kopiowane z bazy danych MySQL, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-1253">If you are copying data from a MySQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="d6179-1254">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1254">Property</span></span> | <span data-ttu-id="d6179-1255">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1255">Description</span></span> | <span data-ttu-id="d6179-1256">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1256">Allowed values</span></span> | <span data-ttu-id="d6179-1257">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1258">query</span><span class="sxs-lookup"><span data-stu-id="d6179-1258">query</span></span> |<span data-ttu-id="d6179-1259">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1259">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-1260">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-1260">SQL query string.</span></span> <span data-ttu-id="d6179-1261">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="d6179-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="d6179-1262">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="d6179-1263">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1263">Example</span></span>
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

<span data-ttu-id="d6179-1264">Aby uzyskać więcej informacji, zobacz [łącznika MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="d6179-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="d6179-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="d6179-1266">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1266">Linked service</span></span>
<span data-ttu-id="d6179-1267">toodefine Oracle połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesOracle**i określ następujące właściwości w hello **typeProperties** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-1267">toodefine an Oracle linked service, set hello **type** of hello linked service too**OnPremisesOracle**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-1268">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1268">Property</span></span> | <span data-ttu-id="d6179-1269">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1269">Description</span></span> | <span data-ttu-id="d6179-1270">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="d6179-1271">driverType</span></span> | <span data-ttu-id="d6179-1272">Określ, które sterownik toouse toocopy dane z / tooOracle bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1272">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="d6179-1273">Dozwolone wartości to **Microsoft** lub **ODP** (ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="d6179-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="d6179-1274">Zobacz [obsługiwanych wersji i instalacji](#supported-versions-and-installation) sekcji Szczegóły sterownika.</span><span class="sxs-lookup"><span data-stu-id="d6179-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="d6179-1275">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1275">No</span></span> |
| <span data-ttu-id="d6179-1276">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="d6179-1276">connectionString</span></span> | <span data-ttu-id="d6179-1277">Określ informacje niezbędne wystąpienie bazy danych Oracle toohello tooconnect hello właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="d6179-1277">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="d6179-1278">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1278">Yes</span></span> |
| <span data-ttu-id="d6179-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-1279">gatewayName</span></span> | <span data-ttu-id="d6179-1280">Nazwa bramy hello, że jest używana tooconnect toohello lokalnego serwera Oracle</span><span class="sxs-lookup"><span data-stu-id="d6179-1280">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="d6179-1281">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1282">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1282">Example</span></span>
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

<span data-ttu-id="d6179-1283">Aby uzyskać więcej informacji, zobacz [łącznika Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="d6179-1284">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1284">Dataset</span></span>
<span data-ttu-id="d6179-1285">toodefine zestawem danych Oracle hello zestaw **typu** hello DataSet za**OracleTable**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1285">toodefine an Oracle dataset, set hello **type** of hello dataset too**OracleTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-1286">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1286">Property</span></span> | <span data-ttu-id="d6179-1287">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1287">Description</span></span> | <span data-ttu-id="d6179-1288">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="d6179-1289">tableName</span></span> |<span data-ttu-id="d6179-1290">Oznacza nazwę tabeli hello na powitania hello połączonej usługi bazy danych programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="d6179-1290">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="d6179-1291">Nie (Jeśli **oracleReaderQuery** z **OracleSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1292">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1292">Example</span></span>

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
<span data-ttu-id="d6179-1293">Aby uzyskać więcej informacji, zobacz [łącznika Oracle](data-factory-onprem-oracle-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="d6179-1294">Oracle źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1295">Jeśli dane są kopiowane z bazy danych Oracle, ustaw hello **typ źródła** hello skopiować działania zbyt**OracleSource**i określ następujące właściwości w hello **źródła** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-1295">If you are copying data from an Oracle database, set hello **source type** of hello copy activity too**OracleSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-1296">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1296">Property</span></span> | <span data-ttu-id="d6179-1297">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1297">Description</span></span> | <span data-ttu-id="d6179-1298">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1298">Allowed values</span></span> | <span data-ttu-id="d6179-1299">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="d6179-1300">oracleReaderQuery</span></span> |<span data-ttu-id="d6179-1301">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1301">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-1302">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-1302">SQL query string.</span></span> <span data-ttu-id="d6179-1303">Na przykład: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="d6179-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="d6179-1304">Jeśli nie zostanie określony, hello instrukcji SQL, która jest wykonywana:`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="d6179-1304">If not specified, hello SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="d6179-1305">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1306">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1306">Example</span></span>

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

<span data-ttu-id="d6179-1307">Aby uzyskać więcej informacji, zobacz [łącznika Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="d6179-1308">Obiekt Sink Oracle w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="d6179-1309">Kopiowania bazy danych Oracle tooam danych, ustaw hello **typu sink** hello skopiować działania zbyt**OracleSink**i określ następujące właściwości w hello **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1309">If you are copying data tooam Oracle database, set hello **sink type** of hello copy activity too**OracleSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="d6179-1310">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1310">Property</span></span> | <span data-ttu-id="d6179-1311">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1311">Description</span></span> | <span data-ttu-id="d6179-1312">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1312">Allowed values</span></span> | <span data-ttu-id="d6179-1313">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="d6179-1314">writeBatchTimeout</span></span> |<span data-ttu-id="d6179-1315">Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1315">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="d6179-1316">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="d6179-1316">timespan</span></span><br/><br/> <span data-ttu-id="d6179-1317">Przykład: 00:30:00 (30 minut).</span><span class="sxs-lookup"><span data-stu-id="d6179-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="d6179-1318">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1318">No</span></span> |
| <span data-ttu-id="d6179-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d6179-1319">writeBatchSize</span></span> |<span data-ttu-id="d6179-1320">Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="d6179-1320">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="d6179-1321">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="d6179-1321">Integer (number of rows)</span></span> |<span data-ttu-id="d6179-1322">Nie (domyślne: 100)</span><span class="sxs-lookup"><span data-stu-id="d6179-1322">No (default: 100)</span></span> |
| <span data-ttu-id="d6179-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="d6179-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="d6179-1324">Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="d6179-1324">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="d6179-1325">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="d6179-1325">A query statement.</span></span> |<span data-ttu-id="d6179-1326">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1326">No</span></span> |
| <span data-ttu-id="d6179-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="d6179-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="d6179-1328">Określ nazwę kolumny toofill działanie kopiowania identyfikatorem wycinek automatycznie generowane, która jest używana tooclean zapasowych określonych wycinek czas ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="d6179-1328">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="d6179-1329">Nazwa kolumny kolumnę o typie danych binary(32).</span><span class="sxs-lookup"><span data-stu-id="d6179-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="d6179-1330">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1331">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1331">Example</span></span>
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
<span data-ttu-id="d6179-1332">Aby uzyskać więcej informacji, zobacz [łącznika Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="d6179-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d6179-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-1334">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1334">Linked service</span></span>
<span data-ttu-id="d6179-1335">toodefine PostgreSQL połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesPostgreSql**i określ następujące właściwości w hello **typeProperties**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1335">toodefine a PostgreSQL linked service, set hello **type** of hello linked service too**OnPremisesPostgreSql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-1336">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1336">Property</span></span> | <span data-ttu-id="d6179-1337">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1337">Description</span></span> | <span data-ttu-id="d6179-1338">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1339">serwer</span><span class="sxs-lookup"><span data-stu-id="d6179-1339">server</span></span> |<span data-ttu-id="d6179-1340">Nazwa serwera PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1340">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="d6179-1341">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1341">Yes</span></span> |
| <span data-ttu-id="d6179-1342">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1342">database</span></span> |<span data-ttu-id="d6179-1343">Nazwa bazy danych PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1343">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="d6179-1344">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1344">Yes</span></span> |
| <span data-ttu-id="d6179-1345">Schemat</span><span class="sxs-lookup"><span data-stu-id="d6179-1345">schema</span></span> |<span data-ttu-id="d6179-1346">Nazwa schematu hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1346">Name of hello schema in hello database.</span></span> <span data-ttu-id="d6179-1347">Nazwa schematu Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-1347">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="d6179-1348">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1348">No</span></span> |
| <span data-ttu-id="d6179-1349">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-1349">authenticationType</span></span> |<span data-ttu-id="d6179-1350">Typ uwierzytelniania używany tooconnect toohello PostgreSQL w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1350">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="d6179-1351">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="d6179-1352">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1352">Yes</span></span> |
| <span data-ttu-id="d6179-1353">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-1353">username</span></span> |<span data-ttu-id="d6179-1354">Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="d6179-1355">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1355">No</span></span> |
| <span data-ttu-id="d6179-1356">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-1356">password</span></span> |<span data-ttu-id="d6179-1357">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d6179-1357">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="d6179-1358">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1358">No</span></span> |
| <span data-ttu-id="d6179-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-1359">gatewayName</span></span> |<span data-ttu-id="d6179-1360">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-1360">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="d6179-1361">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1362">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1362">Example</span></span>

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
<span data-ttu-id="d6179-1363">Aby uzyskać więcej informacji, zobacz [łącznik PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="d6179-1364">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1364">Dataset</span></span>
<span data-ttu-id="d6179-1365">toodefine PostgreSQL zestawu danych, ustaw hello **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1365">toodefine a PostgreSQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-1366">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1366">Property</span></span> | <span data-ttu-id="d6179-1367">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1367">Description</span></span> | <span data-ttu-id="d6179-1368">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="d6179-1369">tableName</span></span> |<span data-ttu-id="d6179-1370">Nazwa tabeli hello w hello wystąpienie bazy danych PostgreSQL, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="d6179-1370">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="d6179-1371">Witaj tableName jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-1371">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="d6179-1372">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1373">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1373">Example</span></span>
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
<span data-ttu-id="d6179-1374">Aby uzyskać więcej informacji, zobacz [łącznik PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="d6179-1375">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1376">Jeśli dane są kopiowane z bazy danych programu PostgreSQL, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1376">If you are copying data from a PostgreSQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="d6179-1377">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1377">Property</span></span> | <span data-ttu-id="d6179-1378">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1378">Description</span></span> | <span data-ttu-id="d6179-1379">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1379">Allowed values</span></span> | <span data-ttu-id="d6179-1380">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1381">query</span><span class="sxs-lookup"><span data-stu-id="d6179-1381">query</span></span> |<span data-ttu-id="d6179-1382">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1382">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-1383">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-1383">SQL query string.</span></span> <span data-ttu-id="d6179-1384">Na przykład: "zapytania": "Wybierz * z \"MySchema\".\" MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="d6179-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="d6179-1385">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1386">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1386">Example</span></span>

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

<span data-ttu-id="d6179-1387">Aby uzyskać więcej informacji, zobacz [łącznik PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="d6179-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="d6179-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="d6179-1389">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1389">Linked service</span></span>
<span data-ttu-id="d6179-1390">toodefine SAP Business magazynu (BW) połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**SapBw**i określ następujące właściwości w hello **typeProperties**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1390">toodefine a SAP Business Warehouse (BW) linked service, set hello **type** of hello linked service too**SapBw**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="d6179-1391">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1391">Property</span></span> | <span data-ttu-id="d6179-1392">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1392">Description</span></span> | <span data-ttu-id="d6179-1393">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1393">Allowed values</span></span> | <span data-ttu-id="d6179-1394">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="d6179-1395">serwer</span><span class="sxs-lookup"><span data-stu-id="d6179-1395">server</span></span> | <span data-ttu-id="d6179-1396">Nazwa serwera hello, na które hello programu SAP BW znajduje się wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="d6179-1396">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="d6179-1397">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1397">string</span></span> | <span data-ttu-id="d6179-1398">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1398">Yes</span></span>
<span data-ttu-id="d6179-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="d6179-1399">systemNumber</span></span> | <span data-ttu-id="d6179-1400">Numer systemu hello systemu SAP BW.</span><span class="sxs-lookup"><span data-stu-id="d6179-1400">System number of hello SAP BW system.</span></span> | <span data-ttu-id="d6179-1401">Liczba dziesiętna dwucyfrowe reprezentowany jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="d6179-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="d6179-1402">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1402">Yes</span></span>
<span data-ttu-id="d6179-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="d6179-1403">clientId</span></span> | <span data-ttu-id="d6179-1404">Identyfikator klienta na powitania klienta w hello systemu SAP W.</span><span class="sxs-lookup"><span data-stu-id="d6179-1404">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="d6179-1405">Trzycyfrowa liczba dziesiętna reprezentowany jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="d6179-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="d6179-1406">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1406">Yes</span></span>
<span data-ttu-id="d6179-1407">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-1407">username</span></span> | <span data-ttu-id="d6179-1408">Nazwa użytkownika hello, kto ma dostęp toohello SAP serwera</span><span class="sxs-lookup"><span data-stu-id="d6179-1408">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="d6179-1409">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1409">string</span></span> | <span data-ttu-id="d6179-1410">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1410">Yes</span></span>
<span data-ttu-id="d6179-1411">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-1411">password</span></span> | <span data-ttu-id="d6179-1412">Hasło dla użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1412">Password for hello user.</span></span> | <span data-ttu-id="d6179-1413">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1413">string</span></span> | <span data-ttu-id="d6179-1414">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1414">Yes</span></span>
<span data-ttu-id="d6179-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-1415">gatewayName</span></span> | <span data-ttu-id="d6179-1416">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalnego programu SAP BW wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="d6179-1416">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="d6179-1417">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1417">string</span></span> | <span data-ttu-id="d6179-1418">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1418">Yes</span></span>
<span data-ttu-id="d6179-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d6179-1419">encryptedCredential</span></span> | <span data-ttu-id="d6179-1420">Witaj zaszyfrowanego ciągu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="d6179-1420">hello encrypted credential string.</span></span> | <span data-ttu-id="d6179-1421">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1421">string</span></span> | <span data-ttu-id="d6179-1422">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="d6179-1423">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1423">Example</span></span>

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

<span data-ttu-id="d6179-1424">Aby uzyskać więcej informacji, zobacz [łącznika SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-1425">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1425">Dataset</span></span>
<span data-ttu-id="d6179-1426">toodefine programu SAP BW zestawu danych, ustaw hello **typu** hello DataSet za**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1426">toodefine a SAP BW dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="d6179-1427">Nie ma żadnych właściwości specyficzne dla typu obsługiwane dla zestawu danych z programu SAP BW hello typu **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1427">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="d6179-1428">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1428">Example</span></span>

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
<span data-ttu-id="d6179-1429">Aby uzyskać więcej informacji, zobacz [łącznika SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="d6179-1430">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1431">Jeśli dane są kopiowane z SAP Business Warehouse, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1431">If you are copying data from SAP Business Warehouse, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="d6179-1432">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1432">Property</span></span> | <span data-ttu-id="d6179-1433">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1433">Description</span></span> | <span data-ttu-id="d6179-1434">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1434">Allowed values</span></span> | <span data-ttu-id="d6179-1435">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1436">query</span><span class="sxs-lookup"><span data-stu-id="d6179-1436">query</span></span> | <span data-ttu-id="d6179-1437">Określa dane tooread zapytania MDX hello z wystąpienia programu SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1437">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="d6179-1438">Zapytania MDX.</span><span class="sxs-lookup"><span data-stu-id="d6179-1438">MDX query.</span></span> | <span data-ttu-id="d6179-1439">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1440">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1440">Example</span></span>

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

<span data-ttu-id="d6179-1441">Aby uzyskać więcej informacji, zobacz [łącznika SAP Business Warehouse](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="d6179-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="d6179-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-1443">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1443">Linked service</span></span>
<span data-ttu-id="d6179-1444">toodefine SAP HANA połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**SapHana**i określ następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1444">toodefine a SAP HANA linked service, set hello **type** of hello linked service too**SapHana**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="d6179-1445">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1445">Property</span></span> | <span data-ttu-id="d6179-1446">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1446">Description</span></span> | <span data-ttu-id="d6179-1447">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1447">Allowed values</span></span> | <span data-ttu-id="d6179-1448">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="d6179-1449">serwer</span><span class="sxs-lookup"><span data-stu-id="d6179-1449">server</span></span> | <span data-ttu-id="d6179-1450">Nazwa serwera hello, na które hello SAP HANA znajduje się wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="d6179-1450">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="d6179-1451">Jeśli serwer używa portu dostosowane, określ `server:port`.</span><span class="sxs-lookup"><span data-stu-id="d6179-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="d6179-1452">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1452">string</span></span> | <span data-ttu-id="d6179-1453">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1453">Yes</span></span>
<span data-ttu-id="d6179-1454">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-1454">authenticationType</span></span> | <span data-ttu-id="d6179-1455">Typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="d6179-1455">Type of authentication.</span></span> | <span data-ttu-id="d6179-1456">Ciąg.</span><span class="sxs-lookup"><span data-stu-id="d6179-1456">string.</span></span> <span data-ttu-id="d6179-1457">"Basic" lub "Windows"</span><span class="sxs-lookup"><span data-stu-id="d6179-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="d6179-1458">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1458">Yes</span></span> 
<span data-ttu-id="d6179-1459">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-1459">username</span></span> | <span data-ttu-id="d6179-1460">Nazwa użytkownika hello, kto ma dostęp toohello SAP serwera</span><span class="sxs-lookup"><span data-stu-id="d6179-1460">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="d6179-1461">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1461">string</span></span> | <span data-ttu-id="d6179-1462">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1462">Yes</span></span>
<span data-ttu-id="d6179-1463">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-1463">password</span></span> | <span data-ttu-id="d6179-1464">Hasło dla użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1464">Password for hello user.</span></span> | <span data-ttu-id="d6179-1465">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1465">string</span></span> | <span data-ttu-id="d6179-1466">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1466">Yes</span></span>
<span data-ttu-id="d6179-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-1467">gatewayName</span></span> | <span data-ttu-id="d6179-1468">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalnego SAP HANA wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="d6179-1468">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="d6179-1469">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1469">string</span></span> | <span data-ttu-id="d6179-1470">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1470">Yes</span></span>
<span data-ttu-id="d6179-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d6179-1471">encryptedCredential</span></span> | <span data-ttu-id="d6179-1472">Witaj zaszyfrowanego ciągu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="d6179-1472">hello encrypted credential string.</span></span> | <span data-ttu-id="d6179-1473">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1473">string</span></span> | <span data-ttu-id="d6179-1474">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="d6179-1475">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1475">Example</span></span>

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
<span data-ttu-id="d6179-1476">Aby uzyskać więcej informacji, zobacz [łącznika SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="d6179-1477">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1477">Dataset</span></span>
<span data-ttu-id="d6179-1478">toodefine zestawu danych SAP HANA, zestaw hello **typu** hello DataSet za**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1478">toodefine a SAP HANA dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="d6179-1479">Nie ma żadnych właściwości specyficzne dla typu obsługiwane dla zestawu danych SAP HANA hello typu **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1479">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="d6179-1480">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1480">Example</span></span>

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
<span data-ttu-id="d6179-1481">Aby uzyskać więcej informacji, zobacz [łącznika SAP HANA](data-factory-sap-hana-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="d6179-1482">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1483">Jeśli dane są kopiowane z magazynu danych SAP HANA, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1483">If you are copying data from a SAP HANA data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-1484">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1484">Property</span></span> | <span data-ttu-id="d6179-1485">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1485">Description</span></span> | <span data-ttu-id="d6179-1486">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1486">Allowed values</span></span> | <span data-ttu-id="d6179-1487">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1488">query</span><span class="sxs-lookup"><span data-stu-id="d6179-1488">query</span></span> | <span data-ttu-id="d6179-1489">Określa hello SQL tooread dane z wystąpieniem SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1489">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="d6179-1490">Zapytanie SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-1490">SQL query.</span></span> | <span data-ttu-id="d6179-1491">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="d6179-1492">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1492">Example</span></span>


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

<span data-ttu-id="d6179-1493">Aby uzyskać więcej informacji, zobacz [łącznika SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="d6179-1494">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="d6179-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-1495">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1495">Linked service</span></span>
<span data-ttu-id="d6179-1496">Tworzenie połączonej usługi typu **OnPremisesSqlServer** toolink fabrykę danych tooa bazy danych programu SQL Server lokalne.</span><span class="sxs-lookup"><span data-stu-id="d6179-1496">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="d6179-1497">Hello w poniższej tabeli przedstawiono opis dla usługi programu SQL Server połączone określonych lokalnych tooon elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="d6179-1497">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="d6179-1498">Witaj w poniższej tabeli przedstawiono opis dla określonych tooSQL elementów JSON usługi Serwer połączony.</span><span class="sxs-lookup"><span data-stu-id="d6179-1498">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="d6179-1499">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1499">Property</span></span> | <span data-ttu-id="d6179-1500">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1500">Description</span></span> | <span data-ttu-id="d6179-1501">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1502">type</span><span class="sxs-lookup"><span data-stu-id="d6179-1502">type</span></span> |<span data-ttu-id="d6179-1503">powinien mieć ustawioną właściwość type Hello: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1503">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="d6179-1504">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1504">Yes</span></span> |
| <span data-ttu-id="d6179-1505">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="d6179-1505">connectionString</span></span> |<span data-ttu-id="d6179-1506">Określ informacje connectionString potrzebne tooconnect toohello lokalnej bazy danych SQL Server przy użyciu uwierzytelniania SQL lub uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-1506">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="d6179-1507">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1507">Yes</span></span> |
| <span data-ttu-id="d6179-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-1508">gatewayName</span></span> |<span data-ttu-id="d6179-1509">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d6179-1509">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="d6179-1510">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1510">Yes</span></span> |
| <span data-ttu-id="d6179-1511">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-1511">username</span></span> |<span data-ttu-id="d6179-1512">Określ nazwę użytkownika, jeśli używasz uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="d6179-1513">Przykład: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="d6179-1514">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1514">No</span></span> |
| <span data-ttu-id="d6179-1515">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-1515">password</span></span> |<span data-ttu-id="d6179-1516">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d6179-1516">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="d6179-1517">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1517">No</span></span> |

<span data-ttu-id="d6179-1518">Można szyfrować poświadczeń przy użyciu hello **AzureRmDataFactoryEncryptValue nowy** polecenia cmdlet i używać ich w parametrach połączenia hello, jak pokazano w hello poniższy przykład (**EncryptedCredential** właściwość):</span><span class="sxs-lookup"><span data-stu-id="d6179-1518">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="d6179-1519">Przykład: JSON dla przy użyciu uwierzytelniania programu SQL</span><span class="sxs-lookup"><span data-stu-id="d6179-1519">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="d6179-1520">Przykład: JSON dla przy użyciu uwierzytelniania systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d6179-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="d6179-1521">Jeśli podano nazwę użytkownika i hasło, brama używa ich tooimpersonate hello określonego tooconnect toohello lokalnego programu SQL Server bazy danych kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d6179-1521">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="d6179-1522">W przeciwnym razie nawiązanie połączenia bramy toohello programu SQL Server bezpośrednio z kontekstu zabezpieczeń hello bramy (jego konta uruchamiania).</span><span class="sxs-lookup"><span data-stu-id="d6179-1522">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="d6179-1523">Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-1524">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1524">Dataset</span></span>
<span data-ttu-id="d6179-1525">toodefine zestawu danych programu SQL Server, zestaw hello **typu** hello DataSet za**SqlServerTable**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1525">toodefine a SQL Server dataset, set hello **type** of hello dataset too**SqlServerTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-1526">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1526">Property</span></span> | <span data-ttu-id="d6179-1527">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1527">Description</span></span> | <span data-ttu-id="d6179-1528">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="d6179-1529">tableName</span></span> |<span data-ttu-id="d6179-1530">Nazwa hello tabeli lub widoku w wystąpieniu bazy danych SQL Server hello, która jest połączona usługa odnosi się do.</span><span class="sxs-lookup"><span data-stu-id="d6179-1530">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="d6179-1531">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1532">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1532">Example</span></span>
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

<span data-ttu-id="d6179-1533">Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="d6179-1534">Źródło SQL w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1535">Jeśli dane są kopiowane z bazy danych programu SQL Server, należy ustawić hello **typ źródła** hello skopiować działania zbyt**SqlSource**i określ następujące właściwości w hello **źródła** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-1535">If you are copying data from a SQL Server database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="d6179-1536">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1536">Property</span></span> | <span data-ttu-id="d6179-1537">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1537">Description</span></span> | <span data-ttu-id="d6179-1538">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1538">Allowed values</span></span> | <span data-ttu-id="d6179-1539">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1540">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="d6179-1540">sqlReaderQuery</span></span> |<span data-ttu-id="d6179-1541">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1541">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-1542">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-1542">SQL query string.</span></span> <span data-ttu-id="d6179-1543">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="d6179-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="d6179-1544">Może odwoływać się wiele tabel z bazy danych hello odwołuje się hello wejściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1544">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="d6179-1545">Jeśli nie zostanie określony, hello instrukcji SQL, która jest wykonywana: Wybierz z MyTable.</span><span class="sxs-lookup"><span data-stu-id="d6179-1545">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="d6179-1546">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1546">No</span></span> |
| <span data-ttu-id="d6179-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="d6179-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="d6179-1548">Nazwa hello przechowywane procedury, która odczytuje dane z hello tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="d6179-1548">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="d6179-1549">Nazwa hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-1549">Name of hello stored procedure.</span></span> |<span data-ttu-id="d6179-1550">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1550">No</span></span> |
| <span data-ttu-id="d6179-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="d6179-1551">storedProcedureParameters</span></span> |<span data-ttu-id="d6179-1552">Parametry hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-1552">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="d6179-1553">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="d6179-1553">Name/value pairs.</span></span> <span data-ttu-id="d6179-1554">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-1554">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="d6179-1555">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1555">No</span></span> |

<span data-ttu-id="d6179-1556">Jeśli hello **sqlReaderQuery** określono hello SqlSource, hello odbywa się działanie kopii tego zapytania hello bazy danych SQL Server źródła tooget hello danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1556">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="d6179-1557">Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="d6179-1557">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="d6179-1558">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello są używane toobuild toorun zapytania select, przed hello bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d6179-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="d6179-1559">Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1559">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="d6179-1560">Jeśli używasz **sqlReaderStoredProcedureName**, należy nadal toospecify wartość dla hello **tableName** właściwości w elemencie dataset hello JSON.</span><span class="sxs-lookup"><span data-stu-id="d6179-1560">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="d6179-1561">Nie ma żadnych operacji sprawdzania poprawności, jednak wykonywać na tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="d6179-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="d6179-1562">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1562">Example</span></span>
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

<span data-ttu-id="d6179-1563">W tym przykładzie **sqlReaderQuery** dla hello SqlSource został określony.</span><span class="sxs-lookup"><span data-stu-id="d6179-1563">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="d6179-1564">Działanie kopiowania Hello jest uruchamiana to zapytanie dla hello danych hello tooget źródła danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d6179-1564">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="d6179-1565">Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="d6179-1565">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="d6179-1566">Hello sqlReaderQuery można odwoływać się wiele tabel w bazie danych hello odwołuje się hello wejściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1566">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="d6179-1567">Nie jest tabelą hello ograniczone tooonly ustawione jako hello typeProperty tableName zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1567">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="d6179-1568">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello są używane toobuild toorun zapytania select, przed hello bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d6179-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="d6179-1569">Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1569">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="d6179-1570">Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="d6179-1571">Obiekt Sink SQL w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="d6179-1572">Kopiowania bazy danych programu SQL Server tooa danych, ustaw hello **typu sink** hello skopiować działania zbyt**SqlSink**i określ następujące właściwości w hello **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1572">If you are copying data tooa SQL Server database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="d6179-1573">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1573">Property</span></span> | <span data-ttu-id="d6179-1574">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1574">Description</span></span> | <span data-ttu-id="d6179-1575">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1575">Allowed values</span></span> | <span data-ttu-id="d6179-1576">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="d6179-1577">writeBatchTimeout</span></span> |<span data-ttu-id="d6179-1578">Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1578">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="d6179-1579">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="d6179-1579">timespan</span></span><br/><br/> <span data-ttu-id="d6179-1580">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="d6179-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="d6179-1581">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1581">No</span></span> |
| <span data-ttu-id="d6179-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d6179-1582">writeBatchSize</span></span> |<span data-ttu-id="d6179-1583">Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="d6179-1583">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="d6179-1584">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="d6179-1584">Integer (number of rows)</span></span> |<span data-ttu-id="d6179-1585">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="d6179-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="d6179-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="d6179-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="d6179-1587">Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="d6179-1587">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="d6179-1588">Aby uzyskać więcej informacji, zobacz [powtarzalności](#repeatability-during-copy) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6179-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="d6179-1589">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="d6179-1589">A query statement.</span></span> |<span data-ttu-id="d6179-1590">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1590">No</span></span> |
| <span data-ttu-id="d6179-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="d6179-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="d6179-1592">Określ nazwę kolumny toofill działanie kopiowania identyfikatorem wycinek automatycznie generowane, która jest używana tooclean zapasowych określonych wycinek czas ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="d6179-1592">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="d6179-1593">Aby uzyskać więcej informacji, zobacz [powtarzalności](#repeatability-during-copy) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6179-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="d6179-1594">Nazwa kolumny kolumnę o typie danych binary(32).</span><span class="sxs-lookup"><span data-stu-id="d6179-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="d6179-1595">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1595">No</span></span> |
| <span data-ttu-id="d6179-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="d6179-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="d6179-1597">Nazwa hello procedury składowanej danych upserts (aktualizacje/INSERT) do tabeli docelowej hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1597">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="d6179-1598">Nazwa hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-1598">Name of hello stored procedure.</span></span> |<span data-ttu-id="d6179-1599">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1599">No</span></span> |
| <span data-ttu-id="d6179-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="d6179-1600">storedProcedureParameters</span></span> |<span data-ttu-id="d6179-1601">Parametry hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-1601">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="d6179-1602">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="d6179-1602">Name/value pairs.</span></span> <span data-ttu-id="d6179-1603">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-1603">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="d6179-1604">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1604">No</span></span> |
| <span data-ttu-id="d6179-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="d6179-1605">sqlWriterTableType</span></span> |<span data-ttu-id="d6179-1606">Określ toobe nazwy typu tabeli używany w procedurze hello przechowywane.</span><span class="sxs-lookup"><span data-stu-id="d6179-1606">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="d6179-1607">Działanie kopiowania udostępnia dane hello przenoszone w tabeli tymczasowej o tym typie tabeli.</span><span class="sxs-lookup"><span data-stu-id="d6179-1607">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="d6179-1608">Procedura składowana kod następnie można scalać dane hello kopiowane z istniejącymi danymi.</span><span class="sxs-lookup"><span data-stu-id="d6179-1608">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="d6179-1609">Nazwa typu tabeli.</span><span class="sxs-lookup"><span data-stu-id="d6179-1609">A table type name.</span></span> |<span data-ttu-id="d6179-1610">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1611">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1611">Example</span></span>
<span data-ttu-id="d6179-1612">potok Hello zawiera działanie kopiowania który jest skonfigurowany toouse te zestawy danych wejściowych i wyjściowych i toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="d6179-1612">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d6179-1613">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i **zbiornika** typu ustawiono zbyt**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1613">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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

<span data-ttu-id="d6179-1614">Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="d6179-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="d6179-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-1616">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1616">Linked service</span></span>
<span data-ttu-id="d6179-1617">toodefine Sybase połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesSybase**i określ następujące właściwości w hello **typeProperties** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-1617">toodefine a Sybase linked service, set hello **type** of hello linked service too**OnPremisesSybase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-1618">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1618">Property</span></span> | <span data-ttu-id="d6179-1619">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1619">Description</span></span> | <span data-ttu-id="d6179-1620">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1621">serwer</span><span class="sxs-lookup"><span data-stu-id="d6179-1621">server</span></span> |<span data-ttu-id="d6179-1622">Nazwa serwera programu Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1622">Name of hello Sybase server.</span></span> |<span data-ttu-id="d6179-1623">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1623">Yes</span></span> |
| <span data-ttu-id="d6179-1624">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1624">database</span></span> |<span data-ttu-id="d6179-1625">Nazwa bazy danych programu Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1625">Name of hello Sybase database.</span></span> |<span data-ttu-id="d6179-1626">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1626">Yes</span></span> |
| <span data-ttu-id="d6179-1627">Schemat</span><span class="sxs-lookup"><span data-stu-id="d6179-1627">schema</span></span> |<span data-ttu-id="d6179-1628">Nazwa schematu hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1628">Name of hello schema in hello database.</span></span> |<span data-ttu-id="d6179-1629">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1629">No</span></span> |
| <span data-ttu-id="d6179-1630">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-1630">authenticationType</span></span> |<span data-ttu-id="d6179-1631">Typ uwierzytelniania używany toohello tooconnect baz danych programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="d6179-1631">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="d6179-1632">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="d6179-1633">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1633">Yes</span></span> |
| <span data-ttu-id="d6179-1634">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-1634">username</span></span> |<span data-ttu-id="d6179-1635">Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="d6179-1636">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1636">No</span></span> |
| <span data-ttu-id="d6179-1637">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-1637">password</span></span> |<span data-ttu-id="d6179-1638">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d6179-1638">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="d6179-1639">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1639">No</span></span> |
| <span data-ttu-id="d6179-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-1640">gatewayName</span></span> |<span data-ttu-id="d6179-1641">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych programu Sybase.</span><span class="sxs-lookup"><span data-stu-id="d6179-1641">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="d6179-1642">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1643">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1643">Example</span></span>
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

<span data-ttu-id="d6179-1644">Aby uzyskać więcej informacji, zobacz [łącznika programu Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-1645">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1645">Dataset</span></span>
<span data-ttu-id="d6179-1646">toodefine zestawu danych programu Sybase, zestaw hello **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1646">toodefine a Sybase dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-1647">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1647">Property</span></span> | <span data-ttu-id="d6179-1648">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1648">Description</span></span> | <span data-ttu-id="d6179-1649">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="d6179-1650">tableName</span></span> |<span data-ttu-id="d6179-1651">Nazwa tabeli hello w hello wystąpienie bazy danych programu Sybase, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="d6179-1651">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="d6179-1652">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1653">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1653">Example</span></span>

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

<span data-ttu-id="d6179-1654">Aby uzyskać więcej informacji, zobacz [łącznika programu Sybase](data-factory-onprem-sybase-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="d6179-1655">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1656">Jeśli dane są kopiowane z bazy danych programu Sybase, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-1656">If you are copying data from a Sybase database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="d6179-1657">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1657">Property</span></span> | <span data-ttu-id="d6179-1658">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1658">Description</span></span> | <span data-ttu-id="d6179-1659">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1659">Allowed values</span></span> | <span data-ttu-id="d6179-1660">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1661">query</span><span class="sxs-lookup"><span data-stu-id="d6179-1661">query</span></span> |<span data-ttu-id="d6179-1662">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1662">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-1663">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-1663">SQL query string.</span></span> <span data-ttu-id="d6179-1664">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="d6179-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="d6179-1665">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1666">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1666">Example</span></span>

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

<span data-ttu-id="d6179-1667">Aby uzyskać więcej informacji, zobacz [łącznika programu Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="d6179-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="d6179-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-1669">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1669">Linked service</span></span>
<span data-ttu-id="d6179-1670">toodefine Teradata połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesTeradata**i określ następujące właściwości w hello **typeProperties** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-1670">toodefine a Teradata linked service, set hello **type** of hello linked service too**OnPremisesTeradata**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-1671">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1671">Property</span></span> | <span data-ttu-id="d6179-1672">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1672">Description</span></span> | <span data-ttu-id="d6179-1673">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1674">serwer</span><span class="sxs-lookup"><span data-stu-id="d6179-1674">server</span></span> |<span data-ttu-id="d6179-1675">Nazwa serwera programu Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1675">Name of hello Teradata server.</span></span> |<span data-ttu-id="d6179-1676">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1676">Yes</span></span> |
| <span data-ttu-id="d6179-1677">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-1677">authenticationType</span></span> |<span data-ttu-id="d6179-1678">Typ uwierzytelniania używany toohello tooconnect bazą danych programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="d6179-1678">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="d6179-1679">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="d6179-1680">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1680">Yes</span></span> |
| <span data-ttu-id="d6179-1681">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-1681">username</span></span> |<span data-ttu-id="d6179-1682">Określ nazwę użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="d6179-1683">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1683">No</span></span> |
| <span data-ttu-id="d6179-1684">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-1684">password</span></span> |<span data-ttu-id="d6179-1685">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d6179-1685">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="d6179-1686">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1686">No</span></span> |
| <span data-ttu-id="d6179-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-1687">gatewayName</span></span> |<span data-ttu-id="d6179-1688">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych programu Teradata.</span><span class="sxs-lookup"><span data-stu-id="d6179-1688">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="d6179-1689">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1690">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1690">Example</span></span>
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

<span data-ttu-id="d6179-1691">Aby uzyskać więcej informacji, zobacz [łącznika programu Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="d6179-1692">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1692">Dataset</span></span>
<span data-ttu-id="d6179-1693">toodefine zestawu danych obiektów Teradata Blob, zestaw hello **typu** hello DataSet za**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1693">toodefine a Teradata Blob dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="d6179-1694">Obecnie nie ma żadnych właściwości typu, obsługiwane dla zestawu danych programu Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1694">Currently, there are no type properties supported for hello Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="d6179-1695">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1695">Example</span></span>
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

<span data-ttu-id="d6179-1696">Aby uzyskać więcej informacji, zobacz [łącznika programu Teradata](data-factory-onprem-teradata-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="d6179-1697">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1698">Jeśli dane są kopiowane z bazy danych programu Teradata, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1698">If you are copying data from a Teradata database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-1699">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1699">Property</span></span> | <span data-ttu-id="d6179-1700">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1700">Description</span></span> | <span data-ttu-id="d6179-1701">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1701">Allowed values</span></span> | <span data-ttu-id="d6179-1702">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1703">query</span><span class="sxs-lookup"><span data-stu-id="d6179-1703">query</span></span> |<span data-ttu-id="d6179-1704">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1704">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-1705">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-1705">SQL query string.</span></span> <span data-ttu-id="d6179-1706">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="d6179-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="d6179-1707">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1708">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1708">Example</span></span>

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

<span data-ttu-id="d6179-1709">Aby uzyskać więcej informacji, zobacz [łącznika programu Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="d6179-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="d6179-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="d6179-1711">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1711">Linked service</span></span>
<span data-ttu-id="d6179-1712">toodefine Cassandra połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesCassandra**i określ następujące właściwości w hello **typeProperties** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-1712">toodefine a Cassandra linked service, set hello **type** of hello linked service too**OnPremisesCassandra**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-1713">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1713">Property</span></span> | <span data-ttu-id="d6179-1714">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1714">Description</span></span> | <span data-ttu-id="d6179-1715">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1716">Host</span><span class="sxs-lookup"><span data-stu-id="d6179-1716">host</span></span> |<span data-ttu-id="d6179-1717">Jeden lub więcej adresów IP lub nazw hostów serwerów Cassandra.</span><span class="sxs-lookup"><span data-stu-id="d6179-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="d6179-1718">Określ rozdzielaną przecinkami listę adresów IP lub serwerów tooall tooconnect nazwy hosta jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="d6179-1718">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="d6179-1719">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1719">Yes</span></span> |
| <span data-ttu-id="d6179-1720">port</span><span class="sxs-lookup"><span data-stu-id="d6179-1720">port</span></span> |<span data-ttu-id="d6179-1721">Hello port TCP, którego hello Cassandra serwer używa toolisten dla połączeń klienta.</span><span class="sxs-lookup"><span data-stu-id="d6179-1721">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="d6179-1722">Nie, wartość domyślna: 9042</span><span class="sxs-lookup"><span data-stu-id="d6179-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="d6179-1723">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-1723">authenticationType</span></span> |<span data-ttu-id="d6179-1724">Podstawowa lub anonimowe</span><span class="sxs-lookup"><span data-stu-id="d6179-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="d6179-1725">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1725">Yes</span></span> |
| <span data-ttu-id="d6179-1726">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-1726">username</span></span> |<span data-ttu-id="d6179-1727">Określ nazwę użytkownika dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1727">Specify user name for hello user account.</span></span> |<span data-ttu-id="d6179-1728">Tak, jeśli authenticationType ustawiono tooBasic.</span><span class="sxs-lookup"><span data-stu-id="d6179-1728">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="d6179-1729">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-1729">password</span></span> |<span data-ttu-id="d6179-1730">Określ hasło dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1730">Specify password for hello user account.</span></span> |<span data-ttu-id="d6179-1731">Tak, jeśli authenticationType ustawiono tooBasic.</span><span class="sxs-lookup"><span data-stu-id="d6179-1731">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="d6179-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-1732">gatewayName</span></span> |<span data-ttu-id="d6179-1733">Nazwa Hello hello bramy, która jest używana tooconnect toohello lokalnymi Cassandra w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1733">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="d6179-1734">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1734">Yes</span></span> |
| <span data-ttu-id="d6179-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d6179-1735">encryptedCredential</span></span> |<span data-ttu-id="d6179-1736">Poświadczenie szyfrowane przez bramę hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1736">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="d6179-1737">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1738">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1738">Example</span></span>

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

<span data-ttu-id="d6179-1739">Aby uzyskać więcej informacji, zobacz [łącznik Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-1740">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1740">Dataset</span></span>
<span data-ttu-id="d6179-1741">toodefine Cassandra zestawu danych, ustaw hello **typu** hello DataSet za**CassandraTable**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1741">toodefine a Cassandra dataset, set hello **type** of hello dataset too**CassandraTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-1742">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1742">Property</span></span> | <span data-ttu-id="d6179-1743">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1743">Description</span></span> | <span data-ttu-id="d6179-1744">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1745">przestrzeni kluczy</span><span class="sxs-lookup"><span data-stu-id="d6179-1745">keyspace</span></span> |<span data-ttu-id="d6179-1746">Nazwa schematu bazy danych Cassandra lub hello przestrzeni kluczy.</span><span class="sxs-lookup"><span data-stu-id="d6179-1746">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="d6179-1747">Tak (Jeśli **zapytania** dla **CassandraSource** nie jest zdefiniowana).</span><span class="sxs-lookup"><span data-stu-id="d6179-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="d6179-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="d6179-1748">tableName</span></span> |<span data-ttu-id="d6179-1749">Nazwa tabeli hello Cassandra bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1749">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="d6179-1750">Tak (Jeśli **zapytania** dla **CassandraSource** nie jest zdefiniowana).</span><span class="sxs-lookup"><span data-stu-id="d6179-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1751">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1751">Example</span></span>

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

<span data-ttu-id="d6179-1752">Aby uzyskać więcej informacji, zobacz [łącznik Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="d6179-1753">Źródło Cassandra w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1754">Jeśli dane są kopiowane z Cassandra, ustaw hello **typ źródła** hello skopiować działania zbyt**CassandraSource**i określ następujące właściwości w hello **źródła** sekcji :</span><span class="sxs-lookup"><span data-stu-id="d6179-1754">If you are copying data from Cassandra, set hello **source type** of hello copy activity too**CassandraSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-1755">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1755">Property</span></span> | <span data-ttu-id="d6179-1756">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1756">Description</span></span> | <span data-ttu-id="d6179-1757">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1757">Allowed values</span></span> | <span data-ttu-id="d6179-1758">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1759">query</span><span class="sxs-lookup"><span data-stu-id="d6179-1759">query</span></span> |<span data-ttu-id="d6179-1760">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1760">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-1761">Zapytania SQL 92 lub CQL zapytania.</span><span class="sxs-lookup"><span data-stu-id="d6179-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="d6179-1762">Zobacz [odwołania CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="d6179-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="d6179-1763">Korzystając z zapytania SQL, określ **nazwa name.table przestrzeni kluczy** toorepresent hello tabelę, która ma tooquery.</span><span class="sxs-lookup"><span data-stu-id="d6179-1763">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="d6179-1764">Nie (jeśli są zdefiniowane tableName oraz przestrzeni kluczy w zestawie danych).</span><span class="sxs-lookup"><span data-stu-id="d6179-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="d6179-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="d6179-1765">consistencyLevel</span></span> |<span data-ttu-id="d6179-1766">poziomu spójności Hello Określa, ile replik musi odpowiadać żądanie odczytu tooa przed zwróceniem aplikacji klienckiej toohello danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1766">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="d6179-1767">Sprawdzanie Cassandra hello określonej liczby replik dla żądania odczytu hello toosatisfy danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1767">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="d6179-1768">JEDNĄ, DWIE, TRZY, KWORUM, WSZYSTKIE, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="d6179-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="d6179-1769">Zobacz [Konfigurowanie spójność danych](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d6179-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="d6179-1770">Nie.</span><span class="sxs-lookup"><span data-stu-id="d6179-1770">No.</span></span> <span data-ttu-id="d6179-1771">Domyślna wartość to jeden.</span><span class="sxs-lookup"><span data-stu-id="d6179-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1772">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
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

<span data-ttu-id="d6179-1773">Aby uzyskać więcej informacji, zobacz [łącznik Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="d6179-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="d6179-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-1775">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1775">Linked service</span></span>
<span data-ttu-id="d6179-1776">toodefine MongoDB połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesMongoDB**i określ następujące właściwości w hello **typeProperties** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-1776">toodefine a MongoDB linked service, set hello **type** of hello linked service too**OnPremisesMongoDB**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-1777">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1777">Property</span></span> | <span data-ttu-id="d6179-1778">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1778">Description</span></span> | <span data-ttu-id="d6179-1779">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1780">serwer</span><span class="sxs-lookup"><span data-stu-id="d6179-1780">server</span></span> |<span data-ttu-id="d6179-1781">Adres IP lub hosta nazwę serwera bazy danych MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1781">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="d6179-1782">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1782">Yes</span></span> |
| <span data-ttu-id="d6179-1783">port</span><span class="sxs-lookup"><span data-stu-id="d6179-1783">port</span></span> |<span data-ttu-id="d6179-1784">Port TCP, którego hello serwera bazy danych MongoDB używa toolisten dla połączeń klienta.</span><span class="sxs-lookup"><span data-stu-id="d6179-1784">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="d6179-1785">Opcjonalne, wartość domyślna: 27017</span><span class="sxs-lookup"><span data-stu-id="d6179-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="d6179-1786">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-1786">authenticationType</span></span> |<span data-ttu-id="d6179-1787">Podstawowy, lub anonimowe.</span><span class="sxs-lookup"><span data-stu-id="d6179-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="d6179-1788">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1788">Yes</span></span> |
| <span data-ttu-id="d6179-1789">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-1789">username</span></span> |<span data-ttu-id="d6179-1790">Tooaccess konta użytkownika bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d6179-1790">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="d6179-1791">Tak (jeśli jest używane uwierzytelnianie podstawowe).</span><span class="sxs-lookup"><span data-stu-id="d6179-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="d6179-1792">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-1792">password</span></span> |<span data-ttu-id="d6179-1793">Hasło dla użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1793">Password for hello user.</span></span> |<span data-ttu-id="d6179-1794">Tak (jeśli jest używane uwierzytelnianie podstawowe).</span><span class="sxs-lookup"><span data-stu-id="d6179-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="d6179-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="d6179-1795">authSource</span></span> |<span data-ttu-id="d6179-1796">Nazwa bazy danych MongoDB hello czy chcesz toouse toocheck swoje poświadczenia dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="d6179-1796">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="d6179-1797">Opcjonalnie (jeśli jest używane uwierzytelnianie podstawowe).</span><span class="sxs-lookup"><span data-stu-id="d6179-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="d6179-1798">domyślne: używa konta administratora hello i hello bazy danych określona za pomocą właściwości databaseName.</span><span class="sxs-lookup"><span data-stu-id="d6179-1798">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="d6179-1799">DatabaseName</span><span class="sxs-lookup"><span data-stu-id="d6179-1799">databaseName</span></span> |<span data-ttu-id="d6179-1800">Nazwa bazy danych MongoDB hello, które mają tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d6179-1800">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="d6179-1801">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1801">Yes</span></span> |
| <span data-ttu-id="d6179-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-1802">gatewayName</span></span> |<span data-ttu-id="d6179-1803">Nazwa bramy hello, który uzyskuje dostęp do magazynu danych hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1803">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="d6179-1804">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1804">Yes</span></span> |
| <span data-ttu-id="d6179-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d6179-1805">encryptedCredential</span></span> |<span data-ttu-id="d6179-1806">Poświadczenie szyfrowane przez bramę.</span><span class="sxs-lookup"><span data-stu-id="d6179-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="d6179-1807">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="d6179-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1808">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="d6179-1809">Aby uzyskać więcej informacji, zobacz [artykułu łącznika bazy danych MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="d6179-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="d6179-1810">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1810">Dataset</span></span>
<span data-ttu-id="d6179-1811">toodefine zestawu danych MongoDB, zestaw hello **typu** hello DataSet za**MongoDbCollection**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1811">toodefine a MongoDB dataset, set hello **type** of hello dataset too**MongoDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-1812">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1812">Property</span></span> | <span data-ttu-id="d6179-1813">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1813">Description</span></span> | <span data-ttu-id="d6179-1814">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1815">CollectionName</span><span class="sxs-lookup"><span data-stu-id="d6179-1815">collectionName</span></span> |<span data-ttu-id="d6179-1816">Nazwa kolekcji hello w bazie danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d6179-1816">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="d6179-1817">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1818">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1818">Example</span></span>

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

<span data-ttu-id="d6179-1819">Aby uzyskać więcej informacji, zobacz [artykułu łącznika bazy danych MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="d6179-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="d6179-1820">Źródłowej bazy danych MongoDB w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1821">Jeśli dane są kopiowane z bazy danych MongoDB, ustaw hello **typ źródła** hello skopiować działania zbyt**MongoDbSource**i określ następujące właściwości w hello **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1821">If you are copying data from MongoDB, set hello **source type** of hello copy activity too**MongoDbSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-1822">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1822">Property</span></span> | <span data-ttu-id="d6179-1823">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1823">Description</span></span> | <span data-ttu-id="d6179-1824">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1824">Allowed values</span></span> | <span data-ttu-id="d6179-1825">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1826">query</span><span class="sxs-lookup"><span data-stu-id="d6179-1826">query</span></span> |<span data-ttu-id="d6179-1827">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1827">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-1828">Ciąg zapytania SQL 92.</span><span class="sxs-lookup"><span data-stu-id="d6179-1828">SQL-92 query string.</span></span> <span data-ttu-id="d6179-1829">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="d6179-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="d6179-1830">Nie (Jeśli **collectionName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1831">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1831">Example</span></span>

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

<span data-ttu-id="d6179-1832">Aby uzyskać więcej informacji, zobacz [artykułu łącznika bazy danych MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="d6179-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="d6179-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="d6179-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="d6179-1834">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1834">Linked service</span></span>
<span data-ttu-id="d6179-1835">toodefine Amazon S3 połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AwsAccessKey**i określ następujące właściwości w hello **typeProperties** sekcji :</span><span class="sxs-lookup"><span data-stu-id="d6179-1835">toodefine an Amazon S3 linked service, set hello **type** of hello linked service too**AwsAccessKey**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-1836">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1836">Property</span></span> | <span data-ttu-id="d6179-1837">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1837">Description</span></span> | <span data-ttu-id="d6179-1838">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1838">Allowed values</span></span> | <span data-ttu-id="d6179-1839">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="d6179-1840">accessKeyID</span></span> |<span data-ttu-id="d6179-1841">Identyfikator klucza tajnego dostępu hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1841">ID of hello secret access key.</span></span> |<span data-ttu-id="d6179-1842">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1842">string</span></span> |<span data-ttu-id="d6179-1843">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1843">Yes</span></span> |
| <span data-ttu-id="d6179-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="d6179-1844">secretAccessKey</span></span> |<span data-ttu-id="d6179-1845">klucz tajny dostępu Hello samej siebie.</span><span class="sxs-lookup"><span data-stu-id="d6179-1845">hello secret access key itself.</span></span> |<span data-ttu-id="d6179-1846">Zaszyfrowanego ciągu tajny</span><span class="sxs-lookup"><span data-stu-id="d6179-1846">Encrypted secret string</span></span> |<span data-ttu-id="d6179-1847">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-1848">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1848">Example</span></span>
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

<span data-ttu-id="d6179-1849">Aby uzyskać więcej informacji, zobacz [Amazon S3 artykułu łącznika](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d6179-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="d6179-1850">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1850">Dataset</span></span>
<span data-ttu-id="d6179-1851">toodefine Amazon S3 zestawu danych, ustaw hello **typu** hello DataSet za**AmazonS3**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1851">toodefine an Amazon S3 dataset, set hello **type** of hello dataset too**AmazonS3**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-1852">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1852">Property</span></span> | <span data-ttu-id="d6179-1853">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1853">Description</span></span> | <span data-ttu-id="d6179-1854">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1854">Allowed values</span></span> | <span data-ttu-id="d6179-1855">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="d6179-1856">bucketName</span></span> |<span data-ttu-id="d6179-1857">Nazwa pakietu Hello S3.</span><span class="sxs-lookup"><span data-stu-id="d6179-1857">hello S3 bucket name.</span></span> |<span data-ttu-id="d6179-1858">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1858">String</span></span> |<span data-ttu-id="d6179-1859">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1859">Yes</span></span> |
| <span data-ttu-id="d6179-1860">key</span><span class="sxs-lookup"><span data-stu-id="d6179-1860">key</span></span> |<span data-ttu-id="d6179-1861">Klucz obiektu Hello S3.</span><span class="sxs-lookup"><span data-stu-id="d6179-1861">hello S3 object key.</span></span> |<span data-ttu-id="d6179-1862">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1862">String</span></span> |<span data-ttu-id="d6179-1863">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1863">No</span></span> |
| <span data-ttu-id="d6179-1864">Prefiks</span><span class="sxs-lookup"><span data-stu-id="d6179-1864">prefix</span></span> |<span data-ttu-id="d6179-1865">Prefiks hello S3 obiektu klucza.</span><span class="sxs-lookup"><span data-stu-id="d6179-1865">Prefix for hello S3 object key.</span></span> <span data-ttu-id="d6179-1866">Wybrano obiektów, w której klucze uruchomienia z tym prefiksem.</span><span class="sxs-lookup"><span data-stu-id="d6179-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="d6179-1867">Ma zastosowanie tylko wtedy, gdy klucz jest pusty.</span><span class="sxs-lookup"><span data-stu-id="d6179-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="d6179-1868">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1868">String</span></span> |<span data-ttu-id="d6179-1869">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1869">No</span></span> |
| <span data-ttu-id="d6179-1870">Wersja</span><span class="sxs-lookup"><span data-stu-id="d6179-1870">version</span></span> |<span data-ttu-id="d6179-1871">Wersja Hello obiektu S3, jeśli włączono S3 przechowywania wersji.</span><span class="sxs-lookup"><span data-stu-id="d6179-1871">hello version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="d6179-1872">Ciąg</span><span class="sxs-lookup"><span data-stu-id="d6179-1872">String</span></span> |<span data-ttu-id="d6179-1873">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1873">No</span></span> |
| <span data-ttu-id="d6179-1874">Format</span><span class="sxs-lookup"><span data-stu-id="d6179-1874">format</span></span> | <span data-ttu-id="d6179-1875">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1875">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d6179-1876">Zestaw hello **typu** właściwości w formacie tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d6179-1876">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d6179-1877">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="d6179-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d6179-1878">Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1878">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d6179-1879">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1879">No</span></span> | |
| <span data-ttu-id="d6179-1880">Kompresja</span><span class="sxs-lookup"><span data-stu-id="d6179-1880">compression</span></span> | <span data-ttu-id="d6179-1881">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1881">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d6179-1882">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="d6179-1883">Witaj obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1883">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d6179-1884">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d6179-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d6179-1885">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="d6179-1886">bucketName + klawisz Określa lokalizację hello obiektu hello S3, gdzie zasobnika jest hello nadrzędny kontener dla obiektów S3, a klucz hello pełną ścieżkę tooS3 obiektu.</span><span class="sxs-lookup"><span data-stu-id="d6179-1886">bucketName + key specifies hello location of hello S3 object where bucket is hello root container for S3 objects and key is hello full path tooS3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="d6179-1887">Przykład: Przykładowego zestawu danych z prefiksem</span><span class="sxs-lookup"><span data-stu-id="d6179-1887">Example: Sample dataset with prefix</span></span>

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
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="d6179-1888">Przykład: Zestaw danych przykładowych (wersją)</span><span class="sxs-lookup"><span data-stu-id="d6179-1888">Example: Sample data set (with version)</span></span>

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

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="d6179-1889">Przykład: Dynamiczne ścieżki S3</span><span class="sxs-lookup"><span data-stu-id="d6179-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="d6179-1890">W przykładowym hello używamy stałe wartości dla właściwości klucza i bucketName w zestawie danych hello Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="d6179-1890">In hello sample, we use fixed values for key and bucketName properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="d6179-1891">Program może obliczyć klucza hello i bucketName dynamicznie w czasie wykonywania za pomocą zmiennych systemowych, takich jak SliceStart fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1891">You can have Data Factory calculate hello key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="d6179-1892">Możesz zrobić hello takie same dla właściwości prefiks hello Amazon S3 zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1892">You can do hello same for hello prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="d6179-1893">Zobacz [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md) listę obsługiwanych funkcjach i zmiennych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="d6179-1894">Aby uzyskać więcej informacji, zobacz [Amazon S3 artykułu łącznika](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d6179-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="d6179-1895">Źródło systemu plików w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1896">Jeśli dane są kopiowane z Amazon S3, ustaw hello **typ źródła** hello skopiować działania zbyt**FileSystemSource**i określ następujące właściwości w hello **źródła** sekcji :</span><span class="sxs-lookup"><span data-stu-id="d6179-1896">If you are copying data from Amazon S3, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="d6179-1897">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1897">Property</span></span> | <span data-ttu-id="d6179-1898">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1898">Description</span></span> | <span data-ttu-id="d6179-1899">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1899">Allowed values</span></span> | <span data-ttu-id="d6179-1900">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1901">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="d6179-1901">recursive</span></span> |<span data-ttu-id="d6179-1902">Określa, czy lista toorecursively S3 obiekty w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1902">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="d6179-1903">wartość true, false</span><span class="sxs-lookup"><span data-stu-id="d6179-1903">true/false</span></span> |<span data-ttu-id="d6179-1904">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="d6179-1905">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1905">Example</span></span>


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

<span data-ttu-id="d6179-1906">Aby uzyskać więcej informacji, zobacz [Amazon S3 artykułu łącznika](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d6179-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="d6179-1907">System plików</span><span class="sxs-lookup"><span data-stu-id="d6179-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="d6179-1908">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-1908">Linked service</span></span>
<span data-ttu-id="d6179-1909">Możesz połączyć fabrykę danych Azure lokalnego pliku system tooan z hello **na lokalnym serwerze plików** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="d6179-1909">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="d6179-1910">Witaj w poniższej tabeli przedstawiono opis elementów JSON, które są określone toohello połączony serwer plików lokalnej usługi.</span><span class="sxs-lookup"><span data-stu-id="d6179-1910">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="d6179-1911">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1911">Property</span></span> | <span data-ttu-id="d6179-1912">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1912">Description</span></span> | <span data-ttu-id="d6179-1913">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1914">type</span><span class="sxs-lookup"><span data-stu-id="d6179-1914">type</span></span> |<span data-ttu-id="d6179-1915">Sprawdź, czy właściwość type hello jest ustawiony za**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1915">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="d6179-1916">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1916">Yes</span></span> |
| <span data-ttu-id="d6179-1917">Host</span><span class="sxs-lookup"><span data-stu-id="d6179-1917">host</span></span> |<span data-ttu-id="d6179-1918">Określa ścieżkę katalogu głównego hello folderu hello, które mają toocopy.</span><span class="sxs-lookup"><span data-stu-id="d6179-1918">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="d6179-1919">Użyj znaku ucieczki hello ' \ ' znaków specjalnych w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1919">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="d6179-1920">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="d6179-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="d6179-1921">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1921">Yes</span></span> |
| <span data-ttu-id="d6179-1922">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-1922">userid</span></span> |<span data-ttu-id="d6179-1923">Określ identyfikator hello hello użytkownik, który ma dostęp do serwera toohello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1923">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="d6179-1924">Nie (Jeśli wybierzesz encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="d6179-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="d6179-1925">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-1925">password</span></span> |<span data-ttu-id="d6179-1926">Określ hasło hello hello użytkownika (nazwa użytkownika).</span><span class="sxs-lookup"><span data-stu-id="d6179-1926">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="d6179-1927">Nie (Jeśli wybierzesz encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d6179-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="d6179-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d6179-1928">encryptedCredential</span></span> |<span data-ttu-id="d6179-1929">Określ poświadczenia hello zaszyfrowane, które można uzyskać, uruchamiając polecenie cmdlet hello AzureRmDataFactoryEncryptValue nowy.</span><span class="sxs-lookup"><span data-stu-id="d6179-1929">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="d6179-1930">Nie (Jeśli wybierzesz toospecify identyfikatora użytkownika i hasła w postaci zwykłego tekstu)</span><span class="sxs-lookup"><span data-stu-id="d6179-1930">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="d6179-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-1931">gatewayName</span></span> |<span data-ttu-id="d6179-1932">Określa nazwę hello hello bramy, że fabryka danych powinien używać serwera plików lokalnych toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d6179-1932">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="d6179-1933">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="d6179-1934">Ścieżka folderu definicje</span><span class="sxs-lookup"><span data-stu-id="d6179-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="d6179-1935">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="d6179-1935">Scenario</span></span> | <span data-ttu-id="d6179-1936">Host w definicji usługi połączonej</span><span class="sxs-lookup"><span data-stu-id="d6179-1936">Host in linked service definition</span></span> | <span data-ttu-id="d6179-1937">folderPath w definicji zestawu danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1938">Folder lokalny na komputerze bramy zarządzania danymi:</span><span class="sxs-lookup"><span data-stu-id="d6179-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="d6179-1939">Przykłady: D:\\ \* lub D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="d6179-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="d6179-1940">D:\\ \\ (dla danych zarządzania bramy 2.0 i nowsze wersje)</span><span class="sxs-lookup"><span data-stu-id="d6179-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="d6179-1941">localhost (dla starszych niż 2.0 bramy zarządzania danych)</span><span class="sxs-lookup"><span data-stu-id="d6179-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="d6179-1942">. \\ \\ lub folderu\\\\podfolder (dla danych zarządzania bramy 2.0 i nowsze wersje)</span><span class="sxs-lookup"><span data-stu-id="d6179-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="d6179-1943">D:\\ \\ lub D:\\\\folderu\\\\podfolder (dla wersji bramy poniżej 2.0)</span><span class="sxs-lookup"><span data-stu-id="d6179-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="d6179-1944">Zdalny folder udostępniony:</span><span class="sxs-lookup"><span data-stu-id="d6179-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="d6179-1945">Przykłady: \\ \\MójSerwer\\udostępnianie\\ \* lub \\ \\MójSerwer\\udostępnianie\\folderu\\podfolderu\\*</span><span class="sxs-lookup"><span data-stu-id="d6179-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="d6179-1946">\\\\\\\\MójSerwer\\\\udziału</span><span class="sxs-lookup"><span data-stu-id="d6179-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="d6179-1947">. \\ \\ lub folderu\\\\podfolderu</span><span class="sxs-lookup"><span data-stu-id="d6179-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="d6179-1948">Przykład: Przy użyciu nazwy użytkownika i hasła w postaci zwykłego tekstu</span><span class="sxs-lookup"><span data-stu-id="d6179-1948">Example: Using username and password in plain text</span></span>

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

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="d6179-1949">Przykład: Użycie encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="d6179-1949">Example: Using encryptedcredential</span></span>

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

<span data-ttu-id="d6179-1950">Aby uzyskać więcej informacji, zobacz [artykułu łącznika systemu plików](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d6179-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="d6179-1951">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-1951">Dataset</span></span>
<span data-ttu-id="d6179-1952">toodefine System plików zestawu danych, ustaw hello **typu** hello DataSet za**udziału plików**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-1952">toodefine a File System dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-1953">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1953">Property</span></span> | <span data-ttu-id="d6179-1954">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1954">Description</span></span> | <span data-ttu-id="d6179-1955">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="d6179-1956">folderPath</span></span> |<span data-ttu-id="d6179-1957">Określa folder toohello podrzędną hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1957">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="d6179-1958">Użyj znaku ucieczki hello ' \' znaków specjalnych w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1958">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="d6179-1959">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="d6179-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="d6179-1960">Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka.</span><span class="sxs-lookup"><span data-stu-id="d6179-1960">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="d6179-1961">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-1961">Yes</span></span> |
| <span data-ttu-id="d6179-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="d6179-1962">fileName</span></span> |<span data-ttu-id="d6179-1963">Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1963">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="d6179-1964">Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1964">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="d6179-1965">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwa hello hello wygenerowany plik jest zgodny z formatem hello:</span><span class="sxs-lookup"><span data-stu-id="d6179-1965">When fileName is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="d6179-1966">`Data.<Guid>.txt`(Przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="d6179-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="d6179-1967">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1967">No</span></span> |
| <span data-ttu-id="d6179-1968">obiektu fileFilter</span><span class="sxs-lookup"><span data-stu-id="d6179-1968">fileFilter</span></span> |<span data-ttu-id="d6179-1969">Określ toobe filtru używane tooselect podzbiór plików w hello folderPath, a nie wszystkich plików.</span><span class="sxs-lookup"><span data-stu-id="d6179-1969">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="d6179-1970">Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).</span><span class="sxs-lookup"><span data-stu-id="d6179-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="d6179-1971">Przykład 1: "obiektu"fileFilter: "* .log"</span><span class="sxs-lookup"><span data-stu-id="d6179-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="d6179-1972">Przykład 2: "obiektu"fileFilter: 2016 - 1-?. txt"</span><span class="sxs-lookup"><span data-stu-id="d6179-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="d6179-1973">Należy pamiętać, że tego obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików.</span><span class="sxs-lookup"><span data-stu-id="d6179-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="d6179-1974">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1974">No</span></span> |
| <span data-ttu-id="d6179-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="d6179-1975">partitionedBy</span></span> |<span data-ttu-id="d6179-1976">Toospecify partitionedBy dynamiczne folderPath/fileName służącego do dane szeregów czasowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1976">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="d6179-1977">Przykładem jest folderPath sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="d6179-1978">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1978">No</span></span> |
| <span data-ttu-id="d6179-1979">Format</span><span class="sxs-lookup"><span data-stu-id="d6179-1979">format</span></span> | <span data-ttu-id="d6179-1980">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1980">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d6179-1981">Zestaw hello **typu** właściwości w formacie tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d6179-1981">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d6179-1982">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="d6179-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d6179-1983">Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-1983">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d6179-1984">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1984">No</span></span> |
| <span data-ttu-id="d6179-1985">Kompresja</span><span class="sxs-lookup"><span data-stu-id="d6179-1985">compression</span></span> | <span data-ttu-id="d6179-1986">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-1986">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d6179-1987">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**; i są obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="d6179-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d6179-1988">zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d6179-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d6179-1989">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="d6179-1990">Nie można użyć nazwy pliku i obiektu fileFilter jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="d6179-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="d6179-1991">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-1991">Example</span></span>

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

<span data-ttu-id="d6179-1992">Aby uzyskać więcej informacji, zobacz [artykułu łącznika systemu plików](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d6179-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="d6179-1993">Źródło systemu plików w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="d6179-1994">Jeśli dane są kopiowane z systemu plików, należy ustawić hello **typ źródła** hello skopiować działania zbyt**FileSystemSource**i określ następujące właściwości w hello **źródła** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-1994">If you are copying data from File System, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-1995">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-1995">Property</span></span> | <span data-ttu-id="d6179-1996">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-1996">Description</span></span> | <span data-ttu-id="d6179-1997">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-1997">Allowed values</span></span> | <span data-ttu-id="d6179-1998">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-1999">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="d6179-1999">recursive</span></span> |<span data-ttu-id="d6179-2000">Wskazuje, czy hello są odczytywane dane rekursywnie z podfoldery hello lub tylko hello określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2000">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="d6179-2001">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="d6179-2001">True, False (default)</span></span> |<span data-ttu-id="d6179-2002">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-2003">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2003">Example</span></span>

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
<span data-ttu-id="d6179-2004">Aby uzyskać więcej informacji, zobacz [artykułu łącznika systemu plików](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d6179-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="d6179-2005">W przypadku działania kopiowania obiektu Sink systemu plików</span><span class="sxs-lookup"><span data-stu-id="d6179-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="d6179-2006">Kopiowania danych tooFile systemu, ustaw hello **typu sink** hello skopiować działania zbyt**FileSystemSink**i określ następujące właściwości w hello **zbiornika** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2006">If you are copying data tooFile System, set hello **sink type** of hello copy activity too**FileSystemSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="d6179-2007">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2007">Property</span></span> | <span data-ttu-id="d6179-2008">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2008">Description</span></span> | <span data-ttu-id="d6179-2009">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-2009">Allowed values</span></span> | <span data-ttu-id="d6179-2010">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="d6179-2011">copyBehavior</span></span> |<span data-ttu-id="d6179-2012">Definiuje zachowanie kopii hello, gdy źródłem hello jest BlobSource lub systemu plików.</span><span class="sxs-lookup"><span data-stu-id="d6179-2012">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="d6179-2013">**PreserveHierarchy:** zachowuje hello hierarchii plików w folderze docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2013">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="d6179-2014">Oznacza to, że hello względnej ścieżki folderu źródłowego toohello pliku źródłowego hello jest hello taka sama jak ścieżka względna hello hello docelowego pliku toohello docelowy folderu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2014">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="d6179-2015">**FlattenHierarchy:** wszystkie pliki z folderu źródłowego hello są tworzone w hello pierwszy poziom folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2015">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="d6179-2016">pliki docelowe Hello są tworzone z automatycznie generowaną nazwą.</span><span class="sxs-lookup"><span data-stu-id="d6179-2016">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="d6179-2017">**MergeFiles:** scala wszystkie pliki z pliku tooone folderu źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2017">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="d6179-2018">Jeśli określono hello pliku nazwy/nazwa obiektu blob, hello scalony plik nazwa jest hello określonej nazwy.</span><span class="sxs-lookup"><span data-stu-id="d6179-2018">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="d6179-2019">W przeciwnym razie jest nazwa pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="d6179-2020">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2020">No</span></span> |
<span data-ttu-id="d6179-2021">Auto-</span><span class="sxs-lookup"><span data-stu-id="d6179-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="d6179-2022">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2022">Example</span></span>

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

<span data-ttu-id="d6179-2023">Aby uzyskać więcej informacji, zobacz [artykułu łącznika systemu plików](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d6179-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="d6179-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="d6179-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-2025">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2025">Linked service</span></span>
<span data-ttu-id="d6179-2026">toodefine FTP połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**SerwerFTP**i określ następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2026">toodefine an FTP linked service, set hello **type** of hello linked service too**FtpServer**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-2027">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2027">Property</span></span> | <span data-ttu-id="d6179-2028">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2028">Description</span></span> | <span data-ttu-id="d6179-2029">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2029">Required</span></span> | <span data-ttu-id="d6179-2030">Domyślne</span><span class="sxs-lookup"><span data-stu-id="d6179-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-2031">Host</span><span class="sxs-lookup"><span data-stu-id="d6179-2031">host</span></span> |<span data-ttu-id="d6179-2032">Nazwa lub adres IP powitania serwera FTP</span><span class="sxs-lookup"><span data-stu-id="d6179-2032">Name or IP address of hello FTP Server</span></span> |<span data-ttu-id="d6179-2033">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="d6179-2034">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-2034">authenticationType</span></span> |<span data-ttu-id="d6179-2035">Określ typ uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="d6179-2035">Specify authentication type</span></span> |<span data-ttu-id="d6179-2036">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2036">Yes</span></span> |<span data-ttu-id="d6179-2037">Basic anonimowe</span><span class="sxs-lookup"><span data-stu-id="d6179-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="d6179-2038">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-2038">username</span></span> |<span data-ttu-id="d6179-2039">Użytkownik, który ma dostęp do serwera FTP toohello</span><span class="sxs-lookup"><span data-stu-id="d6179-2039">User who has access toohello FTP server</span></span> |<span data-ttu-id="d6179-2040">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="d6179-2041">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-2041">password</span></span> |<span data-ttu-id="d6179-2042">Hasło dla użytkownika hello (nazwa_użytkownika)</span><span class="sxs-lookup"><span data-stu-id="d6179-2042">Password for hello user (username)</span></span> |<span data-ttu-id="d6179-2043">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="d6179-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d6179-2044">encryptedCredential</span></span> |<span data-ttu-id="d6179-2045">Serwer FTP hello tooaccess zaszyfrowane poświadczenia</span><span class="sxs-lookup"><span data-stu-id="d6179-2045">Encrypted credential tooaccess hello FTP server</span></span> |<span data-ttu-id="d6179-2046">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="d6179-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-2047">gatewayName</span></span> |<span data-ttu-id="d6179-2048">Nazwa hello brama zarządzania danymi bramy tooconnect tooan lokalnego serwera FTP</span><span class="sxs-lookup"><span data-stu-id="d6179-2048">Name of hello Data Management Gateway gateway tooconnect tooan on-premises FTP server</span></span> |<span data-ttu-id="d6179-2049">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="d6179-2050">port</span><span class="sxs-lookup"><span data-stu-id="d6179-2050">port</span></span> |<span data-ttu-id="d6179-2051">Port, na którym hello FTP nasłuchuje serwer</span><span class="sxs-lookup"><span data-stu-id="d6179-2051">Port on which hello FTP server is listening</span></span> |<span data-ttu-id="d6179-2052">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2052">No</span></span> |<span data-ttu-id="d6179-2053">21</span><span class="sxs-lookup"><span data-stu-id="d6179-2053">21</span></span> |
| <span data-ttu-id="d6179-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="d6179-2054">enableSsl</span></span> |<span data-ttu-id="d6179-2055">Określ, czy toouse FTP za pośrednictwem kanału SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="d6179-2055">Specify whether toouse FTP over SSL/TLS channel</span></span> |<span data-ttu-id="d6179-2056">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2056">No</span></span> |<span data-ttu-id="d6179-2057">Wartość true</span><span class="sxs-lookup"><span data-stu-id="d6179-2057">true</span></span> |
| <span data-ttu-id="d6179-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="d6179-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="d6179-2059">Określ, czy tooenable serwera SSL przy użyciu protokołu FTP za pośrednictwem kanału SSL/TLS, certyfikat weryfikacji</span><span class="sxs-lookup"><span data-stu-id="d6179-2059">Specify whether tooenable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="d6179-2060">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2060">No</span></span> |<span data-ttu-id="d6179-2061">Wartość true</span><span class="sxs-lookup"><span data-stu-id="d6179-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="d6179-2062">Przykład: Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="d6179-2062">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="d6179-2063">Przykład: Przy użyciu nazwy użytkownika i hasła w postaci zwykłego tekstu dla uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="d6179-2063">Example: Using username and password in plain text for basic authentication</span></span>

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

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="d6179-2064">Przykład: Przy użyciu portu, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="d6179-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

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

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="d6179-2065">Przykład: Użycie encryptedCredential uwierzytelniania i bramy</span><span class="sxs-lookup"><span data-stu-id="d6179-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

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

<span data-ttu-id="d6179-2066">Aby uzyskać więcej informacji, zobacz [łącznik FTP](data-factory-ftp-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="d6179-2067">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-2067">Dataset</span></span>
<span data-ttu-id="d6179-2068">toodefine FTP zestawu danych, ustaw hello **typu** hello DataSet za**udziału plików**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2068">toodefine an FTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-2069">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2069">Property</span></span> | <span data-ttu-id="d6179-2070">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2070">Description</span></span> | <span data-ttu-id="d6179-2071">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="d6179-2072">folderPath</span></span> |<span data-ttu-id="d6179-2073">Folder toohello ścieżki Sub.</span><span class="sxs-lookup"><span data-stu-id="d6179-2073">Sub path toohello folder.</span></span> <span data-ttu-id="d6179-2074">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2074">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="d6179-2075">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="d6179-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="d6179-2076">Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka.</span><span class="sxs-lookup"><span data-stu-id="d6179-2076">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="d6179-2077">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2077">Yes</span></span> 
| <span data-ttu-id="d6179-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="d6179-2078">fileName</span></span> |<span data-ttu-id="d6179-2079">Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2079">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="d6179-2080">Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2080">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="d6179-2081">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu:</span><span class="sxs-lookup"><span data-stu-id="d6179-2081">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="d6179-2082">Dane. <Guid>.txt (przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="d6179-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="d6179-2083">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2083">No</span></span> |
| <span data-ttu-id="d6179-2084">obiektu fileFilter</span><span class="sxs-lookup"><span data-stu-id="d6179-2084">fileFilter</span></span> |<span data-ttu-id="d6179-2085">Określ toobe filtru używane tooselect podzbiór plików w hello folderPath, a nie wszystkich plików.</span><span class="sxs-lookup"><span data-stu-id="d6179-2085">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="d6179-2086">Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).</span><span class="sxs-lookup"><span data-stu-id="d6179-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="d6179-2087">Przykład 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="d6179-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="d6179-2088">Przykład 2:`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="d6179-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="d6179-2089">obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików.</span><span class="sxs-lookup"><span data-stu-id="d6179-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="d6179-2090">Ta właściwość nie jest obsługiwana z systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="d6179-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="d6179-2091">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2091">No</span></span> |
| <span data-ttu-id="d6179-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="d6179-2092">partitionedBy</span></span> |<span data-ttu-id="d6179-2093">partitionedBy mogą być używane toospecify folderPath dynamicznych, nazwę pliku dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2093">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="d6179-2094">Na przykład folderPath sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="d6179-2095">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2095">No</span></span> |
| <span data-ttu-id="d6179-2096">Format</span><span class="sxs-lookup"><span data-stu-id="d6179-2096">format</span></span> | <span data-ttu-id="d6179-2097">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2097">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d6179-2098">Zestaw hello **typu** właściwości w formacie tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d6179-2098">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d6179-2099">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="d6179-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d6179-2100">Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2100">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d6179-2101">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2101">No</span></span> |
| <span data-ttu-id="d6179-2102">Kompresja</span><span class="sxs-lookup"><span data-stu-id="d6179-2102">compression</span></span> | <span data-ttu-id="d6179-2103">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2103">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d6179-2104">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**; i są obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d6179-2105">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d6179-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d6179-2106">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2106">No</span></span> |
| <span data-ttu-id="d6179-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="d6179-2107">useBinaryTransfer</span></span> |<span data-ttu-id="d6179-2108">Określ, czy używany tryb transferu binarnego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="d6179-2109">Wartość true dla trybie binarnym i wartość false ASCII.</span><span class="sxs-lookup"><span data-stu-id="d6179-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="d6179-2110">Wartość domyślna: wartość True.</span><span class="sxs-lookup"><span data-stu-id="d6179-2110">Default value: True.</span></span> <span data-ttu-id="d6179-2111">Ta właściwość jest używana tylko w przypadku typu skojarzonej połączonej usługi typu: SerwerFTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="d6179-2112">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="d6179-2113">Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.</span><span class="sxs-lookup"><span data-stu-id="d6179-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="d6179-2114">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="d6179-2115">Aby uzyskać więcej informacji, zobacz [łącznik FTP](data-factory-ftp-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="d6179-2116">Źródło systemu plików w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="d6179-2117">Jeśli dane są kopiowane z serwera FTP, ustaw hello **typ źródła** hello skopiować działania zbyt**FileSystemSource**i określ następujące właściwości w hello **źródła** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-2117">If you are copying data from an FTP server, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-2118">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2118">Property</span></span> | <span data-ttu-id="d6179-2119">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2119">Description</span></span> | <span data-ttu-id="d6179-2120">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-2120">Allowed values</span></span> | <span data-ttu-id="d6179-2121">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-2122">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="d6179-2122">recursive</span></span> |<span data-ttu-id="d6179-2123">Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2123">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="d6179-2124">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="d6179-2124">True, False (default)</span></span> |<span data-ttu-id="d6179-2125">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-2126">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2126">Example</span></span>

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

<span data-ttu-id="d6179-2127">Aby uzyskać więcej informacji, zobacz [łącznik FTP](data-factory-ftp-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="d6179-2128">SYSTEM PLIKÓW HDFS</span><span class="sxs-lookup"><span data-stu-id="d6179-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-2129">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2129">Linked service</span></span>
<span data-ttu-id="d6179-2130">toodefine HDFS połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**systemu plików Hdfs**i określ następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2130">toodefine a HDFS linked service, set hello **type** of hello linked service too**Hdfs**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-2131">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2131">Property</span></span> | <span data-ttu-id="d6179-2132">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2132">Description</span></span> | <span data-ttu-id="d6179-2133">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2134">type</span><span class="sxs-lookup"><span data-stu-id="d6179-2134">type</span></span> |<span data-ttu-id="d6179-2135">musi mieć ustawioną właściwość type Hello: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="d6179-2135">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="d6179-2136">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2136">Yes</span></span> |
| <span data-ttu-id="d6179-2137">Url</span><span class="sxs-lookup"><span data-stu-id="d6179-2137">Url</span></span> |<span data-ttu-id="d6179-2138">Adres URL toohello systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="d6179-2138">URL toohello HDFS</span></span> |<span data-ttu-id="d6179-2139">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2139">Yes</span></span> |
| <span data-ttu-id="d6179-2140">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-2140">authenticationType</span></span> |<span data-ttu-id="d6179-2141">Anonimowe lub Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="d6179-2142">toouse **uwierzytelnianie Kerberos** łącznika systemu plików HDFS, można znaleźć zbyt[w tej sekcji](#use-kerberos-authentication-for-hdfs-connector) tooset się w lokalnym środowisku odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="d6179-2142">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="d6179-2143">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2143">Yes</span></span> |
| <span data-ttu-id="d6179-2144">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-2144">userName</span></span> |<span data-ttu-id="d6179-2145">Uwierzytelnianie nazwy użytkownika dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="d6179-2146">Tak (w przypadku uwierzytelniania systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="d6179-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="d6179-2147">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-2147">password</span></span> |<span data-ttu-id="d6179-2148">Hasło dla uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="d6179-2149">Tak (w przypadku uwierzytelniania systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="d6179-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="d6179-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-2150">gatewayName</span></span> |<span data-ttu-id="d6179-2151">Nazwa bramy hello hello usługi fabryka danych należy używać toohello tooconnect systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="d6179-2151">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="d6179-2152">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2152">Yes</span></span> |
| <span data-ttu-id="d6179-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d6179-2153">encryptedCredential</span></span> |<span data-ttu-id="d6179-2154">[Nowy AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) hello poświadczeń dostępu do danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="d6179-2155">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="d6179-2156">Przykład: Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="d6179-2156">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="d6179-2157">Przykład: Przy użyciu uwierzytelniania systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d6179-2157">Example: Using Windows authentication</span></span>

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

<span data-ttu-id="d6179-2158">Aby uzyskać więcej informacji, zobacz [łącznika systemu plików HDFS](#data-factory-hdfs-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-2159">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-2159">Dataset</span></span>
<span data-ttu-id="d6179-2160">toodefine systemu plików HDFS zestawu danych, ustaw hello **typu** hello DataSet za**udziału plików**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2160">toodefine a HDFS dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-2161">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2161">Property</span></span> | <span data-ttu-id="d6179-2162">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2162">Description</span></span> | <span data-ttu-id="d6179-2163">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="d6179-2164">folderPath</span></span> |<span data-ttu-id="d6179-2165">Ścieżka folderu toohello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2165">Path toohello folder.</span></span> <span data-ttu-id="d6179-2166">Przykład:`myfolder`</span><span class="sxs-lookup"><span data-stu-id="d6179-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="d6179-2167">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2167">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="d6179-2168">Na przykład: folder\subfolder, określ folder\\\\podfolderów i dla d:\samplefolder, określ d:\\\\folder_przykładowy.</span><span class="sxs-lookup"><span data-stu-id="d6179-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="d6179-2169">Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka.</span><span class="sxs-lookup"><span data-stu-id="d6179-2169">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="d6179-2170">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2170">Yes</span></span> |
| <span data-ttu-id="d6179-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="d6179-2171">fileName</span></span> |<span data-ttu-id="d6179-2172">Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2172">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="d6179-2173">Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2173">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="d6179-2174">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu:</span><span class="sxs-lookup"><span data-stu-id="d6179-2174">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="d6179-2175">Dane. <Guid>.txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="d6179-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="d6179-2176">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2176">No</span></span> |
| <span data-ttu-id="d6179-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="d6179-2177">partitionedBy</span></span> |<span data-ttu-id="d6179-2178">partitionedBy mogą być używane toospecify folderPath dynamicznych, nazwę pliku dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2178">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="d6179-2179">Przykład: folderPath sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="d6179-2180">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2180">No</span></span> |
| <span data-ttu-id="d6179-2181">Format</span><span class="sxs-lookup"><span data-stu-id="d6179-2181">format</span></span> | <span data-ttu-id="d6179-2182">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2182">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d6179-2183">Zestaw hello **typu** właściwości w formacie tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d6179-2183">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d6179-2184">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="d6179-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d6179-2185">Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2185">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d6179-2186">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2186">No</span></span> |
| <span data-ttu-id="d6179-2187">Kompresja</span><span class="sxs-lookup"><span data-stu-id="d6179-2187">compression</span></span> | <span data-ttu-id="d6179-2188">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2188">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d6179-2189">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="d6179-2190">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d6179-2191">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d6179-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d6179-2192">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="d6179-2193">Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.</span><span class="sxs-lookup"><span data-stu-id="d6179-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="d6179-2194">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2194">Example</span></span>

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

<span data-ttu-id="d6179-2195">Aby uzyskać więcej informacji, zobacz [łącznika systemu plików HDFS](#data-factory-hdfs-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="d6179-2196">Źródło systemu plików w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="d6179-2197">Jeśli dane są kopiowane z systemu plików HDFS, ustaw hello **typ źródła** hello skopiować działania zbyt**FileSystemSource**i określ następujące właściwości w hello **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2197">If you are copying data from HDFS, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="d6179-2198">**FileSystemSource** obsługuje hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="d6179-2198">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="d6179-2199">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2199">Property</span></span> | <span data-ttu-id="d6179-2200">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2200">Description</span></span> | <span data-ttu-id="d6179-2201">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-2201">Allowed values</span></span> | <span data-ttu-id="d6179-2202">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-2203">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="d6179-2203">recursive</span></span> |<span data-ttu-id="d6179-2204">Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2204">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="d6179-2205">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="d6179-2205">True, False (default)</span></span> |<span data-ttu-id="d6179-2206">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-2207">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2207">Example</span></span>

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

<span data-ttu-id="d6179-2208">Aby uzyskać więcej informacji, zobacz [łącznika systemu plików HDFS](#data-factory-hdfs-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="d6179-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="d6179-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="d6179-2210">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2210">Linked service</span></span>
<span data-ttu-id="d6179-2211">toodefine SFTP połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**Sftp**i określ następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2211">toodefine an SFTP linked service, set hello **type** of hello linked service too**Sftp**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-2212">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2212">Property</span></span> | <span data-ttu-id="d6179-2213">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2213">Description</span></span> | <span data-ttu-id="d6179-2214">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-2215">Host</span><span class="sxs-lookup"><span data-stu-id="d6179-2215">host</span></span> | <span data-ttu-id="d6179-2216">Nazwa lub adres IP serwera SFTP hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2216">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="d6179-2217">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2217">Yes</span></span> |
| <span data-ttu-id="d6179-2218">port</span><span class="sxs-lookup"><span data-stu-id="d6179-2218">port</span></span> |<span data-ttu-id="d6179-2219">Port, na którym hello SFTP serwer nasłuchuje.</span><span class="sxs-lookup"><span data-stu-id="d6179-2219">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="d6179-2220">Witaj, wartość domyślna to: 21</span><span class="sxs-lookup"><span data-stu-id="d6179-2220">hello default value is: 21</span></span> |<span data-ttu-id="d6179-2221">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2221">No</span></span> |
| <span data-ttu-id="d6179-2222">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-2222">authenticationType</span></span> |<span data-ttu-id="d6179-2223">Określ typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="d6179-2223">Specify authentication type.</span></span> <span data-ttu-id="d6179-2224">Dozwolone wartości: **podstawowe**, **parametry SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="d6179-2225">Odwołuje się zbyt[używanie uwierzytelniania podstawowego](#using-basic-authentication) i [przy użyciu publicznego klucza uwierzytelniania SSH](#using-ssh-public-key-authentication) odpowiednio sekcje więcej właściwości i przykłady JSON.</span><span class="sxs-lookup"><span data-stu-id="d6179-2225">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="d6179-2226">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2226">Yes</span></span> |
| <span data-ttu-id="d6179-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="d6179-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="d6179-2228">Określ, czy tooskip hosta klucza weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="d6179-2228">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="d6179-2229">Nie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2229">No.</span></span> <span data-ttu-id="d6179-2230">Witaj wartość domyślna: false</span><span class="sxs-lookup"><span data-stu-id="d6179-2230">hello default value: false</span></span> |
| <span data-ttu-id="d6179-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="d6179-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="d6179-2232">Podaj odcisk palca hello hello klucza hosta.</span><span class="sxs-lookup"><span data-stu-id="d6179-2232">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="d6179-2233">Tak, jeśli hello `skipHostKeyValidation` ustawiono toofalse.</span><span class="sxs-lookup"><span data-stu-id="d6179-2233">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="d6179-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-2234">gatewayName</span></span> |<span data-ttu-id="d6179-2235">Nazwa tooan tooconnect brama zarządzania danymi hello SFTP serwerem lokalnym.</span><span class="sxs-lookup"><span data-stu-id="d6179-2235">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="d6179-2236">Tak, jeśli kopiowanie danych z lokalnego serwera SFTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="d6179-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d6179-2237">encryptedCredential</span></span> | <span data-ttu-id="d6179-2238">Serwer protokołu SFTP hello tooaccess zaszyfrowane poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="d6179-2238">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="d6179-2239">Wygenerowany automatycznie po określeniu opcji Uwierzytelnianie podstawowe (nazwy użytkownika i hasła) lub uwierzytelniania parametry SshPublicKey (nazwy użytkownika i ścieżki do klucza prywatnego lub zawartości) kopiowania kreatora lub hello ClickOnce podręcznego okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="d6179-2240">Nie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2240">No.</span></span> <span data-ttu-id="d6179-2241">Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera SFTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="d6179-2242">Przykład: Przy użyciu uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="d6179-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="d6179-2243">Ustaw toouse uwierzytelnianie podstawowe, `authenticationType` jako `Basic`, a następnie określ następujące właściwości poza hello łącznika SFTP ogólnego z nich wprowadzone w ostatniej sekcji hello hello:</span><span class="sxs-lookup"><span data-stu-id="d6179-2243">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="d6179-2244">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2244">Property</span></span> | <span data-ttu-id="d6179-2245">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2245">Description</span></span> | <span data-ttu-id="d6179-2246">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-2247">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-2247">username</span></span> | <span data-ttu-id="d6179-2248">Użytkownik, który ma dostęp toohello SFTP serwera.</span><span class="sxs-lookup"><span data-stu-id="d6179-2248">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="d6179-2249">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2249">Yes</span></span> |
| <span data-ttu-id="d6179-2250">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-2250">password</span></span> | <span data-ttu-id="d6179-2251">Hasło dla użytkownika hello (nazwa_użytkownika).</span><span class="sxs-lookup"><span data-stu-id="d6179-2251">Password for hello user (username).</span></span> | <span data-ttu-id="d6179-2252">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2252">Yes</span></span> |

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

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="d6179-2253">Przykład: Uwierzytelnianie podstawowe z zaszyfrowanych poświadczeń **</span><span class="sxs-lookup"><span data-stu-id="d6179-2253">Example: Basic authentication with encrypted credential**</span></span>

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

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="d6179-2254">Przy użyciu uwierzytelniania klucza publicznego SSH: **</span><span class="sxs-lookup"><span data-stu-id="d6179-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="d6179-2255">Ustaw toouse uwierzytelnianie podstawowe, `authenticationType` jako `SshPublicKey`, a następnie określ następujące właściwości poza hello łącznika SFTP ogólnego z nich wprowadzone w ostatniej sekcji hello hello:</span><span class="sxs-lookup"><span data-stu-id="d6179-2255">toouse basic authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="d6179-2256">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2256">Property</span></span> | <span data-ttu-id="d6179-2257">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2257">Description</span></span> | <span data-ttu-id="d6179-2258">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-2259">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-2259">username</span></span> |<span data-ttu-id="d6179-2260">Użytkownik, który ma dostęp toohello SFTP serwera</span><span class="sxs-lookup"><span data-stu-id="d6179-2260">User who has access toohello SFTP server</span></span> |<span data-ttu-id="d6179-2261">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2261">Yes</span></span> |
| <span data-ttu-id="d6179-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="d6179-2262">privateKeyPath</span></span> | <span data-ttu-id="d6179-2263">Określ ścieżkę bezwzględną toohello pliku klucza prywatnego może dostęp do tej bramy.</span><span class="sxs-lookup"><span data-stu-id="d6179-2263">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="d6179-2264">Określ albo hello `privateKeyPath` lub `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="d6179-2264">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="d6179-2265">Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera SFTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="d6179-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="d6179-2266">privateKeyContent</span></span> | <span data-ttu-id="d6179-2267">Zserializowany ciąg hello prywatnego klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="d6179-2267">A serialized string of hello private key content.</span></span> <span data-ttu-id="d6179-2268">Witaj kreatora kopiowania może odczytywać hello pliku klucza prywatnego i Wyodrębnij zawartość klucza prywatnego hello automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2268">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="d6179-2269">Jeśli używane są wszystkie inne narzędzie/pakiet SDK, należy użyć właściwości privateKeyPath hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2269">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="d6179-2270">Określ albo hello `privateKeyPath` lub `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="d6179-2270">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="d6179-2271">Hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-2271">passPhrase</span></span> | <span data-ttu-id="d6179-2272">Określ hello przebiegu frazy/hasło toodecrypt hello prywatny klucz, jeśli plik klucza hello jest chroniony przez hasło.</span><span class="sxs-lookup"><span data-stu-id="d6179-2272">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="d6179-2273">Tak, czy plik klucza prywatnego hello jest chroniony przez hasło.</span><span class="sxs-lookup"><span data-stu-id="d6179-2273">Yes if hello private key file is protected by a pass phrase.</span></span> |

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

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="d6179-2274">Przykład: Parametry SshPublicKey uwierzytelniania za pomocą prywatnego klucza zawartości **</span><span class="sxs-lookup"><span data-stu-id="d6179-2274">Example: SshPublicKey authentication using private key content**</span></span>

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
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="d6179-2275">Aby uzyskać więcej informacji, zobacz [łącznika SFTP](data-factory-sftp-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-2276">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-2276">Dataset</span></span>
<span data-ttu-id="d6179-2277">toodefine zestawem danych SFTP hello zestaw **typu** hello DataSet za**udziału plików**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2277">toodefine an SFTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-2278">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2278">Property</span></span> | <span data-ttu-id="d6179-2279">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2279">Description</span></span> | <span data-ttu-id="d6179-2280">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="d6179-2281">folderPath</span></span> |<span data-ttu-id="d6179-2282">Folder toohello ścieżki Sub.</span><span class="sxs-lookup"><span data-stu-id="d6179-2282">Sub path toohello folder.</span></span> <span data-ttu-id="d6179-2283">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2283">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="d6179-2284">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="d6179-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="d6179-2285">Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka.</span><span class="sxs-lookup"><span data-stu-id="d6179-2285">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="d6179-2286">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2286">Yes</span></span> |
| <span data-ttu-id="d6179-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="d6179-2287">fileName</span></span> |<span data-ttu-id="d6179-2288">Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2288">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="d6179-2289">Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2289">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="d6179-2290">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu:</span><span class="sxs-lookup"><span data-stu-id="d6179-2290">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="d6179-2291">Dane. <Guid>.txt (przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="d6179-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="d6179-2292">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2292">No</span></span> |
| <span data-ttu-id="d6179-2293">obiektu fileFilter</span><span class="sxs-lookup"><span data-stu-id="d6179-2293">fileFilter</span></span> |<span data-ttu-id="d6179-2294">Określ toobe filtru używane tooselect podzbiór plików w hello folderPath, a nie wszystkich plików.</span><span class="sxs-lookup"><span data-stu-id="d6179-2294">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="d6179-2295">Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).</span><span class="sxs-lookup"><span data-stu-id="d6179-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="d6179-2296">Przykład 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="d6179-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="d6179-2297">Przykład 2:`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="d6179-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="d6179-2298">obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików.</span><span class="sxs-lookup"><span data-stu-id="d6179-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="d6179-2299">Ta właściwość nie jest obsługiwana z systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="d6179-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="d6179-2300">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2300">No</span></span> |
| <span data-ttu-id="d6179-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="d6179-2301">partitionedBy</span></span> |<span data-ttu-id="d6179-2302">partitionedBy mogą być używane toospecify folderPath dynamicznych, nazwę pliku dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2302">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="d6179-2303">Na przykład folderPath sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="d6179-2304">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2304">No</span></span> |
| <span data-ttu-id="d6179-2305">Format</span><span class="sxs-lookup"><span data-stu-id="d6179-2305">format</span></span> | <span data-ttu-id="d6179-2306">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2306">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d6179-2307">Zestaw hello **typu** właściwości w formacie tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d6179-2307">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d6179-2308">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="d6179-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d6179-2309">Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2309">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d6179-2310">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2310">No</span></span> |
| <span data-ttu-id="d6179-2311">Kompresja</span><span class="sxs-lookup"><span data-stu-id="d6179-2311">compression</span></span> | <span data-ttu-id="d6179-2312">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2312">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d6179-2313">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="d6179-2314">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d6179-2315">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d6179-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d6179-2316">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2316">No</span></span> |
| <span data-ttu-id="d6179-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="d6179-2317">useBinaryTransfer</span></span> |<span data-ttu-id="d6179-2318">Określ, czy używany tryb transferu binarnego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="d6179-2319">Wartość true dla trybie binarnym i wartość false ASCII.</span><span class="sxs-lookup"><span data-stu-id="d6179-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="d6179-2320">Wartość domyślna: wartość True.</span><span class="sxs-lookup"><span data-stu-id="d6179-2320">Default value: True.</span></span> <span data-ttu-id="d6179-2321">Ta właściwość jest używana tylko w przypadku typu skojarzonej połączonej usługi typu: SerwerFTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="d6179-2322">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="d6179-2323">Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.</span><span class="sxs-lookup"><span data-stu-id="d6179-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="d6179-2324">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="d6179-2325">Aby uzyskać więcej informacji, zobacz [łącznika SFTP](data-factory-sftp-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="d6179-2326">Źródło systemu plików w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="d6179-2327">Jeśli dane są kopiowane z użyciem protokołu SFTP źródła, ustaw hello **typ źródła** hello skopiować działania zbyt**FileSystemSource**i określ następujące właściwości w hello **źródła** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-2327">If you are copying data from an SFTP source, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-2328">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2328">Property</span></span> | <span data-ttu-id="d6179-2329">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2329">Description</span></span> | <span data-ttu-id="d6179-2330">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-2330">Allowed values</span></span> | <span data-ttu-id="d6179-2331">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-2332">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="d6179-2332">recursive</span></span> |<span data-ttu-id="d6179-2333">Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2333">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="d6179-2334">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="d6179-2334">True, False (default)</span></span> |<span data-ttu-id="d6179-2335">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="d6179-2336">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2336">Example</span></span>

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

<span data-ttu-id="d6179-2337">Aby uzyskać więcej informacji, zobacz [łącznika SFTP](data-factory-sftp-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="d6179-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="d6179-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-2339">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2339">Linked service</span></span>
<span data-ttu-id="d6179-2340">toodefine HTTP połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**Http**i określ następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2340">toodefine a HTTP linked service, set hello **type** of hello linked service too**Http**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-2341">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2341">Property</span></span> | <span data-ttu-id="d6179-2342">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2342">Description</span></span> | <span data-ttu-id="d6179-2343">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2344">adres URL</span><span class="sxs-lookup"><span data-stu-id="d6179-2344">url</span></span> | <span data-ttu-id="d6179-2345">Podstawowa toohello adres URL serwera sieci Web</span><span class="sxs-lookup"><span data-stu-id="d6179-2345">Base URL toohello Web Server</span></span> | <span data-ttu-id="d6179-2346">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2346">Yes</span></span> |
| <span data-ttu-id="d6179-2347">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-2347">authenticationType</span></span> | <span data-ttu-id="d6179-2348">Określa typ uwierzytelniania hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2348">Specifies hello authentication type.</span></span> <span data-ttu-id="d6179-2349">Dozwolone wartości to: **anonimowe**, **podstawowe**, **szyfrowanego**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="d6179-2350">Dotyczą odpowiednio toosections pod tą tabelą więcej właściwości i przykłady JSON dla tych typów uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="d6179-2350">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="d6179-2351">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2351">Yes</span></span> |
| <span data-ttu-id="d6179-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="d6179-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="d6179-2353">Określ, czy tooenable serwera SSL certyfikatu weryfikacji, jeśli źródło jest serwer sieci Web protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="d6179-2353">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="d6179-2354">Nie, domyślna to true</span><span class="sxs-lookup"><span data-stu-id="d6179-2354">No, default is true</span></span> |
| <span data-ttu-id="d6179-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-2355">gatewayName</span></span> | <span data-ttu-id="d6179-2356">Nazwa tooan tooconnect brama zarządzania danymi hello lokalnego źródła HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2356">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="d6179-2357">Tak, jeśli kopiowanie danych z lokalnego źródła HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="d6179-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d6179-2358">encryptedCredential</span></span> | <span data-ttu-id="d6179-2359">Zaszyfrowane poświadczenia tooaccess hello punkt końcowy HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2359">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="d6179-2360">Wygenerowany automatycznie podczas konfigurowania hello informacje o uwierzytelnianiu w kopii kreatora lub hello ClickOnce podręcznego okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2360">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="d6179-2361">Nie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2361">No.</span></span> <span data-ttu-id="d6179-2362">Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="d6179-2363">Przykład: Uwierzytelnianie podstawowe, szyfrowane lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d6179-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="d6179-2364">Ustaw `authenticationType` jako `Basic`, `Digest`, lub `Windows`i określ następujące właściwości poza hello łącznika HTTP ogólnego tych wprowadzonych powyżej hello:</span><span class="sxs-lookup"><span data-stu-id="d6179-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="d6179-2365">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2365">Property</span></span> | <span data-ttu-id="d6179-2366">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2366">Description</span></span> | <span data-ttu-id="d6179-2367">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2368">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-2368">username</span></span> | <span data-ttu-id="d6179-2369">Nazwa użytkownika tooaccess hello punkt końcowy HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2369">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="d6179-2370">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2370">Yes</span></span> |
| <span data-ttu-id="d6179-2371">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-2371">password</span></span> | <span data-ttu-id="d6179-2372">Hasło dla użytkownika hello (nazwa_użytkownika).</span><span class="sxs-lookup"><span data-stu-id="d6179-2372">Password for hello user (username).</span></span> | <span data-ttu-id="d6179-2373">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2373">Yes</span></span> |

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

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="d6179-2374">Przykład: Przy użyciu uwierzytelniania ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="d6179-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="d6179-2375">Ustaw toouse uwierzytelnianie podstawowe, `authenticationType` jako `ClientCertificate`i określ następujące właściwości poza hello łącznika HTTP ogólnego tych wprowadzonych powyżej hello:</span><span class="sxs-lookup"><span data-stu-id="d6179-2375">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="d6179-2376">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2376">Property</span></span> | <span data-ttu-id="d6179-2377">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2377">Description</span></span> | <span data-ttu-id="d6179-2378">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="d6179-2379">embeddedCertData</span></span> | <span data-ttu-id="d6179-2380">zawartość algorytmem Base64 Hello danych binarnych hello pliku wymiany informacji osobistych (PFX).</span><span class="sxs-lookup"><span data-stu-id="d6179-2380">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="d6179-2381">Określ albo hello `embeddedCertData` lub `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="d6179-2381">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="d6179-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="d6179-2382">certThumbprint</span></span> | <span data-ttu-id="d6179-2383">Witaj odcisk palca certyfikatu hello, który został zainstalowany na komputerze bramy magazynu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="d6179-2383">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="d6179-2384">Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego źródła HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="d6179-2385">Określ albo hello `embeddedCertData` lub `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="d6179-2385">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="d6179-2386">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-2386">password</span></span> | <span data-ttu-id="d6179-2387">Hasło skojarzone z certyfikatem hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2387">Password associated with hello certificate.</span></span> | <span data-ttu-id="d6179-2388">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2388">No</span></span> |

<span data-ttu-id="d6179-2389">Jeśli używasz `certThumbprint` dla certyfikatu uwierzytelniania i hello jest zainstalowany w magazynie osobistym hello hello komputera lokalnego, należy Usługa bramy toohello toogrant hello uprawnienia do odczytu:</span><span class="sxs-lookup"><span data-stu-id="d6179-2389">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="d6179-2390">Uruchom program Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="d6179-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="d6179-2391">Dodaj hello **certyfikaty** tego hello cele przystawki **komputera lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2391">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="d6179-2392">Rozwiń węzeł **certyfikaty**, **osobistych**i kliknij przycisk **certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="d6179-2393">Kliknij prawym przyciskiem myszy hello certyfikatu z magazynu osobistego hello, a następnie wybierz **wszystkie zadania**->**Zarządzaj kluczami prywatnymi...**</span><span class="sxs-lookup"><span data-stu-id="d6179-2393">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="d6179-2394">Na powitania **zabezpieczeń** , Dodaj konto użytkownika hello, pod którą jest uruchomiona usługa hosta bramy zarządzania danymi w certyfikatem toohello hello dostęp do odczytu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2394">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

<span data-ttu-id="d6179-2395">**Przykład: przy użyciu certyfikatu klienta:** to połączone usługi łączy danych fabryki tooan lokalnymi HTTP serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="d6179-2395">**Example: using client certificate:** This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="d6179-2396">Używa certyfikatu klienta, który jest zainstalowany na komputerze hello z zainstalowana brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="d6179-2396">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="d6179-2397">Przykład: przy użyciu certyfikatu klienta w pliku</span><span class="sxs-lookup"><span data-stu-id="d6179-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="d6179-2398">To połączone usługi łączy danych fabryki tooan lokalnymi HTTP serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="d6179-2398">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="d6179-2399">Za pomocą pliku certyfikatu klienta na powitania maszyny i zainstalować bramę zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="d6179-2399">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

<span data-ttu-id="d6179-2400">Aby uzyskać więcej informacji, zobacz [łącznika HTTP](data-factory-http-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="d6179-2401">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-2401">Dataset</span></span>
<span data-ttu-id="d6179-2402">toodefine HTTP zestawu danych, ustaw hello **typu** hello DataSet za**Http**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2402">toodefine a HTTP dataset, set hello **type** of hello dataset too**Http**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-2403">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2403">Property</span></span> | <span data-ttu-id="d6179-2404">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2404">Description</span></span> | <span data-ttu-id="d6179-2405">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d6179-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="d6179-2406">relativeUrl</span></span> | <span data-ttu-id="d6179-2407">Względny adres URL toohello zasób zawierający dane hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2407">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="d6179-2408">Jeśli ścieżka nie jest określona, tylko hello adresu URL określonego w definicji usługi połączone hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="d6179-2408">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="d6179-2409">tooconstruct dynamicznego adresu URL, można użyć [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md), przykład: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="d6179-2409">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="d6179-2410">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2410">No</span></span> |
| <span data-ttu-id="d6179-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="d6179-2411">requestMethod</span></span> | <span data-ttu-id="d6179-2412">Metoda HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2412">Http method.</span></span> <span data-ttu-id="d6179-2413">Dozwolone wartości to **UZYSKAĆ** lub **POST**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="d6179-2414">Nie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2414">No.</span></span> <span data-ttu-id="d6179-2415">Domyślnie jest `GET`.</span><span class="sxs-lookup"><span data-stu-id="d6179-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="d6179-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="d6179-2416">additionalHeaders</span></span> | <span data-ttu-id="d6179-2417">Dodatkowych nagłówków żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="d6179-2418">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2418">No</span></span> |
| <span data-ttu-id="d6179-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="d6179-2419">requestBody</span></span> | <span data-ttu-id="d6179-2420">Treść żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6179-2420">Body for HTTP request.</span></span> | <span data-ttu-id="d6179-2421">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2421">No</span></span> |
| <span data-ttu-id="d6179-2422">Format</span><span class="sxs-lookup"><span data-stu-id="d6179-2422">format</span></span> | <span data-ttu-id="d6179-2423">Jeśli chcesz, aby toosimply **pobrać hello danych z punktu końcowego HTTP jako — jest** bez podczas analizowania, Pomiń ten ustawienia formatu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2423">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="d6179-2424">Należy odpowiedzi hello HTTP tooparse zawartości podczas kopiowania są obsługiwane następujące typy format hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2424">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d6179-2425">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="d6179-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="d6179-2426">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2426">No</span></span> |
| <span data-ttu-id="d6179-2427">Kompresja</span><span class="sxs-lookup"><span data-stu-id="d6179-2427">compression</span></span> | <span data-ttu-id="d6179-2428">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2428">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d6179-2429">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="d6179-2430">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d6179-2431">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d6179-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d6179-2432">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2432">No</span></span> |

#### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="d6179-2433">Przykład: hello metoda GET (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="d6179-2433">Example: using hello GET (default) method</span></span>

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

#### <a name="example-using-hello-post-method"></a><span data-ttu-id="d6179-2434">Przykład: przy użyciu metody POST hello</span><span class="sxs-lookup"><span data-stu-id="d6179-2434">Example: using hello POST method</span></span>

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
<span data-ttu-id="d6179-2435">Aby uzyskać więcej informacji, zobacz [łącznika HTTP](data-factory-http-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="d6179-2436">Źródła HTTP w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="d6179-2437">Jeśli dane są kopiowane ze źródła HTTP, ustaw hello **typ źródła** hello skopiować działania zbyt**HttpSource**i określ następujące właściwości w hello **źródła** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2437">If you are copying data from a HTTP source, set hello **source type** of hello copy activity too**HttpSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-2438">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2438">Property</span></span> | <span data-ttu-id="d6179-2439">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2439">Description</span></span> | <span data-ttu-id="d6179-2440">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="d6179-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="d6179-2441">httpRequestTimeout</span></span> | <span data-ttu-id="d6179-2442">Witaj limitu czasu (TimeSpan) dla tooget żądania HTTP hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d6179-2442">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="d6179-2443">Jest tooget hello limitu czasu odpowiedzi, hello limitu czasu tooread odpowiedzi danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2443">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="d6179-2444">Nie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2444">No.</span></span> <span data-ttu-id="d6179-2445">Wartość domyślna: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="d6179-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="d6179-2446">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
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

<span data-ttu-id="d6179-2447">Aby uzyskać więcej informacji, zobacz [łącznika HTTP](data-factory-http-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="d6179-2448">OData</span><span class="sxs-lookup"><span data-stu-id="d6179-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-2449">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2449">Linked service</span></span>
<span data-ttu-id="d6179-2450">toodefine OData połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OData**i określ następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2450">toodefine an OData linked service, set hello **type** of hello linked service too**OData**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-2451">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2451">Property</span></span> | <span data-ttu-id="d6179-2452">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2452">Description</span></span> | <span data-ttu-id="d6179-2453">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2454">adres URL</span><span class="sxs-lookup"><span data-stu-id="d6179-2454">url</span></span> |<span data-ttu-id="d6179-2455">Adres URL usługi OData hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2455">Url of hello OData service.</span></span> |<span data-ttu-id="d6179-2456">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2456">Yes</span></span> |
| <span data-ttu-id="d6179-2457">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-2457">authenticationType</span></span> |<span data-ttu-id="d6179-2458">Typ uwierzytelniania używany źródło OData toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d6179-2458">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="d6179-2459">Chmury OData możliwe wartości to anonimowe, podstawowe i OAuth (Uwaga obecnie tylko pomocy technicznej usługi fabryka danych Azure OAuth opartej na usłudze Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="d6179-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="d6179-2460">Dla protokołu OData lokalnymi możliwe wartości to anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="d6179-2461">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2461">Yes</span></span> |
| <span data-ttu-id="d6179-2462">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-2462">username</span></span> |<span data-ttu-id="d6179-2463">Określ nazwę użytkownika, jeśli używasz uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="d6179-2464">Tak (tylko wtedy, gdy używasz uwierzytelniania podstawowego)</span><span class="sxs-lookup"><span data-stu-id="d6179-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="d6179-2465">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-2465">password</span></span> |<span data-ttu-id="d6179-2466">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d6179-2466">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="d6179-2467">Tak (tylko wtedy, gdy używasz uwierzytelniania podstawowego)</span><span class="sxs-lookup"><span data-stu-id="d6179-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="d6179-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="d6179-2468">authorizedCredential</span></span> |<span data-ttu-id="d6179-2469">Jeśli używasz uwierzytelniania OAuth, kliknij przycisk **autoryzacji** przycisku na powitania Kreatora kopiowania fabryki danych lub edytorze, a następnie wprowadź Twoje poświadczenia hello wartość tej właściwości będzie wygenerowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2469">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="d6179-2470">Tak (tylko wtedy, gdy używasz uwierzytelniania OAuth)</span><span class="sxs-lookup"><span data-stu-id="d6179-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="d6179-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-2471">gatewayName</span></span> |<span data-ttu-id="d6179-2472">Nazwa bramy hello hello usługi fabryka danych należy używać usługi OData lokalnymi toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d6179-2472">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="d6179-2473">Określ tylko, jeśli dane są kopiowane z lokalnego źródła OData.</span><span class="sxs-lookup"><span data-stu-id="d6179-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="d6179-2474">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="d6179-2475">Przykład — przy użyciu uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="d6179-2475">Example - Using Basic authentication</span></span>
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

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="d6179-2476">Przykład — przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="d6179-2476">Example - Using Anonymous authentication</span></span>

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

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="d6179-2477">Przykład — Windows przy użyciu uwierzytelniania dostępu do lokalnego źródła OData</span><span class="sxs-lookup"><span data-stu-id="d6179-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

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

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="d6179-2478">Przykład — przy użyciu uwierzytelniania OAuth, uzyskiwanie dostępu do chmury źródło OData</span><span class="sxs-lookup"><span data-stu-id="d6179-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="d6179-2479">Aby uzyskać więcej informacji, zobacz [łącznika OData](data-factory-odata-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="d6179-2480">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-2480">Dataset</span></span>
<span data-ttu-id="d6179-2481">toodefine zestawem danych OData hello zestaw **typu** hello DataSet za**ODataResource**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2481">toodefine an OData dataset, set hello **type** of hello dataset too**ODataResource**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-2482">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2482">Property</span></span> | <span data-ttu-id="d6179-2483">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2483">Description</span></span> | <span data-ttu-id="d6179-2484">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2485">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="d6179-2485">path</span></span> |<span data-ttu-id="d6179-2486">Toohello ścieżki OData zasobów</span><span class="sxs-lookup"><span data-stu-id="d6179-2486">Path toohello OData resource</span></span> |<span data-ttu-id="d6179-2487">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-2488">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2488">Example</span></span>

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

<span data-ttu-id="d6179-2489">Aby uzyskać więcej informacji, zobacz [łącznika OData](data-factory-odata-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="d6179-2490">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="d6179-2491">Jeśli dane są kopiowane ze źródła danych OData, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-2491">If you are copying data from an OData source, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-2492">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2492">Property</span></span> | <span data-ttu-id="d6179-2493">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2493">Description</span></span> | <span data-ttu-id="d6179-2494">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2494">Example</span></span> | <span data-ttu-id="d6179-2495">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-2496">query</span><span class="sxs-lookup"><span data-stu-id="d6179-2496">query</span></span> |<span data-ttu-id="d6179-2497">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2497">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-2498">"? $select = nazwa, opis i $top = 5"</span><span class="sxs-lookup"><span data-stu-id="d6179-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="d6179-2499">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-2500">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2500">Example</span></span>

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

<span data-ttu-id="d6179-2501">Aby uzyskać więcej informacji, zobacz [łącznika OData](data-factory-odata-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="d6179-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="d6179-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="d6179-2503">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2503">Linked service</span></span>
<span data-ttu-id="d6179-2504">toodefine ODBC połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**OnPremisesOdbc**i określ następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2504">toodefine an ODBC linked service, set hello **type** of hello linked service too**OnPremisesOdbc**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-2505">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2505">Property</span></span> | <span data-ttu-id="d6179-2506">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2506">Description</span></span> | <span data-ttu-id="d6179-2507">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2508">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="d6179-2508">connectionString</span></span> |<span data-ttu-id="d6179-2509">poświadczenie zaszyfrowana Hello poświadczeń innych niż dostępu część hello ciąg połączenia i opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="d6179-2509">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="d6179-2510">Przykłady w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="d6179-2510">See examples in hello following sections.</span></span> |<span data-ttu-id="d6179-2511">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2511">Yes</span></span> |
| <span data-ttu-id="d6179-2512">poświadczenia</span><span class="sxs-lookup"><span data-stu-id="d6179-2512">credential</span></span> |<span data-ttu-id="d6179-2513">Hello dostępu do poświadczeń część hello parametrów połączenia określonego w formacie wartość właściwości sterownika.</span><span class="sxs-lookup"><span data-stu-id="d6179-2513">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="d6179-2514">Przykład: "Uid =<user ID>; Pwd =<password>; RefreshToken =<secret refresh token>; ".</span><span class="sxs-lookup"><span data-stu-id="d6179-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="d6179-2515">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2515">No</span></span> |
| <span data-ttu-id="d6179-2516">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-2516">authenticationType</span></span> |<span data-ttu-id="d6179-2517">Typ uwierzytelniania używany Magazyn danych ODBC toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d6179-2517">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="d6179-2518">Możliwe wartości to: anonimowych, jak i podstawowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="d6179-2519">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2519">Yes</span></span> |
| <span data-ttu-id="d6179-2520">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-2520">username</span></span> |<span data-ttu-id="d6179-2521">Określ nazwę użytkownika, jeśli używasz uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="d6179-2522">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2522">No</span></span> |
| <span data-ttu-id="d6179-2523">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-2523">password</span></span> |<span data-ttu-id="d6179-2524">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d6179-2524">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="d6179-2525">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2525">No</span></span> |
| <span data-ttu-id="d6179-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-2526">gatewayName</span></span> |<span data-ttu-id="d6179-2527">Nazwa bramy hello hello usługi fabryka danych należy używać magazynu danych ODBC toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d6179-2527">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="d6179-2528">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="d6179-2529">Przykład — przy użyciu uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="d6179-2529">Example - Using Basic authentication</span></span>

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
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="d6179-2530">Przykład — użyciu zaszyfrowane poświadczenia uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="d6179-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="d6179-2531">Można szyfrować poświadczeń hello przy użyciu hello [AzureRMDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/mt603802.aspx) polecenia cmdlet (w wersji 1.0 programu Azure PowerShell) lub [AzureDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 lub starszej wersji hello Program Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d6179-2531">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="d6179-2532">Przykład: Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="d6179-2532">Example: Using Anonymous authentication</span></span>

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

<span data-ttu-id="d6179-2533">Aby uzyskać więcej informacji, zobacz [łącznika ODBC](data-factory-odbc-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-2534">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-2534">Dataset</span></span>
<span data-ttu-id="d6179-2535">toodefine zestawem danych ODBC hello zestaw **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2535">toodefine an ODBC dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-2536">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2536">Property</span></span> | <span data-ttu-id="d6179-2537">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2537">Description</span></span> | <span data-ttu-id="d6179-2538">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="d6179-2539">tableName</span></span> |<span data-ttu-id="d6179-2540">Nazwa tabeli hello w magazynie danych ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2540">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="d6179-2541">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="d6179-2542">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2542">Example</span></span>

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

<span data-ttu-id="d6179-2543">Aby uzyskać więcej informacji, zobacz [łącznika ODBC](data-factory-odbc-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="d6179-2544">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="d6179-2545">Jeśli dane są kopiowane z magazynu danych ODBC, należy ustawić hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-2545">If you are copying data from an ODBC data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-2546">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2546">Property</span></span> | <span data-ttu-id="d6179-2547">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2547">Description</span></span> | <span data-ttu-id="d6179-2548">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-2548">Allowed values</span></span> | <span data-ttu-id="d6179-2549">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-2550">query</span><span class="sxs-lookup"><span data-stu-id="d6179-2550">query</span></span> |<span data-ttu-id="d6179-2551">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2551">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-2552">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-2552">SQL query string.</span></span> <span data-ttu-id="d6179-2553">Na przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="d6179-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="d6179-2554">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-2555">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2555">Example</span></span>

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

<span data-ttu-id="d6179-2556">Aby uzyskać więcej informacji, zobacz [łącznika ODBC](data-factory-odbc-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="d6179-2557">SalesForce</span><span class="sxs-lookup"><span data-stu-id="d6179-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="d6179-2558">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2558">Linked service</span></span>
<span data-ttu-id="d6179-2559">toodefine Salesforce połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**Salesforce**i określ następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2559">toodefine a Salesforce linked service, set hello **type** of hello linked service too**Salesforce**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-2560">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2560">Property</span></span> | <span data-ttu-id="d6179-2561">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2561">Description</span></span> | <span data-ttu-id="d6179-2562">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="d6179-2563">environmentUrl</span></span> | <span data-ttu-id="d6179-2564">Określ wystąpienie adres URL usługi Salesforce hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2564">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="d6179-2565">-Domyślna to "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="d6179-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="d6179-2566">-toocopy danych z piaskownicy, określ "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="d6179-2566">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="d6179-2567">-toocopy dane z domeny niestandardowej, określić, na przykład "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="d6179-2567">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="d6179-2568">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2568">No</span></span> |
| <span data-ttu-id="d6179-2569">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-2569">username</span></span> |<span data-ttu-id="d6179-2570">Określ nazwę użytkownika dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2570">Specify a user name for hello user account.</span></span> |<span data-ttu-id="d6179-2571">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2571">Yes</span></span> |
| <span data-ttu-id="d6179-2572">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-2572">password</span></span> |<span data-ttu-id="d6179-2573">Określ hasło dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2573">Specify a password for hello user account.</span></span> |<span data-ttu-id="d6179-2574">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2574">Yes</span></span> |
| <span data-ttu-id="d6179-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="d6179-2575">securityToken</span></span> |<span data-ttu-id="d6179-2576">Określ tokenu zabezpieczającego dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2576">Specify a security token for hello user account.</span></span> <span data-ttu-id="d6179-2577">Zobacz [uzyskać token zabezpieczeń](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) instrukcje na temat tooreset/get tokenu zabezpieczającego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="d6179-2578">Ogólnie rzecz biorąc, zobacz toolearn o tokeny zabezpieczające [zabezpieczeń i hello interfejsu API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="d6179-2578">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="d6179-2579">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-2580">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2580">Example</span></span>

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

<span data-ttu-id="d6179-2581">Aby uzyskać więcej informacji, zobacz [łącznika usług Salesforce](data-factory-salesforce-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-2582">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-2582">Dataset</span></span>
<span data-ttu-id="d6179-2583">toodefine Salesforce zestawu danych, ustaw hello **typu** hello DataSet za**RelationalTable**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2583">toodefine a Salesforce dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-2584">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2584">Property</span></span> | <span data-ttu-id="d6179-2585">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2585">Description</span></span> | <span data-ttu-id="d6179-2586">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="d6179-2587">tableName</span></span> |<span data-ttu-id="d6179-2588">Nazwa tabeli hello w usłudze Salesforce.</span><span class="sxs-lookup"><span data-stu-id="d6179-2588">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="d6179-2589">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-2590">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2590">Example</span></span>

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

<span data-ttu-id="d6179-2591">Aby uzyskać więcej informacji, zobacz [łącznika usług Salesforce](data-factory-salesforce-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="d6179-2592">Relacyjnego źródła w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="d6179-2593">Jeśli dane są kopiowane z usług Salesforce, ustaw hello **typ źródła** hello skopiować działania zbyt**RelationalSource**i określ następujące właściwości w hello **źródła** sekcja:</span><span class="sxs-lookup"><span data-stu-id="d6179-2593">If you are copying data from Salesforce, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="d6179-2594">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2594">Property</span></span> | <span data-ttu-id="d6179-2595">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2595">Description</span></span> | <span data-ttu-id="d6179-2596">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="d6179-2596">Allowed values</span></span> | <span data-ttu-id="d6179-2597">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d6179-2598">query</span><span class="sxs-lookup"><span data-stu-id="d6179-2598">query</span></span> |<span data-ttu-id="d6179-2599">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2599">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d6179-2600">Zapytania SQL 92 lub [Salesforce obiektu Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) zapytania.</span><span class="sxs-lookup"><span data-stu-id="d6179-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="d6179-2601">Przykład: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="d6179-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="d6179-2602">Nie (jeśli hello **tableName** z hello **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="d6179-2602">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-2603">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
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
> <span data-ttu-id="d6179-2604">Witaj "__c" część hello Nazwa interfejsu API jest wymagany dla dowolnych niestandardowych obiektów.</span><span class="sxs-lookup"><span data-stu-id="d6179-2604">hello "__c" part of hello API Name is needed for any custom object.</span></span>

<span data-ttu-id="d6179-2605">Aby uzyskać więcej informacji, zobacz [łącznika usług Salesforce](data-factory-salesforce-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="d6179-2606">Dane sieci Web</span><span class="sxs-lookup"><span data-stu-id="d6179-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="d6179-2607">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2607">Linked service</span></span>
<span data-ttu-id="d6179-2608">toodefine sieci Web połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**sieci Web**i określ następujące właściwości w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2608">toodefine a Web linked service, set hello **type** of hello linked service too**Web**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-2609">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2609">Property</span></span> | <span data-ttu-id="d6179-2610">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2610">Description</span></span> | <span data-ttu-id="d6179-2611">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2612">Url</span><span class="sxs-lookup"><span data-stu-id="d6179-2612">Url</span></span> |<span data-ttu-id="d6179-2613">Adres URL źródła toohello w sieci Web</span><span class="sxs-lookup"><span data-stu-id="d6179-2613">URL toohello Web source</span></span> |<span data-ttu-id="d6179-2614">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2614">Yes</span></span> |
| <span data-ttu-id="d6179-2615">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="d6179-2615">authenticationType</span></span> |<span data-ttu-id="d6179-2616">Anonimowe.</span><span class="sxs-lookup"><span data-stu-id="d6179-2616">Anonymous.</span></span> |<span data-ttu-id="d6179-2617">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="d6179-2618">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2618">Example</span></span>


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

<span data-ttu-id="d6179-2619">Aby uzyskać więcej informacji, zobacz [łącznika tabeli Web](data-factory-web-table-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="d6179-2620">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="d6179-2620">Dataset</span></span>
<span data-ttu-id="d6179-2621">toodefine zestawu danych w sieci Web, zestaw hello **typu** hello DataSet za**tabeli WebTable**i określ następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2621">toodefine a Web dataset, set hello **type** of hello dataset too**WebTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="d6179-2622">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2622">Property</span></span> | <span data-ttu-id="d6179-2623">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2623">Description</span></span> | <span data-ttu-id="d6179-2624">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d6179-2625">type</span><span class="sxs-lookup"><span data-stu-id="d6179-2625">type</span></span> |<span data-ttu-id="d6179-2626">Typ hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2626">type of hello dataset.</span></span> <span data-ttu-id="d6179-2627">musi być ustawiona zbyt**tabeli WebTable**</span><span class="sxs-lookup"><span data-stu-id="d6179-2627">must be set too**WebTable**</span></span> |<span data-ttu-id="d6179-2628">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2628">Yes</span></span> |
| <span data-ttu-id="d6179-2629">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="d6179-2629">path</span></span> |<span data-ttu-id="d6179-2630">Względny adres URL toohello zasób zawiera tabelę hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2630">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="d6179-2631">Nie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2631">No.</span></span> <span data-ttu-id="d6179-2632">Jeśli ścieżka nie jest określona, tylko hello adresu URL określonego w definicji usługi połączone hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="d6179-2632">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="d6179-2633">Indeks</span><span class="sxs-lookup"><span data-stu-id="d6179-2633">index</span></span> |<span data-ttu-id="d6179-2634">Indeks Hello hello tabeli w zasobie hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2634">hello index of hello table in hello resource.</span></span> <span data-ttu-id="d6179-2635">Zobacz [Get indeksu tabeli na stronie HTML](#get-index-of-a-table-in-an-html-page) sekcji kroki toogetting indeksu tabeli na stronie HTML.</span><span class="sxs-lookup"><span data-stu-id="d6179-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="d6179-2636">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="d6179-2637">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2637">Example</span></span>

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

<span data-ttu-id="d6179-2638">Aby uzyskać więcej informacji, zobacz [łącznika tabeli Web](data-factory-web-table-connector.md#dataset-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="d6179-2639">Źródło w sieci Web w przypadku działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="d6179-2640">Jeśli dane są kopiowane z tabeli sieci web, należy ustawić hello **typ źródła** hello skopiować działania zbyt**WebSource**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2640">If you are copying data from a web table, set hello **source type** of hello copy activity too**WebSource**.</span></span> <span data-ttu-id="d6179-2641">Obecnie, gdy hello źródła w przypadku działania kopiowania jest typu **WebSource**, są obsługiwane żadne dodatkowe właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-2641">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="d6179-2642">Przykład</span><span class="sxs-lookup"><span data-stu-id="d6179-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
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

<span data-ttu-id="d6179-2643">Aby uzyskać więcej informacji, zobacz [łącznika tabeli Web](data-factory-web-table-connector.md#copy-activity-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="d6179-2644">ŚRODOWISKA OBLICZENIOWE</span><span class="sxs-lookup"><span data-stu-id="d6179-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="d6179-2645">Witaj poniższej tabeli wymieniono hello środowiska obliczeniowe obsługiwane przez fabrykę danych oraz hello działania przekształcania, które można uruchomić na nich.</span><span class="sxs-lookup"><span data-stu-id="d6179-2645">hello following table lists hello compute environments supported by Data Factory and hello transformation activities that can run on them.</span></span> <span data-ttu-id="d6179-2646">Kliknij łącze hello hello obliczania jesteś zainteresowani schematów JSON hello toosee dla połączonej usługi toolink on tooa fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2646">Click hello link for hello compute you are interested in toosee hello JSON schemas for linked service toolink it tooa data factory.</span></span> 

| <span data-ttu-id="d6179-2647">Środowisko obliczeniowe</span><span class="sxs-lookup"><span data-stu-id="d6179-2647">Compute environment</span></span> | <span data-ttu-id="d6179-2648">Działania</span><span class="sxs-lookup"><span data-stu-id="d6179-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="d6179-2649">[Klaster usługi HDInsight na żądanie](#on-demand-azure-hdinsight-cluster) lub [klastrem usługi HDInsight](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="d6179-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="d6179-2650">[Działania niestandardowego .NET](#net-custom-activity), [Hive działania](#hdinsight-hive-activity), [wieprzowa działania] (#hdinsight-pig działania [działania MapReduce](#hdinsight-mapreduce-activity), [przesyłanie strumieniowe działania Hadoop](#hdinsight-streaming-activityd), [Spark działania](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="d6179-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="d6179-2651">Partia zadań Azure</span><span class="sxs-lookup"><span data-stu-id="d6179-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="d6179-2652">Niestandardowe działanie platformy .NET</span><span class="sxs-lookup"><span data-stu-id="d6179-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="d6179-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d6179-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="d6179-2654">[Działanie wykonywania wsadowego uczenia maszynowego](#machine-learning-batch-execution-activity), [działanie aktualizacji zasobu uczenia maszynowego](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="d6179-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="d6179-2655">Usługi Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d6179-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="d6179-2656">Język U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d6179-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="d6179-2657">[Baza danych Azure SQL](#azure-sql-database-1), [magazyn danych Azure SQL](#azure-sql-data-warehouse-1), [programu SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="d6179-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="d6179-2658">Procedura składowana</span><span class="sxs-lookup"><span data-stu-id="d6179-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="d6179-2659">Klaster Azure HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="d6179-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="d6179-2660">Witaj usługi fabryka danych Azure może automatycznie tworzyć opartych na systemie Windows/Linux na żądanie HDInsight klastra tooprocess danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2660">hello Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster tooprocess data.</span></span> <span data-ttu-id="d6179-2661">klaster Hello jest tworzony w tym samym regionie co konto magazynu hello (właściwość linkedServiceName w hello JSON) skojarzone z klastrem hello hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2661">hello cluster is created in hello same region as hello storage account (linkedServiceName property in hello JSON) associated with hello cluster.</span></span> <span data-ttu-id="d6179-2662">Możesz uruchomić powitania po transformacji działania w tej połączonej usługi: [działania niestandardowego .NET](#net-custom-activity), [Hive działania](#hdinsight-hive-activity), [wieprzowa działania] (#hdinsight-pig działania [działania MapReduce ](#hdinsight-mapreduce-activity), [Przesyłanie strumieniowe działania Hadoop](#hdinsight-streaming-activityd), [Spark działania](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="d6179-2662">You can run hello following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="d6179-2663">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2663">Linked service</span></span> 
<span data-ttu-id="d6179-2664">Hello w poniższej tabeli opisano hello właściwości używane w definicji Azure JSON hello usługi HDInsight połączony na żądanie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2664">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="d6179-2665">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2665">Property</span></span> | <span data-ttu-id="d6179-2666">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2666">Description</span></span> | <span data-ttu-id="d6179-2667">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2668">type</span><span class="sxs-lookup"><span data-stu-id="d6179-2668">type</span></span> |<span data-ttu-id="d6179-2669">właściwości typu Hello należy ustawić wartość zbyt**HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2669">hello type property should be set too**HDInsightOnDemand**.</span></span> |<span data-ttu-id="d6179-2670">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2670">Yes</span></span> |
| <span data-ttu-id="d6179-2671">Wartość ClusterSize</span><span class="sxs-lookup"><span data-stu-id="d6179-2671">clusterSize</span></span> |<span data-ttu-id="d6179-2672">Liczba węzłów procesu roboczego/danych w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2672">Number of worker/data nodes in hello cluster.</span></span> <span data-ttu-id="d6179-2673">klaster usługi HDInsight Hello jest tworzony z głównymi węzłami 2 oraz hello liczba węzłów procesu roboczego, które określisz dla tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-2673">hello HDInsight cluster is created with 2 head nodes along with hello number of worker nodes you specify for this property.</span></span> <span data-ttu-id="d6179-2674">węzły Hello mają rozmiar Standard_D3, który ma 4 rdzenie, więc klastra z węzłem procesu roboczego 4 przyjmuje 24 rdzenie (4\*4 = 16 rdzenie dla węzłów procesu roboczego, a także 2\*rdzenie 4 = 8 dla węzłów głównych).</span><span class="sxs-lookup"><span data-stu-id="d6179-2674">hello nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="d6179-2675">Zobacz [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) szczegółowe informacje o hello Standard_D3 warstwy.</span><span class="sxs-lookup"><span data-stu-id="d6179-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about hello Standard_D3 tier.</span></span> |<span data-ttu-id="d6179-2676">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2676">Yes</span></span> |
| <span data-ttu-id="d6179-2677">wartość TimeToLive</span><span class="sxs-lookup"><span data-stu-id="d6179-2677">timetolive</span></span> |<span data-ttu-id="d6179-2678">Witaj dozwolony czas bezczynności klastra usługi HDInsight na żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2678">hello allowed idle time for hello on-demand HDInsight cluster.</span></span> <span data-ttu-id="d6179-2679">Określa, jak długo klastra usługi HDInsight na żądanie hello pozostaje aktywne po zakończeniu działania uruchamiania, jeśli w klastrze hello nie ma żadnych aktywnych działań.</span><span class="sxs-lookup"><span data-stu-id="d6179-2679">Specifies how long hello on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in hello cluster.</span></span><br/><br/><span data-ttu-id="d6179-2680">Na przykład, jeśli działanie Uruchom przyjmuje 6 minut i timetolive jest too5 minut, pozostaje klastra hello aktywności 5 minut po hello 6 minut przetwarzania uruchamiania działania hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2680">For example, if an activity run takes 6 minutes and timetolive is set too5 minutes, hello cluster stays alive for 5 minutes after hello 6 minutes of processing hello activity run.</span></span> <span data-ttu-id="d6179-2681">Jeśli inny uruchamiania działania jest wykonywane z okna 6 minut hello, jednak jest przetwarzany przez hello tego samego klastra.</span><span class="sxs-lookup"><span data-stu-id="d6179-2681">If another activity run is executed with hello 6 minutes window, it is processed by hello same cluster.</span></span><br/><br/><span data-ttu-id="d6179-2682">Tworzenie klastra usługi HDInsight na żądanie jest kosztowna operacja (może to potrwać pewien czas), więc użyć tego ustawienia jako wydajności wymagane tooimprove fabryki danych przez ponowne użycie klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed tooimprove performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="d6179-2683">Jeśli ustawisz too0 wartość timetolive klaster hello jest usunięty jak działanie hello uruchomić w przetworzone.</span><span class="sxs-lookup"><span data-stu-id="d6179-2683">If you set timetolive value too0, hello cluster is deleted as soon as hello activity run in processed.</span></span> <span data-ttu-id="d6179-2684">Na powitania drugiej strony, jeśli ustawisz wysokiej wartości, hello klastra może pozostać bezczynny, co niepotrzebnie wysokich kosztów.</span><span class="sxs-lookup"><span data-stu-id="d6179-2684">On hello other hand, if you set a high value, hello cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="d6179-2685">Dlatego jest ważne, aby ustawić odpowiednią wartość hello na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="d6179-2685">Therefore, it is important that you set hello appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="d6179-2686">Można udostępniać wielu potoki hello tego samego wystąpienia klastra usługi HDInsight na żądanie hello, jeśli wartość właściwości timetolive hello jest skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="d6179-2686">Multiple pipelines can share hello same instance of hello on-demand HDInsight cluster if hello timetolive property value is appropriately set</span></span> |<span data-ttu-id="d6179-2687">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2687">Yes</span></span> |
| <span data-ttu-id="d6179-2688">Wersja</span><span class="sxs-lookup"><span data-stu-id="d6179-2688">version</span></span> |<span data-ttu-id="d6179-2689">Wersja klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2689">Version of hello HDInsight cluster.</span></span> <span data-ttu-id="d6179-2690">Aby uzyskać więcej informacji, zobacz [obsługiwane wersje usługi HDInsight w fabryce danych Azure](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="d6179-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="d6179-2691">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2691">No</span></span> |
| <span data-ttu-id="d6179-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d6179-2692">linkedServiceName</span></span> |<span data-ttu-id="d6179-2693">Usługa Azure Storage połączone toobe usługi używane przez klaster na żądanie hello do przechowywania i przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2693">Azure Storage linked service toobe used by hello on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="d6179-2694">Obecnie nie można utworzyć klastra usługi HDInsight na żądanie, korzystającą z usługi Azure Data Lake Store jako hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as hello storage.</span></span> <span data-ttu-id="d6179-2695">Jeśli chcesz toostore hello dane z usługi HDInsight przetwarzania w usłudze Azure Data Lake Store, użyj danych hello toocopy działanie kopiowania z toohello magazynu obiektów Blob Azure hello Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d6179-2695">If you want toostore hello result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity toocopy hello data from hello Azure Blob Storage toohello Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="d6179-2696">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2696">Yes</span></span> |
| <span data-ttu-id="d6179-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="d6179-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="d6179-2698">Określa, że dodatkowe konta magazynu dla hello HDInsight połączonej usługi, dzięki czemu usługi fabryka danych hello można zarejestrować je w Twoim imieniu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2698">Specifies additional storage accounts for hello HDInsight linked service so that hello Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="d6179-2699">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2699">No</span></span> |
| <span data-ttu-id="d6179-2700">osType</span><span class="sxs-lookup"><span data-stu-id="d6179-2700">osType</span></span> |<span data-ttu-id="d6179-2701">Typ systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2701">Type of operating system.</span></span> <span data-ttu-id="d6179-2702">Dozwolone wartości to: (domyślnie) systemu Windows i Linux</span><span class="sxs-lookup"><span data-stu-id="d6179-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="d6179-2703">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2703">No</span></span> |
| <span data-ttu-id="d6179-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d6179-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="d6179-2705">Nazwa Hello Azure SQL połączone usługi bazy danych HCatalog toohello punktu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2705">hello name of Azure SQL linked service that point toohello HCatalog database.</span></span> <span data-ttu-id="d6179-2706">klaster usługi HDInsight na żądanie Hello jest tworzona przy użyciu bazy danych Azure SQL hello jako hello potrzeby magazynu metadanych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2706">hello on-demand HDInsight cluster is created by using hello Azure SQL database as hello metastore.</span></span> |<span data-ttu-id="d6179-2707">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="d6179-2708">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-2708">JSON example</span></span>
<span data-ttu-id="d6179-2709">powitania po JSON definiuje opartych na systemie Linux usługi HDInsight połączony na żądanie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2709">hello following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="d6179-2710">Witaj usługi fabryka danych automatycznie tworzy **opartych na systemie Linux** klastra usługi HDInsight podczas przetwarzania wycinka danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2710">hello Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

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

<span data-ttu-id="d6179-2711">Aby uzyskać więcej informacji, zobacz [obliczeniowe połączonych usług](data-factory-compute-linked-services.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="d6179-2712">Istniejący klaster Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6179-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="d6179-2713">Klaster usługi HDInsight można utworzyć tooregister usługi Azure HDInsight połączone z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2713">You can create an Azure HDInsight linked service tooregister your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="d6179-2714">Możesz uruchomić hello następujące działania przekształcania danych na tej połączonej usługi: [działania niestandardowego .NET](#net-custom-activity), [Hive działania](#hdinsight-hive-activity), [wieprzowa działania] (#hdinsight-pig działania [MapReduce działanie](#hdinsight-mapreduce-activity), [przesyłanie strumieniowe działania Hadoop](#hdinsight-streaming-activityd), [Spark działania](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="d6179-2714">You can run hello following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="d6179-2715">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2715">Linked service</span></span>
<span data-ttu-id="d6179-2716">w poniższej tabeli Hello zawiera opisy hello właściwości używane w definicji Azure JSON hello usługi Azure HDInsight połączone.</span><span class="sxs-lookup"><span data-stu-id="d6179-2716">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="d6179-2717">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2717">Property</span></span> | <span data-ttu-id="d6179-2718">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2718">Description</span></span> | <span data-ttu-id="d6179-2719">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2720">type</span><span class="sxs-lookup"><span data-stu-id="d6179-2720">type</span></span> |<span data-ttu-id="d6179-2721">właściwości typu Hello należy ustawić wartość zbyt**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2721">hello type property should be set too**HDInsight**.</span></span> |<span data-ttu-id="d6179-2722">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2722">Yes</span></span> |
| <span data-ttu-id="d6179-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="d6179-2723">clusterUri</span></span> |<span data-ttu-id="d6179-2724">Witaj URI hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6179-2724">hello URI of hello HDInsight cluster.</span></span> |<span data-ttu-id="d6179-2725">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2725">Yes</span></span> |
| <span data-ttu-id="d6179-2726">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-2726">username</span></span> |<span data-ttu-id="d6179-2727">Określ nazwę hello toobe użytkownika hello używanych tooconnect tooan istniejącym klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6179-2727">Specify hello name of hello user toobe used tooconnect tooan existing HDInsight cluster.</span></span> |<span data-ttu-id="d6179-2728">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2728">Yes</span></span> |
| <span data-ttu-id="d6179-2729">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-2729">password</span></span> |<span data-ttu-id="d6179-2730">Określ hasło dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2730">Specify password for hello user account.</span></span> |<span data-ttu-id="d6179-2731">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2731">Yes</span></span> |
| <span data-ttu-id="d6179-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d6179-2732">linkedServiceName</span></span> | <span data-ttu-id="d6179-2733">Nazwa hello połączoną usługą magazynu Azure odwołujące się do magazynu obiektów blob Azure toohello używana przez hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6179-2733">Name of hello Azure Storage linked service that refers toohello Azure blob storage used by hello HDInsight cluster.</span></span> <p><span data-ttu-id="d6179-2734">Obecnie nie można określić, czy usługa Azure Data Lake Store połączonej usługi dla tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="d6179-2735">Jeśli klaster usługi HDInsight hello ma toohello dostępu do usługi Data Lake Store może dostęp do danych w hello Azure Data Lake Store z skryptów usługi Hive/Pig.</span><span class="sxs-lookup"><span data-stu-id="d6179-2735">You may access data in hello Azure Data Lake Store from Hive/Pig scripts if hello HDInsight cluster has access toohello Data Lake Store.</span></span> </p>  |<span data-ttu-id="d6179-2736">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2736">Yes</span></span> |

<span data-ttu-id="d6179-2737">Dla wersji obsługiwane klastrów usługi HDInsight, zobacz [obsługiwane wersje HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="d6179-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="d6179-2738">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-2738">JSON example</span></span>

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

## <a name="azure-batch"></a><span data-ttu-id="d6179-2739">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="d6179-2739">Azure Batch</span></span>
<span data-ttu-id="d6179-2740">Tooregister usługi partia zadań Azure połączone można utworzyć puli partii maszynach wirtualnych (VM) przy użyciu fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2740">You can create an Azure Batch linked service tooregister a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="d6179-2741">Możesz uruchomić niestandardowych działań platformy .NET przy użyciu partii zadań Azure lub usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6179-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="d6179-2742">Można uruchomić [działania niestandardowego .NET](#net-custom-activity) na tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="d6179-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="d6179-2743">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2743">Linked service</span></span>
<span data-ttu-id="d6179-2744">Hello w poniższej tabeli opisano właściwości hello używane w definicji Azure JSON hello usługi partia zadań Azure połączone.</span><span class="sxs-lookup"><span data-stu-id="d6179-2744">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="d6179-2745">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2745">Property</span></span> | <span data-ttu-id="d6179-2746">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2746">Description</span></span> | <span data-ttu-id="d6179-2747">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2748">type</span><span class="sxs-lookup"><span data-stu-id="d6179-2748">type</span></span> |<span data-ttu-id="d6179-2749">właściwości typu Hello należy ustawić wartość zbyt**AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2749">hello type property should be set too**AzureBatch**.</span></span> |<span data-ttu-id="d6179-2750">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2750">Yes</span></span> |
| <span data-ttu-id="d6179-2751">Nazwa konta</span><span class="sxs-lookup"><span data-stu-id="d6179-2751">accountName</span></span> |<span data-ttu-id="d6179-2752">Nazwa konta usługi partia zadań Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2752">Name of hello Azure Batch account.</span></span> |<span data-ttu-id="d6179-2753">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2753">Yes</span></span> |
| <span data-ttu-id="d6179-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="d6179-2754">accessKey</span></span> |<span data-ttu-id="d6179-2755">Klucz dostępu dla konta usługi partia zadań Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2755">Access key for hello Azure Batch account.</span></span> |<span data-ttu-id="d6179-2756">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2756">Yes</span></span> |
| <span data-ttu-id="d6179-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="d6179-2757">poolName</span></span> |<span data-ttu-id="d6179-2758">Nazwa puli hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2758">Name of hello pool of virtual machines.</span></span> |<span data-ttu-id="d6179-2759">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2759">Yes</span></span> |
| <span data-ttu-id="d6179-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d6179-2760">linkedServiceName</span></span> |<span data-ttu-id="d6179-2761">Nazwa hello połączoną usługą magazynu Azure skojarzony z tą usługą partii zadań Azure połączone.</span><span class="sxs-lookup"><span data-stu-id="d6179-2761">Name of hello Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="d6179-2762">Tej połączonej usługi jest używany na potrzeby przemieszczania plików wymagane działania hello toorun i przechowywanie dzienniki wykonywania hello działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-2762">This linked service is used for staging files required toorun hello activity and storing hello activity execution logs.</span></span> |<span data-ttu-id="d6179-2763">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="d6179-2764">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-2764">JSON example</span></span>

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

## <a name="azure-machine-learning"></a><span data-ttu-id="d6179-2765">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d6179-2765">Azure Machine Learning</span></span>
<span data-ttu-id="d6179-2766">Możesz utworzyć tooregister usługi Azure Machine Learning połączone punktu końcowego z fabryką danych oceniania partii uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2766">You create an Azure Machine Learning linked service tooregister a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="d6179-2767">Dwa przekształcania działań, które można uruchomić na tym połączonej usługi: [działanie wykonywania wsadowego przez Machine Learning](#machine-learning-batch-execution-activity), [Machine Learning aktualizacji zasobów działania](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="d6179-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="d6179-2768">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2768">Linked service</span></span>
<span data-ttu-id="d6179-2769">Hello w poniższej tabeli opisano właściwości hello używane w definicji hello Azure JSON usługi Azure Machine Learning połączone.</span><span class="sxs-lookup"><span data-stu-id="d6179-2769">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="d6179-2770">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2770">Property</span></span> | <span data-ttu-id="d6179-2771">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2771">Description</span></span> | <span data-ttu-id="d6179-2772">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2773">Typ</span><span class="sxs-lookup"><span data-stu-id="d6179-2773">Type</span></span> |<span data-ttu-id="d6179-2774">powinien mieć ustawioną właściwość type Hello: **uczenie maszynowe Azure**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2774">hello type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="d6179-2775">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2775">Yes</span></span> |
| <span data-ttu-id="d6179-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="d6179-2776">mlEndpoint</span></span> |<span data-ttu-id="d6179-2777">Witaj URL wsadowego oceniania.</span><span class="sxs-lookup"><span data-stu-id="d6179-2777">hello batch scoring URL.</span></span> |<span data-ttu-id="d6179-2778">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2778">Yes</span></span> |
| <span data-ttu-id="d6179-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="d6179-2779">apiKey</span></span> |<span data-ttu-id="d6179-2780">Witaj opublikowane interfejs API modelu obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2780">hello published workspace model’s API.</span></span> |<span data-ttu-id="d6179-2781">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="d6179-2782">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-2782">JSON example</span></span>

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

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="d6179-2783">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d6179-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="d6179-2784">Możesz utworzyć **Azure Data Lake Analytics** połączone toolink usługi fabryki danych Azure tooan usługi Azure Data Lake Analytics obliczeń przed użyciem hello [działanie U-SQL w programie Data Lake Analytics](data-factory-usql-activity.md) w potoku .</span><span class="sxs-lookup"><span data-stu-id="d6179-2784">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory before using hello [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="d6179-2785">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2785">Linked service</span></span>

<span data-ttu-id="d6179-2786">w poniższej tabeli Hello zawiera opisy hello właściwości używane w definicji JSON hello usługi Azure Data Lake Analytics połączone.</span><span class="sxs-lookup"><span data-stu-id="d6179-2786">hello following table provides descriptions for hello properties used in hello JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="d6179-2787">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2787">Property</span></span> | <span data-ttu-id="d6179-2788">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2788">Description</span></span> | <span data-ttu-id="d6179-2789">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2790">Typ</span><span class="sxs-lookup"><span data-stu-id="d6179-2790">Type</span></span> |<span data-ttu-id="d6179-2791">powinien mieć ustawioną właściwość type Hello: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2791">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="d6179-2792">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2792">Yes</span></span> |
| <span data-ttu-id="d6179-2793">Nazwa konta</span><span class="sxs-lookup"><span data-stu-id="d6179-2793">accountName</span></span> |<span data-ttu-id="d6179-2794">Nazwa konta usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="d6179-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="d6179-2795">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2795">Yes</span></span> |
| <span data-ttu-id="d6179-2796">Element dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="d6179-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="d6179-2797">Identyfikator URI, usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="d6179-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="d6179-2798">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2798">No</span></span> |
| <span data-ttu-id="d6179-2799">Autoryzacji</span><span class="sxs-lookup"><span data-stu-id="d6179-2799">authorization</span></span> |<span data-ttu-id="d6179-2800">Kod autoryzacji jest automatycznie pobierany po kliknięciu przycisku **autoryzacji** przycisk hello Edytor fabryki danych i kończenie hello operacji logowania OAuth.</span><span class="sxs-lookup"><span data-stu-id="d6179-2800">Authorization code is automatically retrieved after clicking **Authorize** button in hello Data Factory Editor and completing hello OAuth login.</span></span> |<span data-ttu-id="d6179-2801">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2801">Yes</span></span> |
| <span data-ttu-id="d6179-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="d6179-2802">subscriptionId</span></span> |<span data-ttu-id="d6179-2803">Identyfikator subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d6179-2803">Azure subscription id</span></span> |<span data-ttu-id="d6179-2804">Nie (Jeśli nie określono subskrypcji hello jest używana fabryka danych).</span><span class="sxs-lookup"><span data-stu-id="d6179-2804">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="d6179-2805">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="d6179-2805">resourceGroupName</span></span> |<span data-ttu-id="d6179-2806">Nazwa grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d6179-2806">Azure resource group name</span></span> |<span data-ttu-id="d6179-2807">Nie (Jeśli nie określono grupy zasobów hello jest używana fabryka danych).</span><span class="sxs-lookup"><span data-stu-id="d6179-2807">No (If not specified, resource group of hello data factory is used).</span></span> |
| <span data-ttu-id="d6179-2808">Identyfikator sesji</span><span class="sxs-lookup"><span data-stu-id="d6179-2808">sessionId</span></span> |<span data-ttu-id="d6179-2809">Identyfikator sesji z sesji autoryzacji OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2809">session id from hello OAuth authorization session.</span></span> <span data-ttu-id="d6179-2810">Każdy identyfikator sesji jest unikatowy i mogą być użyte tylko raz.</span><span class="sxs-lookup"><span data-stu-id="d6179-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="d6179-2811">Gdy używasz hello Edytor fabryki danych, ten identyfikator jest generowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2811">When you use hello Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="d6179-2812">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="d6179-2813">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-2813">JSON example</span></span>
<span data-ttu-id="d6179-2814">Poniższy przykład Hello zawiera definicję JSON dla usługi Azure Data Lake Analytics połączone.</span><span class="sxs-lookup"><span data-stu-id="d6179-2814">hello following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

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

## <a name="azure-sql-database"></a><span data-ttu-id="d6179-2815">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d6179-2815">Azure SQL Database</span></span>
<span data-ttu-id="d6179-2816">Tworzenie usługi SQL Azure połączone i korzystania z niego hello [działania dotyczącego procedury składowanej](#stored-procedure-activity) tooinvoke procedury składowanej z potoku fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2816">You create an Azure SQL linked service and use it with hello [Stored Procedure Activity](#stored-procedure-activity) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="d6179-2817">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2817">Linked service</span></span>
<span data-ttu-id="d6179-2818">toodefine bazy danych SQL Azure połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureSqlDatabase**i określ następujące właściwości w hello **typeProperties**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2818">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-2819">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2819">Property</span></span> | <span data-ttu-id="d6179-2820">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2820">Description</span></span> | <span data-ttu-id="d6179-2821">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2822">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="d6179-2822">connectionString</span></span> |<span data-ttu-id="d6179-2823">Określ informacje niezbędne wystąpienie bazy danych SQL Azure toohello tooconnect hello właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="d6179-2823">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="d6179-2824">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="d6179-2825">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-2825">JSON example</span></span>

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

<span data-ttu-id="d6179-2826">Zobacz [Łącznik usług SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) artykułu, aby uzyskać szczegółowe informacje o tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="d6179-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="d6179-2827">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d6179-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d6179-2828">Tworzenie usługi Azure SQL Data Warehouse połączone i korzystania z niego hello [działania dotyczącego procedury składowanej](data-factory-stored-proc-activity.md) tooinvoke procedury składowanej z potoku fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2828">You create an Azure SQL Data Warehouse linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="d6179-2829">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2829">Linked service</span></span>
<span data-ttu-id="d6179-2830">toodefine Azure SQL Data Warehouse połączonej usługi, zestaw hello **typu** z hello połączona usługa zbyt**AzureSqlDW**i określ następujące właściwości w hello **typeProperties**sekcji:</span><span class="sxs-lookup"><span data-stu-id="d6179-2830">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="d6179-2831">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2831">Property</span></span> | <span data-ttu-id="d6179-2832">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2832">Description</span></span> | <span data-ttu-id="d6179-2833">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2834">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="d6179-2834">connectionString</span></span> |<span data-ttu-id="d6179-2835">Określ informacje potrzebne wystąpienia usługi Azure SQL Data Warehouse toohello tooconnect hello właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="d6179-2835">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="d6179-2836">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="d6179-2837">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-2837">JSON example</span></span>

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

<span data-ttu-id="d6179-2838">Aby uzyskać więcej informacji, zobacz [łącznika usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="d6179-2839">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="d6179-2839">SQL Server</span></span> 
<span data-ttu-id="d6179-2840">Tworzenie usługi SQL Server połączone i korzystania z niego hello [działania dotyczącego procedury składowanej](data-factory-stored-proc-activity.md) tooinvoke procedury składowanej z potoku fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2840">You create a SQL Server linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="d6179-2841">Połączona usługa</span><span class="sxs-lookup"><span data-stu-id="d6179-2841">Linked service</span></span>
<span data-ttu-id="d6179-2842">Tworzenie połączonej usługi typu **OnPremisesSqlServer** toolink fabrykę danych tooa bazy danych programu SQL Server lokalne.</span><span class="sxs-lookup"><span data-stu-id="d6179-2842">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="d6179-2843">Hello w poniższej tabeli przedstawiono opis dla usługi programu SQL Server połączone określonych lokalnych tooon elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="d6179-2843">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="d6179-2844">Witaj w poniższej tabeli przedstawiono opis dla określonych tooSQL elementów JSON usługi Serwer połączony.</span><span class="sxs-lookup"><span data-stu-id="d6179-2844">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="d6179-2845">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2845">Property</span></span> | <span data-ttu-id="d6179-2846">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2846">Description</span></span> | <span data-ttu-id="d6179-2847">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2848">type</span><span class="sxs-lookup"><span data-stu-id="d6179-2848">type</span></span> |<span data-ttu-id="d6179-2849">powinien mieć ustawioną właściwość type Hello: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2849">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="d6179-2850">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2850">Yes</span></span> |
| <span data-ttu-id="d6179-2851">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="d6179-2851">connectionString</span></span> |<span data-ttu-id="d6179-2852">Określ informacje connectionString potrzebne tooconnect toohello lokalnej bazy danych SQL Server przy użyciu uwierzytelniania SQL lub uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-2852">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="d6179-2853">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2853">Yes</span></span> |
| <span data-ttu-id="d6179-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d6179-2854">gatewayName</span></span> |<span data-ttu-id="d6179-2855">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d6179-2855">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="d6179-2856">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2856">Yes</span></span> |
| <span data-ttu-id="d6179-2857">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d6179-2857">username</span></span> |<span data-ttu-id="d6179-2858">Określ nazwę użytkownika, jeśli używasz uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6179-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="d6179-2859">Przykład: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="d6179-2860">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2860">No</span></span> |
| <span data-ttu-id="d6179-2861">hasło</span><span class="sxs-lookup"><span data-stu-id="d6179-2861">password</span></span> |<span data-ttu-id="d6179-2862">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d6179-2862">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="d6179-2863">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2863">No</span></span> |

<span data-ttu-id="d6179-2864">Można szyfrować poświadczeń przy użyciu hello **AzureRmDataFactoryEncryptValue nowy** polecenia cmdlet i używać ich w parametrach połączenia hello, jak pokazano w hello poniższy przykład (**EncryptedCredential** właściwość):</span><span class="sxs-lookup"><span data-stu-id="d6179-2864">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="d6179-2865">Przykład: JSON dla przy użyciu uwierzytelniania programu SQL</span><span class="sxs-lookup"><span data-stu-id="d6179-2865">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="d6179-2866">Przykład: JSON dla przy użyciu uwierzytelniania systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d6179-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="d6179-2867">Jeśli podano nazwę użytkownika i hasło, brama używa ich tooimpersonate hello określonego tooconnect toohello lokalnego programu SQL Server bazy danych kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d6179-2867">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="d6179-2868">W przeciwnym razie nawiązanie połączenia bramy toohello programu SQL Server bezpośrednio z kontekstu zabezpieczeń hello bramy (jego konta uruchamiania).</span><span class="sxs-lookup"><span data-stu-id="d6179-2868">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="d6179-2869">Aby uzyskać więcej informacji, zobacz [łącznika programu SQL Server](data-factory-sqlserver-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="d6179-2870">DZIAŁANIA PRZEKSZTAŁCENIA DANYCH</span><span class="sxs-lookup"><span data-stu-id="d6179-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="d6179-2871">Działanie</span><span class="sxs-lookup"><span data-stu-id="d6179-2871">Activity</span></span> | <span data-ttu-id="d6179-2872">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="d6179-2873">Działanie HDInsight Hive</span><span class="sxs-lookup"><span data-stu-id="d6179-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="d6179-2874">Witaj HDInsight Hive działania w potoku fabryki danych wykonuje zapytań programu Hive samodzielnie lub w klastrze systemu Windows/Linux-based HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2874">hello HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="d6179-2875">Działanie HDInsight Pig</span><span class="sxs-lookup"><span data-stu-id="d6179-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="d6179-2876">Witaj HDInsight Pig działania w potoku fabryki danych wykonuje zapytania Pig samodzielnie lub klastra systemu Windows/Linux-based HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2876">hello HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="d6179-2877">Działania technologii MapReduce w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6179-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="d6179-2878">Witaj działania HDInsight MapReduce w potoku fabryki danych wykonuje programy MapReduce samodzielnie lub klastra systemu Windows/Linux-based HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2878">hello HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="d6179-2879">Działania przesyłania strumieniowego usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6179-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="d6179-2880">Witaj HDInsight działaniu przesyłania strumieniowego w potoku fabryki danych wykonuje przesyłania strumieniowego usługi Hadoop programy samodzielnie lub klastra systemu Windows/Linux-based HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="d6179-2880">hello HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="d6179-2881">Działania platformy Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6179-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="d6179-2882">Witaj HDInsight Spark działania w potoku fabryki danych wykonuje programy Spark w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6179-2882">hello HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="d6179-2883">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d6179-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="d6179-2884">Azure umożliwia fabryki danych tooeasily możesz utworzyć potoki korzystających z opublikowanych uczenie maszynowe Azure w sieci web usługi analizy predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="d6179-2884">Azure Data Factory enables you tooeasily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="d6179-2885">Witaj działanie wykonywania wsadowego w potoku fabryki danych Azure można wywołać usługi Machine Learning web toomake operacje przewidywania dla usługi na powitania danych w partii.</span><span class="sxs-lookup"><span data-stu-id="d6179-2885">Using hello Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service toomake predictions on hello data in batch.</span></span> 
[<span data-ttu-id="d6179-2886">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d6179-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="d6179-2887">Wraz z upływem czasu hello modeli predykcyjnych w hello uczenia maszynowego oceniania eksperymenty muszą toobe retrained przy użyciu nowych danych wejściowych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-2887">Over time, hello predictive models in hello Machine Learning scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="d6179-2888">Po wykonaniu ponownego trenowania chcesz hello tooupdate oceniania usługi sieci web z hello retrained modelu uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2888">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained Machine Learning model.</span></span> <span data-ttu-id="d6179-2889">Można użyć hello usługi sieci web hello tooupdate działanie aktualizacji zasobu z hello nowo uczenia modelu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2889">You can use hello Update Resource Activity tooupdate hello web service with hello newly trained model.</span></span>
[<span data-ttu-id="d6179-2890">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="d6179-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="d6179-2891">Można użyć działania procedura składowana hello w tooinvoke potoku fabryki danych procedury składowanej w jednym z powitania po magazynów danych: baza danych SQL Azure, Magazyn danych SQL Azure, bazy danych serwera SQL w przedsiębiorstwie lub maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-2891">You can use hello Stored Procedure activity in a Data Factory pipeline tooinvoke a stored procedure in one of hello following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="d6179-2892">Data Lake Analytics U-SQL działania</span><span class="sxs-lookup"><span data-stu-id="d6179-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="d6179-2893">Data Lake Analytics U-SQL działanie uruchamia skrypt U-SQL w klastrze usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="d6179-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="d6179-2894">Niestandardowe działanie platformy .NET</span><span class="sxs-lookup"><span data-stu-id="d6179-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="d6179-2895">Dane tootransform w taki sposób, który nie jest obsługiwany przez fabrykę danych należy można tworzyć niestandardowe działania na własną logikę przetwarzania danych i użyj hello działania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2895">If you need tootransform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use hello activity in hello pipeline.</span></span> <span data-ttu-id="d6179-2896">Można skonfigurować hello niestandardowych .NET działania toorun przy użyciu usługi partia zadań Azure lub klaster Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6179-2896">You can configure hello custom .NET activity toorun using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="d6179-2897">Działania technologii Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6179-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="d6179-2898">Można określić hello następujące właściwości w definicji Hive JSON działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-2898">You can specify hello following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="d6179-2899">Właściwość typu Hello hello działania musi być: **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2899">hello type property for hello activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="d6179-2900">Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-2900">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="d6179-2901">Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooHDInsightHive działania:</span><span class="sxs-lookup"><span data-stu-id="d6179-2901">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightHive:</span></span>

| <span data-ttu-id="d6179-2902">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2902">Property</span></span> | <span data-ttu-id="d6179-2903">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2903">Description</span></span> | <span data-ttu-id="d6179-2904">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2905">Skrypt</span><span class="sxs-lookup"><span data-stu-id="d6179-2905">script</span></span> |<span data-ttu-id="d6179-2906">Określ wbudowanego skryptu Hive hello</span><span class="sxs-lookup"><span data-stu-id="d6179-2906">Specify hello Hive script inline</span></span> |<span data-ttu-id="d6179-2907">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2907">No</span></span> |
| <span data-ttu-id="d6179-2908">Ścieżka skryptu</span><span class="sxs-lookup"><span data-stu-id="d6179-2908">script path</span></span> |<span data-ttu-id="d6179-2909">Magazyn hello Hive skryptu w magazynie obiektów blob platformy Azure i podaj hello ścieżki toohello pliku.</span><span class="sxs-lookup"><span data-stu-id="d6179-2909">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="d6179-2910">Użyj właściwości 'script' lub "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="d6179-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="d6179-2911">Nie można używać razem.</span><span class="sxs-lookup"><span data-stu-id="d6179-2911">Both cannot be used together.</span></span> <span data-ttu-id="d6179-2912">Nazwa pliku Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-2912">hello file name is case-sensitive.</span></span> |<span data-ttu-id="d6179-2913">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2913">No</span></span> |
| <span data-ttu-id="d6179-2914">Definiuje</span><span class="sxs-lookup"><span data-stu-id="d6179-2914">defines</span></span> |<span data-ttu-id="d6179-2915">Określ parametry jako pary klucz wartość dla odwołania do skryptu Hive hello za pomocą "hiveconf"</span><span class="sxs-lookup"><span data-stu-id="d6179-2915">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="d6179-2916">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2916">No</span></span> |

<span data-ttu-id="d6179-2917">Te właściwości typu są określone toohello Hive działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-2917">These type properties are specific toohello Hive Activity.</span></span> <span data-ttu-id="d6179-2918">Inne właściwości (poza sekcji typeProperties hello) są obsługiwane dla wszystkich działań.</span><span class="sxs-lookup"><span data-stu-id="d6179-2918">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="d6179-2919">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-2919">JSON example</span></span>
<span data-ttu-id="d6179-2920">powitania po JSON definiuje działania HDInsight Hive w potoku.</span><span class="sxs-lookup"><span data-stu-id="d6179-2920">hello following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

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

<span data-ttu-id="d6179-2921">Aby uzyskać więcej informacji, zobacz [Hive działania](data-factory-hive-activity.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="d6179-2922">Działania technologii Pig w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6179-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="d6179-2923">Można określić hello następujące właściwości w definicji Pig działania w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="d6179-2923">You can specify hello following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="d6179-2924">Właściwość typu Hello hello działania musi być: **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2924">hello type property for hello activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="d6179-2925">Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-2925">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="d6179-2926">Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooHDInsightPig działania:</span><span class="sxs-lookup"><span data-stu-id="d6179-2926">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightPig:</span></span> 

| <span data-ttu-id="d6179-2927">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2927">Property</span></span> | <span data-ttu-id="d6179-2928">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2928">Description</span></span> | <span data-ttu-id="d6179-2929">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2930">Skrypt</span><span class="sxs-lookup"><span data-stu-id="d6179-2930">script</span></span> |<span data-ttu-id="d6179-2931">Określ hello Pig skrypt wbudowany</span><span class="sxs-lookup"><span data-stu-id="d6179-2931">Specify hello Pig script inline</span></span> |<span data-ttu-id="d6179-2932">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2932">No</span></span> |
| <span data-ttu-id="d6179-2933">Ścieżka skryptu</span><span class="sxs-lookup"><span data-stu-id="d6179-2933">script path</span></span> |<span data-ttu-id="d6179-2934">Przechowywanie skrypt programu Pig hello w magazynie obiektów blob platformy Azure i podaj hello ścieżki toohello pliku.</span><span class="sxs-lookup"><span data-stu-id="d6179-2934">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="d6179-2935">Użyj właściwości 'script' lub "scriptPath".</span><span class="sxs-lookup"><span data-stu-id="d6179-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="d6179-2936">Nie można używać razem.</span><span class="sxs-lookup"><span data-stu-id="d6179-2936">Both cannot be used together.</span></span> <span data-ttu-id="d6179-2937">Nazwa pliku Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-2937">hello file name is case-sensitive.</span></span> |<span data-ttu-id="d6179-2938">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2938">No</span></span> |
| <span data-ttu-id="d6179-2939">Definiuje</span><span class="sxs-lookup"><span data-stu-id="d6179-2939">defines</span></span> |<span data-ttu-id="d6179-2940">Określ parametry jako pary klucz wartość dla przywołującego w hello skrypt programu Pig</span><span class="sxs-lookup"><span data-stu-id="d6179-2940">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="d6179-2941">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2941">No</span></span> |

<span data-ttu-id="d6179-2942">Te właściwości typu są określone toohello Pig działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-2942">These type properties are specific toohello Pig Activity.</span></span> <span data-ttu-id="d6179-2943">Inne właściwości (poza sekcji typeProperties hello) są obsługiwane dla wszystkich działań.</span><span class="sxs-lookup"><span data-stu-id="d6179-2943">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="d6179-2944">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-2944">JSON example</span></span>

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

<span data-ttu-id="d6179-2945">Aby uzyskać więcej informacji, zobacz [działania Pig](#data-factory-pig-activity.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="d6179-2946">Działania technologii MapReduce w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6179-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="d6179-2947">Można określić hello następujące właściwości w definicji JSON działania MapReduce.</span><span class="sxs-lookup"><span data-stu-id="d6179-2947">You can specify hello following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="d6179-2948">Właściwość typu Hello hello działania musi być: **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2948">hello type property for hello activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="d6179-2949">Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-2949">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="d6179-2950">Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooHDInsightMapReduce działania:</span><span class="sxs-lookup"><span data-stu-id="d6179-2950">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightMapReduce:</span></span> 

| <span data-ttu-id="d6179-2951">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2951">Property</span></span> | <span data-ttu-id="d6179-2952">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2952">Description</span></span> | <span data-ttu-id="d6179-2953">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="d6179-2954">jarLinkedService</span></span> | <span data-ttu-id="d6179-2955">Nazwa hello połączonej usługi dla usługi Azure Storage, który zawiera plik JAR hello hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2955">Name of hello linked service for hello Azure Storage that contains hello JAR file.</span></span> | <span data-ttu-id="d6179-2956">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2956">Yes</span></span> |
| <span data-ttu-id="d6179-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="d6179-2957">jarFilePath</span></span> | <span data-ttu-id="d6179-2958">Ścieżka pliku JAR toohello w hello Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d6179-2958">Path toohello JAR file in hello Azure Storage.</span></span> | <span data-ttu-id="d6179-2959">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2959">Yes</span></span> | 
| <span data-ttu-id="d6179-2960">className</span><span class="sxs-lookup"><span data-stu-id="d6179-2960">className</span></span> | <span data-ttu-id="d6179-2961">Nazwa klasy głównym hello w pliku JAR hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2961">Name of hello main class in hello JAR file.</span></span> | <span data-ttu-id="d6179-2962">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-2962">Yes</span></span> | 
| <span data-ttu-id="d6179-2963">Argumenty</span><span class="sxs-lookup"><span data-stu-id="d6179-2963">arguments</span></span> | <span data-ttu-id="d6179-2964">Lista argumentów rozdzielonych przecinkami hello MapReduce programu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2964">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="d6179-2965">W czasie wykonywania, zobacz kilka dodatkowych argumentów (na przykład: mapreduce.job.tags) z platformy MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="d6179-2966">toodifferentiate argumentów z argumentami MapReduce hello, rozważ użycie zarówno opcji i wartości jako argumenty, jak pokazano w hello poniższy przykład (- s, — dane wejściowe,--itp., dane wyjściowe są opcje bezpośrednio następuje ich wartości)</span><span class="sxs-lookup"><span data-stu-id="d6179-2966">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="d6179-2967">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="d6179-2968">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
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
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="d6179-2969">Aby uzyskać więcej informacji, zobacz [działania MapReduce](data-factory-map-reduce.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="d6179-2970">Działania przesyłania strumieniowego usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6179-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="d6179-2971">Można określić hello następujące właściwości w definicji działania przesyłania strumieniowego usługi Hadoop w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="d6179-2971">You can specify hello following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="d6179-2972">Właściwość typu Hello hello działania musi być: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="d6179-2972">hello type property for hello activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="d6179-2973">Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-2973">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="d6179-2974">Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooHDInsightStreaming działania:</span><span class="sxs-lookup"><span data-stu-id="d6179-2974">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightStreaming:</span></span> 

| <span data-ttu-id="d6179-2975">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-2975">Property</span></span> | <span data-ttu-id="d6179-2976">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="d6179-2977">mapowania</span><span class="sxs-lookup"><span data-stu-id="d6179-2977">mapper</span></span> | <span data-ttu-id="d6179-2978">Nazwa pliku wykonywalnego mapowania hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2978">Name of hello mapper executable.</span></span> <span data-ttu-id="d6179-2979">Przykład Witaj cat.exe to hello mapowania pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2979">In hello example, cat.exe is hello mapper executable.</span></span>| 
| <span data-ttu-id="d6179-2980">Reduktor</span><span class="sxs-lookup"><span data-stu-id="d6179-2980">reducer</span></span> | <span data-ttu-id="d6179-2981">Nazwa pliku wykonywalnego reduktor hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2981">Name of hello reducer executable.</span></span> <span data-ttu-id="d6179-2982">Przykład Witaj wc.exe to reduktor hello pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2982">In hello example, wc.exe is hello reducer executable.</span></span> | 
| <span data-ttu-id="d6179-2983">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="d6179-2983">input</span></span> | <span data-ttu-id="d6179-2984">Plik wejściowy (w tym miejscu) dla hello mapowania.</span><span class="sxs-lookup"><span data-stu-id="d6179-2984">Input file (including location) for hello mapper.</span></span> <span data-ttu-id="d6179-2985">W przykładzie hello: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample jest hello kontenera obiektów blob, przykład/data/Gutenberg jest hello folder i davinci.txt jest hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d6179-2985">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span> |
| <span data-ttu-id="d6179-2986">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="d6179-2986">output</span></span> | <span data-ttu-id="d6179-2987">Plik wyjściowy (w tym miejscu) dla reduktor hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2987">Output file (including location) for hello reducer.</span></span> <span data-ttu-id="d6179-2988">dane wyjściowe zadania przesyłania strumieniowego usługi Hadoop hello Hello są zapisywane toohello lokalizacji określonej dla tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-2988">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span> |
| <span data-ttu-id="d6179-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="d6179-2989">filePaths</span></span> | <span data-ttu-id="d6179-2990">Ścieżki do plików wykonywalnych mapowania i reduktor hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2990">Paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="d6179-2991">W przykładzie hello: "adfsample/example/apps/wc.exe" adfsample jest hello kontenera obiektów blob, przykład/aplikacji hello folderu, i wc.exe jest hello pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="d6179-2991">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span> | 
| <span data-ttu-id="d6179-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="d6179-2992">fileLinkedService</span></span> | <span data-ttu-id="d6179-2993">Usługa Azure Storage połączone usługi, która reprezentuje hello Azure magazynu, który zawiera pliki hello określone w sekcji filePaths hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2993">Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span> | 
| <span data-ttu-id="d6179-2994">Argumenty</span><span class="sxs-lookup"><span data-stu-id="d6179-2994">arguments</span></span> | <span data-ttu-id="d6179-2995">Lista argumentów rozdzielonych przecinkami hello MapReduce programu.</span><span class="sxs-lookup"><span data-stu-id="d6179-2995">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="d6179-2996">W czasie wykonywania, zobacz kilka dodatkowych argumentów (na przykład: mapreduce.job.tags) z platformy MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="d6179-2997">toodifferentiate argumentów z argumentami MapReduce hello, rozważ użycie zarówno opcji i wartości jako argumenty, jak pokazano w hello poniższy przykład (- s, — dane wejściowe,--itp., dane wyjściowe są opcje bezpośrednio następuje ich wartości)</span><span class="sxs-lookup"><span data-stu-id="d6179-2997">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="d6179-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="d6179-2998">getDebugInfo</span></span> | <span data-ttu-id="d6179-2999">Element opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d6179-2999">An optional element.</span></span> <span data-ttu-id="d6179-3000">Jeśli je skonfigurowano tooFailure, dzienniki hello są pobierane tylko w przypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="d6179-3000">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="d6179-3001">Jeśli je skonfigurowano tooAll, dzienniki są zawsze pobierane niezależnie od hello stanu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d6179-3001">When it is set tooAll, logs are always downloaded irrespective of hello execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="d6179-3002">Należy określić wyjściowy zestaw danych hello działaniu przesyłania strumieniowego usługi Hadoop dla hello **generuje** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-3002">You must specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="d6179-3003">Ten zestaw danych można tylko fikcyjny zestawu danych, który jest wymagany toodrive hello potoku harmonogram (co godzinę, codziennie, itp.).</span><span class="sxs-lookup"><span data-stu-id="d6179-3003">This dataset can be just a dummy dataset that is required toodrive hello pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="d6179-3004">Działanie hello nie przyjmuje dane wejściowe, można pominąć Określanie zestawem danych wejściowych dla działania hello na powitania **dane wejściowe** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-3004">If hello activity doesn't take an input, you can skip specifying an input dataset for hello activity for hello **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="d6179-3005">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-3005">JSON example</span></span>

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

<span data-ttu-id="d6179-3006">Aby uzyskać więcej informacji, zobacz [działaniu przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="d6179-3007">Działania platformy Spark w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6179-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="d6179-3008">Można określić hello następujące właściwości w definicji Spark działania w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="d6179-3008">You can specify hello following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="d6179-3009">Właściwość typu Hello hello działania musi być: **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="d6179-3009">hello type property for hello activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="d6179-3010">Należy najpierw utworzyć usługi HDInsight połączone i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-3010">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="d6179-3011">Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooHDInsightSpark działania:</span><span class="sxs-lookup"><span data-stu-id="d6179-3011">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightSpark:</span></span> 

| <span data-ttu-id="d6179-3012">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-3012">Property</span></span> | <span data-ttu-id="d6179-3013">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-3013">Description</span></span> | <span data-ttu-id="d6179-3014">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="d6179-3015">Właściwość rootPath</span><span class="sxs-lookup"><span data-stu-id="d6179-3015">rootPath</span></span> | <span data-ttu-id="d6179-3016">Witaj kontenera obiektów Blob platformy Azure i folder zawierający plik Spark hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-3016">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="d6179-3017">Nazwa pliku Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-3017">hello file name is case-sensitive.</span></span> | <span data-ttu-id="d6179-3018">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-3018">Yes</span></span> |
| <span data-ttu-id="d6179-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="d6179-3019">entryFilePath</span></span> | <span data-ttu-id="d6179-3020">Względna ścieżka folderu głównego toohello hello pakietu kodu Spark.</span><span class="sxs-lookup"><span data-stu-id="d6179-3020">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="d6179-3021">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-3021">Yes</span></span> |
| <span data-ttu-id="d6179-3022">className</span><span class="sxs-lookup"><span data-stu-id="d6179-3022">className</span></span> | <span data-ttu-id="d6179-3023">Klasy głównym aplikacji Java/Spark</span><span class="sxs-lookup"><span data-stu-id="d6179-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="d6179-3024">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-3024">No</span></span> | 
| <span data-ttu-id="d6179-3025">Argumenty</span><span class="sxs-lookup"><span data-stu-id="d6179-3025">arguments</span></span> | <span data-ttu-id="d6179-3026">Lista argumentów wiersza polecenia toohello Spark program.</span><span class="sxs-lookup"><span data-stu-id="d6179-3026">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="d6179-3027">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-3027">No</span></span> | 
| <span data-ttu-id="d6179-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="d6179-3028">proxyUser</span></span> | <span data-ttu-id="d6179-3029">program Spark hello tooexecute tooimpersonate Hello użytkownika konta</span><span class="sxs-lookup"><span data-stu-id="d6179-3029">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="d6179-3030">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-3030">No</span></span> | 
| <span data-ttu-id="d6179-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="d6179-3031">sparkConfig</span></span> | <span data-ttu-id="d6179-3032">Właściwości konfiguracji platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="d6179-3032">Spark configuration properties.</span></span> | <span data-ttu-id="d6179-3033">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-3033">No</span></span> | 
| <span data-ttu-id="d6179-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="d6179-3034">getDebugInfo</span></span> | <span data-ttu-id="d6179-3035">Określa, kiedy pliki dziennika Spark hello są kopiowane toohello magazynu Azure używanego przez klaster usługi HDInsight (lub) został określony przez sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="d6179-3035">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="d6179-3036">Dozwolone wartości: None, zawsze lub niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="d6179-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="d6179-3037">Wartość domyślna: Brak.</span><span class="sxs-lookup"><span data-stu-id="d6179-3037">Default value: None.</span></span> | <span data-ttu-id="d6179-3038">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-3038">No</span></span> | 
| <span data-ttu-id="d6179-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="d6179-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="d6179-3040">Witaj połączoną usługą magazynu Azure zawierający plik zadania hello Spark, zależności i dzienniki.</span><span class="sxs-lookup"><span data-stu-id="d6179-3040">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="d6179-3041">Jeśli nie określisz wartości dla tej właściwości, jest używany Magazyn hello skojarzony z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6179-3041">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="d6179-3042">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="d6179-3043">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-3043">JSON example</span></span>

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
<span data-ttu-id="d6179-3044">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="d6179-3044">Note hello following points:</span></span> 

- <span data-ttu-id="d6179-3045">Witaj **typu** właściwość jest ustawiona zbyt**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="d6179-3045">hello **type** property is set too**HDInsightSpark**.</span></span>
- <span data-ttu-id="d6179-3046">Witaj **właściwość rootPath** ustawiono zbyt**adfspark\\pyFiles** gdzie adfspark jest pyFiles i kontener obiektów Blob Azure hello jest poprawnie folderu, w tym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="d6179-3046">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="d6179-3047">W tym przykładzie hello magazynu obiektów Blob Azure jest hello, który jest skojarzony z klastrem Spark hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-3047">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="d6179-3048">Możesz przekazać tooa pliku hello innego magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-3048">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="d6179-3049">Jeśli tak zrobisz, należy utworzyć toolink usługi Azure Storage połączone tej fabryki danych toohello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6179-3049">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="d6179-3050">Następnie określ nazwę hello hello połączone usługi jako wartość hello **sparkJobLinkedService** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-3050">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="d6179-3051">Zobacz [właściwości działania Spark](#spark-activity-properties) szczegóły dotyczące tej właściwości oraz inne właściwości obsługiwanych przez hello działania Spark.</span><span class="sxs-lookup"><span data-stu-id="d6179-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>
- <span data-ttu-id="d6179-3052">Witaj **entryFilePath** ustawiono toohello **test.py**, czyli plik python hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-3052">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span> 
- <span data-ttu-id="d6179-3053">Witaj **getDebugInfo** właściwość jest ustawiona zbyt**zawsze**, co oznacza, że pliki dziennika hello są zawsze generowany (powodzenie lub niepowodzenie).</span><span class="sxs-lookup"><span data-stu-id="d6179-3053">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="d6179-3054">Zaleca się, czy nie ustawisz tooAlways tej właściwości w środowisku produkcyjnym, chyba że są Rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="d6179-3054">We recommend that you do not set this property tooAlways in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="d6179-3055">Witaj **generuje** sekcja ma jeden wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-3055">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="d6179-3056">Należy określić wyjściowy zestaw danych, nawet jeśli hello spark program nie zwraca żadnych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-3056">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="d6179-3057">Hello wyjściowego zestawu danych dysków hello harmonogram dla potoku hello (co godzinę, codziennie, itp.).</span><span class="sxs-lookup"><span data-stu-id="d6179-3057">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="d6179-3058">Aby uzyskać więcej informacji o działaniu hello, zobacz [działania Spark](data-factory-spark.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-3058">For more information about hello activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="d6179-3059">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d6179-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="d6179-3060">Można określić hello następujące właściwości w definicji usługi Azure ML wsadowe wykonywanie działania JSON.</span><span class="sxs-lookup"><span data-stu-id="d6179-3060">You can specify hello following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="d6179-3061">Właściwość typu Hello hello działania musi być: **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="d6179-3061">hello type property for hello activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="d6179-3062">Musisz utworzyć maszyny platformy Azure, najpierw uczenia połączonej usługi i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-3062">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="d6179-3063">Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooAzureMLBatchExecution działania:</span><span class="sxs-lookup"><span data-stu-id="d6179-3063">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLBatchExecution:</span></span>

<span data-ttu-id="d6179-3064">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-3064">Property</span></span> | <span data-ttu-id="d6179-3065">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-3065">Description</span></span> | <span data-ttu-id="d6179-3066">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="d6179-3067">WebServiceInputActivity</span><span class="sxs-lookup"><span data-stu-id="d6179-3067">webServiceInput</span></span> | <span data-ttu-id="d6179-3068">Hello dataset toobe przekazany jako dane wejściowe dla hello usługi sieci web uczenie Maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-3068">hello dataset toobe passed as an input for hello Azure ML web service.</span></span> <span data-ttu-id="d6179-3069">Ten zestaw danych muszą także być ujęte w danych wejściowych hello hello działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-3069">This dataset must also be included in hello inputs for hello activity.</span></span> |<span data-ttu-id="d6179-3070">Użyj WebServiceInputActivity lub webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="d6179-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="d6179-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="d6179-3071">webServiceInputs</span></span> | <span data-ttu-id="d6179-3072">Określ zestawy danych toobe przekazany jako dane wejściowe dla hello usługi sieci web uczenie Maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-3072">Specify datasets toobe passed as inputs for hello Azure ML web service.</span></span> <span data-ttu-id="d6179-3073">Jeśli usługa sieci web hello przyjmuje wielu danych wejściowych, należy użyć właściwości webServiceInputs hello zamiast hello WebServiceInputActivity właściwość.</span><span class="sxs-lookup"><span data-stu-id="d6179-3073">If hello web service takes multiple inputs, use hello webServiceInputs property instead of using hello webServiceInput property.</span></span> <span data-ttu-id="d6179-3074">Zestawy danych, które odwołują się hello **webServiceInputs** również muszą być zawarte w hello działania **dane wejściowe**.</span><span class="sxs-lookup"><span data-stu-id="d6179-3074">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span> | <span data-ttu-id="d6179-3075">Użyj WebServiceInputActivity lub webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="d6179-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="d6179-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="d6179-3076">webServiceOutputs</span></span> | <span data-ttu-id="d6179-3077">Witaj zestawów danych, które są przypisane jako dane wyjściowe dla usługi sieci web uczenie Maszynowe Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-3077">hello datasets that are assigned as outputs for hello Azure ML web service.</span></span> <span data-ttu-id="d6179-3078">Usługa sieci web Hello zwraca dane wyjściowe w tym zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-3078">hello web service returns output data in this dataset.</span></span> | <span data-ttu-id="d6179-3079">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-3079">Yes</span></span> | 
<span data-ttu-id="d6179-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="d6179-3080">globalParameters</span></span> | <span data-ttu-id="d6179-3081">Określ wartości dla parametrów usługi sieci web hello w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6179-3081">Specify values for hello web service parameters in this section.</span></span> | <span data-ttu-id="d6179-3082">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="d6179-3083">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-3083">JSON example</span></span>
<span data-ttu-id="d6179-3084">W tym przykładzie działanie hello ma hello dataset **MLSqlInput** jako dane wejściowe i **MLSqlOutput** jako dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-3084">In this example, hello activity has hello dataset **MLSqlInput** as input and **MLSqlOutput** as hello output.</span></span> <span data-ttu-id="d6179-3085">Witaj **MLSqlInput** jest przekazywany jako usługi sieci web toohello wejściowych przez przy użyciu hello **WebServiceInputActivity** właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="d6179-3085">hello **MLSqlInput** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="d6179-3086">Witaj **MLSqlOutput** jest przekazywany jako usługi sieci Web dane wyjściowe toohello przez przy użyciu hello **webServiceOutputs** właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="d6179-3086">hello **MLSqlOutput** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span> 

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

<span data-ttu-id="d6179-3087">W przykładzie JSON hello hello wdrożona Azure Machine Learning w sieci Web usługi używa czytnika i zapisywania danych tooread/zapisu dla modułu z / tooan bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d6179-3087">In hello JSON example, hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="d6179-3088">Ta usługa sieci Web udostępnia następujące cztery parametry hello: Nazwa serwera, nazwa bazy danych, nazwę konta użytkownika serwera i hasło konta użytkownika serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-3088">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="d6179-3089">Tylko wejściami i wyjściami hello AzureMLBatchExecution działania mogą być przekazywane jako parametry toohello usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d6179-3089">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="d6179-3090">Na przykład hello powyżej fragment kodu JSON, MLSqlInput jest wejściowych toohello AzureMLBatchExecution działalność, która jest przekazywany jako wejściowych toohello usługi sieci Web za pomocą parametru WebServiceInputActivity.</span><span class="sxs-lookup"><span data-stu-id="d6179-3090">For example, in hello above JSON snippet, MLSqlInput is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="d6179-3091">Działanie aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d6179-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="d6179-3092">Można określić hello następujące właściwości w definicji usługi Azure ML aktualizacji zasobów działania JSON.</span><span class="sxs-lookup"><span data-stu-id="d6179-3092">You can specify hello following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="d6179-3093">Właściwość typu Hello hello działania musi być: **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="d6179-3093">hello type property for hello activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="d6179-3094">Musisz utworzyć maszyny platformy Azure, najpierw uczenia połączonej usługi i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-3094">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="d6179-3095">Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooAzureMLUpdateResource działania:</span><span class="sxs-lookup"><span data-stu-id="d6179-3095">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLUpdateResource:</span></span>

<span data-ttu-id="d6179-3096">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-3096">Property</span></span> | <span data-ttu-id="d6179-3097">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-3097">Description</span></span> | <span data-ttu-id="d6179-3098">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="d6179-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="d6179-3099">trainedModelName</span></span> | <span data-ttu-id="d6179-3100">Nazwa hello retrained modelu.</span><span class="sxs-lookup"><span data-stu-id="d6179-3100">Name of hello retrained model.</span></span> | <span data-ttu-id="d6179-3101">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-3101">Yes</span></span> |  
<span data-ttu-id="d6179-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="d6179-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="d6179-3103">Pliku zestawu danych wskazujące toohello iLearner zwrócony przez hello ponownego trenowania operacji.</span><span class="sxs-lookup"><span data-stu-id="d6179-3103">Dataset pointing toohello iLearner file returned by hello retraining operation.</span></span> | <span data-ttu-id="d6179-3104">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="d6179-3105">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-3105">JSON example</span></span>
<span data-ttu-id="d6179-3106">potok Hello ma dwa działania: **AzureMLBatchExecution** i **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="d6179-3106">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="d6179-3107">Witaj działanie wykonywania wsadowego usługi uczenie Maszynowe Azure pobiera dane szkoleniowe hello jako dane wejściowe i tworzy plik iLearner jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="d6179-3107">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="d6179-3108">działanie Hello wywołuje usługę sieci web szkolenia hello (eksperyment uczenia udostępniony jako usługa sieci web) przy użyciu danych wejściowych hello szkolenia danych i odbiera plik ilearner hello z hello Usługa sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d6179-3108">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="d6179-3109">Hello placeholderBlob jest tylko fikcyjny wyjściowego zestawu danych, który jest wymagany przez hello fabryki danych Azure usługa toorun hello potoku.</span><span class="sxs-lookup"><span data-stu-id="d6179-3109">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>


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

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="d6179-3110">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="d6179-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="d6179-3111">Można określić hello następujące właściwości w definicji JSON działanie U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-3111">You can specify hello following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="d6179-3112">Właściwość typu Hello hello działania musi być: **DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="d6179-3112">hello type property for hello activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="d6179-3113">Musisz utworzyć usługi Azure Data Lake Analytics połączone i określ nazwę hello jej jako wartości dla hello **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-3113">You must create an Azure Data Lake Analytics linked service and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="d6179-3114">Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello działania tooDataLakeAnalyticsU-SQL:</span><span class="sxs-lookup"><span data-stu-id="d6179-3114">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="d6179-3115">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-3115">Property</span></span> | <span data-ttu-id="d6179-3116">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-3116">Description</span></span> | <span data-ttu-id="d6179-3117">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d6179-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="d6179-3118">scriptPath</span></span> |<span data-ttu-id="d6179-3119">Ścieżka toofolder, zawierający skrypt hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d6179-3119">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="d6179-3120">Nazwa pliku hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d6179-3120">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="d6179-3121">Nie (Jeśli używasz skryptu)</span><span class="sxs-lookup"><span data-stu-id="d6179-3121">No (if you use script)</span></span> |
| <span data-ttu-id="d6179-3122">Element scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="d6179-3122">scriptLinkedService</span></span> |<span data-ttu-id="d6179-3123">Połączonej usługi, która łączy hello magazynu, który zawiera hello skryptu toohello usługi fabryka danych</span><span class="sxs-lookup"><span data-stu-id="d6179-3123">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="d6179-3124">Nie (Jeśli używasz skryptu)</span><span class="sxs-lookup"><span data-stu-id="d6179-3124">No (if you use script)</span></span> |
| <span data-ttu-id="d6179-3125">Skrypt</span><span class="sxs-lookup"><span data-stu-id="d6179-3125">script</span></span> |<span data-ttu-id="d6179-3126">Określ skrypt wbudowany zamiast określania scriptPath i scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="d6179-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="d6179-3127">Na przykład: "skrypt": "Test Utwórz bazę danych".</span><span class="sxs-lookup"><span data-stu-id="d6179-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="d6179-3128">Nie (Jeśli używasz scriptPath i scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="d6179-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="d6179-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="d6179-3129">degreeOfParallelism</span></span> |<span data-ttu-id="d6179-3130">Maksymalna liczba węzłów Hello używać jednocześnie toorun hello zadania.</span><span class="sxs-lookup"><span data-stu-id="d6179-3130">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="d6179-3131">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-3131">No</span></span> |
| <span data-ttu-id="d6179-3132">Priorytet</span><span class="sxs-lookup"><span data-stu-id="d6179-3132">priority</span></span> |<span data-ttu-id="d6179-3133">Określa, które spośród wszystkich znajdujących się w kolejce zadań powinna być wybranego toorun najpierw.</span><span class="sxs-lookup"><span data-stu-id="d6179-3133">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="d6179-3134">Witaj hello niższą, wyższy priorytet hello hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-3134">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="d6179-3135">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-3135">No</span></span> |
| <span data-ttu-id="d6179-3136">parameters</span><span class="sxs-lookup"><span data-stu-id="d6179-3136">parameters</span></span> |<span data-ttu-id="d6179-3137">Parametry skryptu hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="d6179-3137">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="d6179-3138">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="d6179-3139">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-3139">JSON example</span></span>

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

<span data-ttu-id="d6179-3140">Aby uzyskać więcej informacji, zobacz [Data Lake Analytics U-SQL działania](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="d6179-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="d6179-3141">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="d6179-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="d6179-3142">Można określić hello następujące właściwości w definicji przechowywane procedury działania JSON.</span><span class="sxs-lookup"><span data-stu-id="d6179-3142">You can specify hello following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="d6179-3143">Właściwość typu Hello hello działania musi być: **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="d6179-3143">hello type property for hello activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="d6179-3144">Należy utworzyć jednego ze hello następujące połączone usługi oraz określić nazwę hello hello połączone usługi jako wartość hello **linkedServiceName** właściwości:</span><span class="sxs-lookup"><span data-stu-id="d6179-3144">You must create an one of hello following linked services and specify hello name of hello linked service as a value for hello **linkedServiceName** property:</span></span>

- <span data-ttu-id="d6179-3145">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="d6179-3145">SQL Server</span></span> 
- <span data-ttu-id="d6179-3146">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d6179-3146">Azure SQL Database</span></span>
- <span data-ttu-id="d6179-3147">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d6179-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="d6179-3148">Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooSqlServerStoredProcedure działania:</span><span class="sxs-lookup"><span data-stu-id="d6179-3148">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooSqlServerStoredProcedure:</span></span>

| <span data-ttu-id="d6179-3149">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-3149">Property</span></span> | <span data-ttu-id="d6179-3150">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-3150">Description</span></span> | <span data-ttu-id="d6179-3151">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d6179-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="d6179-3152">storedProcedureName</span></span> |<span data-ttu-id="d6179-3153">Określ nazwę hello procedury hello przechowywane w bazie danych Azure SQL hello lub Azure SQL Data Warehouse jest reprezentowana przez hello połączone usługi, która hello używa tabeli danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d6179-3153">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="d6179-3154">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-3154">Yes</span></span> |
| <span data-ttu-id="d6179-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="d6179-3155">storedProcedureParameters</span></span> |<span data-ttu-id="d6179-3156">Określ wartości dla parametrów procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="d6179-3157">Jeśli potrzebujesz toopass wartości null dla parametru, należy użyć składni hello: "param1": wartość null (małe litery).</span><span class="sxs-lookup"><span data-stu-id="d6179-3157">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="d6179-3158">Zobacz powitania po toolearn próbki o korzystaniu z tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-3158">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="d6179-3159">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-3159">No</span></span> |

<span data-ttu-id="d6179-3160">Jeśli określisz wejściowy zestaw danych, musi być dostępny (w stanie "Gotowe") dla hello przechowywane procedury toorun działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="d6179-3161">Witaj wejściowy zestaw danych nie mogą być używane w procedurze hello przechowywane jako parametr.</span><span class="sxs-lookup"><span data-stu-id="d6179-3161">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="d6179-3162">Jest tylko zależności hello toocheck używane przed początkowy hello przechowywane procedury działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-3162">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> <span data-ttu-id="d6179-3163">Należy określić zestaw danych wyjściowych dla działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="d6179-3164">Wyjściowy zestaw danych określa hello **harmonogram** hello przechowywane procedury działania (co godzinę, co tydzień, co miesiąc, itp.).</span><span class="sxs-lookup"><span data-stu-id="d6179-3164">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="d6179-3165">Witaj wyjściowego zestawu danych musi używać **połączona usługa** przywołujący tooan bazy danych SQL Azure lub usługi Azure SQL Data Warehouse lub baza danych SQL Server w której ma zostać hello toorun procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-3165">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="d6179-3166">Witaj wyjściowego zestawu danych może służyć jako wynik hello toopass sposób hello przechowywane procedury dla dalszego przetwarzania przez inne działanie ([łańcucha działania](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-3166">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in hello pipeline.</span></span> <span data-ttu-id="d6179-3167">Jednak automatycznie fabryki danych nie zapisuje dane wyjściowe hello toothis procedury przechowywanej zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="d6179-3167">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="d6179-3168">Jest to hello tej tabeli SQL tooa zapisy hello punktów zestawu danych wyjściowych do procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="d6179-3168">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="d6179-3169">W niektórych przypadkach może być hello wyjściowy zestaw danych **fikcyjny dataset**, który jest używany tylko toospecify hello harmonogramu uruchamiania hello przechowywane procedury działania.</span><span class="sxs-lookup"><span data-stu-id="d6179-3169">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="d6179-3170">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-3170">JSON example</span></span>

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

<span data-ttu-id="d6179-3171">Aby uzyskać więcej informacji, zobacz [działania dotyczącego procedury składowanej](data-factory-stored-proc-activity.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="d6179-3172">Niestandardowe działanie platformy .NET</span><span class="sxs-lookup"><span data-stu-id="d6179-3172">.NET custom activity</span></span>
<span data-ttu-id="d6179-3173">Można określić hello następujące właściwości niestandardowe działanie .NET definicji JSON.</span><span class="sxs-lookup"><span data-stu-id="d6179-3173">You can specify hello following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="d6179-3174">Właściwość typu Hello hello działania musi być: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="d6179-3174">hello type property for hello activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="d6179-3175">Należy utworzyć usługi Azure HDInsight połączone lub partii zadań Azure połączone usługi i określ nazwę hello hello połączone usługi jako wartość hello **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6179-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify hello name of hello linked service as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="d6179-3176">Witaj następujące właściwości są obsługiwane w hello **typeProperties** sekcji w przypadku ustawienia typu hello tooDotNetActivity działania:</span><span class="sxs-lookup"><span data-stu-id="d6179-3176">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDotNetActivity:</span></span>
 
| <span data-ttu-id="d6179-3177">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d6179-3177">Property</span></span> | <span data-ttu-id="d6179-3178">Opis</span><span class="sxs-lookup"><span data-stu-id="d6179-3178">Description</span></span> | <span data-ttu-id="d6179-3179">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d6179-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d6179-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="d6179-3180">AssemblyName</span></span> | <span data-ttu-id="d6179-3181">Nazwa zestawu hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-3181">Name of hello assembly.</span></span> <span data-ttu-id="d6179-3182">W przykładzie hello jest: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="d6179-3182">In hello example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="d6179-3183">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-3183">Yes</span></span> |
| <span data-ttu-id="d6179-3184">Punkt wejścia</span><span class="sxs-lookup"><span data-stu-id="d6179-3184">EntryPoint</span></span> |<span data-ttu-id="d6179-3185">Nazwa klasy hello, który implementuje interfejs IDotNetActivity hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-3185">Name of hello class that implements hello IDotNetActivity interface.</span></span> <span data-ttu-id="d6179-3186">W przykładzie hello jest: **MyDotNetActivityNS.MyDotNetActivity** gdzie MyDotNetActivityNS jest hello przestrzeni nazw, a MyDotNetActivity hello klasy.</span><span class="sxs-lookup"><span data-stu-id="d6179-3186">In hello example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is hello namespace and MyDotNetActivity is hello class.</span></span>  | <span data-ttu-id="d6179-3187">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-3187">Yes</span></span> | 
| <span data-ttu-id="d6179-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="d6179-3188">PackageLinkedService</span></span> | <span data-ttu-id="d6179-3189">Nazwa hello połączoną usługą magazynu Azure wskazujące toohello magazynu obiektów blob, zawierający plik zip hello działania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="d6179-3189">Name of hello Azure Storage linked service that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="d6179-3190">W przykładzie hello jest: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="d6179-3190">In hello example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="d6179-3191">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-3191">Yes</span></span> |
| <span data-ttu-id="d6179-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="d6179-3192">PackageFile</span></span> | <span data-ttu-id="d6179-3193">Nazwa pliku zip hello.</span><span class="sxs-lookup"><span data-stu-id="d6179-3193">Name of hello zip file.</span></span> <span data-ttu-id="d6179-3194">W przykładzie hello jest: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="d6179-3194">In hello example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="d6179-3195">Tak</span><span class="sxs-lookup"><span data-stu-id="d6179-3195">Yes</span></span> |
| <span data-ttu-id="d6179-3196">właściwości rozszerzone</span><span class="sxs-lookup"><span data-stu-id="d6179-3196">extendedProperties</span></span> | <span data-ttu-id="d6179-3197">Rozszerzone właściwości, które można definiować i przekazywania toohello kodu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="d6179-3197">Extended properties that you can define and pass on toohello .NET code.</span></span> <span data-ttu-id="d6179-3198">W tym przykładzie hello **SliceStart** zmienna jest ustawiona wartość tooa oparta na powitania SliceStart zmienna.</span><span class="sxs-lookup"><span data-stu-id="d6179-3198">In this example, hello **SliceStart** variable is set tooa value based on hello SliceStart system variable.</span></span> | <span data-ttu-id="d6179-3199">Nie</span><span class="sxs-lookup"><span data-stu-id="d6179-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="d6179-3200">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="d6179-3200">JSON example</span></span>

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

<span data-ttu-id="d6179-3201">Aby uzyskać szczegółowe informacje, zobacz [skorzystać z działań niestandardowych w fabryce danych](data-factory-use-custom-activities.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6179-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d6179-3202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6179-3202">Next Steps</span></span>
<span data-ttu-id="d6179-3203">Zobacz hello następujące samouczki:</span><span class="sxs-lookup"><span data-stu-id="d6179-3203">See hello following tutorials:</span></span> 

- [<span data-ttu-id="d6179-3204">Samouczek: tworzenie potoku z działanie kopiowania</span><span class="sxs-lookup"><span data-stu-id="d6179-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="d6179-3205">Samouczek: tworzenie potoku z działaniem gałęzi</span><span class="sxs-lookup"><span data-stu-id="d6179-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)