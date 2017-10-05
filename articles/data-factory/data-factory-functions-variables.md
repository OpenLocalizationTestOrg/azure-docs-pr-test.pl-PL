---
title: Funkcje fabryki danych i zmienne systemu | Dokumentacja firmy Microsoft
description: "Zawiera listę funkcji fabryki danych Azure i zmienne systemu"
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 72a966bdc271f86b9568d3310d2e22d83b447594
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="e6f9e-103">Fabryki danych Azure — funkcje i zmienne systemu</span><span class="sxs-lookup"><span data-stu-id="e6f9e-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="e6f9e-104">Ten artykuł zawiera informacje o funkcjach i zmiennych obsługiwane przez usługi fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="e6f9e-105">Zmienne systemowe fabryki danych</span><span class="sxs-lookup"><span data-stu-id="e6f9e-105">Data Factory system variables</span></span>
| <span data-ttu-id="e6f9e-106">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="e6f9e-106">Variable Name</span></span> | <span data-ttu-id="e6f9e-107">Opis</span><span class="sxs-lookup"><span data-stu-id="e6f9e-107">Description</span></span> | <span data-ttu-id="e6f9e-108">Zakres obiektu</span><span class="sxs-lookup"><span data-stu-id="e6f9e-108">Object Scope</span></span> | <span data-ttu-id="e6f9e-109">Zakres JSON i przypadki użycia</span><span class="sxs-lookup"><span data-stu-id="e6f9e-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e6f9e-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="e6f9e-110">WindowStart</span></span> |<span data-ttu-id="e6f9e-111">Początek przedziału czasu bieżącego działania Uruchom okno</span><span class="sxs-lookup"><span data-stu-id="e6f9e-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="e6f9e-112">Działanie</span><span class="sxs-lookup"><span data-stu-id="e6f9e-112">activity</span></span> |<ol><li><span data-ttu-id="e6f9e-113">Określ kwerend danych zaznaczenia.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-113">Specify data selection queries.</span></span> <span data-ttu-id="e6f9e-114">Zobacz artykuły łącznika, do którego odwołuje się [działań przepływu danych](data-factory-data-movement-activities.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-114">See connector articles referenced in the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="e6f9e-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="e6f9e-115">WindowEnd</span></span> |<span data-ttu-id="e6f9e-116">Koniec przedziału czasu bieżącego działania Uruchom okno</span><span class="sxs-lookup"><span data-stu-id="e6f9e-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="e6f9e-117">Działanie</span><span class="sxs-lookup"><span data-stu-id="e6f9e-117">activity</span></span> |<span data-ttu-id="e6f9e-118">taka sama jak WindowStart.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-118">same as WindowStart.</span></span> |
| <span data-ttu-id="e6f9e-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="e6f9e-119">SliceStart</span></span> |<span data-ttu-id="e6f9e-120">Początek przedziału czasu dla tworzonym wycinka danych</span><span class="sxs-lookup"><span data-stu-id="e6f9e-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="e6f9e-121">Działanie</span><span class="sxs-lookup"><span data-stu-id="e6f9e-121">activity</span></span><br/><span data-ttu-id="e6f9e-122">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="e6f9e-122">dataset</span></span> |<ol><li><span data-ttu-id="e6f9e-123">Określ folder dynamiczne ścieżki i nazwy plików podczas pracy z [obiektów Blob platformy Azure](data-factory-azure-blob-connector.md) i [zestawów danych systemu plików](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="e6f9e-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="e6f9e-124">Określ zależności wejściowych z funkcji fabryki danych w kolekcji danych wejściowych działania.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="e6f9e-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="e6f9e-125">SliceEnd</span></span> |<span data-ttu-id="e6f9e-126">Koniec przedziału czasu dla bieżącego wycinka danych.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="e6f9e-127">Działanie</span><span class="sxs-lookup"><span data-stu-id="e6f9e-127">activity</span></span><br/><span data-ttu-id="e6f9e-128">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="e6f9e-128">dataset</span></span> |<span data-ttu-id="e6f9e-129">taka sama jak SliceStart.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="e6f9e-130">Obecnie fabryki danych wymaga, czy określony w działaniu dokładnie harmonogram jest zgodny z harmonogramem określonym w dostępności wyjściowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-130">Currently data factory requires that the schedule specified in the activity exactly matches the schedule specified in availability of the output dataset.</span></span> <span data-ttu-id="e6f9e-131">W związku z tym WindowStart, WindowEnd i SliceStart i SliceEnd zawsze są mapowane na ten sam okres czasu i wycinek pojedynczym wyjściowym.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map to the same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="e6f9e-132">Przykład zmiennej systemowej</span><span class="sxs-lookup"><span data-stu-id="e6f9e-132">Example for using a system variable</span></span>
<span data-ttu-id="e6f9e-133">W poniższym przykładzie, rok, miesiąc, dzień i czas **SliceStart** są wyodrębniane do oddzielnych zmiennych, które są używane przez **folderPath** i **fileName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-133">In the following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a><span data-ttu-id="e6f9e-134">Funkcje fabryki danych</span><span class="sxs-lookup"><span data-stu-id="e6f9e-134">Data Factory functions</span></span>
<span data-ttu-id="e6f9e-135">Możesz użyć funkcji w fabryce danych wraz z zmienne systemowe, do następujących celów:</span><span class="sxs-lookup"><span data-stu-id="e6f9e-135">You can use functions in data factory along with system variables for the following purposes:</span></span>

1. <span data-ttu-id="e6f9e-136">Określanie zapytania wyboru danych (zobacz artykuły łącznika odwołuje się [działań przepływu danych](data-factory-data-movement-activities.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-136">Specifying data selection queries (see connector articles referenced by the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="e6f9e-137">Składnia służąca do wywołania funkcji fabryki danych jest:  **$$ <function>**  danych zapytania wyboru i innych właściwości w działaniu i zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-137">The syntax to invoke a data factory function is: **$$<function>** for data selection queries and other properties in the activity and datasets.</span></span>  
2. <span data-ttu-id="e6f9e-138">Określanie wejściowych zależności przy użyciu funkcji fabryki danych w kolekcji danych wejściowych działania.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="e6f9e-139">$$ nie jest potrzebna do określenia wyrażeń wejściowych zależności.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="e6f9e-140">W poniższym przykładzie **sqlReaderQuery** właściwość w pliku JSON jest przypisany do wartości zwracanych przez `Text.Format` funkcji.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-140">In the following sample, **sqlReaderQuery** property in a JSON file is assigned to a value returned by the `Text.Format` function.</span></span> <span data-ttu-id="e6f9e-141">W tym przykładzie użyto również zmiennej systemu o nazwie **WindowStart**, który reprezentuje czas rozpoczęcia okna uruchamiania działania.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-141">This sample also uses a system variable named **WindowStart**, which represents the start time of the activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="e6f9e-142">Zobacz [niestandardowe ciągi daty i godziny Format](https://msdn.microsoft.com/library/8kb3ddd4.aspx) temat, który opisano różne opcje formatowania, można użyć (na przykład: dni, a rrrr).</span><span class="sxs-lookup"><span data-stu-id="e6f9e-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="e6f9e-143">Funkcje</span><span class="sxs-lookup"><span data-stu-id="e6f9e-143">Functions</span></span>
<span data-ttu-id="e6f9e-144">W poniższych tabelach przedstawiono wszystkie funkcje w fabryce danych Azure:</span><span class="sxs-lookup"><span data-stu-id="e6f9e-144">The following tables list all the functions in Azure Data Factory:</span></span>

| <span data-ttu-id="e6f9e-145">Kategoria</span><span class="sxs-lookup"><span data-stu-id="e6f9e-145">Category</span></span> | <span data-ttu-id="e6f9e-146">Funkcja</span><span class="sxs-lookup"><span data-stu-id="e6f9e-146">Function</span></span> | <span data-ttu-id="e6f9e-147">Parametry</span><span class="sxs-lookup"><span data-stu-id="e6f9e-147">Parameters</span></span> | <span data-ttu-id="e6f9e-148">Opis</span><span class="sxs-lookup"><span data-stu-id="e6f9e-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e6f9e-149">Time</span><span class="sxs-lookup"><span data-stu-id="e6f9e-149">Time</span></span> |<span data-ttu-id="e6f9e-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-150">AddHours(X,Y)</span></span> |<span data-ttu-id="e6f9e-151">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="e6f9e-152">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="e6f9e-152">Y: int</span></span> |<span data-ttu-id="e6f9e-153">Dodaje Y godziny do chwili X.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-153">Adds Y hours to the given time X.</span></span> <br/><br/><span data-ttu-id="e6f9e-154">Przykład:`9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="e6f9e-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="e6f9e-155">Time</span><span class="sxs-lookup"><span data-stu-id="e6f9e-155">Time</span></span> |<span data-ttu-id="e6f9e-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="e6f9e-157">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="e6f9e-158">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="e6f9e-158">Y: int</span></span> |<span data-ttu-id="e6f9e-159">Dodaje minut Y-X.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-159">Adds Y minutes to X.</span></span><br/><br/><span data-ttu-id="e6f9e-160">Przykład:`9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="e6f9e-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="e6f9e-161">Time</span><span class="sxs-lookup"><span data-stu-id="e6f9e-161">Time</span></span> |<span data-ttu-id="e6f9e-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-162">StartOfHour(X)</span></span> |<span data-ttu-id="e6f9e-163">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-163">X: Datetime</span></span> |<span data-ttu-id="e6f9e-164">Pobiera godzinę rozpoczęcia, godzinę reprezentowany przez składnik godziny z wartości x.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-164">Gets the starting time for the hour represented by the hour component of X.</span></span> <br/><br/><span data-ttu-id="e6f9e-165">Przykład:`StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="e6f9e-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="e6f9e-166">Date</span><span class="sxs-lookup"><span data-stu-id="e6f9e-166">Date</span></span> |<span data-ttu-id="e6f9e-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-167">AddDays(X,Y)</span></span> |<span data-ttu-id="e6f9e-168">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-168">X: DateTime</span></span><br/><br/><span data-ttu-id="e6f9e-169">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="e6f9e-169">Y: int</span></span> |<span data-ttu-id="e6f9e-170">Dodaje Y dni do X.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-170">Adds Y days to X.</span></span> <br/><br/><span data-ttu-id="e6f9e-171">Przykład: 9/15/2013 12:00:00 PM + 2 dni = 9/17/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="e6f9e-172">Zbyt odejmowania dni, określając Y jako wartość ujemną.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="e6f9e-173">Przykład: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="e6f9e-174">Date</span><span class="sxs-lookup"><span data-stu-id="e6f9e-174">Date</span></span> |<span data-ttu-id="e6f9e-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="e6f9e-176">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-176">X: DateTime</span></span><br/><br/><span data-ttu-id="e6f9e-177">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="e6f9e-177">Y: int</span></span> |<span data-ttu-id="e6f9e-178">Dodaje Y miesięcy do X.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-178">Adds Y months to X.</span></span><br/><br/><span data-ttu-id="e6f9e-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="e6f9e-180">Miesięcy można odejmować zbyt określając Y jako wartość ujemną.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="e6f9e-181">Przykład: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="e6f9e-182">Date</span><span class="sxs-lookup"><span data-stu-id="e6f9e-182">Date</span></span> |<span data-ttu-id="e6f9e-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="e6f9e-184">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="e6f9e-185">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="e6f9e-185">Y: int</span></span> |<span data-ttu-id="e6f9e-186">Dodaje Y * X 3 miesięcy.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-186">Adds Y * 3 months to X.</span></span><br/><br/><span data-ttu-id="e6f9e-187">Przykład:`9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="e6f9e-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="e6f9e-188">Date</span><span class="sxs-lookup"><span data-stu-id="e6f9e-188">Date</span></span> |<span data-ttu-id="e6f9e-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="e6f9e-190">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-190">X: DateTime</span></span><br/><br/><span data-ttu-id="e6f9e-191">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="e6f9e-191">Y: int</span></span> |<span data-ttu-id="e6f9e-192">Dodaje Y * X 7 dni</span><span class="sxs-lookup"><span data-stu-id="e6f9e-192">Adds Y * 7 days to X</span></span><br/><br/><span data-ttu-id="e6f9e-193">Przykład: 9/15/2013 12:00:00 PM + 1 tydzień = 9/22/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="e6f9e-194">Tygodnie można odejmować zbyt określając Y jako wartość ujemną.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="e6f9e-195">Przykład: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="e6f9e-196">Date</span><span class="sxs-lookup"><span data-stu-id="e6f9e-196">Date</span></span> |<span data-ttu-id="e6f9e-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-197">AddYears(X,Y)</span></span> |<span data-ttu-id="e6f9e-198">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-198">X: DateTime</span></span><br/><br/><span data-ttu-id="e6f9e-199">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="e6f9e-199">Y: int</span></span> |<span data-ttu-id="e6f9e-200">Dodaje Y lat do X.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-200">Adds Y years to X.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="e6f9e-201">Lat można odejmować zbyt określając Y jako wartość ujemną.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="e6f9e-202">Przykład: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="e6f9e-203">Date</span><span class="sxs-lookup"><span data-stu-id="e6f9e-203">Date</span></span> |<span data-ttu-id="e6f9e-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-204">Day(X)</span></span> |<span data-ttu-id="e6f9e-205">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-205">X: DateTime</span></span> |<span data-ttu-id="e6f9e-206">Pobiera składnik dni z wartości X.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-206">Gets the day component of X.</span></span><br/><br/><span data-ttu-id="e6f9e-207">Przykład: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="e6f9e-208">Date</span><span class="sxs-lookup"><span data-stu-id="e6f9e-208">Date</span></span> |<span data-ttu-id="e6f9e-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-209">DayOfWeek(X)</span></span> |<span data-ttu-id="e6f9e-210">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-210">X: DateTime</span></span> |<span data-ttu-id="e6f9e-211">Pobiera dzień tygodnia składnika wartości X.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-211">Gets the day of week component of X.</span></span><br/><br/><span data-ttu-id="e6f9e-212">Przykład: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="e6f9e-213">Date</span><span class="sxs-lookup"><span data-stu-id="e6f9e-213">Date</span></span> |<span data-ttu-id="e6f9e-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-214">DayOfYear(X)</span></span> |<span data-ttu-id="e6f9e-215">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-215">X: DateTime</span></span> |<span data-ttu-id="e6f9e-216">Pobiera dzień w roku reprezentowany przez składnik roku x.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-216">Gets the day in the year represented by the year component of X.</span></span><br/><br/><span data-ttu-id="e6f9e-217">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="e6f9e-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="e6f9e-218">Date</span><span class="sxs-lookup"><span data-stu-id="e6f9e-218">Date</span></span> |<span data-ttu-id="e6f9e-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-219">DaysInMonth(X)</span></span> |<span data-ttu-id="e6f9e-220">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-220">X: DateTime</span></span> |<span data-ttu-id="e6f9e-221">Pobiera dni w miesiącu reprezentowany przez składnik miesiąca parametr X.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-221">Gets the days in the month represented by the month component of parameter X.</span></span><br/><br/><span data-ttu-id="e6f9e-222">Przykład: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span></span> |
| <span data-ttu-id="e6f9e-223">Date</span><span class="sxs-lookup"><span data-stu-id="e6f9e-223">Date</span></span> |<span data-ttu-id="e6f9e-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-224">EndOfDay(X)</span></span> |<span data-ttu-id="e6f9e-225">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-225">X: DateTime</span></span> |<span data-ttu-id="e6f9e-226">Pobiera daty i godziny zakończenia dnia (składnik dni) x.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-226">Gets the date-time that represents the end of the day (day component) of X.</span></span><br/><br/><span data-ttu-id="e6f9e-227">Przykład: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="e6f9e-228">Date</span><span class="sxs-lookup"><span data-stu-id="e6f9e-228">Date</span></span> |<span data-ttu-id="e6f9e-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-229">EndOfMonth(X)</span></span> |<span data-ttu-id="e6f9e-230">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-230">X: DateTime</span></span> |<span data-ttu-id="e6f9e-231">Pobiera koniec miesiąca reprezentowany przez składnik miesiąca parametru X.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-231">Gets the end of the month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="e6f9e-232">Przykład: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (Data i godzina zakończenia miesiąca września)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents the end of September month)</span></span> |
| <span data-ttu-id="e6f9e-233">Date</span><span class="sxs-lookup"><span data-stu-id="e6f9e-233">Date</span></span> |<span data-ttu-id="e6f9e-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-234">StartOfDay(X)</span></span> |<span data-ttu-id="e6f9e-235">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-235">X: DateTime</span></span> |<span data-ttu-id="e6f9e-236">Pobiera początek dnia reprezentowany przez składnik dni z wartości parametru X.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-236">Gets the start of the day represented by the day component of parameter X.</span></span><br/><br/><span data-ttu-id="e6f9e-237">Przykład: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="e6f9e-238">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-238">DateTime</span></span> |<span data-ttu-id="e6f9e-239">FROM(X)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-239">From(X)</span></span> |<span data-ttu-id="e6f9e-240">X: ciąg</span><span class="sxs-lookup"><span data-stu-id="e6f9e-240">X: String</span></span> |<span data-ttu-id="e6f9e-241">Przeanalizować ciągu X na czas daty.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-241">Parse string X to a date time.</span></span> |
| <span data-ttu-id="e6f9e-242">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-242">DateTime</span></span> |<span data-ttu-id="e6f9e-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-243">Ticks(X)</span></span> |<span data-ttu-id="e6f9e-244">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="e6f9e-244">X: DateTime</span></span> |<span data-ttu-id="e6f9e-245">Pobiera właściwość parametru X to znaczniki osi. Jeden znaczników jest równy 100 nanosekundach.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-245">Gets the ticks property of the parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="e6f9e-246">Wartość ta właściwość reprezentuje liczbę znaczników, które upłynęły od północy 12:00:00 1 stycznia 0001.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-246">The value of this property represents the number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="e6f9e-247">Tekst</span><span class="sxs-lookup"><span data-stu-id="e6f9e-247">Text</span></span> |<span data-ttu-id="e6f9e-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="e6f9e-248">Format(X)</span></span> |<span data-ttu-id="e6f9e-249">X: zmienna string</span><span class="sxs-lookup"><span data-stu-id="e6f9e-249">X: String variable</span></span> |<span data-ttu-id="e6f9e-250">Formatuje tekst (Użyj `\\'` kombinacja ucieczki `'` znaków).</span><span class="sxs-lookup"><span data-stu-id="e6f9e-250">Formats the text (use `\\'` combination to escape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="e6f9e-251">Podczas korzystania z funkcji w innej funkcji, nie trzeba używać  **$$**  prefiks dla funkcji wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-251">When using a function within another function, you do not need to use **$$** prefix for the inner function.</span></span> <span data-ttu-id="e6f9e-252">Na przykład: $$Text.Format ("PartitionKey eq \\" my_pkey_filter_value\\"i RowKey ge \\" {0: yyyy-MM-dd gg}\\'', Time.AddHours (SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="e6f9e-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="e6f9e-253">W tym przykładzie należy zauważyć, że  **$$**  prefiks nie jest używany przez **Time.AddHours** funkcji.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-253">In this example, notice that **$$** prefix is not used for the **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="e6f9e-254">Przykład</span><span class="sxs-lookup"><span data-stu-id="e6f9e-254">Example</span></span>
<span data-ttu-id="e6f9e-255">W poniższym przykładzie parametrów wejściowych i wyjściowych działania gałęzi są określane za pomocą `Text.Format` funkcji i SliceStart zmiennej systemowej.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-255">In the following example, input and output parameters for the Hive activity are determined by using the `Text.Format` function and SliceStart system variable.</span></span> 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a><span data-ttu-id="e6f9e-256">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="e6f9e-256">Example 2</span></span>

<span data-ttu-id="e6f9e-257">W poniższym przykładzie parametr daty i godziny dla działania dotyczącego procedury składowanej jest określany przy użyciu tekstu.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-257">In the following example, the DateTime parameter for the Stored Procedure Activity is determined by using the Text.</span></span> <span data-ttu-id="e6f9e-258">Funkcja format, a zmienna SliceStart.</span><span class="sxs-lookup"><span data-stu-id="e6f9e-258">Format function and the SliceStart variable.</span></span> 

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
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a><span data-ttu-id="e6f9e-259">Przykład 3</span><span class="sxs-lookup"><span data-stu-id="e6f9e-259">Example 3</span></span>
<span data-ttu-id="e6f9e-260">Można odczytać danych z poprzedniego dnia zamiast reprezentowany przez SliceStart dzień, należy użyć funkcji AddDays, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="e6f9e-260">To read data from previous day instead of day represented by the SliceStart, use the AddDays function as shown in the following example:</span></span> 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
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

<span data-ttu-id="e6f9e-261">Zobacz [niestandardowe ciągi daty i godziny Format](https://msdn.microsoft.com/library/8kb3ddd4.aspx) temat, który opisano różne opcje formatowania, można użyć (na przykład: RR a rrrr).</span><span class="sxs-lookup"><span data-stu-id="e6f9e-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

