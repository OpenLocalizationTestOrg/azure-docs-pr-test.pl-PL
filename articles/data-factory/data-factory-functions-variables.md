---
title: aaaData fabryki funkcje i zmienne systemu | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="c84a7-103">Fabryki danych Azure — funkcje i zmienne systemu</span><span class="sxs-lookup"><span data-stu-id="c84a7-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="c84a7-104">Ten artykuł zawiera informacje o funkcjach i zmiennych obsługiwane przez usługi fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="c84a7-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="c84a7-105">Zmienne systemowe fabryki danych</span><span class="sxs-lookup"><span data-stu-id="c84a7-105">Data Factory system variables</span></span>
| <span data-ttu-id="c84a7-106">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="c84a7-106">Variable Name</span></span> | <span data-ttu-id="c84a7-107">Opis</span><span class="sxs-lookup"><span data-stu-id="c84a7-107">Description</span></span> | <span data-ttu-id="c84a7-108">Zakres obiektu</span><span class="sxs-lookup"><span data-stu-id="c84a7-108">Object Scope</span></span> | <span data-ttu-id="c84a7-109">Zakres JSON i przypadki użycia</span><span class="sxs-lookup"><span data-stu-id="c84a7-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c84a7-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="c84a7-110">WindowStart</span></span> |<span data-ttu-id="c84a7-111">Początek przedziału czasu bieżącego działania Uruchom okno</span><span class="sxs-lookup"><span data-stu-id="c84a7-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="c84a7-112">Działanie</span><span class="sxs-lookup"><span data-stu-id="c84a7-112">activity</span></span> |<ol><li><span data-ttu-id="c84a7-113">Określ kwerend danych zaznaczenia.</span><span class="sxs-lookup"><span data-stu-id="c84a7-113">Specify data selection queries.</span></span> <span data-ttu-id="c84a7-114">Zobacz artykuły łącznika, do którego odwołuje się hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c84a7-114">See connector articles referenced in hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="c84a7-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="c84a7-115">WindowEnd</span></span> |<span data-ttu-id="c84a7-116">Koniec przedziału czasu bieżącego działania Uruchom okno</span><span class="sxs-lookup"><span data-stu-id="c84a7-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="c84a7-117">Działanie</span><span class="sxs-lookup"><span data-stu-id="c84a7-117">activity</span></span> |<span data-ttu-id="c84a7-118">taka sama jak WindowStart.</span><span class="sxs-lookup"><span data-stu-id="c84a7-118">same as WindowStart.</span></span> |
| <span data-ttu-id="c84a7-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="c84a7-119">SliceStart</span></span> |<span data-ttu-id="c84a7-120">Początek przedziału czasu dla tworzonym wycinka danych</span><span class="sxs-lookup"><span data-stu-id="c84a7-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="c84a7-121">Działanie</span><span class="sxs-lookup"><span data-stu-id="c84a7-121">activity</span></span><br/><span data-ttu-id="c84a7-122">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="c84a7-122">dataset</span></span> |<ol><li><span data-ttu-id="c84a7-123">Określ folder dynamiczne ścieżki i nazwy plików podczas pracy z [obiektów Blob platformy Azure](data-factory-azure-blob-connector.md) i [zestawów danych systemu plików](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="c84a7-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="c84a7-124">Określ zależności wejściowych z funkcji fabryki danych w kolekcji danych wejściowych działania.</span><span class="sxs-lookup"><span data-stu-id="c84a7-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="c84a7-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="c84a7-125">SliceEnd</span></span> |<span data-ttu-id="c84a7-126">Koniec przedziału czasu dla bieżącego wycinka danych.</span><span class="sxs-lookup"><span data-stu-id="c84a7-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="c84a7-127">Działanie</span><span class="sxs-lookup"><span data-stu-id="c84a7-127">activity</span></span><br/><span data-ttu-id="c84a7-128">Zestaw danych</span><span class="sxs-lookup"><span data-stu-id="c84a7-128">dataset</span></span> |<span data-ttu-id="c84a7-129">taka sama jak SliceStart.</span><span class="sxs-lookup"><span data-stu-id="c84a7-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="c84a7-130">Obecnie fabryki danych wymaga tego hello zaplanować hello określony w działanie dokładnie odpowiada harmonogram hello określony w dostępności hello wyjściowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="c84a7-130">Currently data factory requires that hello schedule specified in hello activity exactly matches hello schedule specified in availability of hello output dataset.</span></span> <span data-ttu-id="c84a7-131">W związku z tym WindowStart, WindowEnd i SliceStart i SliceEnd zawsze mapy toohello sam czas okresu i wycinek pojedynczym wyjściowym.</span><span class="sxs-lookup"><span data-stu-id="c84a7-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map toohello same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="c84a7-132">Przykład zmiennej systemowej</span><span class="sxs-lookup"><span data-stu-id="c84a7-132">Example for using a system variable</span></span>
<span data-ttu-id="c84a7-133">W powitania po przykład, rok, miesiąc, dzień i czas **SliceStart** są wyodrębniane do oddzielnych zmiennych, które są używane przez **folderPath** i **fileName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="c84a7-133">In hello following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

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

## <a name="data-factory-functions"></a><span data-ttu-id="c84a7-134">Funkcje fabryki danych</span><span class="sxs-lookup"><span data-stu-id="c84a7-134">Data Factory functions</span></span>
<span data-ttu-id="c84a7-135">Możesz użyć funkcji w fabryce danych wraz z zmienne systemowe dla hello następujących celów:</span><span class="sxs-lookup"><span data-stu-id="c84a7-135">You can use functions in data factory along with system variables for hello following purposes:</span></span>

1. <span data-ttu-id="c84a7-136">Określanie zapytania wyboru danych (zobacz artykuły łącznika odwołuje się hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c84a7-136">Specifying data selection queries (see connector articles referenced by hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="c84a7-137">Witaj tooinvoke składni jest funkcja fabryki danych:  **$$ <function>**  dla danych zapytania wyboru i inne właściwości działania hello i zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="c84a7-137">hello syntax tooinvoke a data factory function is: **$$<function>** for data selection queries and other properties in hello activity and datasets.</span></span>  
2. <span data-ttu-id="c84a7-138">Określanie wejściowych zależności przy użyciu funkcji fabryki danych w kolekcji danych wejściowych działania.</span><span class="sxs-lookup"><span data-stu-id="c84a7-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="c84a7-139">$$ nie jest potrzebna do określenia wyrażeń wejściowych zależności.</span><span class="sxs-lookup"><span data-stu-id="c84a7-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="c84a7-140">W hello następujące przykładowe **sqlReaderQuery** właściwość w pliku JSON jest przypisywana wartość tooa zwrócony przez hello `Text.Format` funkcji.</span><span class="sxs-lookup"><span data-stu-id="c84a7-140">In hello following sample, **sqlReaderQuery** property in a JSON file is assigned tooa value returned by hello `Text.Format` function.</span></span> <span data-ttu-id="c84a7-141">W tym przykładzie użyto również zmiennej systemu o nazwie **WindowStart**, reprezentuje hello godzina rozpoczęcia działania hello Uruchom okno.</span><span class="sxs-lookup"><span data-stu-id="c84a7-141">This sample also uses a system variable named **WindowStart**, which represents hello start time of hello activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="c84a7-142">Zobacz [niestandardowe ciągi daty i godziny Format](https://msdn.microsoft.com/library/8kb3ddd4.aspx) temat, który opisano różne opcje formatowania, można użyć (na przykład: dni, a rrrr).</span><span class="sxs-lookup"><span data-stu-id="c84a7-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="c84a7-143">Funkcje</span><span class="sxs-lookup"><span data-stu-id="c84a7-143">Functions</span></span>
<span data-ttu-id="c84a7-144">następujące tabele Hello lista wszystkich funkcji hello w fabryce danych Azure:</span><span class="sxs-lookup"><span data-stu-id="c84a7-144">hello following tables list all hello functions in Azure Data Factory:</span></span>

| <span data-ttu-id="c84a7-145">Kategoria</span><span class="sxs-lookup"><span data-stu-id="c84a7-145">Category</span></span> | <span data-ttu-id="c84a7-146">Funkcja</span><span class="sxs-lookup"><span data-stu-id="c84a7-146">Function</span></span> | <span data-ttu-id="c84a7-147">Parametry</span><span class="sxs-lookup"><span data-stu-id="c84a7-147">Parameters</span></span> | <span data-ttu-id="c84a7-148">Opis</span><span class="sxs-lookup"><span data-stu-id="c84a7-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c84a7-149">Time</span><span class="sxs-lookup"><span data-stu-id="c84a7-149">Time</span></span> |<span data-ttu-id="c84a7-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="c84a7-150">AddHours(X,Y)</span></span> |<span data-ttu-id="c84a7-151">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="c84a7-152">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="c84a7-152">Y: int</span></span> |<span data-ttu-id="c84a7-153">Dodaje podany czas X toohello godziny Y.</span><span class="sxs-lookup"><span data-stu-id="c84a7-153">Adds Y hours toohello given time X.</span></span> <br/><br/><span data-ttu-id="c84a7-154">Przykład:`9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="c84a7-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="c84a7-155">Time</span><span class="sxs-lookup"><span data-stu-id="c84a7-155">Time</span></span> |<span data-ttu-id="c84a7-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="c84a7-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="c84a7-157">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="c84a7-158">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="c84a7-158">Y: int</span></span> |<span data-ttu-id="c84a7-159">Dodaje Y tooX minut.</span><span class="sxs-lookup"><span data-stu-id="c84a7-159">Adds Y minutes tooX.</span></span><br/><br/><span data-ttu-id="c84a7-160">Przykład:`9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="c84a7-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="c84a7-161">Time</span><span class="sxs-lookup"><span data-stu-id="c84a7-161">Time</span></span> |<span data-ttu-id="c84a7-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="c84a7-162">StartOfHour(X)</span></span> |<span data-ttu-id="c84a7-163">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-163">X: Datetime</span></span> |<span data-ttu-id="c84a7-164">Pobiera hello początkowy czas na godzinę hello reprezentowany przez składnik godziny hello x.</span><span class="sxs-lookup"><span data-stu-id="c84a7-164">Gets hello starting time for hello hour represented by hello hour component of X.</span></span> <br/><br/><span data-ttu-id="c84a7-165">Przykład:`StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="c84a7-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="c84a7-166">Date</span><span class="sxs-lookup"><span data-stu-id="c84a7-166">Date</span></span> |<span data-ttu-id="c84a7-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="c84a7-167">AddDays(X,Y)</span></span> |<span data-ttu-id="c84a7-168">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-168">X: DateTime</span></span><br/><br/><span data-ttu-id="c84a7-169">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="c84a7-169">Y: int</span></span> |<span data-ttu-id="c84a7-170">Dodaje Y tooX dni.</span><span class="sxs-lookup"><span data-stu-id="c84a7-170">Adds Y days tooX.</span></span> <br/><br/><span data-ttu-id="c84a7-171">Przykład: 9/15/2013 12:00:00 PM + 2 dni = 9/17/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="c84a7-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="c84a7-172">Zbyt odejmowania dni, określając Y jako wartość ujemną.</span><span class="sxs-lookup"><span data-stu-id="c84a7-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="c84a7-173">Przykład: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="c84a7-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="c84a7-174">Date</span><span class="sxs-lookup"><span data-stu-id="c84a7-174">Date</span></span> |<span data-ttu-id="c84a7-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="c84a7-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="c84a7-176">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-176">X: DateTime</span></span><br/><br/><span data-ttu-id="c84a7-177">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="c84a7-177">Y: int</span></span> |<span data-ttu-id="c84a7-178">Dodaje tooX miesięcy Y.</span><span class="sxs-lookup"><span data-stu-id="c84a7-178">Adds Y months tooX.</span></span><br/><br/><span data-ttu-id="c84a7-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="c84a7-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="c84a7-180">Miesięcy można odejmować zbyt określając Y jako wartość ujemną.</span><span class="sxs-lookup"><span data-stu-id="c84a7-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="c84a7-181">Przykład: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="c84a7-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="c84a7-182">Date</span><span class="sxs-lookup"><span data-stu-id="c84a7-182">Date</span></span> |<span data-ttu-id="c84a7-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="c84a7-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="c84a7-184">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="c84a7-185">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="c84a7-185">Y: int</span></span> |<span data-ttu-id="c84a7-186">Dodaje Y * tooX 3 miesiące.</span><span class="sxs-lookup"><span data-stu-id="c84a7-186">Adds Y * 3 months tooX.</span></span><br/><br/><span data-ttu-id="c84a7-187">Przykład:`9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="c84a7-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="c84a7-188">Date</span><span class="sxs-lookup"><span data-stu-id="c84a7-188">Date</span></span> |<span data-ttu-id="c84a7-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="c84a7-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="c84a7-190">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-190">X: DateTime</span></span><br/><br/><span data-ttu-id="c84a7-191">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="c84a7-191">Y: int</span></span> |<span data-ttu-id="c84a7-192">Dodaje Y * tooX 7 dni</span><span class="sxs-lookup"><span data-stu-id="c84a7-192">Adds Y * 7 days tooX</span></span><br/><br/><span data-ttu-id="c84a7-193">Przykład: 9/15/2013 12:00:00 PM + 1 tydzień = 9/22/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="c84a7-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="c84a7-194">Tygodnie można odejmować zbyt określając Y jako wartość ujemną.</span><span class="sxs-lookup"><span data-stu-id="c84a7-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="c84a7-195">Przykład: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="c84a7-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="c84a7-196">Date</span><span class="sxs-lookup"><span data-stu-id="c84a7-196">Date</span></span> |<span data-ttu-id="c84a7-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="c84a7-197">AddYears(X,Y)</span></span> |<span data-ttu-id="c84a7-198">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-198">X: DateTime</span></span><br/><br/><span data-ttu-id="c84a7-199">/ Y: int</span><span class="sxs-lookup"><span data-stu-id="c84a7-199">Y: int</span></span> |<span data-ttu-id="c84a7-200">Dodaje tooX lat Y.</span><span class="sxs-lookup"><span data-stu-id="c84a7-200">Adds Y years tooX.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="c84a7-201">Lat można odejmować zbyt określając Y jako wartość ujemną.</span><span class="sxs-lookup"><span data-stu-id="c84a7-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="c84a7-202">Przykład: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="c84a7-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="c84a7-203">Date</span><span class="sxs-lookup"><span data-stu-id="c84a7-203">Date</span></span> |<span data-ttu-id="c84a7-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="c84a7-204">Day(X)</span></span> |<span data-ttu-id="c84a7-205">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-205">X: DateTime</span></span> |<span data-ttu-id="c84a7-206">Pobiera hello składnik dni z wartości X.</span><span class="sxs-lookup"><span data-stu-id="c84a7-206">Gets hello day component of X.</span></span><br/><br/><span data-ttu-id="c84a7-207">Przykład: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="c84a7-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="c84a7-208">Date</span><span class="sxs-lookup"><span data-stu-id="c84a7-208">Date</span></span> |<span data-ttu-id="c84a7-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="c84a7-209">DayOfWeek(X)</span></span> |<span data-ttu-id="c84a7-210">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-210">X: DateTime</span></span> |<span data-ttu-id="c84a7-211">Pobiera hello dzień tygodnia składnika wartości X.</span><span class="sxs-lookup"><span data-stu-id="c84a7-211">Gets hello day of week component of X.</span></span><br/><br/><span data-ttu-id="c84a7-212">Przykład: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="c84a7-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="c84a7-213">Date</span><span class="sxs-lookup"><span data-stu-id="c84a7-213">Date</span></span> |<span data-ttu-id="c84a7-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="c84a7-214">DayOfYear(X)</span></span> |<span data-ttu-id="c84a7-215">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-215">X: DateTime</span></span> |<span data-ttu-id="c84a7-216">Pobiera hello dzień w roku hello reprezentowany przez składnik roku hello x.</span><span class="sxs-lookup"><span data-stu-id="c84a7-216">Gets hello day in hello year represented by hello year component of X.</span></span><br/><br/><span data-ttu-id="c84a7-217">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="c84a7-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="c84a7-218">Date</span><span class="sxs-lookup"><span data-stu-id="c84a7-218">Date</span></span> |<span data-ttu-id="c84a7-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="c84a7-219">DaysInMonth(X)</span></span> |<span data-ttu-id="c84a7-220">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-220">X: DateTime</span></span> |<span data-ttu-id="c84a7-221">Pobiera hello dni w miesiącu hello reprezentowany przez składnik miesiąca hello parametru X.</span><span class="sxs-lookup"><span data-stu-id="c84a7-221">Gets hello days in hello month represented by hello month component of parameter X.</span></span><br/><br/><span data-ttu-id="c84a7-222">Przykład: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span><span class="sxs-lookup"><span data-stu-id="c84a7-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span></span> |
| <span data-ttu-id="c84a7-223">Date</span><span class="sxs-lookup"><span data-stu-id="c84a7-223">Date</span></span> |<span data-ttu-id="c84a7-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="c84a7-224">EndOfDay(X)</span></span> |<span data-ttu-id="c84a7-225">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-225">X: DateTime</span></span> |<span data-ttu-id="c84a7-226">Pobiera hello daty i godziny, reprezentujący hello koniec dnia hello (składnik dni) x.</span><span class="sxs-lookup"><span data-stu-id="c84a7-226">Gets hello date-time that represents hello end of hello day (day component) of X.</span></span><br/><br/><span data-ttu-id="c84a7-227">Przykład: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="c84a7-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="c84a7-228">Date</span><span class="sxs-lookup"><span data-stu-id="c84a7-228">Date</span></span> |<span data-ttu-id="c84a7-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="c84a7-229">EndOfMonth(X)</span></span> |<span data-ttu-id="c84a7-230">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-230">X: DateTime</span></span> |<span data-ttu-id="c84a7-231">Pobiera hello koniec miesiąca hello reprezentowany przez składnik miesiąca parametru X.</span><span class="sxs-lookup"><span data-stu-id="c84a7-231">Gets hello end of hello month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="c84a7-232">Przykład: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (Data i godzina reprezentujący hello koniec miesiąca września)</span><span class="sxs-lookup"><span data-stu-id="c84a7-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents hello end of September month)</span></span> |
| <span data-ttu-id="c84a7-233">Date</span><span class="sxs-lookup"><span data-stu-id="c84a7-233">Date</span></span> |<span data-ttu-id="c84a7-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="c84a7-234">StartOfDay(X)</span></span> |<span data-ttu-id="c84a7-235">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-235">X: DateTime</span></span> |<span data-ttu-id="c84a7-236">Pobiera początek hello dnia hello reprezentowany przez składnik dni hello parametru X.</span><span class="sxs-lookup"><span data-stu-id="c84a7-236">Gets hello start of hello day represented by hello day component of parameter X.</span></span><br/><br/><span data-ttu-id="c84a7-237">Przykład: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="c84a7-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="c84a7-238">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-238">DateTime</span></span> |<span data-ttu-id="c84a7-239">FROM(X)</span><span class="sxs-lookup"><span data-stu-id="c84a7-239">From(X)</span></span> |<span data-ttu-id="c84a7-240">X: ciąg</span><span class="sxs-lookup"><span data-stu-id="c84a7-240">X: String</span></span> |<span data-ttu-id="c84a7-241">Przeanalizować składni ciągu X tooa Data i godzina.</span><span class="sxs-lookup"><span data-stu-id="c84a7-241">Parse string X tooa date time.</span></span> |
| <span data-ttu-id="c84a7-242">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-242">DateTime</span></span> |<span data-ttu-id="c84a7-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="c84a7-243">Ticks(X)</span></span> |<span data-ttu-id="c84a7-244">X: Data i godzina</span><span class="sxs-lookup"><span data-stu-id="c84a7-244">X: DateTime</span></span> |<span data-ttu-id="c84a7-245">Pobiera znaczniki hello właściwość parametru hello X. Jeden znaczników jest równy 100 nanosekundach.</span><span class="sxs-lookup"><span data-stu-id="c84a7-245">Gets hello ticks property of hello parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="c84a7-246">wartość tej właściwości Hello reprezentuje hello liczbę znaczników, które upłynęły od północy 12:00:00 1 stycznia 0001.</span><span class="sxs-lookup"><span data-stu-id="c84a7-246">hello value of this property represents hello number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="c84a7-247">Tekst</span><span class="sxs-lookup"><span data-stu-id="c84a7-247">Text</span></span> |<span data-ttu-id="c84a7-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="c84a7-248">Format(X)</span></span> |<span data-ttu-id="c84a7-249">X: zmienna string</span><span class="sxs-lookup"><span data-stu-id="c84a7-249">X: String variable</span></span> |<span data-ttu-id="c84a7-250">Formaty hello tekst (Użyj `\\'` tooescape kombinacja `'` znaków).</span><span class="sxs-lookup"><span data-stu-id="c84a7-250">Formats hello text (use `\\'` combination tooescape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="c84a7-251">Podczas korzystania z funkcji w innej funkcji, nie trzeba toouse  **$$**  prefiks hello funkcji wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="c84a7-251">When using a function within another function, you do not need toouse **$$** prefix for hello inner function.</span></span> <span data-ttu-id="c84a7-252">Na przykład: $$Text.Format ("PartitionKey eq \\" my_pkey_filter_value\\"i RowKey ge \\" {0: yyyy-MM-dd gg}\\'', Time.AddHours (SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="c84a7-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="c84a7-253">W tym przykładzie należy zauważyć, że  **$$**  prefiks nie jest używany przez hello **Time.AddHours** funkcji.</span><span class="sxs-lookup"><span data-stu-id="c84a7-253">In this example, notice that **$$** prefix is not used for hello **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="c84a7-254">Przykład</span><span class="sxs-lookup"><span data-stu-id="c84a7-254">Example</span></span>
<span data-ttu-id="c84a7-255">W hello następujące parametry przykład wejściowe i wyjściowe działania Hive hello są określane za pomocą hello `Text.Format` funkcji i SliceStart zmiennej systemowej.</span><span class="sxs-lookup"><span data-stu-id="c84a7-255">In hello following example, input and output parameters for hello Hive activity are determined by using hello `Text.Format` function and SliceStart system variable.</span></span> 

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

### <a name="example-2"></a><span data-ttu-id="c84a7-256">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="c84a7-256">Example 2</span></span>

<span data-ttu-id="c84a7-257">W hello poniższy przykład parametr DateTime hello hello działania dotyczącego procedury składowanej jest określany przy użyciu hello tekstu.</span><span class="sxs-lookup"><span data-stu-id="c84a7-257">In hello following example, hello DateTime parameter for hello Stored Procedure Activity is determined by using hello Text.</span></span> <span data-ttu-id="c84a7-258">Format funkcji i hello SliceStart zmiennej.</span><span class="sxs-lookup"><span data-stu-id="c84a7-258">Format function and hello SliceStart variable.</span></span> 

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

### <a name="example-3"></a><span data-ttu-id="c84a7-259">Przykład 3</span><span class="sxs-lookup"><span data-stu-id="c84a7-259">Example 3</span></span>
<span data-ttu-id="c84a7-260">tooread danych z poprzedniego dnia zamiast dzień reprezentowany przez hello SliceStart, użyj funkcji AddDays hello, jak pokazano hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="c84a7-260">tooread data from previous day instead of day represented by hello SliceStart, use hello AddDays function as shown in hello following example:</span></span> 

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

<span data-ttu-id="c84a7-261">Zobacz [niestandardowe ciągi daty i godziny Format](https://msdn.microsoft.com/library/8kb3ddd4.aspx) temat, który opisano różne opcje formatowania, można użyć (na przykład: RR a rrrr).</span><span class="sxs-lookup"><span data-stu-id="c84a7-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

