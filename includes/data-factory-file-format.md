## <a name="specifying-formats"></a><span data-ttu-id="cfb2a-101">Określanie formatów</span><span class="sxs-lookup"><span data-stu-id="cfb2a-101">Specifying formats</span></span>
<span data-ttu-id="cfb2a-102">Fabryka danych Azure obsługuje następujące typy format hello:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-102">Azure Data Factory supports hello following format types:</span></span>

* [<span data-ttu-id="cfb2a-103">Format tekstu</span><span class="sxs-lookup"><span data-stu-id="cfb2a-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="cfb2a-104">Format JSON</span><span class="sxs-lookup"><span data-stu-id="cfb2a-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="cfb2a-105">Format Avro</span><span class="sxs-lookup"><span data-stu-id="cfb2a-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="cfb2a-106">Format ORC</span><span class="sxs-lookup"><span data-stu-id="cfb2a-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="cfb2a-107">Format Parquet</span><span class="sxs-lookup"><span data-stu-id="cfb2a-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="cfb2a-108">Określanie formatu TextFormat</span><span class="sxs-lookup"><span data-stu-id="cfb2a-108">Specifying TextFormat</span></span>
<span data-ttu-id="cfb2a-109">Pliki tekstowe hello tooparse lub zapisać hello danych w formacie tekstowym, ustaw hello `format` `type` właściwości zbyt**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-109">If you want tooparse hello text files or write hello data in text format, set hello `format` `type` property too**TextFormat**.</span></span> <span data-ttu-id="cfb2a-110">Można również określić następujące hello **opcjonalne** właściwości w hello `format` sekcji.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-110">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="cfb2a-111">Zobacz [przykład TextFormat](#textformat-example) sekcję na temat tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-111">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="cfb2a-112">Właściwość</span><span class="sxs-lookup"><span data-stu-id="cfb2a-112">Property</span></span> | <span data-ttu-id="cfb2a-113">Opis</span><span class="sxs-lookup"><span data-stu-id="cfb2a-113">Description</span></span> | <span data-ttu-id="cfb2a-114">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="cfb2a-114">Allowed values</span></span> | <span data-ttu-id="cfb2a-115">Wymagany</span><span class="sxs-lookup"><span data-stu-id="cfb2a-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cfb2a-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="cfb2a-116">columnDelimiter</span></span> |<span data-ttu-id="cfb2a-117">znak Hello używać tooseparate kolumn w pliku.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-117">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="cfb2a-118">Można rozważyć toouse rzadkich char nie do drukowania, który prawdopodobnie nie istnieje w danych: Określ, np. "\u0001" reprezentujące Start z pozycji (raportu o kondycji).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-118">You can consider toouse a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="cfb2a-119">Dozwolony jest tylko jeden znak.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-119">Only one character is allowed.</span></span> <span data-ttu-id="cfb2a-120">Witaj **domyślne** wartość jest **przecinkiem (',')**.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-120">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="cfb2a-121">toouse znaków Unicode, można znaleźć zbyt[znaków Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello odpowiedni kod dla niego.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-121">toouse an Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="cfb2a-122">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-122">No</span></span> |
| <span data-ttu-id="cfb2a-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="cfb2a-123">rowDelimiter</span></span> |<span data-ttu-id="cfb2a-124">znak Hello używać tooseparate wierszy w pliku.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-124">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="cfb2a-125">Dozwolony jest tylko jeden znak.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-125">Only one character is allowed.</span></span> <span data-ttu-id="cfb2a-126">Witaj **domyślne** wartość jest dowolne hello następujące wartości na odczyt: **["\r\n", "\r", "\n"]** i **"\r\n"** podczas zapisu.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-126">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="cfb2a-127">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-127">No</span></span> |
| <span data-ttu-id="cfb2a-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="cfb2a-128">escapeChar</span></span> |<span data-ttu-id="cfb2a-129">znaki specjalne Hello używane tooescape ogranicznik kolumny w hello zawartość pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-129">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="cfb2a-130">W przypadku tabeli nie można określić zarówno właściwości escapeChar, jak i quoteChar.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="cfb2a-131">Dozwolony jest tylko jeden znak.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-131">Only one character is allowed.</span></span> <span data-ttu-id="cfb2a-132">Brak wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-132">No default value.</span></span> <br/><br/><span data-ttu-id="cfb2a-133">Przykład: Jeśli masz przecinkiem (', ') ogranicznik kolumny hello, ale ma toohave hello przecinkami znaków w tekście hello (przykład: "tekst Hello, world"), można zdefiniować '$' jako znak ucieczki hello i użyj ciągu "Hello$, world" w źródle hello.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-133">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="cfb2a-134">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-134">No</span></span> |
| <span data-ttu-id="cfb2a-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="cfb2a-135">quoteChar</span></span> |<span data-ttu-id="cfb2a-136">znak Hello używany tooquote wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-136">hello character used tooquote a string value.</span></span> <span data-ttu-id="cfb2a-137">ograniczniki kolumn i wierszy wewnątrz znaków cudzysłowu hello Hello będzie traktowane jako część hello wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-137">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="cfb2a-138">Ta właściwość ma zastosowanie tooboth danych wejściowych i wyjściowych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-138">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="cfb2a-139">W przypadku tabeli nie można określić zarówno właściwości escapeChar, jak i quoteChar.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="cfb2a-140">Dozwolony jest tylko jeden znak.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-140">Only one character is allowed.</span></span> <span data-ttu-id="cfb2a-141">Brak wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-141">No default value.</span></span> <br/><br/><span data-ttu-id="cfb2a-142">Na przykład, jeśli masz przecinkiem (', ') ogranicznik kolumny hello, ale ma toohave przecinkami znaków w tekście hello (przykład: < Hello, world >), można zdefiniować "(podwójnego cudzysłowu) jako hello znaku cudzysłowu i używać ciąg hello"Hello, world"w źródle hello.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-142">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="cfb2a-143">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-143">No</span></span> |
| <span data-ttu-id="cfb2a-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="cfb2a-144">nullValue</span></span> |<span data-ttu-id="cfb2a-145">Co najmniej jeden znak używany toorepresent wartość null.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-145">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="cfb2a-146">Co najmniej jeden znak.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-146">One or more characters.</span></span> <span data-ttu-id="cfb2a-147">Witaj **domyślne** wartości są **"\N" i "NULL"** na odczyt i **"\N"** podczas zapisu.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-147">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="cfb2a-148">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-148">No</span></span> |
| <span data-ttu-id="cfb2a-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="cfb2a-149">encodingName</span></span> |<span data-ttu-id="cfb2a-150">Określ nazwę kodowania hello.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-150">Specify hello encoding name.</span></span> |<span data-ttu-id="cfb2a-151">Prawidłowa nazwa kodowania.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-151">A valid encoding name.</span></span> <span data-ttu-id="cfb2a-152">Zobacz [właściwość Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="cfb2a-153">Przykład: windows-1250 lub shift_jis.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="cfb2a-154">Witaj **domyślne** wartość jest **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-154">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="cfb2a-155">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-155">No</span></span> |
| <span data-ttu-id="cfb2a-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="cfb2a-156">firstRowAsHeader</span></span> |<span data-ttu-id="cfb2a-157">Określa, czy tooconsider hello pierwszego wiersza jako nagłówka.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-157">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="cfb2a-158">W przypadku zestawu danych wejściowych usługa Data Factory odczytuje pierwszy wiersz jako nagłówek.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="cfb2a-159">W przypadku zestawu danych wyjściowych usługa Data Factory zapisuje pierwszy wiersz jako nagłówek.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="cfb2a-160">Aby uzyskać przykładowe scenariusze, zobacz sekcję [Scenariusze użycia właściwości `firstRowAsHeader` oraz `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="cfb2a-161">True</span><span class="sxs-lookup"><span data-stu-id="cfb2a-161">True</span></span><br/><span data-ttu-id="cfb2a-162">**False (domyślnie)**</span><span class="sxs-lookup"><span data-stu-id="cfb2a-162">**False (default)**</span></span> |<span data-ttu-id="cfb2a-163">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-163">No</span></span> |
| <span data-ttu-id="cfb2a-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="cfb2a-164">skipLineCount</span></span> |<span data-ttu-id="cfb2a-165">Wskazuje liczbę hello tooskip wierszy podczas odczytywania danych z plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-165">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="cfb2a-166">Jeśli został określony zarówno skipLineCount i firstRowAsHeader, wiersze hello są pomijane najpierw, a następnie informacje o nagłówku hello jest do odczytu z pliku wejściowego hello.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-166">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="cfb2a-167">Aby uzyskać przykładowe scenariusze, zobacz sekcję [Scenariusze użycia właściwości `firstRowAsHeader` oraz `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="cfb2a-168">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="cfb2a-168">Integer</span></span> |<span data-ttu-id="cfb2a-169">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-169">No</span></span> |
| <span data-ttu-id="cfb2a-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="cfb2a-170">treatEmptyAsNull</span></span> |<span data-ttu-id="cfb2a-171">Określa, czy wartość tootreat null lub pusty ciąg jako wartość null, podczas odczytywania danych z pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-171">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="cfb2a-172">**True (domyślnie)**</span><span class="sxs-lookup"><span data-stu-id="cfb2a-172">**True (default)**</span></span><br/><span data-ttu-id="cfb2a-173">False</span><span class="sxs-lookup"><span data-stu-id="cfb2a-173">False</span></span> |<span data-ttu-id="cfb2a-174">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="cfb2a-175">Przykład formatu TextFormat</span><span class="sxs-lookup"><span data-stu-id="cfb2a-175">TextFormat example</span></span>
<span data-ttu-id="cfb2a-176">Witaj poniższy przykład przedstawia niektóre właściwości formatu hello dla TextFormat.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-176">hello following sample shows some of hello format properties for TextFormat.</span></span>

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

<span data-ttu-id="cfb2a-177">toouse `escapeChar` zamiast `quoteChar`, Zastąp wiersza hello `quoteChar` z następujących elementów escapeChar hello:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-177">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="cfb2a-178">Scenariusze użycia właściwości firstRowAsHeader oraz skipLineCount</span><span class="sxs-lookup"><span data-stu-id="cfb2a-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="cfb2a-179">Są kopiowane z pliku źródłowego z systemem innym niż plik tooa tekstu i chcesz tooadd wiersz nagłówka, zawierający metadane schematu hello (na przykład: schematu SQL).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-179">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="cfb2a-180">Określ `firstRowAsHeader` jako wartości true w hello wyjściowy zestaw danych dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-180">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="cfb2a-181">Kopiowania z pliku tekstowego zawierającego zbiorniku plików z systemem innym niż tooa wiersz nagłówka i chcesz toodrop, który wiersz.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-181">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="cfb2a-182">Określ `firstRowAsHeader` jako wartość true w zestawie danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-182">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="cfb2a-183">Kopiowania z pliku tekstowego i mają tooskip kilka wierszy na początku hello, które nie zawierają żadnych informacji danych lub nagłówek.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-183">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="cfb2a-184">Określ `skipLineCount` tooindicate hello liczba wierszy toobe pominięte.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-184">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="cfb2a-185">Jeśli hello pozostałej części pliku hello zawiera wiersz nagłówka, można również określić `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-185">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="cfb2a-186">Jeśli oba `skipLineCount` i `firstRowAsHeader` są określone wiersze hello są pomijane najpierw, a następnie informacje o nagłówku hello jest do odczytu z pliku wejściowego hello</span><span class="sxs-lookup"><span data-stu-id="cfb2a-186">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="cfb2a-187">Określanie formatu JsonFormat</span><span class="sxs-lookup"><span data-stu-id="cfb2a-187">Specifying JsonFormat</span></span>
<span data-ttu-id="cfb2a-188">zbyt**importu/eksportu pliki JSON-jest do/z bazy danych Azure rozwiązania Cosmos**, zobacz [dokumentów JSON importu/eksportu](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) części hello Azure DB rozwiązania Cosmos łącznika ze szczegółami.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-188">too**import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in hello Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="cfb2a-189">Pliki w formacie JSON hello tooparse lub zapisać danych hello w formacie JSON, ustaw hello `format` `type` właściwości zbyt**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-189">If you want tooparse hello JSON files or write hello data in JSON format, set hello `format` `type` property too**JsonFormat**.</span></span> <span data-ttu-id="cfb2a-190">Można również określić następujące hello **opcjonalne** właściwości w hello `format` sekcji.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-190">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="cfb2a-191">Zobacz [JsonFormat przykład](#jsonformat-example) sekcję na temat tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-191">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="cfb2a-192">Właściwość</span><span class="sxs-lookup"><span data-stu-id="cfb2a-192">Property</span></span> | <span data-ttu-id="cfb2a-193">Opis</span><span class="sxs-lookup"><span data-stu-id="cfb2a-193">Description</span></span> | <span data-ttu-id="cfb2a-194">Wymagany</span><span class="sxs-lookup"><span data-stu-id="cfb2a-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cfb2a-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="cfb2a-195">filePattern</span></span> |<span data-ttu-id="cfb2a-196">Wskazuje wzorzec hello danych przechowywanych w każdym pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-196">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="cfb2a-197">Dozwolone wartości to: **setOfObjects** i **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="cfb2a-198">Witaj **domyślne** wartość jest **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-198">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="cfb2a-199">Aby uzyskać szczegółowe informacje o tych wzorcach, zobacz sekcję [Wzorce plików JSON](#json-file-patterns).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="cfb2a-200">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-200">No</span></span> |
| <span data-ttu-id="cfb2a-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="cfb2a-201">jsonNodeReference</span></span> | <span data-ttu-id="cfb2a-202">Tooiterate i wyodrębniania danych z obiektów hello wewnątrz tablicy pola z hello sam wzorzec, określ ścieżkę JSON hello tablicy.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-202">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="cfb2a-203">Ta właściwość jest obsługiwana tylko podczas kopiowania danych z plików JSON.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="cfb2a-204">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-204">No</span></span> |
| <span data-ttu-id="cfb2a-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="cfb2a-205">jsonPathDefinition</span></span> | <span data-ttu-id="cfb2a-206">Określ wyrażenie ścieżki JSON powitania dla każdego mapowania kolumn z nazwą dostosowanego kolumna (start małymi literami).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-206">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="cfb2a-207">Ta właściwość jest obsługiwana tylko podczas kopiowania danych z plików JSON; dane możesz wyodrębnić z obiektu lub tablicy.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="cfb2a-208">W przypadku pól w obszarze katalogu głównego obiektu zaczynać się od $ głównego; dla pola w tablicy hello wybierany przez `jsonNodeReference` właściwości, początkową hello elementu tablicy.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-208">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="cfb2a-209">Zobacz [JsonFormat przykład](#jsonformat-example) sekcję na temat tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-209">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="cfb2a-210">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-210">No</span></span> |
| <span data-ttu-id="cfb2a-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="cfb2a-211">encodingName</span></span> |<span data-ttu-id="cfb2a-212">Określ nazwę kodowania hello.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-212">Specify hello encoding name.</span></span> <span data-ttu-id="cfb2a-213">Aby hello listę prawidłowych nazw kodowania, zobacz: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) właściwości.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-213">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="cfb2a-214">Na przykład: windows-1250 lub shift_jis.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="cfb2a-215">Witaj **domyślne** wartość to: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-215">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="cfb2a-216">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-216">No</span></span> |
| <span data-ttu-id="cfb2a-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="cfb2a-217">nestingSeparator</span></span> |<span data-ttu-id="cfb2a-218">Znak, który jest używany tooseparate poziomów zagnieżdżenia.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-218">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="cfb2a-219">Witaj, wartością domyślną jest "." (kropką).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-219">hello default value is '.' (dot).</span></span> |<span data-ttu-id="cfb2a-220">Nie</span><span class="sxs-lookup"><span data-stu-id="cfb2a-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="cfb2a-221">Wzorce plików JSON</span><span class="sxs-lookup"><span data-stu-id="cfb2a-221">JSON file patterns</span></span>

<span data-ttu-id="cfb2a-222">Działanie kopiowania może przeanalizować poniższe wzorce plików JSON:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="cfb2a-223">**Typ I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="cfb2a-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="cfb2a-224">Każdy plik zawiera pojedynczy obiekt lub wiele obiektów rozdzielonych wierszami bądź połączonych.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="cfb2a-225">W przypadku wybrania tej opcji w zestawie danych wyjściowych działanie kopiowania tworzy pojedynczy plik JSON z każdym obiektem w osobnym wierszu (rozdzielanie wierszami).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="cfb2a-226">**przykład kodu JSON z pojedynczym obiektem**</span><span class="sxs-lookup"><span data-stu-id="cfb2a-226">**single object JSON example**</span></span>

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

    * <span data-ttu-id="cfb2a-227">**przykład kodu JSON z obiektami rozdzielonymi wierszami**</span><span class="sxs-lookup"><span data-stu-id="cfb2a-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="cfb2a-228">**przykład kodu JSON z obiektami połączonymi**</span><span class="sxs-lookup"><span data-stu-id="cfb2a-228">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="cfb2a-229">**Typ II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="cfb2a-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="cfb2a-230">Każdy plik zawiera tablicę obiektów.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-230">Each file contains an array of objects.</span></span>

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

#### <a name="jsonformat-example"></a><span data-ttu-id="cfb2a-231">Przykład formatu JsonFormat</span><span class="sxs-lookup"><span data-stu-id="cfb2a-231">JsonFormat example</span></span>

<span data-ttu-id="cfb2a-232">**Przypadek 1. Kopiowanie danych z plików JSON**</span><span class="sxs-lookup"><span data-stu-id="cfb2a-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="cfb2a-233">Podczas kopiowania danych z plików JSON są wymienione poniżej dwa typy próbek i hello toonote ogólnego punktów:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-233">See below two types of samples when copying data from JSON files, and hello generic points toonote:</span></span>

<span data-ttu-id="cfb2a-234">**Przykład 1. Wyodrębnianie danych z obiektu i tablicy**</span><span class="sxs-lookup"><span data-stu-id="cfb2a-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="cfb2a-235">W tym przykładzie spodziewasz się, co główny obiekt JSON mapy toosingle rekordu w wyniku tabelarycznych.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-235">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="cfb2a-236">Jeśli masz plik JSON z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-236">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="cfb2a-237">i mają toocopy sformatować go do tabeli Azure SQL w następujących hello przez wyodrębniania danych z obiektów i tablicy:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-237">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="cfb2a-238">id</span><span class="sxs-lookup"><span data-stu-id="cfb2a-238">id</span></span> | <span data-ttu-id="cfb2a-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="cfb2a-239">deviceType</span></span> | <span data-ttu-id="cfb2a-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="cfb2a-240">targetResourceType</span></span> | <span data-ttu-id="cfb2a-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="cfb2a-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="cfb2a-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="cfb2a-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="cfb2a-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="cfb2a-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="cfb2a-244">PC</span><span class="sxs-lookup"><span data-stu-id="cfb2a-244">PC</span></span> | <span data-ttu-id="cfb2a-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="cfb2a-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="cfb2a-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="cfb2a-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="cfb2a-247">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="cfb2a-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="cfb2a-248">Witaj wejściowy zestaw danych o **JsonFormat** typ jest zdefiniowany w następujący sposób: (częściowa definicja z tylko hello odpowiednich części).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-248">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="cfb2a-249">Więcej szczegółów:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-249">More specifically:</span></span>

- <span data-ttu-id="cfb2a-250">`structure`sekcja definiuje hello dostosować nazwy kolumn i hello odpowiadającego typu danych podczas konwertowania danych tootabular.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-250">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="cfb2a-251">Ta sekcja ma **opcjonalne** chyba, że należy toodo mapowania kolumn.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-251">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="cfb2a-252">Aby uzyskać bardziej szczegółowe informacje, zobacz sekcję [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) (Określanie definicji struktury dla prostokątnych zestawów danych).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="cfb2a-253">`jsonPathDefinition`Określa ścieżkę JSON powitania dla każdej kolumny wskazujące, gdzie tooextract hello dane.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-253">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="cfb2a-254">toocopy danych z tablicy, można użyć **.property tablicy [x]** tooextract wartość hello podanej właściwości z obiektu x hello, lub można użyć  **tablicy [*] .property** toofind wartość Hello z dowolnych obiektów zawierających takie właściwości.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-254">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

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

<span data-ttu-id="cfb2a-255">**Przykład 2: cross zastosować wiele obiektów o hello sam wzorca z tablicy**</span><span class="sxs-lookup"><span data-stu-id="cfb2a-255">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="cfb2a-256">W tym przykładzie oczekujesz tootransform jeden główny obiekt JSON do wielu rekordów w wyniku tabelarycznych.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-256">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="cfb2a-257">Jeśli masz plik JSON z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-257">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="cfb2a-258">i chcesz sformatować go do tabeli Azure SQL w następujących hello przez spłaszczanie hello danych wewnątrz tablicy hello toocopy i krzyżowe z użyciem informacji hello wspólnej głównej:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-258">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="cfb2a-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="cfb2a-259">ordernumber</span></span> | <span data-ttu-id="cfb2a-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="cfb2a-260">orderdate</span></span> | <span data-ttu-id="cfb2a-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="cfb2a-261">order_pd</span></span> | <span data-ttu-id="cfb2a-262">order_price</span><span class="sxs-lookup"><span data-stu-id="cfb2a-262">order_price</span></span> | <span data-ttu-id="cfb2a-263">city</span><span class="sxs-lookup"><span data-stu-id="cfb2a-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="cfb2a-264">01</span><span class="sxs-lookup"><span data-stu-id="cfb2a-264">01</span></span> | <span data-ttu-id="cfb2a-265">20170122</span><span class="sxs-lookup"><span data-stu-id="cfb2a-265">20170122</span></span> | <span data-ttu-id="cfb2a-266">P1</span><span class="sxs-lookup"><span data-stu-id="cfb2a-266">P1</span></span> | <span data-ttu-id="cfb2a-267">23</span><span class="sxs-lookup"><span data-stu-id="cfb2a-267">23</span></span> | <span data-ttu-id="cfb2a-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="cfb2a-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="cfb2a-269">01</span><span class="sxs-lookup"><span data-stu-id="cfb2a-269">01</span></span> | <span data-ttu-id="cfb2a-270">20170122</span><span class="sxs-lookup"><span data-stu-id="cfb2a-270">20170122</span></span> | <span data-ttu-id="cfb2a-271">P2</span><span class="sxs-lookup"><span data-stu-id="cfb2a-271">P2</span></span> | <span data-ttu-id="cfb2a-272">13</span><span class="sxs-lookup"><span data-stu-id="cfb2a-272">13</span></span> | <span data-ttu-id="cfb2a-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="cfb2a-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="cfb2a-274">01</span><span class="sxs-lookup"><span data-stu-id="cfb2a-274">01</span></span> | <span data-ttu-id="cfb2a-275">20170122</span><span class="sxs-lookup"><span data-stu-id="cfb2a-275">20170122</span></span> | <span data-ttu-id="cfb2a-276">P3</span><span class="sxs-lookup"><span data-stu-id="cfb2a-276">P3</span></span> | <span data-ttu-id="cfb2a-277">231</span><span class="sxs-lookup"><span data-stu-id="cfb2a-277">231</span></span> | <span data-ttu-id="cfb2a-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="cfb2a-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="cfb2a-279">Witaj wejściowy zestaw danych o **JsonFormat** typ jest zdefiniowany w następujący sposób: (częściowa definicja z tylko hello odpowiednich części).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-279">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="cfb2a-280">Więcej szczegółów:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-280">More specifically:</span></span>

- <span data-ttu-id="cfb2a-281">`structure`sekcja definiuje hello dostosować nazwy kolumn i hello odpowiadającego typu danych podczas konwertowania danych tootabular.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-281">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="cfb2a-282">Ta sekcja ma **opcjonalne** chyba, że należy toodo mapowania kolumn.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-282">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="cfb2a-283">Aby uzyskać bardziej szczegółowe informacje, zobacz sekcję [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) (Określanie definicji struktury dla prostokątnych zestawów danych).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="cfb2a-284">`jsonNodeReference`Wskazuje tooiterate i wyodrębniania danych z obiektów hello hello sam wzorca w obszarze **tablicy** orderlines.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-284">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="cfb2a-285">`jsonPathDefinition`Określa ścieżkę JSON powitania dla każdej kolumny wskazujące, gdzie tooextract hello dane.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-285">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="cfb2a-286">W tym przykładzie "ordernumber", "orderdate" i "Miasto" podlegają główny obiekt ze ścieżką JSON, począwszy od "$.", podczas gdy "order_pd" i "order_price" są zdefiniowane z pochodzi od elementu tablicy hello bez "$". ścieżka.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

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

<span data-ttu-id="cfb2a-287">**Należy zwrócić uwagę hello następujące punkty:**</span><span class="sxs-lookup"><span data-stu-id="cfb2a-287">**Note hello following points:**</span></span>

* <span data-ttu-id="cfb2a-288">Jeśli hello `structure` i `jsonPathDefinition` nie są zdefiniowane w zestawie danych usługi fabryka danych hello, hello działanie kopiowania wykrywa hello schematu z pierwszego obiektu hello i spłaszczanie hello całym obiektem.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-288">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="cfb2a-289">Jeśli w danych wejściowych JSON hello tablicy, domyślnie hello działanie kopiowania konwertuje hello cała tablica wartości na ciąg.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-289">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="cfb2a-290">Można wybrać tooextract danych za pomocą `jsonNodeReference` i/lub `jsonPathDefinition`, lub ją pominąć, nie określając je w `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-290">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="cfb2a-291">Jeśli istnieją zduplikowane nazwy w hello tym samym poziomie, hello działanie kopiowania wybiera hello ostatnią.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-291">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="cfb2a-292">W przypadku nazw właściwości wielkość liter ma znaczenie.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-292">Property names are case-sensitive.</span></span> <span data-ttu-id="cfb2a-293">Dwie właściwości o takiej samej nazwie, ale zapisanej przy użyciu różnej wielkości liter, są traktowane jako dwie osobne właściwości.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="cfb2a-294">**Przypadek 2: Zapisywanie danych tooJSON pliku**</span><span class="sxs-lookup"><span data-stu-id="cfb2a-294">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="cfb2a-295">Jeśli masz poniższą tabelę w usłudze SQL Database:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="cfb2a-296">id</span><span class="sxs-lookup"><span data-stu-id="cfb2a-296">id</span></span> | <span data-ttu-id="cfb2a-297">order_date</span><span class="sxs-lookup"><span data-stu-id="cfb2a-297">order_date</span></span> | <span data-ttu-id="cfb2a-298">order_price</span><span class="sxs-lookup"><span data-stu-id="cfb2a-298">order_price</span></span> | <span data-ttu-id="cfb2a-299">order_by</span><span class="sxs-lookup"><span data-stu-id="cfb2a-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cfb2a-300">1</span><span class="sxs-lookup"><span data-stu-id="cfb2a-300">1</span></span> | <span data-ttu-id="cfb2a-301">20170119</span><span class="sxs-lookup"><span data-stu-id="cfb2a-301">20170119</span></span> | <span data-ttu-id="cfb2a-302">2000</span><span class="sxs-lookup"><span data-stu-id="cfb2a-302">2000</span></span> | <span data-ttu-id="cfb2a-303">David</span><span class="sxs-lookup"><span data-stu-id="cfb2a-303">David</span></span> |
| <span data-ttu-id="cfb2a-304">2</span><span class="sxs-lookup"><span data-stu-id="cfb2a-304">2</span></span> | <span data-ttu-id="cfb2a-305">20170120</span><span class="sxs-lookup"><span data-stu-id="cfb2a-305">20170120</span></span> | <span data-ttu-id="cfb2a-306">3500</span><span class="sxs-lookup"><span data-stu-id="cfb2a-306">3500</span></span> | <span data-ttu-id="cfb2a-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="cfb2a-307">Patrick</span></span> |
| <span data-ttu-id="cfb2a-308">3</span><span class="sxs-lookup"><span data-stu-id="cfb2a-308">3</span></span> | <span data-ttu-id="cfb2a-309">20170121</span><span class="sxs-lookup"><span data-stu-id="cfb2a-309">20170121</span></span> | <span data-ttu-id="cfb2a-310">4000</span><span class="sxs-lookup"><span data-stu-id="cfb2a-310">4000</span></span> | <span data-ttu-id="cfb2a-311">Jason</span><span class="sxs-lookup"><span data-stu-id="cfb2a-311">Jason</span></span> |

<span data-ttu-id="cfb2a-312">i dla każdego rekordu spodziewasz się toowrite obiekt JSON tooa w format:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-312">and for each record, you expect toowrite tooa JSON object in below format:</span></span>
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

<span data-ttu-id="cfb2a-313">Witaj wyjściowy zestaw danych z **JsonFormat** typ jest zdefiniowany w następujący sposób: (częściowa definicja z tylko hello odpowiednich części).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-313">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="cfb2a-314">W szczególności `structure` sekcja definiuje hello dostosować nazwy właściwości w pliku docelowym `nestingSeparator` (domyślna to ".") będą używane tooidentify hello zagnieżdżania warstwy z hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-314">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") will be used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="cfb2a-315">Ta sekcja ma **opcjonalne** chyba, że nazwa właściwości hello toochange porównanie z nazwą kolumny źródła lub zagnieździć niektóre właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-315">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

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

### <a name="specifying-avroformat"></a><span data-ttu-id="cfb2a-316">Określanie formatu AvroFormat</span><span class="sxs-lookup"><span data-stu-id="cfb2a-316">Specifying AvroFormat</span></span>
<span data-ttu-id="cfb2a-317">Tooparse hello Avro plików lub zapis danych hello format Avro, ustaw hello `format` `type` właściwości zbyt**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-317">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="cfb2a-318">Nie trzeba toospecify wszystkie właściwości w sekcji Format hello wewnątrz sekcji typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-318">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="cfb2a-319">Przykład:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="cfb2a-320">format Avro toouse w tabeli programu Hive, można odwoływać się za[Apache Hive samouczek](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-320">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="cfb2a-321">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-321">Note hello following points:</span></span>  

* <span data-ttu-id="cfb2a-322">[Złożone typy danych](http://avro.apache.org/docs/current/spec.html#schema_complex) nie są obsługiwane (rekordy, wyliczenia, tablice, mapy, unie i typy stałe).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="cfb2a-323">Określanie formatu OrcFormat</span><span class="sxs-lookup"><span data-stu-id="cfb2a-323">Specifying OrcFormat</span></span>
<span data-ttu-id="cfb2a-324">Plików ORC hello tooparse lub zapisać danych hello w formacie ORC, ustaw hello `format` `type` właściwości zbyt**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-324">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="cfb2a-325">Nie trzeba toospecify wszystkie właściwości w sekcji Format hello wewnątrz sekcji typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-325">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="cfb2a-326">Przykład:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="cfb2a-327">Jeśli nie kopiowania plików ORC **jako — jest** między lokalnymi i w chmurze magazyny danych należy hello tooinstall środowiska JRE 8 (Java Runtime Environment) na komputerze bramy.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="cfb2a-328">Brama 64-bitowa wymaga 64-bitowego środowiska JRE, natomiast brama 32-bitowa — 32-bitowego środowiska JRE.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="cfb2a-329">Obie wersje można znaleźć [tutaj](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="cfb2a-330">Wybierz odpowiednie hello.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-330">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="cfb2a-331">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-331">Note hello following points:</span></span>

* <span data-ttu-id="cfb2a-332">Złożone typy danych nie są obsługiwane (struktura, mapa, lista, unia)</span><span class="sxs-lookup"><span data-stu-id="cfb2a-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="cfb2a-333">Plik ORC ma trzy [opcje związane z kompresją](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="cfb2a-334">Usługa Data Factory obsługuje odczyt danych z pliku ORC w dowolnym z tych skompresowanych formatów.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="cfb2a-335">Używa kompresji hello kodera-dekodera jest hello metadanych tooread hello danych.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-335">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="cfb2a-336">Jednak podczas zapisywania plików ORC tooan, fabryki danych wybiera ZLIB, który jest domyślnym hello ORC.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-336">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="cfb2a-337">Obecnie nie są toooverride nie opcji to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-337">Currently, there is no option toooverride this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="cfb2a-338">Określanie formatu ParquetFormat</span><span class="sxs-lookup"><span data-stu-id="cfb2a-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="cfb2a-339">Tooparse hello Parquet plików lub zapis danych hello w formacie Parquet, ustaw hello `format` `type` właściwości zbyt**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-339">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="cfb2a-340">Nie trzeba toospecify wszystkie właściwości w sekcji Format hello wewnątrz sekcji typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-340">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="cfb2a-341">Przykład:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="cfb2a-342">Jeśli nie są kopiowane pliki Parquet **jako — jest** między lokalnymi i w chmurze magazyny danych należy hello tooinstall środowiska JRE 8 (Java Runtime Environment) na komputerze bramy.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="cfb2a-343">Brama 64-bitowa wymaga 64-bitowego środowiska JRE, natomiast brama 32-bitowa — 32-bitowego środowiska JRE.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="cfb2a-344">Obie wersje można znaleźć [tutaj](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="cfb2a-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="cfb2a-345">Wybierz odpowiednie hello.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-345">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="cfb2a-346">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="cfb2a-346">Note hello following points:</span></span>

* <span data-ttu-id="cfb2a-347">Złożone typy danych nie są obsługiwane (mapa, lista)</span><span class="sxs-lookup"><span data-stu-id="cfb2a-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="cfb2a-348">Plik parquet ma następujące opcje związane z kompresji hello: NONE, SNAPPY GZIP i LZO.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-348">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="cfb2a-349">Usługa Data Factory obsługuje odczyt danych z pliku ORC w dowolnym z tych skompresowanych formatów.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="cfb2a-350">Koder-dekoder kompresji hello używa hello metadanych tooread hello danych.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-350">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="cfb2a-351">Jednak podczas zapisywania pliku Parquet tooa, fabryki danych wybiera SNAPPY, jest domyślna hello Parquet formatu.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-351">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="cfb2a-352">Obecnie nie są toooverride nie opcji to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="cfb2a-352">Currently, there is no option toooverride this behavior.</span></span>
