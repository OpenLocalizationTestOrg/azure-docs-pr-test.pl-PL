---
title: formaty aaaFile i kompresji w fabryce danych Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat hello formatów plików obsługiwanych przez usługi fabryka danych Azure."
keywords: "dane obiektów blob, kopiowania obiektów blob platformy azure"
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
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="91fb1-104">Formaty plików i kompresji obsługiwane przez usługi fabryka danych Azure</span><span class="sxs-lookup"><span data-stu-id="91fb1-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="91fb1-105">*Ten temat dotyczy toohello następujące łączniki: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [obiektów Blob platformy Azure](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [systemu plików](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), i [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="91fb1-105">*This topic applies toohello following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="91fb1-106">Fabryka danych Azure obsługuje następujące typy format pliku hello:</span><span class="sxs-lookup"><span data-stu-id="91fb1-106">Azure Data Factory supports hello following file format types:</span></span>

* [<span data-ttu-id="91fb1-107">Format tekstu</span><span class="sxs-lookup"><span data-stu-id="91fb1-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="91fb1-108">JSON format</span><span class="sxs-lookup"><span data-stu-id="91fb1-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="91fb1-109">Avro format</span><span class="sxs-lookup"><span data-stu-id="91fb1-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="91fb1-110">ORC format</span><span class="sxs-lookup"><span data-stu-id="91fb1-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="91fb1-111">Parquet format</span><span class="sxs-lookup"><span data-stu-id="91fb1-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="91fb1-112">Format tekstu</span><span class="sxs-lookup"><span data-stu-id="91fb1-112">Text format</span></span>
<span data-ttu-id="91fb1-113">Tooread z pliku tekstowego lub zapisać plik tekstowy tooa, ustaw hello `type` właściwości w hello `format` części zestawu danych hello zbyt**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="91fb1-113">If you want tooread from a text file or write tooa text file, set hello `type` property in hello `format` section of hello dataset too**TextFormat**.</span></span> <span data-ttu-id="91fb1-114">Można również określić następujące hello **opcjonalne** właściwości w hello `format` sekcji.</span><span class="sxs-lookup"><span data-stu-id="91fb1-114">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="91fb1-115">Zobacz [przykład TextFormat](#textformat-example) sekcję na temat tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="91fb1-115">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="91fb1-116">Właściwość</span><span class="sxs-lookup"><span data-stu-id="91fb1-116">Property</span></span> | <span data-ttu-id="91fb1-117">Opis</span><span class="sxs-lookup"><span data-stu-id="91fb1-117">Description</span></span> | <span data-ttu-id="91fb1-118">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="91fb1-118">Allowed values</span></span> | <span data-ttu-id="91fb1-119">Wymagany</span><span class="sxs-lookup"><span data-stu-id="91fb1-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="91fb1-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="91fb1-120">columnDelimiter</span></span> |<span data-ttu-id="91fb1-121">znak Hello używać tooseparate kolumn w pliku.</span><span class="sxs-lookup"><span data-stu-id="91fb1-121">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="91fb1-122">Należy rozważyć toouse istnieje rzadkich char nie do drukowania, który prawdopodobnie nie może w Twoich danych.</span><span class="sxs-lookup"><span data-stu-id="91fb1-122">You can consider toouse a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="91fb1-123">Na przykład określić "\u0001", reprezentujący Start z pozycji (raportu o kondycji).</span><span class="sxs-lookup"><span data-stu-id="91fb1-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="91fb1-124">Dozwolony jest tylko jeden znak.</span><span class="sxs-lookup"><span data-stu-id="91fb1-124">Only one character is allowed.</span></span> <span data-ttu-id="91fb1-125">Witaj **domyślne** wartość jest **przecinkiem (',')**.</span><span class="sxs-lookup"><span data-stu-id="91fb1-125">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="91fb1-126">toouse znaku Unicode, można znaleźć zbyt[znaków Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello odpowiedni kod dla niego.</span><span class="sxs-lookup"><span data-stu-id="91fb1-126">toouse a Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="91fb1-127">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-127">No</span></span> |
| <span data-ttu-id="91fb1-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="91fb1-128">rowDelimiter</span></span> |<span data-ttu-id="91fb1-129">znak Hello używać tooseparate wierszy w pliku.</span><span class="sxs-lookup"><span data-stu-id="91fb1-129">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="91fb1-130">Dozwolony jest tylko jeden znak.</span><span class="sxs-lookup"><span data-stu-id="91fb1-130">Only one character is allowed.</span></span> <span data-ttu-id="91fb1-131">Witaj **domyślne** wartość jest dowolne hello następujące wartości na odczyt: **["\r\n", "\r", "\n"]** i **"\r\n"** podczas zapisu.</span><span class="sxs-lookup"><span data-stu-id="91fb1-131">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="91fb1-132">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-132">No</span></span> |
| <span data-ttu-id="91fb1-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="91fb1-133">escapeChar</span></span> |<span data-ttu-id="91fb1-134">znaki specjalne Hello używane tooescape ogranicznik kolumny w hello zawartość pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="91fb1-134">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="91fb1-135">W przypadku tabeli nie można określić zarówno właściwości escapeChar, jak i quoteChar.</span><span class="sxs-lookup"><span data-stu-id="91fb1-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="91fb1-136">Dozwolony jest tylko jeden znak.</span><span class="sxs-lookup"><span data-stu-id="91fb1-136">Only one character is allowed.</span></span> <span data-ttu-id="91fb1-137">Brak wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="91fb1-137">No default value.</span></span> <br/><br/><span data-ttu-id="91fb1-138">Przykład: Jeśli masz przecinkiem (', ') ogranicznik kolumny hello, ale ma toohave hello przecinkami znaków w tekście hello (przykład: "tekst Hello, world"), można zdefiniować '$' jako znak ucieczki hello i użyj ciągu "Hello$, world" w źródle hello.</span><span class="sxs-lookup"><span data-stu-id="91fb1-138">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="91fb1-139">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-139">No</span></span> |
| <span data-ttu-id="91fb1-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="91fb1-140">quoteChar</span></span> |<span data-ttu-id="91fb1-141">znak Hello używany tooquote wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="91fb1-141">hello character used tooquote a string value.</span></span> <span data-ttu-id="91fb1-142">ograniczniki kolumn i wierszy wewnątrz znaków cudzysłowu hello Hello będzie traktowane jako część hello wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="91fb1-142">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="91fb1-143">Ta właściwość ma zastosowanie tooboth danych wejściowych i wyjściowych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="91fb1-143">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="91fb1-144">W przypadku tabeli nie można określić zarówno właściwości escapeChar, jak i quoteChar.</span><span class="sxs-lookup"><span data-stu-id="91fb1-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="91fb1-145">Dozwolony jest tylko jeden znak.</span><span class="sxs-lookup"><span data-stu-id="91fb1-145">Only one character is allowed.</span></span> <span data-ttu-id="91fb1-146">Brak wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="91fb1-146">No default value.</span></span> <br/><br/><span data-ttu-id="91fb1-147">Na przykład, jeśli masz przecinkiem (', ') ogranicznik kolumny hello, ale ma toohave przecinkami znaków w tekście hello (przykład: < Hello, world >), można zdefiniować "(podwójnego cudzysłowu) jako hello znaku cudzysłowu i używać ciąg hello"Hello, world"w źródle hello.</span><span class="sxs-lookup"><span data-stu-id="91fb1-147">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="91fb1-148">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-148">No</span></span> |
| <span data-ttu-id="91fb1-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="91fb1-149">nullValue</span></span> |<span data-ttu-id="91fb1-150">Co najmniej jeden znak używany toorepresent wartość null.</span><span class="sxs-lookup"><span data-stu-id="91fb1-150">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="91fb1-151">Co najmniej jeden znak.</span><span class="sxs-lookup"><span data-stu-id="91fb1-151">One or more characters.</span></span> <span data-ttu-id="91fb1-152">Witaj **domyślne** wartości są **"\N" i "NULL"** na odczyt i **"\N"** podczas zapisu.</span><span class="sxs-lookup"><span data-stu-id="91fb1-152">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="91fb1-153">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-153">No</span></span> |
| <span data-ttu-id="91fb1-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="91fb1-154">encodingName</span></span> |<span data-ttu-id="91fb1-155">Określ nazwę kodowania hello.</span><span class="sxs-lookup"><span data-stu-id="91fb1-155">Specify hello encoding name.</span></span> |<span data-ttu-id="91fb1-156">Prawidłowa nazwa kodowania.</span><span class="sxs-lookup"><span data-stu-id="91fb1-156">A valid encoding name.</span></span> <span data-ttu-id="91fb1-157">Zobacz [właściwość Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="91fb1-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="91fb1-158">Przykład: windows-1250 lub shift_jis.</span><span class="sxs-lookup"><span data-stu-id="91fb1-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="91fb1-159">Witaj **domyślne** wartość jest **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="91fb1-159">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="91fb1-160">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-160">No</span></span> |
| <span data-ttu-id="91fb1-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="91fb1-161">firstRowAsHeader</span></span> |<span data-ttu-id="91fb1-162">Określa, czy tooconsider hello pierwszego wiersza jako nagłówka.</span><span class="sxs-lookup"><span data-stu-id="91fb1-162">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="91fb1-163">W przypadku zestawu danych wejściowych usługa Data Factory odczytuje pierwszy wiersz jako nagłówek.</span><span class="sxs-lookup"><span data-stu-id="91fb1-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="91fb1-164">W przypadku zestawu danych wyjściowych usługa Data Factory zapisuje pierwszy wiersz jako nagłówek.</span><span class="sxs-lookup"><span data-stu-id="91fb1-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="91fb1-165">Aby uzyskać przykładowe scenariusze, zobacz sekcję [Scenariusze użycia właściwości `firstRowAsHeader` oraz `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="91fb1-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="91fb1-166">True</span><span class="sxs-lookup"><span data-stu-id="91fb1-166">True</span></span><br/><span data-ttu-id="91fb1-167"><b>False (domyślnie)</b></span><span class="sxs-lookup"><span data-stu-id="91fb1-167"><b>False (default)</b></span></span> |<span data-ttu-id="91fb1-168">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-168">No</span></span> |
| <span data-ttu-id="91fb1-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="91fb1-169">skipLineCount</span></span> |<span data-ttu-id="91fb1-170">Wskazuje liczbę hello tooskip wierszy podczas odczytywania danych z plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="91fb1-170">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="91fb1-171">Jeśli został określony zarówno skipLineCount i firstRowAsHeader, wiersze hello są pomijane najpierw, a następnie informacje o nagłówku hello jest do odczytu z pliku wejściowego hello.</span><span class="sxs-lookup"><span data-stu-id="91fb1-171">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="91fb1-172">Aby uzyskać przykładowe scenariusze, zobacz sekcję [Scenariusze użycia właściwości `firstRowAsHeader` oraz `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="91fb1-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="91fb1-173">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="91fb1-173">Integer</span></span> |<span data-ttu-id="91fb1-174">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-174">No</span></span> |
| <span data-ttu-id="91fb1-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="91fb1-175">treatEmptyAsNull</span></span> |<span data-ttu-id="91fb1-176">Określa, czy wartość tootreat null lub pusty ciąg jako wartość null, podczas odczytywania danych z pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="91fb1-176">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="91fb1-177">**True (domyślnie)**</span><span class="sxs-lookup"><span data-stu-id="91fb1-177">**True (default)**</span></span><br/><span data-ttu-id="91fb1-178">False</span><span class="sxs-lookup"><span data-stu-id="91fb1-178">False</span></span> |<span data-ttu-id="91fb1-179">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="91fb1-180">Przykład formatu TextFormat</span><span class="sxs-lookup"><span data-stu-id="91fb1-180">TextFormat example</span></span>
<span data-ttu-id="91fb1-181">W hello po definicji JSON dla zestawu danych niektóre właściwości opcjonalne hello określony.</span><span class="sxs-lookup"><span data-stu-id="91fb1-181">In hello following JSON definition for a dataset, some of hello optional properties are specified.</span></span>

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

<span data-ttu-id="91fb1-182">toouse `escapeChar` zamiast `quoteChar`, Zastąp wiersza hello `quoteChar` z następujących elementów escapeChar hello:</span><span class="sxs-lookup"><span data-stu-id="91fb1-182">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="91fb1-183">Scenariusze użycia właściwości firstRowAsHeader oraz skipLineCount</span><span class="sxs-lookup"><span data-stu-id="91fb1-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="91fb1-184">Są kopiowane z pliku źródłowego z systemem innym niż plik tooa tekstu i chcesz tooadd wiersz nagłówka, zawierający metadane schematu hello (na przykład: schematu SQL).</span><span class="sxs-lookup"><span data-stu-id="91fb1-184">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="91fb1-185">Określ `firstRowAsHeader` jako wartości true w hello wyjściowy zestaw danych dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="91fb1-185">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="91fb1-186">Kopiowania z pliku tekstowego zawierającego zbiorniku plików z systemem innym niż tooa wiersz nagłówka i chcesz toodrop, który wiersz.</span><span class="sxs-lookup"><span data-stu-id="91fb1-186">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="91fb1-187">Określ `firstRowAsHeader` jako wartość true w zestawie danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="91fb1-187">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="91fb1-188">Kopiowania z pliku tekstowego i mają tooskip kilka wierszy na początku hello, które nie zawierają żadnych informacji danych lub nagłówek.</span><span class="sxs-lookup"><span data-stu-id="91fb1-188">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="91fb1-189">Określ `skipLineCount` tooindicate hello liczba wierszy toobe pominięte.</span><span class="sxs-lookup"><span data-stu-id="91fb1-189">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="91fb1-190">Jeśli hello pozostałej części pliku hello zawiera wiersz nagłówka, można również określić `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="91fb1-190">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="91fb1-191">Jeśli oba `skipLineCount` i `firstRowAsHeader` są określone wiersze hello są pomijane najpierw, a następnie informacje o nagłówku hello jest do odczytu z pliku wejściowego hello</span><span class="sxs-lookup"><span data-stu-id="91fb1-191">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

## <a name="json-format"></a><span data-ttu-id="91fb1-192">JSON format</span><span class="sxs-lookup"><span data-stu-id="91fb1-192">JSON format</span></span>
<span data-ttu-id="91fb1-193">zbyt**importu/eksportu pliku JSON jako — jest do/z bazy danych Azure rozwiązania Cosmos**, zobacz hello [dokumentów JSON importu/eksportu](data-factory-azure-documentdb-connector.md#importexport-json-documents) sekcji [przenoszenie danych do/z bazy danych Azure rozwiązania Cosmos](data-factory-azure-documentdb-connector.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="91fb1-193">too**import/export a JSON file as-is into/from Azure Cosmos DB**, hello see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="91fb1-194">Pliki w formacie JSON hello tooparse lub zapisać danych hello w formacie JSON, ustaw hello `type` właściwości w hello `format` sekcji zbyt**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="91fb1-194">If you want tooparse hello JSON files or write hello data in JSON format, set hello `type` property in hello `format` section too**JsonFormat**.</span></span> <span data-ttu-id="91fb1-195">Można również określić następujące hello **opcjonalne** właściwości w hello `format` sekcji.</span><span class="sxs-lookup"><span data-stu-id="91fb1-195">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="91fb1-196">Zobacz [JsonFormat przykład](#jsonformat-example) sekcję na temat tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="91fb1-196">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="91fb1-197">Właściwość</span><span class="sxs-lookup"><span data-stu-id="91fb1-197">Property</span></span> | <span data-ttu-id="91fb1-198">Opis</span><span class="sxs-lookup"><span data-stu-id="91fb1-198">Description</span></span> | <span data-ttu-id="91fb1-199">Wymagany</span><span class="sxs-lookup"><span data-stu-id="91fb1-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="91fb1-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="91fb1-200">filePattern</span></span> |<span data-ttu-id="91fb1-201">Wskazuje wzorzec hello danych przechowywanych w każdym pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="91fb1-201">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="91fb1-202">Dozwolone wartości to: **setOfObjects** i **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="91fb1-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="91fb1-203">Witaj **domyślne** wartość jest **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="91fb1-203">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="91fb1-204">Aby uzyskać szczegółowe informacje o tych wzorcach, zobacz sekcję [Wzorce plików JSON](#json-file-patterns).</span><span class="sxs-lookup"><span data-stu-id="91fb1-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="91fb1-205">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-205">No</span></span> |
| <span data-ttu-id="91fb1-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="91fb1-206">jsonNodeReference</span></span> | <span data-ttu-id="91fb1-207">Tooiterate i wyodrębniania danych z obiektów hello wewnątrz tablicy pola z hello sam wzorzec, określ ścieżkę JSON hello tablicy.</span><span class="sxs-lookup"><span data-stu-id="91fb1-207">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="91fb1-208">Ta właściwość jest obsługiwana tylko podczas kopiowania danych z plików JSON.</span><span class="sxs-lookup"><span data-stu-id="91fb1-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="91fb1-209">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-209">No</span></span> |
| <span data-ttu-id="91fb1-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="91fb1-210">jsonPathDefinition</span></span> | <span data-ttu-id="91fb1-211">Określ wyrażenie ścieżki JSON powitania dla każdego mapowania kolumn z nazwą dostosowanego kolumna (start małymi literami).</span><span class="sxs-lookup"><span data-stu-id="91fb1-211">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="91fb1-212">Ta właściwość jest obsługiwana tylko podczas kopiowania danych z plików JSON; dane możesz wyodrębnić z obiektu lub tablicy.</span><span class="sxs-lookup"><span data-stu-id="91fb1-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="91fb1-213">W przypadku pól w obszarze katalogu głównego obiektu zaczynać się od $ głównego; dla pola w tablicy hello wybierany przez `jsonNodeReference` właściwości, początkową hello elementu tablicy.</span><span class="sxs-lookup"><span data-stu-id="91fb1-213">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="91fb1-214">Zobacz [JsonFormat przykład](#jsonformat-example) sekcję na temat tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="91fb1-214">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="91fb1-215">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-215">No</span></span> |
| <span data-ttu-id="91fb1-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="91fb1-216">encodingName</span></span> |<span data-ttu-id="91fb1-217">Określ nazwę kodowania hello.</span><span class="sxs-lookup"><span data-stu-id="91fb1-217">Specify hello encoding name.</span></span> <span data-ttu-id="91fb1-218">Aby hello listę prawidłowych nazw kodowania, zobacz: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) właściwości.</span><span class="sxs-lookup"><span data-stu-id="91fb1-218">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="91fb1-219">Na przykład: windows-1250 lub shift_jis.</span><span class="sxs-lookup"><span data-stu-id="91fb1-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="91fb1-220">Witaj **domyślne** wartość to: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="91fb1-220">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="91fb1-221">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-221">No</span></span> |
| <span data-ttu-id="91fb1-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="91fb1-222">nestingSeparator</span></span> |<span data-ttu-id="91fb1-223">Znak, który jest używany tooseparate poziomów zagnieżdżenia.</span><span class="sxs-lookup"><span data-stu-id="91fb1-223">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="91fb1-224">Witaj, wartością domyślną jest "." (kropką).</span><span class="sxs-lookup"><span data-stu-id="91fb1-224">hello default value is '.' (dot).</span></span> |<span data-ttu-id="91fb1-225">Nie</span><span class="sxs-lookup"><span data-stu-id="91fb1-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="91fb1-226">Wzorce plików JSON</span><span class="sxs-lookup"><span data-stu-id="91fb1-226">JSON file patterns</span></span>

<span data-ttu-id="91fb1-227">Działanie kopiowania może przeanalizować składni powitania po wzorce pliki w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="91fb1-227">Copy activity can parse hello following patterns of JSON files:</span></span>

- <span data-ttu-id="91fb1-228">**Typ I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="91fb1-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="91fb1-229">Każdy plik zawiera pojedynczy obiekt lub wiele obiektów rozdzielonych wierszami bądź połączonych.</span><span class="sxs-lookup"><span data-stu-id="91fb1-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="91fb1-230">W przypadku wybrania tej opcji w zestawie danych wyjściowych działanie kopiowania tworzy pojedynczy plik JSON z każdym obiektem w osobnym wierszu (rozdzielanie wierszami).</span><span class="sxs-lookup"><span data-stu-id="91fb1-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="91fb1-231">**przykład kodu JSON z pojedynczym obiektem**</span><span class="sxs-lookup"><span data-stu-id="91fb1-231">**single object JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * <span data-ttu-id="91fb1-232">**przykład kodu JSON z obiektami rozdzielonymi wierszami**</span><span class="sxs-lookup"><span data-stu-id="91fb1-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="91fb1-233">**przykład kodu JSON z obiektami połączonymi**</span><span class="sxs-lookup"><span data-stu-id="91fb1-233">**concatenated JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- <span data-ttu-id="91fb1-234">**Typ II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="91fb1-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="91fb1-235">Każdy plik zawiera tablicę obiektów.</span><span class="sxs-lookup"><span data-stu-id="91fb1-235">Each file contains an array of objects.</span></span>

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a><span data-ttu-id="91fb1-236">Przykład formatu JsonFormat</span><span class="sxs-lookup"><span data-stu-id="91fb1-236">JsonFormat example</span></span>

<span data-ttu-id="91fb1-237">**Przypadek 1. Kopiowanie danych z plików JSON**</span><span class="sxs-lookup"><span data-stu-id="91fb1-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="91fb1-238">Zobacz powitania po dwóch próbek podczas kopiowania danych z plików JSON.</span><span class="sxs-lookup"><span data-stu-id="91fb1-238">See hello following two samples when copying data from JSON files.</span></span> <span data-ttu-id="91fb1-239">Witaj toonote punktów ogólne:</span><span class="sxs-lookup"><span data-stu-id="91fb1-239">hello generic points toonote:</span></span>

<span data-ttu-id="91fb1-240">**Przykład 1. Wyodrębnianie danych z obiektu i tablicy**</span><span class="sxs-lookup"><span data-stu-id="91fb1-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="91fb1-241">W tym przykładzie spodziewasz się, co główny obiekt JSON mapy toosingle rekordu w wyniku tabelarycznych.</span><span class="sxs-lookup"><span data-stu-id="91fb1-241">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="91fb1-242">Jeśli masz plik JSON z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="91fb1-242">If you have a JSON file with hello following content:</span></span>  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
<span data-ttu-id="91fb1-243">i mają toocopy sformatować go do tabeli Azure SQL w następujących hello przez wyodrębniania danych z obiektów i tablicy:</span><span class="sxs-lookup"><span data-stu-id="91fb1-243">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="91fb1-244">id</span><span class="sxs-lookup"><span data-stu-id="91fb1-244">id</span></span> | <span data-ttu-id="91fb1-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="91fb1-245">deviceType</span></span> | <span data-ttu-id="91fb1-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="91fb1-246">targetResourceType</span></span> | <span data-ttu-id="91fb1-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="91fb1-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="91fb1-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="91fb1-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="91fb1-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="91fb1-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="91fb1-250">PC</span><span class="sxs-lookup"><span data-stu-id="91fb1-250">PC</span></span> | <span data-ttu-id="91fb1-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="91fb1-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="91fb1-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="91fb1-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="91fb1-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="91fb1-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="91fb1-254">Witaj wejściowy zestaw danych o **JsonFormat** typ jest zdefiniowany w następujący sposób: (częściowa definicja z tylko hello odpowiednich części).</span><span class="sxs-lookup"><span data-stu-id="91fb1-254">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="91fb1-255">Więcej szczegółów:</span><span class="sxs-lookup"><span data-stu-id="91fb1-255">More specifically:</span></span>

- <span data-ttu-id="91fb1-256">`structure`sekcja definiuje hello dostosować nazwy kolumn i hello odpowiadającego typu danych podczas konwertowania danych tootabular.</span><span class="sxs-lookup"><span data-stu-id="91fb1-256">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="91fb1-257">Ta sekcja ma **opcjonalne** chyba, że należy toodo mapowania kolumn.</span><span class="sxs-lookup"><span data-stu-id="91fb1-257">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="91fb1-258">Zobacz [mapy kolumnach dataset toodestination kolumny zestawu danych źródła](data-factory-map-columns.md) sekcji, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="91fb1-258">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="91fb1-259">`jsonPathDefinition`Określa ścieżkę JSON powitania dla każdej kolumny wskazujące, gdzie tooextract hello dane.</span><span class="sxs-lookup"><span data-stu-id="91fb1-259">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="91fb1-260">toocopy danych z tablicy, można użyć **.property tablicy [x]** tooextract wartość hello podanej właściwości z obiektu x hello, lub można użyć  **tablicy [*] .property** toofind wartość Hello z dowolnych obiektów zawierających takie właściwości.</span><span class="sxs-lookup"><span data-stu-id="91fb1-260">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

<span data-ttu-id="91fb1-261">**Przykład 2: cross zastosować wiele obiektów o hello sam wzorca z tablicy**</span><span class="sxs-lookup"><span data-stu-id="91fb1-261">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="91fb1-262">W tym przykładzie oczekujesz tootransform jeden główny obiekt JSON do wielu rekordów w wyniku tabelarycznych.</span><span class="sxs-lookup"><span data-stu-id="91fb1-262">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="91fb1-263">Jeśli masz plik JSON z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="91fb1-263">If you have a JSON file with hello following content:</span></span>  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
<span data-ttu-id="91fb1-264">i chcesz sformatować go do tabeli Azure SQL w następujących hello przez spłaszczanie hello danych wewnątrz tablicy hello toocopy i krzyżowe z użyciem informacji hello wspólnej głównej:</span><span class="sxs-lookup"><span data-stu-id="91fb1-264">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="91fb1-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="91fb1-265">ordernumber</span></span> | <span data-ttu-id="91fb1-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="91fb1-266">orderdate</span></span> | <span data-ttu-id="91fb1-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="91fb1-267">order_pd</span></span> | <span data-ttu-id="91fb1-268">order_price</span><span class="sxs-lookup"><span data-stu-id="91fb1-268">order_price</span></span> | <span data-ttu-id="91fb1-269">city</span><span class="sxs-lookup"><span data-stu-id="91fb1-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="91fb1-270">01</span><span class="sxs-lookup"><span data-stu-id="91fb1-270">01</span></span> | <span data-ttu-id="91fb1-271">20170122</span><span class="sxs-lookup"><span data-stu-id="91fb1-271">20170122</span></span> | <span data-ttu-id="91fb1-272">P1</span><span class="sxs-lookup"><span data-stu-id="91fb1-272">P1</span></span> | <span data-ttu-id="91fb1-273">23</span><span class="sxs-lookup"><span data-stu-id="91fb1-273">23</span></span> | <span data-ttu-id="91fb1-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="91fb1-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="91fb1-275">01</span><span class="sxs-lookup"><span data-stu-id="91fb1-275">01</span></span> | <span data-ttu-id="91fb1-276">20170122</span><span class="sxs-lookup"><span data-stu-id="91fb1-276">20170122</span></span> | <span data-ttu-id="91fb1-277">P2</span><span class="sxs-lookup"><span data-stu-id="91fb1-277">P2</span></span> | <span data-ttu-id="91fb1-278">13</span><span class="sxs-lookup"><span data-stu-id="91fb1-278">13</span></span> | <span data-ttu-id="91fb1-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="91fb1-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="91fb1-280">01</span><span class="sxs-lookup"><span data-stu-id="91fb1-280">01</span></span> | <span data-ttu-id="91fb1-281">20170122</span><span class="sxs-lookup"><span data-stu-id="91fb1-281">20170122</span></span> | <span data-ttu-id="91fb1-282">P3</span><span class="sxs-lookup"><span data-stu-id="91fb1-282">P3</span></span> | <span data-ttu-id="91fb1-283">231</span><span class="sxs-lookup"><span data-stu-id="91fb1-283">231</span></span> | <span data-ttu-id="91fb1-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="91fb1-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="91fb1-285">Witaj wejściowy zestaw danych o **JsonFormat** typ jest zdefiniowany w następujący sposób: (częściowa definicja z tylko hello odpowiednich części).</span><span class="sxs-lookup"><span data-stu-id="91fb1-285">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="91fb1-286">Więcej szczegółów:</span><span class="sxs-lookup"><span data-stu-id="91fb1-286">More specifically:</span></span>

- <span data-ttu-id="91fb1-287">`structure`sekcja definiuje hello dostosować nazwy kolumn i hello odpowiadającego typu danych podczas konwertowania danych tootabular.</span><span class="sxs-lookup"><span data-stu-id="91fb1-287">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="91fb1-288">Ta sekcja ma **opcjonalne** chyba, że należy toodo mapowania kolumn.</span><span class="sxs-lookup"><span data-stu-id="91fb1-288">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="91fb1-289">Zobacz [mapy kolumnach dataset toodestination kolumny zestawu danych źródła](data-factory-map-columns.md) sekcji, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="91fb1-289">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="91fb1-290">`jsonNodeReference`Wskazuje tooiterate i wyodrębniania danych z obiektów hello hello sam wzorca w obszarze **tablicy** orderlines.</span><span class="sxs-lookup"><span data-stu-id="91fb1-290">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="91fb1-291">`jsonPathDefinition`Określa ścieżkę JSON powitania dla każdej kolumny wskazujące, gdzie tooextract hello dane.</span><span class="sxs-lookup"><span data-stu-id="91fb1-291">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="91fb1-292">W tym przykładzie "ordernumber", "orderdate" i "Miasto" podlegają główny obiekt ze ścieżką JSON, począwszy od "$.", podczas gdy "order_pd" i "order_price" są zdefiniowane z pochodzi od elementu tablicy hello bez "$". ścieżka.</span><span class="sxs-lookup"><span data-stu-id="91fb1-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

<span data-ttu-id="91fb1-293">**Należy zwrócić uwagę hello następujące punkty:**</span><span class="sxs-lookup"><span data-stu-id="91fb1-293">**Note hello following points:**</span></span>

* <span data-ttu-id="91fb1-294">Jeśli hello `structure` i `jsonPathDefinition` nie są zdefiniowane w zestawie danych usługi fabryka danych hello, hello działanie kopiowania wykrywa hello schematu z pierwszego obiektu hello i spłaszczanie hello całym obiektem.</span><span class="sxs-lookup"><span data-stu-id="91fb1-294">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="91fb1-295">Jeśli w danych wejściowych JSON hello tablicy, domyślnie hello działanie kopiowania konwertuje hello cała tablica wartości na ciąg.</span><span class="sxs-lookup"><span data-stu-id="91fb1-295">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="91fb1-296">Można wybrać tooextract danych za pomocą `jsonNodeReference` i/lub `jsonPathDefinition`, lub ją pominąć, nie określając je w `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="91fb1-296">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="91fb1-297">Jeśli istnieją zduplikowane nazwy w hello tym samym poziomie, hello działanie kopiowania wybiera hello ostatnią.</span><span class="sxs-lookup"><span data-stu-id="91fb1-297">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="91fb1-298">W przypadku nazw właściwości wielkość liter ma znaczenie.</span><span class="sxs-lookup"><span data-stu-id="91fb1-298">Property names are case-sensitive.</span></span> <span data-ttu-id="91fb1-299">Dwie właściwości o takiej samej nazwie, ale zapisanej przy użyciu różnej wielkości liter, są traktowane jako dwie osobne właściwości.</span><span class="sxs-lookup"><span data-stu-id="91fb1-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="91fb1-300">**Przypadek 2: Zapisywanie danych tooJSON pliku**</span><span class="sxs-lookup"><span data-stu-id="91fb1-300">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="91fb1-301">Jeśli masz hello w poniższej tabeli w bazie danych SQL:</span><span class="sxs-lookup"><span data-stu-id="91fb1-301">If you have hello following table in SQL Database:</span></span>

| <span data-ttu-id="91fb1-302">id</span><span class="sxs-lookup"><span data-stu-id="91fb1-302">id</span></span> | <span data-ttu-id="91fb1-303">order_date</span><span class="sxs-lookup"><span data-stu-id="91fb1-303">order_date</span></span> | <span data-ttu-id="91fb1-304">order_price</span><span class="sxs-lookup"><span data-stu-id="91fb1-304">order_price</span></span> | <span data-ttu-id="91fb1-305">order_by</span><span class="sxs-lookup"><span data-stu-id="91fb1-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="91fb1-306">1</span><span class="sxs-lookup"><span data-stu-id="91fb1-306">1</span></span> | <span data-ttu-id="91fb1-307">20170119</span><span class="sxs-lookup"><span data-stu-id="91fb1-307">20170119</span></span> | <span data-ttu-id="91fb1-308">2000</span><span class="sxs-lookup"><span data-stu-id="91fb1-308">2000</span></span> | <span data-ttu-id="91fb1-309">David</span><span class="sxs-lookup"><span data-stu-id="91fb1-309">David</span></span> |
| <span data-ttu-id="91fb1-310">2</span><span class="sxs-lookup"><span data-stu-id="91fb1-310">2</span></span> | <span data-ttu-id="91fb1-311">20170120</span><span class="sxs-lookup"><span data-stu-id="91fb1-311">20170120</span></span> | <span data-ttu-id="91fb1-312">3500</span><span class="sxs-lookup"><span data-stu-id="91fb1-312">3500</span></span> | <span data-ttu-id="91fb1-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="91fb1-313">Patrick</span></span> |
| <span data-ttu-id="91fb1-314">3</span><span class="sxs-lookup"><span data-stu-id="91fb1-314">3</span></span> | <span data-ttu-id="91fb1-315">20170121</span><span class="sxs-lookup"><span data-stu-id="91fb1-315">20170121</span></span> | <span data-ttu-id="91fb1-316">4000</span><span class="sxs-lookup"><span data-stu-id="91fb1-316">4000</span></span> | <span data-ttu-id="91fb1-317">Jason</span><span class="sxs-lookup"><span data-stu-id="91fb1-317">Jason</span></span> |

<span data-ttu-id="91fb1-318">i dla każdego rekordu oczekujesz obiekt JSON tooa toowrite w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="91fb1-318">and for each record, you expect toowrite tooa JSON object in hello following format:</span></span>
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

<span data-ttu-id="91fb1-319">Witaj wyjściowy zestaw danych z **JsonFormat** typ jest zdefiniowany w następujący sposób: (częściowa definicja z tylko hello odpowiednich części).</span><span class="sxs-lookup"><span data-stu-id="91fb1-319">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="91fb1-320">W szczególności `structure` sekcja definiuje hello dostosować nazwy właściwości w pliku docelowym `nestingSeparator` (domyślna to ".") są używane tooidentify hello zagnieżdżania warstwy z hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="91fb1-320">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") are used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="91fb1-321">Ta sekcja ma **opcjonalne** chyba, że nazwa właściwości hello toochange porównanie z nazwą kolumny źródła lub zagnieździć niektóre właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="91fb1-321">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a><span data-ttu-id="91fb1-322">AVRO format</span><span class="sxs-lookup"><span data-stu-id="91fb1-322">AVRO format</span></span>
<span data-ttu-id="91fb1-323">Tooparse hello Avro plików lub zapis danych hello format Avro, ustaw hello `format` `type` właściwości zbyt**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="91fb1-323">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="91fb1-324">Nie trzeba toospecify wszystkie właściwości w sekcji Format hello wewnątrz sekcji typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="91fb1-324">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="91fb1-325">Przykład:</span><span class="sxs-lookup"><span data-stu-id="91fb1-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="91fb1-326">format Avro toouse w tabeli programu Hive, można odwoływać się za[Apache Hive samouczek](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="91fb1-326">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="91fb1-327">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="91fb1-327">Note hello following points:</span></span>  

* <span data-ttu-id="91fb1-328">[Złożone typy danych](http://avro.apache.org/docs/current/spec.html#schema_complex) nie są obsługiwane (rejestruje, wyliczeń, tablic, map, Unii i usunięciu).</span><span class="sxs-lookup"><span data-stu-id="91fb1-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="91fb1-329">ORC format</span><span class="sxs-lookup"><span data-stu-id="91fb1-329">ORC format</span></span>
<span data-ttu-id="91fb1-330">Plików ORC hello tooparse lub zapisać danych hello w formacie ORC, ustaw hello `format` `type` właściwości zbyt**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="91fb1-330">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="91fb1-331">Nie trzeba toospecify wszystkie właściwości w sekcji Format hello wewnątrz sekcji typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="91fb1-331">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="91fb1-332">Przykład:</span><span class="sxs-lookup"><span data-stu-id="91fb1-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="91fb1-333">Jeśli nie kopiowania plików ORC **jako — jest** między lokalnymi i w chmurze magazyny danych należy hello tooinstall środowiska JRE 8 (Java Runtime Environment) na komputerze bramy.</span><span class="sxs-lookup"><span data-stu-id="91fb1-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="91fb1-334">Brama 64-bitowa wymaga 64-bitowego środowiska JRE, natomiast brama 32-bitowa — 32-bitowego środowiska JRE.</span><span class="sxs-lookup"><span data-stu-id="91fb1-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="91fb1-335">Obie wersje można znaleźć [tutaj](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="91fb1-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="91fb1-336">Wybierz odpowiednie hello.</span><span class="sxs-lookup"><span data-stu-id="91fb1-336">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="91fb1-337">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="91fb1-337">Note hello following points:</span></span>

* <span data-ttu-id="91fb1-338">Złożone typy danych nie są obsługiwane (struktura, mapa, lista, unia)</span><span class="sxs-lookup"><span data-stu-id="91fb1-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="91fb1-339">Plik ORC ma trzy [opcje związane z kompresją](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="91fb1-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="91fb1-340">Usługa Data Factory obsługuje odczyt danych z pliku ORC w dowolnym z tych skompresowanych formatów.</span><span class="sxs-lookup"><span data-stu-id="91fb1-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="91fb1-341">Używa kompresji hello kodera-dekodera jest hello metadanych tooread hello danych.</span><span class="sxs-lookup"><span data-stu-id="91fb1-341">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="91fb1-342">Jednak podczas zapisywania plików ORC tooan, fabryki danych wybiera ZLIB, który jest domyślnym hello ORC.</span><span class="sxs-lookup"><span data-stu-id="91fb1-342">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="91fb1-343">Obecnie nie są toooverride nie opcji to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="91fb1-343">Currently, there is no option toooverride this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="91fb1-344">Parquet format</span><span class="sxs-lookup"><span data-stu-id="91fb1-344">Parquet format</span></span>
<span data-ttu-id="91fb1-345">Tooparse hello Parquet plików lub zapis danych hello w formacie Parquet, ustaw hello `format` `type` właściwości zbyt**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="91fb1-345">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="91fb1-346">Nie trzeba toospecify wszystkie właściwości w sekcji Format hello wewnątrz sekcji typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="91fb1-346">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="91fb1-347">Przykład:</span><span class="sxs-lookup"><span data-stu-id="91fb1-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="91fb1-348">Jeśli nie są kopiowane pliki Parquet **jako — jest** między lokalnymi i w chmurze magazyny danych należy hello tooinstall środowiska JRE 8 (Java Runtime Environment) na komputerze bramy.</span><span class="sxs-lookup"><span data-stu-id="91fb1-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="91fb1-349">Brama 64-bitowa wymaga 64-bitowego środowiska JRE, natomiast brama 32-bitowa — 32-bitowego środowiska JRE.</span><span class="sxs-lookup"><span data-stu-id="91fb1-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="91fb1-350">Obie wersje można znaleźć [tutaj](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="91fb1-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="91fb1-351">Wybierz odpowiednie hello.</span><span class="sxs-lookup"><span data-stu-id="91fb1-351">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="91fb1-352">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="91fb1-352">Note hello following points:</span></span>

* <span data-ttu-id="91fb1-353">Złożone typy danych nie są obsługiwane (mapa, lista)</span><span class="sxs-lookup"><span data-stu-id="91fb1-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="91fb1-354">Plik parquet ma następujące opcje związane z kompresji hello: NONE, SNAPPY GZIP i LZO.</span><span class="sxs-lookup"><span data-stu-id="91fb1-354">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="91fb1-355">Usługa Data Factory obsługuje odczyt danych z pliku ORC w dowolnym z tych skompresowanych formatów.</span><span class="sxs-lookup"><span data-stu-id="91fb1-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="91fb1-356">Koder-dekoder kompresji hello używa hello metadanych tooread hello danych.</span><span class="sxs-lookup"><span data-stu-id="91fb1-356">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="91fb1-357">Jednak podczas zapisywania pliku Parquet tooa, fabryki danych wybiera SNAPPY, jest domyślna hello Parquet formatu.</span><span class="sxs-lookup"><span data-stu-id="91fb1-357">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="91fb1-358">Obecnie nie są toooverride nie opcji to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="91fb1-358">Currently, there is no option toooverride this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="91fb1-359">Obsługa kompresji</span><span class="sxs-lookup"><span data-stu-id="91fb1-359">Compression support</span></span>
<span data-ttu-id="91fb1-360">Przetwarzania dużych zestawów danych może spowodować błąd We/Wy i sieci wąskich gardeł.</span><span class="sxs-lookup"><span data-stu-id="91fb1-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="91fb1-361">W związku z tym skompresowane dane w magazynach można nie tylko przyspieszenie działania transferu danych przez sieć hello i zaoszczędzić miejsce na dysku, ale również przełączyć istotne ulepszenia wydajności przetwarzania danych big data.</span><span class="sxs-lookup"><span data-stu-id="91fb1-361">Therefore, compressed data in stores can not only speed up data transfer across hello network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="91fb1-362">Obecnie kompresja jest obsługiwana dla magazynów danych opartych na plikach, takich jak obiektów Blob platformy Azure lub lokalnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="91fb1-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="91fb1-363">Kompresja toospecify dla zestawu danych, użyj hello **kompresji** właściwości w elemencie dataset hello JSON jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="91fb1-363">toospecify compression for a dataset, use hello **compression** property in hello dataset JSON as in hello following example:</span></span>   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

<span data-ttu-id="91fb1-364">Załóżmy, że hello przykładowego zestawu danych jest używany jako dane wyjściowe hello działanie kopiowania, hello kompresuje działania kopiowania hello dane wyjściowe z kodera-dekodera GZIP przy użyciu optymalny stosunek, a następnie wpisz hello skompresowane dane do pliku o nazwie pagecounts.csv.gz w hello magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="91fb1-364">Suppose hello sample dataset is used as hello output of a copy activity, hello copy activity compresses hello output data with GZIP codec using optimal ratio and then write hello compressed data into a file named pagecounts.csv.gz in hello Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="91fb1-365">Ustawienia kompresji nie są obsługiwane dla danych w hello **AvroFormat**, **OrcFormat**, lub **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="91fb1-365">Compression settings are not supported for data in hello **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="91fb1-366">Podczas odczytywania plików w tych formatach, fabryki danych wykrywa i używa koder-dekoder kompresji hello w hello metadanych.</span><span class="sxs-lookup"><span data-stu-id="91fb1-366">When reading files in these formats, Data Factory detects and uses hello compression codec in hello metadata.</span></span> <span data-ttu-id="91fb1-367">Podczas zapisywania toofiles w tych formatach, fabryki danych wybiera hello domyślne koder-dekoder kompresji w tym formacie.</span><span class="sxs-lookup"><span data-stu-id="91fb1-367">When writing toofiles in these formats, Data Factory chooses hello default compression codec for that format.</span></span> <span data-ttu-id="91fb1-368">Na przykład ZLIB OrcFormat i SNAPPY dla ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="91fb1-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="91fb1-369">Witaj **kompresji** sekcji ma dwie właściwości:</span><span class="sxs-lookup"><span data-stu-id="91fb1-369">hello **compression** section has two properties:</span></span>  

* <span data-ttu-id="91fb1-370">**Typ:** hello koder-dekoder kompresji, które mogą być **GZIP**, **Deflate**, **BZIP2**, lub **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="91fb1-370">**Type:** hello compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="91fb1-371">**Poziom:** hello kompresji, które mogą być **optymalna** lub **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="91fb1-371">**Level:** hello compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="91fb1-372">**Najszybszym:** hello kompresji operacji powinno zakończyć się tak szybko jak to możliwe, nawet jeśli nie jest optymalnie skompresowany plik wynikowy hello.</span><span class="sxs-lookup"><span data-stu-id="91fb1-372">**Fastest:** hello compression operation should complete as quickly as possible, even if hello resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="91fb1-373">**Optymalne**: hello kompresji operacja powinna być optymalnie kompresowana, nawet jeśli hello operacja trwa dłużej toocomplete czasu.</span><span class="sxs-lookup"><span data-stu-id="91fb1-373">**Optimal**: hello compression operation should be optimally compressed, even if hello operation takes a longer time toocomplete.</span></span>

    <span data-ttu-id="91fb1-374">Aby uzyskać więcej informacji, zobacz [poziom kompresji](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="91fb1-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="91fb1-375">Po określeniu `compression` właściwość w zestawie danych wejściowych JSON, hello potoku można odczytać skompresowane dane ze źródła hello; i po określeniu właściwości hello w zestawie danych wyjściowych JSON aktywności kopiowania hello może zapisywać docelowego toohello skompresowane dane.</span><span class="sxs-lookup"><span data-stu-id="91fb1-375">When you specify `compression` property in an input dataset JSON, hello pipeline can read compressed data from hello source; and when you specify hello property in an output dataset JSON, hello copy activity can write compressed data toohello destination.</span></span> <span data-ttu-id="91fb1-376">Poniżej przedstawiono kilka przykładowych scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="91fb1-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="91fb1-377">Odczytywać skompresowane GZIP danych obiektów blob platformy Azure, zdekompresować i zapisać wynik danych tooan — bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="91fb1-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data tooan Azure SQL database.</span></span> <span data-ttu-id="91fb1-378">Zdefiniuj hello wejściowych obiektu Blob Azure zestaw danych o hello `compression` `type` właściwość JSON jako GZIP.</span><span class="sxs-lookup"><span data-stu-id="91fb1-378">You define hello input Azure Blob dataset with hello `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="91fb1-379">Odczyt danych z pliku tekstowego z lokalnego systemu plików, skompresować je w formacie GZip i zapisać hello skompresowane dane tooan obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="91fb1-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write hello compressed data tooan Azure blob.</span></span> <span data-ttu-id="91fb1-380">Zdefiniuj wyjściowy zestaw danych obiektów Blob platformy Azure z hello `compression` `type` właściwość JSON jako GZip.</span><span class="sxs-lookup"><span data-stu-id="91fb1-380">You define an output Azure Blob dataset with hello `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="91fb1-381">Plik zip odczytu z serwera FTP zdekompresować plików hello tooget wewnątrz i trafić tych plików do usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="91fb1-381">Read .zip file from FTP server, decompress it tooget hello files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="91fb1-382">Zdefiniuj zestaw danych wejściowych FTP z hello `compression` `type` właściwość JSON jako ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="91fb1-382">You define an input FTP dataset with hello `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="91fb1-383">Odczytywać skompresowane GZIP danych obiektów blob platformy Azure, zdekompresować skompresować je przy użyciu BZIP2 i zapisać wynik tooan danych obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="91fb1-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data tooan Azure blob.</span></span> <span data-ttu-id="91fb1-384">Zdefiniuj hello wejściowych obiektu Blob Azure zestaw danych o `compression` `type` ustawić tooGZIP i hello wyjściowy zestaw danych z `compression` `type` ustawiony w tym przypadku tooBZIP2.</span><span class="sxs-lookup"><span data-stu-id="91fb1-384">You define hello input Azure Blob dataset with `compression` `type` set tooGZIP and hello output dataset with `compression` `type` set tooBZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="91fb1-385">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91fb1-385">Next steps</span></span>
<span data-ttu-id="91fb1-386">Zobacz powitania po artykułach magazynów opartych na plikach danych obsługiwane przez usługi fabryka danych Azure:</span><span class="sxs-lookup"><span data-stu-id="91fb1-386">See hello following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="91fb1-387">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="91fb1-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="91fb1-388">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="91fb1-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="91fb1-389">FTP</span><span class="sxs-lookup"><span data-stu-id="91fb1-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="91fb1-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="91fb1-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="91fb1-391">System plików</span><span class="sxs-lookup"><span data-stu-id="91fb1-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="91fb1-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="91fb1-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
