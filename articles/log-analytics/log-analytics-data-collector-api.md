---
title: "aaaLog API modułów zbierających dane HTTP Analytics | Dokumentacja firmy Microsoft"
description: "Za pomocą hello interfejsu API modułów zbierających dane dziennika Analytics HTTP tooadd POST JSON danych toohello analizy dzienników repozytorium za pomocą dowolnego klienta, który można wywołać hello interfejsu API REST. W tym artykule opisano sposób toouse hello interfejsu API i zawiera przykłady toopublish danych przy użyciu różnych języków programowania."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a><span data-ttu-id="a1a70-104">Wysyłanie danych tooLog Analytics z hello interfejsu API modułów zbierających dane HTTP</span><span class="sxs-lookup"><span data-stu-id="a1a70-104">Send data tooLog Analytics with hello HTTP Data Collector API</span></span>
<span data-ttu-id="a1a70-105">W tym artykule opisano, jak toouse hello interfejsu API modułów zbierających dane HTTP toosend danych tooLog Analytics z klienta interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="a1a70-105">This article shows you how toouse hello HTTP Data Collector API toosend data tooLog Analytics from a REST API client.</span></span>  <span data-ttu-id="a1a70-106">Opisuje jak tooformat danych zbieranych przez skrypt lub aplikację, dołączyć go w żądaniu i mieć tego żądania uprawnień przez analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="a1a70-106">It describes how tooformat data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="a1a70-107">Przykłady są dostępne dla programu PowerShell, C# i Python.</span><span class="sxs-lookup"><span data-stu-id="a1a70-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="a1a70-108">Pojęcia</span><span class="sxs-lookup"><span data-stu-id="a1a70-108">Concepts</span></span>
<span data-ttu-id="a1a70-109">Możesz użyć hello interfejsu API modułów zbierających dane HTTP toosend danych tooLog Analytics za pomocą dowolnego klienta, który można wywołać interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="a1a70-109">You can use hello HTTP Data Collector API toosend data tooLog Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="a1a70-110">Może to być element runbook automatyzacji Azure, która gromadzi zarządzania danych z platformy Azure lub innej chmurze lub może być system zarządzania alternatywnego, który używa tooconsolidate analizy dzienników i analizowania danych.</span><span class="sxs-lookup"><span data-stu-id="a1a70-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics tooconsolidate and analyze data.</span></span>

<span data-ttu-id="a1a70-111">Wszystkie dane w repozytorium analizy dzienników hello są przechowywane jako rekord typu określonego rekordu.</span><span class="sxs-lookup"><span data-stu-id="a1a70-111">All data in hello Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="a1a70-112">Twoje dane toosend toohello interfejsu API modułów zbierających dane HTTP formacie wielu rekordów w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="a1a70-112">You format your data toosend toohello HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="a1a70-113">Podczas przesyłania danych hello pojedynczego rekordu jest tworzony w repozytorium powitania dla każdego rekordu w ładunku żądania hello.</span><span class="sxs-lookup"><span data-stu-id="a1a70-113">When you submit hello data, an individual record is created in hello repository for each record in hello request payload.</span></span>


![Omówienie modułów zbierających dane HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="a1a70-115">Utwórz żądanie</span><span class="sxs-lookup"><span data-stu-id="a1a70-115">Create a request</span></span>
<span data-ttu-id="a1a70-116">Moduł zbierający dane hello HTTP toouse interfejsu API, Utwórz żądanie POST zawiera toosend danych hello w JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="a1a70-116">toouse hello HTTP Data Collector API, you create a POST request that includes hello data toosend in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="a1a70-117">Witaj trzech kolejnych tabel listy hello atrybutów, które są wymagane dla każdego żądania.</span><span class="sxs-lookup"><span data-stu-id="a1a70-117">hello next three tables list hello attributes that are required for each request.</span></span> <span data-ttu-id="a1a70-118">Opisano każdy atrybut bardziej szczegółowo w dalszej części artykułu hello.</span><span class="sxs-lookup"><span data-stu-id="a1a70-118">We describe each attribute in more detail later in hello article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="a1a70-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="a1a70-119">Request URI</span></span>
| <span data-ttu-id="a1a70-120">Atrybut</span><span class="sxs-lookup"><span data-stu-id="a1a70-120">Attribute</span></span> | <span data-ttu-id="a1a70-121">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a1a70-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="a1a70-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="a1a70-122">Method</span></span> |<span data-ttu-id="a1a70-123">POST</span><span class="sxs-lookup"><span data-stu-id="a1a70-123">POST</span></span> |
| <span data-ttu-id="a1a70-124">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a1a70-124">URI</span></span> |<span data-ttu-id="a1a70-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="a1a70-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="a1a70-126">Typ zawartości</span><span class="sxs-lookup"><span data-stu-id="a1a70-126">Content type</span></span> |<span data-ttu-id="a1a70-127">application/json</span><span class="sxs-lookup"><span data-stu-id="a1a70-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="a1a70-128">Parametry identyfikatora URI żądania</span><span class="sxs-lookup"><span data-stu-id="a1a70-128">Request URI parameters</span></span>
| <span data-ttu-id="a1a70-129">Parametr</span><span class="sxs-lookup"><span data-stu-id="a1a70-129">Parameter</span></span> | <span data-ttu-id="a1a70-130">Opis</span><span class="sxs-lookup"><span data-stu-id="a1a70-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a1a70-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="a1a70-131">CustomerID</span></span> |<span data-ttu-id="a1a70-132">Witaj Unikatowy identyfikator dla obszaru roboczego programu Microsoft Operations Management Suite hello.</span><span class="sxs-lookup"><span data-stu-id="a1a70-132">hello unique identifier for hello Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="a1a70-133">Zasób</span><span class="sxs-lookup"><span data-stu-id="a1a70-133">Resource</span></span> |<span data-ttu-id="a1a70-134">Nazwa zasobu Hello interfejsu API: / api/logs.</span><span class="sxs-lookup"><span data-stu-id="a1a70-134">hello API resource name: /api/logs.</span></span> |
| <span data-ttu-id="a1a70-135">Wersja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a1a70-135">API Version</span></span> |<span data-ttu-id="a1a70-136">Wersja Hello toouse hello interfejsu API z tym żądaniem.</span><span class="sxs-lookup"><span data-stu-id="a1a70-136">hello version of hello API toouse with this request.</span></span> <span data-ttu-id="a1a70-137">Obecnie jest 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="a1a70-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a1a70-138">Nagłówki żądania</span><span class="sxs-lookup"><span data-stu-id="a1a70-138">Request headers</span></span>
| <span data-ttu-id="a1a70-139">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="a1a70-139">Header</span></span> | <span data-ttu-id="a1a70-140">Opis</span><span class="sxs-lookup"><span data-stu-id="a1a70-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a1a70-141">Autoryzacja</span><span class="sxs-lookup"><span data-stu-id="a1a70-141">Authorization</span></span> |<span data-ttu-id="a1a70-142">Witaj autoryzacji podpisu.</span><span class="sxs-lookup"><span data-stu-id="a1a70-142">hello authorization signature.</span></span> <span data-ttu-id="a1a70-143">W dalszej części artykułu hello możesz przeczytać temat toocreate SHA256 HMAC nagłówka.</span><span class="sxs-lookup"><span data-stu-id="a1a70-143">Later in hello article, you can read about how toocreate an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="a1a70-144">Typ dziennika</span><span class="sxs-lookup"><span data-stu-id="a1a70-144">Log-Type</span></span> |<span data-ttu-id="a1a70-145">Określ typ rekordu hello danych hello jest przesyłane.</span><span class="sxs-lookup"><span data-stu-id="a1a70-145">Specify hello record type of hello data that is being submitted.</span></span> <span data-ttu-id="a1a70-146">Typ dziennika hello obsługuje obecnie tylko znaki alfanumeryczne.</span><span class="sxs-lookup"><span data-stu-id="a1a70-146">Currently, hello log type supports only alpha characters.</span></span> <span data-ttu-id="a1a70-147">Nie obsługuje wartości numeryczne i znaki specjalne.</span><span class="sxs-lookup"><span data-stu-id="a1a70-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="a1a70-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="a1a70-148">x-ms-date</span></span> |<span data-ttu-id="a1a70-149">Data Hello przetworzono Żądanie hello w formacie RFC 1123.</span><span class="sxs-lookup"><span data-stu-id="a1a70-149">hello date that hello request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="a1a70-150">czas wygenerowany — pola</span><span class="sxs-lookup"><span data-stu-id="a1a70-150">time-generated-field</span></span> |<span data-ttu-id="a1a70-151">Hello nazwę pola danych hello zawiera sygnaturę czasową hello hello elementu danych.</span><span class="sxs-lookup"><span data-stu-id="a1a70-151">hello name of a field in hello data that contains hello timestamp of hello data item.</span></span> <span data-ttu-id="a1a70-152">Jeśli określisz pola, a następnie jego zawartość jest używana dla **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="a1a70-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="a1a70-153">Jeśli to pole nie jest określony, domyślnie dla hello **TimeGenerated** jest czas hello tego hello jest pozyskanych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="a1a70-153">If this field isn’t specified, hello default for **TimeGenerated** is hello time that hello message is ingested.</span></span> <span data-ttu-id="a1a70-154">Witaj zawartość pola wiadomość hello należy stosować hello ISO 8601 w formacie RRRR-MM-Ddtgg.</span><span class="sxs-lookup"><span data-stu-id="a1a70-154">hello contents of hello message field should follow hello ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="a1a70-155">Autoryzacja</span><span class="sxs-lookup"><span data-stu-id="a1a70-155">Authorization</span></span>
<span data-ttu-id="a1a70-156">Wszelkie toohello żądania interfejsu API modułów zbierających dane dziennika Analytics HTTP musi zawierać nagłówek uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="a1a70-156">Any request toohello Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="a1a70-157">tooauthenticate żądanie, musisz zalogować się Żądanie hello hello podstawowego lub hello dodatkowy klucz dla obszaru roboczego hello, w której wysłano żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="a1a70-157">tooauthenticate a request, you must sign hello request with either hello primary or hello secondary key for hello workspace that is making hello request.</span></span> <span data-ttu-id="a1a70-158">Następnie przekaż tego podpisu, jako część żądania hello.</span><span class="sxs-lookup"><span data-stu-id="a1a70-158">Then, pass that signature as part of hello request.</span></span>   

<span data-ttu-id="a1a70-159">Oto hello format nagłówka autoryzacji hello:</span><span class="sxs-lookup"><span data-stu-id="a1a70-159">Here's hello format for hello authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="a1a70-160">*WorkspaceID* jest unikatowy identyfikator obszaru roboczego usługi Operations Management Suite hello hello.</span><span class="sxs-lookup"><span data-stu-id="a1a70-160">*WorkspaceID* is hello unique identifier for hello Operations Management Suite workspace.</span></span> <span data-ttu-id="a1a70-161">*Podpis* jest [Hash-based kodu (metoda HMAC Message Authentication)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) jest utworzone na podstawie żądania hello i następnie obliczane przy użyciu hello [algorytm SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1a70-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from hello request and then computed by using hello [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="a1a70-162">Następnie należy kodować je przy użyciu kodowania Base64.</span><span class="sxs-lookup"><span data-stu-id="a1a70-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="a1a70-163">Użyj tego formatu hello tooencode **SharedKey** podpisu ciągu:</span><span class="sxs-lookup"><span data-stu-id="a1a70-163">Use this format tooencode hello **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="a1a70-164">Oto przykład ciągu podpisu:</span><span class="sxs-lookup"><span data-stu-id="a1a70-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="a1a70-165">Jeśli masz ciąg podpisu hello, kodować je przy użyciu hello Algorytm HMAC SHA256 na powitania ciąg algorytmem UTF-8, a następnie kodowanie hello wynik w postaci Base64.</span><span class="sxs-lookup"><span data-stu-id="a1a70-165">When you have hello signature string, encode it by using hello HMAC-SHA256 algorithm on hello UTF-8-encoded string, and then encode hello result as Base64.</span></span> <span data-ttu-id="a1a70-166">Użyj następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="a1a70-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="a1a70-167">Witaj w kolejnych sekcjach hello mają przykładowy kod toohelp utworzyć nagłówek autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="a1a70-167">hello samples in hello next sections have sample code toohelp you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="a1a70-168">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a1a70-168">Request body</span></span>
<span data-ttu-id="a1a70-169">Witaj treść wiadomości powitania musi być w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="a1a70-169">hello body of hello message must be in JSON.</span></span> <span data-ttu-id="a1a70-170">Musi zawierać co najmniej jeden rekord z pary nazw i wartości właściwości hello w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="a1a70-170">It must include one or more records with hello property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="a1a70-171">Partii z wielu rekordów razem w jednym żądaniu, za pomocą hello zgodny z formatem.</span><span class="sxs-lookup"><span data-stu-id="a1a70-171">You can batch multiple records together in a single request by using hello following format.</span></span> <span data-ttu-id="a1a70-172">Wszystkie rekordy hello musi być hello rekordów samego typu.</span><span class="sxs-lookup"><span data-stu-id="a1a70-172">All hello records must be hello same record type.</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a><span data-ttu-id="a1a70-173">Typ rekordu i właściwości</span><span class="sxs-lookup"><span data-stu-id="a1a70-173">Record type and properties</span></span>
<span data-ttu-id="a1a70-174">Typ niestandardowy rekord należy zdefiniować podczas przesyłania danych za pośrednictwem hello interfejsu API modułów zbierających dane dziennika Analytics HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1a70-174">You define a custom record type when you submit data through hello Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="a1a70-175">Obecnie nie można zapisać danych tooexisting typy rekordów, które zostały utworzone przez inne typy danych i rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="a1a70-175">Currently, you can't write data tooexisting record types that were created by other data types and solutions.</span></span> <span data-ttu-id="a1a70-176">Analiza dzienników odczytuje hello przychodzących danych, a następnie tworzy właściwości, które są zgodne z typami danych hello hello wartości, które należy wprowadzić.</span><span class="sxs-lookup"><span data-stu-id="a1a70-176">Log Analytics reads hello incoming data and then creates properties that match hello data types of hello values that you enter.</span></span>

<span data-ttu-id="a1a70-177">Każdy toohello żądanie musi zawierać interfejs API analizy dziennika **typ dziennika** nagłówek o nazwie hello hello typu rekordu.</span><span class="sxs-lookup"><span data-stu-id="a1a70-177">Each request toohello Log Analytics API must include a **Log-Type** header with hello name for hello record type.</span></span> <span data-ttu-id="a1a70-178">sufiks Hello **_CL** jest nazwą automatycznie dołączany toohello wprowadź toodistinguish ona z dziennika inne typy jako dziennik niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="a1a70-178">hello suffix **_CL** is automatically appended toohello name you enter toodistinguish it from other log types as a custom log.</span></span> <span data-ttu-id="a1a70-179">Na przykład, jeśli wprowadzona nazwa hello **MyNewRecordType**, analizy dzienników tworzy rekord typu hello **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="a1a70-179">For example, if you enter hello name **MyNewRecordType**, Log Analytics creates a record with hello type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="a1a70-180">Pomaga to zapewnić, że nie występują żadne konflikty między nazwami utworzonych przez użytkownika typu i te w obecne lub przyszłe rozwiązania firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a1a70-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="a1a70-181">Typ danych właściwości tooidentify, analizy dzienników dodaje sufiks nazwy właściwości toohello.</span><span class="sxs-lookup"><span data-stu-id="a1a70-181">tooidentify a property's data type, Log Analytics adds a suffix toohello property name.</span></span> <span data-ttu-id="a1a70-182">Jeśli jakaś właściwość zawiera wartość null, właściwość hello jest niedostępna w tym rekordzie.</span><span class="sxs-lookup"><span data-stu-id="a1a70-182">If a property contains a null value, hello property is not included in that record.</span></span> <span data-ttu-id="a1a70-183">Poniższa tabela zawiera typ danych właściwości hello i odpowiedniego sufiksu:</span><span class="sxs-lookup"><span data-stu-id="a1a70-183">This table lists hello property data type and corresponding suffix:</span></span>

| <span data-ttu-id="a1a70-184">Typ danych właściwości</span><span class="sxs-lookup"><span data-stu-id="a1a70-184">Property data type</span></span> | <span data-ttu-id="a1a70-185">Sufiks</span><span class="sxs-lookup"><span data-stu-id="a1a70-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="a1a70-186">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a1a70-186">String</span></span> |<span data-ttu-id="a1a70-187">_s</span><span class="sxs-lookup"><span data-stu-id="a1a70-187">_s</span></span> |
| <span data-ttu-id="a1a70-188">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a1a70-188">Boolean</span></span> |<span data-ttu-id="a1a70-189">_b</span><span class="sxs-lookup"><span data-stu-id="a1a70-189">_b</span></span> |
| <span data-ttu-id="a1a70-190">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="a1a70-190">Double</span></span> |<span data-ttu-id="a1a70-191">_d</span><span class="sxs-lookup"><span data-stu-id="a1a70-191">_d</span></span> |
| <span data-ttu-id="a1a70-192">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="a1a70-192">Date/time</span></span> |<span data-ttu-id="a1a70-193">_t —</span><span class="sxs-lookup"><span data-stu-id="a1a70-193">_t</span></span> |
| <span data-ttu-id="a1a70-194">IDENTYFIKATOR GUID</span><span class="sxs-lookup"><span data-stu-id="a1a70-194">GUID</span></span> |<span data-ttu-id="a1a70-195">_g</span><span class="sxs-lookup"><span data-stu-id="a1a70-195">_g</span></span> |

<span data-ttu-id="a1a70-196">Typ danych Hello, który używa analizy dzienników dla każdej właściwości zależy od tego, czy typ rekordu hello hello nowy rekord już istnieje.</span><span class="sxs-lookup"><span data-stu-id="a1a70-196">hello data type that Log Analytics uses for each property depends on whether hello record type for hello new record already exists.</span></span>

* <span data-ttu-id="a1a70-197">Jeśli nie istnieje typ rekordu hello, analizy dzienników tworzy nową.</span><span class="sxs-lookup"><span data-stu-id="a1a70-197">If hello record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="a1a70-198">Analiza dzienników używa typu JSON hello wnioskowania typu danych hello toodetermine dla każdej właściwości w nowym rekordzie hello.</span><span class="sxs-lookup"><span data-stu-id="a1a70-198">Log Analytics uses hello JSON type inference toodetermine hello data type for each property for hello new record.</span></span>
* <span data-ttu-id="a1a70-199">Jeśli istnieje typ rekordu hello, analizy dzienników prób toocreate nowy rekord na podstawie istniejącej właściwości.</span><span class="sxs-lookup"><span data-stu-id="a1a70-199">If hello record type does exist, Log Analytics attempts toocreate a new record based on existing properties.</span></span> <span data-ttu-id="a1a70-200">Jeśli hello typ danych właściwości w hello nowy rekord nie odpowiada i nie może być skonwertowany toohello istniejący typ lub jeśli hello rekord zawiera właściwość, która nie istnieje, analizy dzienników tworzy nową właściwość, która ma hello odpowiedniego sufiksu.</span><span class="sxs-lookup"><span data-stu-id="a1a70-200">If hello data type for a property in hello new record doesn’t match and can’t be converted toohello existing type, or if hello record includes a property that doesn’t exist, Log Analytics creates a new property that has hello relevant suffix.</span></span>

<span data-ttu-id="a1a70-201">Na przykład utworzyć rekord z trzech właściwości tego wpisu przesyłania **number_d**, **boolean_b**, i **string_s**:</span><span class="sxs-lookup"><span data-stu-id="a1a70-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Przykładowy rekord 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="a1a70-203">Jeśli tego wpisu dalej, następnie przesłane ze wszystkich wartości w formacie ciągów, hello właściwości nie może zmienić.</span><span class="sxs-lookup"><span data-stu-id="a1a70-203">If you then submitted this next entry, with all values formatted as strings, hello properties would not change.</span></span> <span data-ttu-id="a1a70-204">Te wartości mogą być przekonwertowana tooexisting typów danych:</span><span class="sxs-lookup"><span data-stu-id="a1a70-204">These values can be converted tooexisting data types:</span></span>

![Przykładowy rekord 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="a1a70-206">Ale jeśli wprowadzono następnie tego przesłania dalej, analizy dzienników utworzyć hello nowe właściwości **boolean_d** i **string_d**.</span><span class="sxs-lookup"><span data-stu-id="a1a70-206">But, if you then made this next submission, Log Analytics would create hello new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="a1a70-207">Nie można przekonwertować wartości:</span><span class="sxs-lookup"><span data-stu-id="a1a70-207">These values can't be converted:</span></span>

![Przykładowy rekord 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="a1a70-209">Jeśli następnie przesłane powitania od wejścia, przed utworzeniem typu rekordu hello, analizy dzienników utworzyć rekord z trzech właściwości **liczba_s**, **boolean_s**, i **string_s**.</span><span class="sxs-lookup"><span data-stu-id="a1a70-209">If you then submitted hello following entry, before hello record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="a1a70-210">W tym wpisie wartości początkowej hello jest sformatowany jako ciąg:</span><span class="sxs-lookup"><span data-stu-id="a1a70-210">In this entry, each of hello initial values is formatted as a string:</span></span>

![Przykładowy rekord 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="a1a70-212">Limity danych</span><span class="sxs-lookup"><span data-stu-id="a1a70-212">Data limits</span></span>
<span data-ttu-id="a1a70-213">Istnieją pewne ograniczenia wokół danych hello zaksięgowany toohello dane analizy dziennika kolekcji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a1a70-213">There are some constraints around hello data posted toohello Log Analytics Data collection API.</span></span>

* <span data-ttu-id="a1a70-214">Maksymalnie 30 MB na post tooLog interfejsu API modułów zbierających dane analizy.</span><span class="sxs-lookup"><span data-stu-id="a1a70-214">Maximum of 30 MB per post tooLog Analytics Data Collector API.</span></span> <span data-ttu-id="a1a70-215">Jest to limit rozmiaru dla pojedynczego żądania post.</span><span class="sxs-lookup"><span data-stu-id="a1a70-215">This is a size limit for a single post.</span></span> <span data-ttu-id="a1a70-216">Jeśli hello dane z pojedynczego post, która przekracza 30 MB, należy rozdzielić hello fragmentów danych w górę toosmaller o rozmiarze i wyślij je jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="a1a70-216">If hello data from a single post that exceeds 30 MB, you should split hello data up toosmaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="a1a70-217">Maksymalny limit 32 KB wartości pól.</span><span class="sxs-lookup"><span data-stu-id="a1a70-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="a1a70-218">Jeśli wartość pola hello jest większa niż 32 KB, zostanie obcięta hello danych.</span><span class="sxs-lookup"><span data-stu-id="a1a70-218">If hello field value is greater than 32 KB, hello data will be truncated.</span></span>
* <span data-ttu-id="a1a70-219">Zalecana maksymalna liczba pól dla danego typu jest 50.</span><span class="sxs-lookup"><span data-stu-id="a1a70-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="a1a70-220">Jest to limit praktyczne doświadczenie użyteczność i wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a1a70-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="a1a70-221">Kody powrotne</span><span class="sxs-lookup"><span data-stu-id="a1a70-221">Return codes</span></span>
<span data-ttu-id="a1a70-222">Kod stanu HTTP 200 Hello oznacza, że otrzymano Żądanie hello do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="a1a70-222">hello HTTP status code 200 means that hello request has been received for processing.</span></span> <span data-ttu-id="a1a70-223">Oznacza to, że hello została pomyślnie zakończona.</span><span class="sxs-lookup"><span data-stu-id="a1a70-223">This indicates that hello operation completed successfully.</span></span>

<span data-ttu-id="a1a70-224">Poniższa tabela zawiera kompletny zestaw kodów stanu, które mogą zwracać usługi hello hello:</span><span class="sxs-lookup"><span data-stu-id="a1a70-224">This table lists hello complete set of status codes that hello service might return:</span></span>

| <span data-ttu-id="a1a70-225">Kod</span><span class="sxs-lookup"><span data-stu-id="a1a70-225">Code</span></span> | <span data-ttu-id="a1a70-226">Stan</span><span class="sxs-lookup"><span data-stu-id="a1a70-226">Status</span></span> | <span data-ttu-id="a1a70-227">Kod błędu:</span><span class="sxs-lookup"><span data-stu-id="a1a70-227">Error code</span></span> | <span data-ttu-id="a1a70-228">Opis</span><span class="sxs-lookup"><span data-stu-id="a1a70-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a1a70-229">200</span><span class="sxs-lookup"><span data-stu-id="a1a70-229">200</span></span> |<span data-ttu-id="a1a70-230">OK</span><span class="sxs-lookup"><span data-stu-id="a1a70-230">OK</span></span> | |<span data-ttu-id="a1a70-231">pomyślnie zaakceptowano żądanie Hello.</span><span class="sxs-lookup"><span data-stu-id="a1a70-231">hello request was successfully accepted.</span></span> |
| <span data-ttu-id="a1a70-232">400</span><span class="sxs-lookup"><span data-stu-id="a1a70-232">400</span></span> |<span data-ttu-id="a1a70-233">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="a1a70-233">Bad request</span></span> |<span data-ttu-id="a1a70-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="a1a70-234">InactiveCustomer</span></span> |<span data-ttu-id="a1a70-235">obszar roboczy Hello został zamknięty.</span><span class="sxs-lookup"><span data-stu-id="a1a70-235">hello workspace has been closed.</span></span> |
| <span data-ttu-id="a1a70-236">400</span><span class="sxs-lookup"><span data-stu-id="a1a70-236">400</span></span> |<span data-ttu-id="a1a70-237">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="a1a70-237">Bad request</span></span> |<span data-ttu-id="a1a70-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="a1a70-238">InvalidApiVersion</span></span> |<span data-ttu-id="a1a70-239">Określona wersja Hello interfejsu API nie został rozpoznany przez usługę hello.</span><span class="sxs-lookup"><span data-stu-id="a1a70-239">hello API version that you specified was not recognized by hello service.</span></span> |
| <span data-ttu-id="a1a70-240">400</span><span class="sxs-lookup"><span data-stu-id="a1a70-240">400</span></span> |<span data-ttu-id="a1a70-241">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="a1a70-241">Bad request</span></span> |<span data-ttu-id="a1a70-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="a1a70-242">InvalidCustomerId</span></span> |<span data-ttu-id="a1a70-243">Określony identyfikator obszaru roboczego Hello jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="a1a70-243">hello workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="a1a70-244">400</span><span class="sxs-lookup"><span data-stu-id="a1a70-244">400</span></span> |<span data-ttu-id="a1a70-245">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="a1a70-245">Bad request</span></span> |<span data-ttu-id="a1a70-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="a1a70-246">InvalidDataFormat</span></span> |<span data-ttu-id="a1a70-247">Przekazano nieprawidłowy JSON.</span><span class="sxs-lookup"><span data-stu-id="a1a70-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="a1a70-248">treść odpowiedzi Hello może zawierać więcej informacji na temat sposobu tooresolve hello błędu.</span><span class="sxs-lookup"><span data-stu-id="a1a70-248">hello response body might contain more information about how tooresolve hello error.</span></span> |
| <span data-ttu-id="a1a70-249">400</span><span class="sxs-lookup"><span data-stu-id="a1a70-249">400</span></span> |<span data-ttu-id="a1a70-250">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="a1a70-250">Bad request</span></span> |<span data-ttu-id="a1a70-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="a1a70-251">InvalidLogType</span></span> |<span data-ttu-id="a1a70-252">Typ dziennika Hello określony zawartych w niej znaków specjalnych ani wartości numeryczne.</span><span class="sxs-lookup"><span data-stu-id="a1a70-252">hello log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="a1a70-253">400</span><span class="sxs-lookup"><span data-stu-id="a1a70-253">400</span></span> |<span data-ttu-id="a1a70-254">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="a1a70-254">Bad request</span></span> |<span data-ttu-id="a1a70-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="a1a70-255">MissingApiVersion</span></span> |<span data-ttu-id="a1a70-256">wersja interfejsu API Hello nie została określona.</span><span class="sxs-lookup"><span data-stu-id="a1a70-256">hello API version wasn’t specified.</span></span> |
| <span data-ttu-id="a1a70-257">400</span><span class="sxs-lookup"><span data-stu-id="a1a70-257">400</span></span> |<span data-ttu-id="a1a70-258">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="a1a70-258">Bad request</span></span> |<span data-ttu-id="a1a70-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="a1a70-259">MissingContentType</span></span> |<span data-ttu-id="a1a70-260">nie określono Hello typu zawartości.</span><span class="sxs-lookup"><span data-stu-id="a1a70-260">hello content type wasn’t specified.</span></span> |
| <span data-ttu-id="a1a70-261">400</span><span class="sxs-lookup"><span data-stu-id="a1a70-261">400</span></span> |<span data-ttu-id="a1a70-262">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="a1a70-262">Bad request</span></span> |<span data-ttu-id="a1a70-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="a1a70-263">MissingLogType</span></span> |<span data-ttu-id="a1a70-264">Hello wymagany typ wartości dziennika nie został określony.</span><span class="sxs-lookup"><span data-stu-id="a1a70-264">hello required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="a1a70-265">400</span><span class="sxs-lookup"><span data-stu-id="a1a70-265">400</span></span> |<span data-ttu-id="a1a70-266">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="a1a70-266">Bad request</span></span> |<span data-ttu-id="a1a70-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="a1a70-267">UnsupportedContentType</span></span> |<span data-ttu-id="a1a70-268">Typ zawartości Hello nie została ustawiona zbyt**application/json**.</span><span class="sxs-lookup"><span data-stu-id="a1a70-268">hello content type was not set too**application/json**.</span></span> |
| <span data-ttu-id="a1a70-269">403</span><span class="sxs-lookup"><span data-stu-id="a1a70-269">403</span></span> |<span data-ttu-id="a1a70-270">Dostęp zabroniony</span><span class="sxs-lookup"><span data-stu-id="a1a70-270">Forbidden</span></span> |<span data-ttu-id="a1a70-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="a1a70-271">InvalidAuthorization</span></span> |<span data-ttu-id="a1a70-272">Usługa Hello nie tooauthenticate hello żądania.</span><span class="sxs-lookup"><span data-stu-id="a1a70-272">hello service failed tooauthenticate hello request.</span></span> <span data-ttu-id="a1a70-273">Sprawdź tego hello obszaru roboczego połączenia i identyfikator klucza są poprawne.</span><span class="sxs-lookup"><span data-stu-id="a1a70-273">Verify that hello workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="a1a70-274">404</span><span class="sxs-lookup"><span data-stu-id="a1a70-274">404</span></span> |<span data-ttu-id="a1a70-275">Nie można odnaleźć</span><span class="sxs-lookup"><span data-stu-id="a1a70-275">Not Found</span></span> | | <span data-ttu-id="a1a70-276">Podany adres URL hello jest niepoprawna albo hello żądania jest za duży.</span><span class="sxs-lookup"><span data-stu-id="a1a70-276">Either hello URL provided is incorrect, or hello request is too large.</span></span> |
| <span data-ttu-id="a1a70-277">429</span><span class="sxs-lookup"><span data-stu-id="a1a70-277">429</span></span> |<span data-ttu-id="a1a70-278">Zbyt wiele żądań</span><span class="sxs-lookup"><span data-stu-id="a1a70-278">Too Many Requests</span></span> | | <span data-ttu-id="a1a70-279">Usługa Hello występuje duża liczba dane z konta.</span><span class="sxs-lookup"><span data-stu-id="a1a70-279">hello service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="a1a70-280">Spróbuj ponownie później hello żądania.</span><span class="sxs-lookup"><span data-stu-id="a1a70-280">Please retry hello request later.</span></span> |
| <span data-ttu-id="a1a70-281">500</span><span class="sxs-lookup"><span data-stu-id="a1a70-281">500</span></span> |<span data-ttu-id="a1a70-282">Wewnętrzny błąd serwera</span><span class="sxs-lookup"><span data-stu-id="a1a70-282">Internal Server Error</span></span> |<span data-ttu-id="a1a70-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="a1a70-283">UnspecifiedError</span></span> |<span data-ttu-id="a1a70-284">Usługa Hello napotkał błąd wewnętrzny.</span><span class="sxs-lookup"><span data-stu-id="a1a70-284">hello service encountered an internal error.</span></span> <span data-ttu-id="a1a70-285">Ponów żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="a1a70-285">Please retry hello request.</span></span> |
| <span data-ttu-id="a1a70-286">503</span><span class="sxs-lookup"><span data-stu-id="a1a70-286">503</span></span> |<span data-ttu-id="a1a70-287">Usługa jest niedostępna</span><span class="sxs-lookup"><span data-stu-id="a1a70-287">Service Unavailable</span></span> |<span data-ttu-id="a1a70-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="a1a70-288">ServiceUnavailable</span></span> |<span data-ttu-id="a1a70-289">Usługa Hello jest obecnie niedostępna tooreceive żądań.</span><span class="sxs-lookup"><span data-stu-id="a1a70-289">hello service currently is unavailable tooreceive requests.</span></span> <span data-ttu-id="a1a70-290">Ponów żądanie.</span><span class="sxs-lookup"><span data-stu-id="a1a70-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="a1a70-291">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="a1a70-291">Query data</span></span>
<span data-ttu-id="a1a70-292">tooquery danych przesyłanych przez hello interfejsu API z modułu zbierającego dane HTTP Analytics dziennika, Wyszukaj rekordy z **typu** który jest taki sam toohello **LogType** wartość, która została określona, dołączony **_CL**.</span><span class="sxs-lookup"><span data-stu-id="a1a70-292">tooquery data submitted by hello Log Analytics HTTP Data Collector API, search for records with **Type** that is equal toohello **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="a1a70-293">Na przykład jeśli użyto **MyCustomLog**, a następnie zwróci wszystkie rekordy z **typu = MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="a1a70-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="a1a70-294">Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.</span><span class="sxs-lookup"><span data-stu-id="a1a70-294">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="a1a70-295">Próbki żądań</span><span class="sxs-lookup"><span data-stu-id="a1a70-295">Sample requests</span></span>
<span data-ttu-id="a1a70-296">W kolejnych sekcjach hello znajdują się przykłady tego, jak toosubmit toohello danych interfejsu API modułów zbierających dane dziennika Analytics HTTP przy użyciu różnych języków programowania.</span><span class="sxs-lookup"><span data-stu-id="a1a70-296">In hello next sections, you'll find samples of how toosubmit data toohello Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="a1a70-297">Dla każdej próbki wykonaj te kroki tooset hello zmienne dla nagłówka autoryzacji hello:</span><span class="sxs-lookup"><span data-stu-id="a1a70-297">For each sample, do these steps tooset hello variables for hello authorization header:</span></span>

1. <span data-ttu-id="a1a70-298">W portalu usługi Operations Management Suite hello, wybierz hello **ustawienia** Kafelek, a następnie wybierz hello **połączonych źródeł** kartę.</span><span class="sxs-lookup"><span data-stu-id="a1a70-298">In hello Operations Management Suite portal, select hello **Settings** tile, and then select hello **Connected Sources** tab.</span></span>
2. <span data-ttu-id="a1a70-299">toohello prawo **identyfikator obszaru roboczego**, wybierz ikonę kopiowania hello, a następnie wklej identyfikator hello jako wartość hello hello **identyfikator klienta** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="a1a70-299">toohello right of **Workspace ID**, select hello copy icon, and then paste hello ID as hello value of hello **Customer ID** variable.</span></span>
3. <span data-ttu-id="a1a70-300">toohello prawo **klucza podstawowego**, wybierz ikonę kopiowania hello, a następnie wklej identyfikator hello jako wartość hello hello **klucz wstępny** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="a1a70-300">toohello right of **Primary Key**, select hello copy icon, and then paste hello ID as hello value of hello **Shared Key** variable.</span></span>

<span data-ttu-id="a1a70-301">Można również zmienić hello zmienne typu dziennika hello oraz dane JSON.</span><span class="sxs-lookup"><span data-stu-id="a1a70-301">Alternatively, you can change hello variables for hello log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="a1a70-302">Przykładowe programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1a70-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="a1a70-303">Przykład w języku C#</span><span class="sxs-lookup"><span data-stu-id="a1a70-303">C# sample</span></span>
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a><span data-ttu-id="a1a70-304">Przykładowe Python</span><span class="sxs-lookup"><span data-stu-id="a1a70-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a><span data-ttu-id="a1a70-305">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a1a70-305">Next steps</span></span>
- <span data-ttu-id="a1a70-306">Użyj hello [interfejs API dziennika wyszukiwania](log-analytics-log-search-api.md) tooretrieve danych z hello analizy dzienników repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a1a70-306">Use hello [Log Search API](log-analytics-log-search-api.md) tooretrieve data from hello Log Analytics repository.</span></span>
