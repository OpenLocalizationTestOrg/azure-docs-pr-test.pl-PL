---
title: "Dziennika modułów zbierających dane HTTP analizy interfejsu API | Dokumentacja firmy Microsoft"
description: "Interfejs API modułów zbierających dane HTTP Analytics dziennika umożliwia dodawanie danych POST JSON do repozytorium analizy dzienników za pomocą dowolnego klienta, który można wywołać interfejsu API REST. W tym artykule opisano sposób użycia interfejsu API i zawiera przykłady publikowania danych przy użyciu różnych języków programowania."
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
ms.openlocfilehash: b0c45ff8c1d4c9d35fbb3c8839b38a20df277055
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="send-data-to-log-analytics-with-the-http-data-collector-api"></a><span data-ttu-id="9b932-104">Wysyłanie danych do analizy dzienników przy użyciu interfejsu API modułów zbierających dane HTTP</span><span class="sxs-lookup"><span data-stu-id="9b932-104">Send data to Log Analytics with the HTTP Data Collector API</span></span>
<span data-ttu-id="9b932-105">W tym artykule przedstawiono sposób wysyłania danych do analizy dzienników z klienta interfejsu API REST za pomocą interfejsu API modułów zbierających dane HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b932-105">This article shows you how to use the HTTP Data Collector API to send data to Log Analytics from a REST API client.</span></span>  <span data-ttu-id="9b932-106">Przedstawiono sposób formatowania danych zbieranych przez skrypt lub aplikację, dołączyć go w żądaniu i mieć tego żądania uprawnień przez analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="9b932-106">It describes how to format data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="9b932-107">Przykłady są dostępne dla programu PowerShell, C# i Python.</span><span class="sxs-lookup"><span data-stu-id="9b932-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="9b932-108">Pojęcia</span><span class="sxs-lookup"><span data-stu-id="9b932-108">Concepts</span></span>
<span data-ttu-id="9b932-109">Interfejs API modułów zbierających dane HTTP służy do wysyłania danych do analizy dzienników z dowolnego klienta, który można wywołać interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="9b932-109">You can use the HTTP Data Collector API to send data to Log Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="9b932-110">Może to być element runbook automatyzacji Azure, która gromadzi zarządzania danych z platformy Azure lub innej chmurze lub może być system zarządzania alternatywne, używaną do konsolidacji i analizowanie danych analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="9b932-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics to consolidate and analyze data.</span></span>

<span data-ttu-id="9b932-111">Wszystkie dane w repozytorium analizy dzienników są przechowywane jako rekord typu określonego rekordu.</span><span class="sxs-lookup"><span data-stu-id="9b932-111">All data in the Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="9b932-112">Formatowanie danych do wysyłania do interfejsu API modułów zbierających dane HTTP jako wielu rekordów w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="9b932-112">You format your data to send to the HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="9b932-113">Podczas przesyłania danych pojedynczego rekordu jest tworzony w repozytorium dla każdego rekordu w ładunku żądania.</span><span class="sxs-lookup"><span data-stu-id="9b932-113">When you submit the data, an individual record is created in the repository for each record in the request payload.</span></span>


![Omówienie modułów zbierających dane HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="9b932-115">Utwórz żądanie</span><span class="sxs-lookup"><span data-stu-id="9b932-115">Create a request</span></span>
<span data-ttu-id="9b932-116">Aby za pomocą interfejsu API modułów zbierających dane HTTP, należy utworzyć żądania POST, który zawiera dane do wysłania w JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="9b932-116">To use the HTTP Data Collector API, you create a POST request that includes the data to send in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="9b932-117">Kolejne trzy tabele zawierają listę atrybutów, które są wymagane dla każdego żądania.</span><span class="sxs-lookup"><span data-stu-id="9b932-117">The next three tables list the attributes that are required for each request.</span></span> <span data-ttu-id="9b932-118">Opisano każdy atrybut bardziej szczegółowo w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="9b932-118">We describe each attribute in more detail later in the article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="9b932-119">Identyfikator URI żądania</span><span class="sxs-lookup"><span data-stu-id="9b932-119">Request URI</span></span>
| <span data-ttu-id="9b932-120">Atrybut</span><span class="sxs-lookup"><span data-stu-id="9b932-120">Attribute</span></span> | <span data-ttu-id="9b932-121">Właściwość</span><span class="sxs-lookup"><span data-stu-id="9b932-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="9b932-122">Metoda</span><span class="sxs-lookup"><span data-stu-id="9b932-122">Method</span></span> |<span data-ttu-id="9b932-123">POST</span><span class="sxs-lookup"><span data-stu-id="9b932-123">POST</span></span> |
| <span data-ttu-id="9b932-124">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="9b932-124">URI</span></span> |<span data-ttu-id="9b932-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="9b932-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="9b932-126">Typ zawartości</span><span class="sxs-lookup"><span data-stu-id="9b932-126">Content type</span></span> |<span data-ttu-id="9b932-127">application/json</span><span class="sxs-lookup"><span data-stu-id="9b932-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="9b932-128">Parametry identyfikatora URI żądania</span><span class="sxs-lookup"><span data-stu-id="9b932-128">Request URI parameters</span></span>
| <span data-ttu-id="9b932-129">Parametr</span><span class="sxs-lookup"><span data-stu-id="9b932-129">Parameter</span></span> | <span data-ttu-id="9b932-130">Opis</span><span class="sxs-lookup"><span data-stu-id="9b932-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9b932-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="9b932-131">CustomerID</span></span> |<span data-ttu-id="9b932-132">Unikatowy identyfikator dla obszaru roboczego programu Microsoft Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="9b932-132">The unique identifier for the Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="9b932-133">Zasób</span><span class="sxs-lookup"><span data-stu-id="9b932-133">Resource</span></span> |<span data-ttu-id="9b932-134">Nazwa zasobu interfejsu API: / api/logs.</span><span class="sxs-lookup"><span data-stu-id="9b932-134">The API resource name: /api/logs.</span></span> |
| <span data-ttu-id="9b932-135">Wersja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="9b932-135">API Version</span></span> |<span data-ttu-id="9b932-136">Wersja interfejsu API do używania z tym żądaniem.</span><span class="sxs-lookup"><span data-stu-id="9b932-136">The version of the API to use with this request.</span></span> <span data-ttu-id="9b932-137">Obecnie jest 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="9b932-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9b932-138">Nagłówki żądania</span><span class="sxs-lookup"><span data-stu-id="9b932-138">Request headers</span></span>
| <span data-ttu-id="9b932-139">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="9b932-139">Header</span></span> | <span data-ttu-id="9b932-140">Opis</span><span class="sxs-lookup"><span data-stu-id="9b932-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9b932-141">Autoryzacja</span><span class="sxs-lookup"><span data-stu-id="9b932-141">Authorization</span></span> |<span data-ttu-id="9b932-142">Podpis autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="9b932-142">The authorization signature.</span></span> <span data-ttu-id="9b932-143">W dalszej części tego artykułu można uzyskać informacje dotyczące sposobu tworzenia nagłówka HMAC SHA256.</span><span class="sxs-lookup"><span data-stu-id="9b932-143">Later in the article, you can read about how to create an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="9b932-144">Typ dziennika</span><span class="sxs-lookup"><span data-stu-id="9b932-144">Log-Type</span></span> |<span data-ttu-id="9b932-145">Określ typ rekordu jest przesyłane dane.</span><span class="sxs-lookup"><span data-stu-id="9b932-145">Specify the record type of the data that is being submitted.</span></span> <span data-ttu-id="9b932-146">Typ dziennika obsługuje obecnie tylko znaki alfanumeryczne.</span><span class="sxs-lookup"><span data-stu-id="9b932-146">Currently, the log type supports only alpha characters.</span></span> <span data-ttu-id="9b932-147">Nie obsługuje wartości numeryczne i znaki specjalne.</span><span class="sxs-lookup"><span data-stu-id="9b932-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="9b932-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="9b932-148">x-ms-date</span></span> |<span data-ttu-id="9b932-149">Żądanie zostało przetworzone, w formacie RFC 1123 Data.</span><span class="sxs-lookup"><span data-stu-id="9b932-149">The date that the request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="9b932-150">czas wygenerowany — pola</span><span class="sxs-lookup"><span data-stu-id="9b932-150">time-generated-field</span></span> |<span data-ttu-id="9b932-151">Nazwa pola danych, które zawiera sygnaturę czasową elementu danych.</span><span class="sxs-lookup"><span data-stu-id="9b932-151">The name of a field in the data that contains the timestamp of the data item.</span></span> <span data-ttu-id="9b932-152">Jeśli określisz pola, a następnie jego zawartość jest używana dla **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="9b932-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="9b932-153">Jeśli to pole nie zostanie określona, wartością domyślną **TimeGenerated** jest czas, który jest pozyskanych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="9b932-153">If this field isn’t specified, the default for **TimeGenerated** is the time that the message is ingested.</span></span> <span data-ttu-id="9b932-154">Zawartość pola wiadomości należy wykonać w formacie ISO 8601 RRRR-MM-Ddtgg.</span><span class="sxs-lookup"><span data-stu-id="9b932-154">The contents of the message field should follow the ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="9b932-155">Autoryzacja</span><span class="sxs-lookup"><span data-stu-id="9b932-155">Authorization</span></span>
<span data-ttu-id="9b932-156">Każde żądanie API modułu zbierającego dane dziennika Analytics HTTP musi zawierać nagłówek uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="9b932-156">Any request to the Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="9b932-157">Aby uwierzytelnić żądanie, musisz zalogować się żądanie z serwera podstawowego lub dodatkowego klucza dla obszaru roboczego, który wysłał żądanie.</span><span class="sxs-lookup"><span data-stu-id="9b932-157">To authenticate a request, you must sign the request with either the primary or the secondary key for the workspace that is making the request.</span></span> <span data-ttu-id="9b932-158">Następnie przekaż tego podpisu, jako część żądania.</span><span class="sxs-lookup"><span data-stu-id="9b932-158">Then, pass that signature as part of the request.</span></span>   

<span data-ttu-id="9b932-159">Oto format nagłówka autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="9b932-159">Here's the format for the authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="9b932-160">*WorkspaceID* jest unikatowym identyfikatorem dla obszaru roboczego usługi Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="9b932-160">*WorkspaceID* is the unique identifier for the Operations Management Suite workspace.</span></span> <span data-ttu-id="9b932-161">*Podpis* jest [Hash-based kodu (metoda HMAC Message Authentication)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) jest tworzony z żądania i następnie obliczane przy użyciu [algorytm SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b932-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from the request and then computed by using the [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="9b932-162">Następnie należy kodować je przy użyciu kodowania Base64.</span><span class="sxs-lookup"><span data-stu-id="9b932-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="9b932-163">Użyj tego formatu do kodowania **SharedKey** podpisu ciągu:</span><span class="sxs-lookup"><span data-stu-id="9b932-163">Use this format to encode the **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="9b932-164">Oto przykład ciągu podpisu:</span><span class="sxs-lookup"><span data-stu-id="9b932-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="9b932-165">Jeśli masz ciąg podpisu kodować je przy użyciu Algorytm HMAC SHA256 na ciąg kodowany UTF-8, a następnie kodowanie wynik w postaci Base64.</span><span class="sxs-lookup"><span data-stu-id="9b932-165">When you have the signature string, encode it by using the HMAC-SHA256 algorithm on the UTF-8-encoded string, and then encode the result as Base64.</span></span> <span data-ttu-id="9b932-166">Użyj następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="9b932-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="9b932-167">Przykłady w kolejnych sekcjach ma przykładowy kod, aby utworzyć nagłówek autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="9b932-167">The samples in the next sections have sample code to help you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="9b932-168">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="9b932-168">Request body</span></span>
<span data-ttu-id="9b932-169">Treść komunikatu musi być w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="9b932-169">The body of the message must be in JSON.</span></span> <span data-ttu-id="9b932-170">Musi zawierać co najmniej jeden rekord z pary nazw i wartości właściwości w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="9b932-170">It must include one or more records with the property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="9b932-171">Partii z wielu rekordów razem w jednym żądaniu, przy użyciu następującego formatu.</span><span class="sxs-lookup"><span data-stu-id="9b932-171">You can batch multiple records together in a single request by using the following format.</span></span> <span data-ttu-id="9b932-172">Wszystkie rekordy muszą być tego samego typu rekordu.</span><span class="sxs-lookup"><span data-stu-id="9b932-172">All the records must be the same record type.</span></span>

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

## <a name="record-type-and-properties"></a><span data-ttu-id="9b932-173">Typ rekordu i właściwości</span><span class="sxs-lookup"><span data-stu-id="9b932-173">Record type and properties</span></span>
<span data-ttu-id="9b932-174">Typ niestandardowy rekord należy zdefiniować podczas przesyłania danych za pośrednictwem interfejsu API modułów zbierających dane HTTP analizy dziennika.</span><span class="sxs-lookup"><span data-stu-id="9b932-174">You define a custom record type when you submit data through the Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="9b932-175">Obecnie nie można zapisać danych do istniejących typów rekordów, które zostały utworzone przez inne typy danych i rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="9b932-175">Currently, you can't write data to existing record types that were created by other data types and solutions.</span></span> <span data-ttu-id="9b932-176">Analiza dzienników odczytuje przychodzących danych, a następnie tworzy właściwości, które pasują do typów danych wartości, które należy wprowadzić.</span><span class="sxs-lookup"><span data-stu-id="9b932-176">Log Analytics reads the incoming data and then creates properties that match the data types of the values that you enter.</span></span>

<span data-ttu-id="9b932-177">Każde żądanie do interfejsu API analizy dziennika musi zawierać **typ dziennika** nagłówek o nazwie dla typu rekordu.</span><span class="sxs-lookup"><span data-stu-id="9b932-177">Each request to the Log Analytics API must include a **Log-Type** header with the name for the record type.</span></span> <span data-ttu-id="9b932-178">Sufiks **_CL** jest automatycznie dołączane do nazwy wprowadź odróżniający go od innych typów dziennika jako dziennik niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="9b932-178">The suffix **_CL** is automatically appended to the name you enter to distinguish it from other log types as a custom log.</span></span> <span data-ttu-id="9b932-179">Na przykład wprowadź nazwę **MyNewRecordType**, analizy dzienników tworzy rekord z typem **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="9b932-179">For example, if you enter the name **MyNewRecordType**, Log Analytics creates a record with the type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="9b932-180">Pomaga to zapewnić, że nie występują żadne konflikty między nazwami utworzonych przez użytkownika typu i te w obecne lub przyszłe rozwiązania firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9b932-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="9b932-181">Aby określić typ danych właściwości, analizy dzienników dodaje sufiks nazwy właściwości.</span><span class="sxs-lookup"><span data-stu-id="9b932-181">To identify a property's data type, Log Analytics adds a suffix to the property name.</span></span> <span data-ttu-id="9b932-182">Jeśli jakaś właściwość zawiera wartość null, właściwość nie jest uwzględniony w tym rekordzie.</span><span class="sxs-lookup"><span data-stu-id="9b932-182">If a property contains a null value, the property is not included in that record.</span></span> <span data-ttu-id="9b932-183">Poniższa tabela zawiera typ danych właściwości i odpowiedniego sufiksu:</span><span class="sxs-lookup"><span data-stu-id="9b932-183">This table lists the property data type and corresponding suffix:</span></span>

| <span data-ttu-id="9b932-184">Typ danych właściwości</span><span class="sxs-lookup"><span data-stu-id="9b932-184">Property data type</span></span> | <span data-ttu-id="9b932-185">Sufiks</span><span class="sxs-lookup"><span data-stu-id="9b932-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="9b932-186">Ciąg</span><span class="sxs-lookup"><span data-stu-id="9b932-186">String</span></span> |<span data-ttu-id="9b932-187">_s</span><span class="sxs-lookup"><span data-stu-id="9b932-187">_s</span></span> |
| <span data-ttu-id="9b932-188">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="9b932-188">Boolean</span></span> |<span data-ttu-id="9b932-189">_b</span><span class="sxs-lookup"><span data-stu-id="9b932-189">_b</span></span> |
| <span data-ttu-id="9b932-190">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="9b932-190">Double</span></span> |<span data-ttu-id="9b932-191">_d</span><span class="sxs-lookup"><span data-stu-id="9b932-191">_d</span></span> |
| <span data-ttu-id="9b932-192">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="9b932-192">Date/time</span></span> |<span data-ttu-id="9b932-193">_t —</span><span class="sxs-lookup"><span data-stu-id="9b932-193">_t</span></span> |
| <span data-ttu-id="9b932-194">IDENTYFIKATOR GUID</span><span class="sxs-lookup"><span data-stu-id="9b932-194">GUID</span></span> |<span data-ttu-id="9b932-195">_g</span><span class="sxs-lookup"><span data-stu-id="9b932-195">_g</span></span> |

<span data-ttu-id="9b932-196">Typ danych, który używa analizy dzienników dla każdej właściwości zależy od tego, czy istnieje już typ rekordu w nowym rekordzie.</span><span class="sxs-lookup"><span data-stu-id="9b932-196">The data type that Log Analytics uses for each property depends on whether the record type for the new record already exists.</span></span>

* <span data-ttu-id="9b932-197">Jeśli nie istnieje typ rekordu, analizy dzienników tworzy nową.</span><span class="sxs-lookup"><span data-stu-id="9b932-197">If the record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="9b932-198">Analiza dzienników używa wnioskowanie o typie JSON można ustalić typu danych dla każdej właściwości w nowym rekordzie.</span><span class="sxs-lookup"><span data-stu-id="9b932-198">Log Analytics uses the JSON type inference to determine the data type for each property for the new record.</span></span>
* <span data-ttu-id="9b932-199">Jeśli istnieje typ rekordu, analizy dzienników próbuje utworzyć nowy rekord na podstawie istniejącej właściwości.</span><span class="sxs-lookup"><span data-stu-id="9b932-199">If the record type does exist, Log Analytics attempts to create a new record based on existing properties.</span></span> <span data-ttu-id="9b932-200">Jeśli typ danych dla właściwości w nowym rekordzie nie odpowiada i nie można przekonwertować na typ istniejący lub jeśli rekord zawiera właściwość, która nie istnieje, analizy dzienników tworzy nowe właściwości, która ma zastosowanie sufiks.</span><span class="sxs-lookup"><span data-stu-id="9b932-200">If the data type for a property in the new record doesn’t match and can’t be converted to the existing type, or if the record includes a property that doesn’t exist, Log Analytics creates a new property that has the relevant suffix.</span></span>

<span data-ttu-id="9b932-201">Na przykład utworzyć rekord z trzech właściwości tego wpisu przesyłania **number_d**, **boolean_b**, i **string_s**:</span><span class="sxs-lookup"><span data-stu-id="9b932-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Przykładowy rekord 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="9b932-203">Jeśli tego wpisu dalej, następnie przesłane ze wszystkich wartości w formacie ciągów, właściwości nie może zmienić.</span><span class="sxs-lookup"><span data-stu-id="9b932-203">If you then submitted this next entry, with all values formatted as strings, the properties would not change.</span></span> <span data-ttu-id="9b932-204">Te wartości można przekonwertować istniejących typów danych:</span><span class="sxs-lookup"><span data-stu-id="9b932-204">These values can be converted to existing data types:</span></span>

![Przykładowy rekord 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="9b932-206">Jednak jeśli wprowadzono następnie tego przesłania dalej, analizy dzienników utworzyć nowe właściwości **boolean_d** i **string_d**.</span><span class="sxs-lookup"><span data-stu-id="9b932-206">But, if you then made this next submission, Log Analytics would create the new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="9b932-207">Nie można przekonwertować wartości:</span><span class="sxs-lookup"><span data-stu-id="9b932-207">These values can't be converted:</span></span>

![Przykładowy rekord 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="9b932-209">Jeśli następnie przesłane następujący wpis przed utworzeniem typu rekordu, analizy dzienników utworzyć rekord z trzech właściwości **liczba_s**, **boolean_s**, i **string_s**.</span><span class="sxs-lookup"><span data-stu-id="9b932-209">If you then submitted the following entry, before the record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="9b932-210">W tej pozycji początkowej wartości jest sformatowany jako ciąg:</span><span class="sxs-lookup"><span data-stu-id="9b932-210">In this entry, each of the initial values is formatted as a string:</span></span>

![Przykładowy rekord 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="9b932-212">Limity danych</span><span class="sxs-lookup"><span data-stu-id="9b932-212">Data limits</span></span>
<span data-ttu-id="9b932-213">Istnieją pewne ograniczenia wokół dane publikowane w kolekcji dane analizy dziennika interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9b932-213">There are some constraints around the data posted to the Log Analytics Data collection API.</span></span>

* <span data-ttu-id="9b932-214">Maksymalnie 30 MB na post API modułów zbierających dane analizy dziennika.</span><span class="sxs-lookup"><span data-stu-id="9b932-214">Maximum of 30 MB per post to Log Analytics Data Collector API.</span></span> <span data-ttu-id="9b932-215">Jest to limit rozmiaru dla pojedynczego żądania post.</span><span class="sxs-lookup"><span data-stu-id="9b932-215">This is a size limit for a single post.</span></span> <span data-ttu-id="9b932-216">Jeśli po danych z jednej, która przekracza 30 MB, należy rozdzielić maksymalnie mniejsze fragmenty wielkości i wysyłać je jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="9b932-216">If the data from a single post that exceeds 30 MB, you should split the data up to smaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="9b932-217">Maksymalny limit 32 KB wartości pól.</span><span class="sxs-lookup"><span data-stu-id="9b932-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="9b932-218">Jeśli wartość pola jest większa niż 32 KB, dane zostaną obcięte.</span><span class="sxs-lookup"><span data-stu-id="9b932-218">If the field value is greater than 32 KB, the data will be truncated.</span></span>
* <span data-ttu-id="9b932-219">Zalecana maksymalna liczba pól dla danego typu jest 50.</span><span class="sxs-lookup"><span data-stu-id="9b932-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="9b932-220">Jest to limit praktyczne doświadczenie użyteczność i wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="9b932-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="9b932-221">Kody powrotne</span><span class="sxs-lookup"><span data-stu-id="9b932-221">Return codes</span></span>
<span data-ttu-id="9b932-222">Kod stanu HTTP 200 oznacza, że otrzymał żądanie do przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="9b932-222">The HTTP status code 200 means that the request has been received for processing.</span></span> <span data-ttu-id="9b932-223">Oznacza to, że operacja została ukończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="9b932-223">This indicates that the operation completed successfully.</span></span>

<span data-ttu-id="9b932-224">Poniższa tabela zawiera pełen zestaw kodów stanu, które mogą zwracać usługi:</span><span class="sxs-lookup"><span data-stu-id="9b932-224">This table lists the complete set of status codes that the service might return:</span></span>

| <span data-ttu-id="9b932-225">Kod</span><span class="sxs-lookup"><span data-stu-id="9b932-225">Code</span></span> | <span data-ttu-id="9b932-226">Stan</span><span class="sxs-lookup"><span data-stu-id="9b932-226">Status</span></span> | <span data-ttu-id="9b932-227">Kod błędu:</span><span class="sxs-lookup"><span data-stu-id="9b932-227">Error code</span></span> | <span data-ttu-id="9b932-228">Opis</span><span class="sxs-lookup"><span data-stu-id="9b932-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9b932-229">200</span><span class="sxs-lookup"><span data-stu-id="9b932-229">200</span></span> |<span data-ttu-id="9b932-230">OK</span><span class="sxs-lookup"><span data-stu-id="9b932-230">OK</span></span> | |<span data-ttu-id="9b932-231">Pomyślnie zaakceptowano żądanie.</span><span class="sxs-lookup"><span data-stu-id="9b932-231">The request was successfully accepted.</span></span> |
| <span data-ttu-id="9b932-232">400</span><span class="sxs-lookup"><span data-stu-id="9b932-232">400</span></span> |<span data-ttu-id="9b932-233">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="9b932-233">Bad request</span></span> |<span data-ttu-id="9b932-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="9b932-234">InactiveCustomer</span></span> |<span data-ttu-id="9b932-235">Obszar roboczy został zamknięty.</span><span class="sxs-lookup"><span data-stu-id="9b932-235">The workspace has been closed.</span></span> |
| <span data-ttu-id="9b932-236">400</span><span class="sxs-lookup"><span data-stu-id="9b932-236">400</span></span> |<span data-ttu-id="9b932-237">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="9b932-237">Bad request</span></span> |<span data-ttu-id="9b932-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="9b932-238">InvalidApiVersion</span></span> |<span data-ttu-id="9b932-239">Określona wersja interfejsu API nie został rozpoznany przez usługę.</span><span class="sxs-lookup"><span data-stu-id="9b932-239">The API version that you specified was not recognized by the service.</span></span> |
| <span data-ttu-id="9b932-240">400</span><span class="sxs-lookup"><span data-stu-id="9b932-240">400</span></span> |<span data-ttu-id="9b932-241">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="9b932-241">Bad request</span></span> |<span data-ttu-id="9b932-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="9b932-242">InvalidCustomerId</span></span> |<span data-ttu-id="9b932-243">Określony identyfikator obszaru roboczego jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="9b932-243">The workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="9b932-244">400</span><span class="sxs-lookup"><span data-stu-id="9b932-244">400</span></span> |<span data-ttu-id="9b932-245">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="9b932-245">Bad request</span></span> |<span data-ttu-id="9b932-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="9b932-246">InvalidDataFormat</span></span> |<span data-ttu-id="9b932-247">Przekazano nieprawidłowy JSON.</span><span class="sxs-lookup"><span data-stu-id="9b932-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="9b932-248">Treść odpowiedzi może zawierać więcej informacji na temat sposobu rozwiązania błędu.</span><span class="sxs-lookup"><span data-stu-id="9b932-248">The response body might contain more information about how to resolve the error.</span></span> |
| <span data-ttu-id="9b932-249">400</span><span class="sxs-lookup"><span data-stu-id="9b932-249">400</span></span> |<span data-ttu-id="9b932-250">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="9b932-250">Bad request</span></span> |<span data-ttu-id="9b932-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="9b932-251">InvalidLogType</span></span> |<span data-ttu-id="9b932-252">Typ dziennika określony zawartych w niej znaków specjalnych ani wartości numeryczne.</span><span class="sxs-lookup"><span data-stu-id="9b932-252">The log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="9b932-253">400</span><span class="sxs-lookup"><span data-stu-id="9b932-253">400</span></span> |<span data-ttu-id="9b932-254">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="9b932-254">Bad request</span></span> |<span data-ttu-id="9b932-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="9b932-255">MissingApiVersion</span></span> |<span data-ttu-id="9b932-256">Nie określono wersji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9b932-256">The API version wasn’t specified.</span></span> |
| <span data-ttu-id="9b932-257">400</span><span class="sxs-lookup"><span data-stu-id="9b932-257">400</span></span> |<span data-ttu-id="9b932-258">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="9b932-258">Bad request</span></span> |<span data-ttu-id="9b932-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="9b932-259">MissingContentType</span></span> |<span data-ttu-id="9b932-260">Nie określono typu zawartości.</span><span class="sxs-lookup"><span data-stu-id="9b932-260">The content type wasn’t specified.</span></span> |
| <span data-ttu-id="9b932-261">400</span><span class="sxs-lookup"><span data-stu-id="9b932-261">400</span></span> |<span data-ttu-id="9b932-262">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="9b932-262">Bad request</span></span> |<span data-ttu-id="9b932-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="9b932-263">MissingLogType</span></span> |<span data-ttu-id="9b932-264">Nie określono typu dziennika wymaganej wartości.</span><span class="sxs-lookup"><span data-stu-id="9b932-264">The required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="9b932-265">400</span><span class="sxs-lookup"><span data-stu-id="9b932-265">400</span></span> |<span data-ttu-id="9b932-266">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="9b932-266">Bad request</span></span> |<span data-ttu-id="9b932-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="9b932-267">UnsupportedContentType</span></span> |<span data-ttu-id="9b932-268">Typ zawartości nie został ustawiony na **application/json**.</span><span class="sxs-lookup"><span data-stu-id="9b932-268">The content type was not set to **application/json**.</span></span> |
| <span data-ttu-id="9b932-269">403</span><span class="sxs-lookup"><span data-stu-id="9b932-269">403</span></span> |<span data-ttu-id="9b932-270">Dostęp zabroniony</span><span class="sxs-lookup"><span data-stu-id="9b932-270">Forbidden</span></span> |<span data-ttu-id="9b932-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="9b932-271">InvalidAuthorization</span></span> |<span data-ttu-id="9b932-272">Usługa nie może uwierzytelnić żądania.</span><span class="sxs-lookup"><span data-stu-id="9b932-272">The service failed to authenticate the request.</span></span> <span data-ttu-id="9b932-273">Sprawdź, czy klucz połączenia i identyfikator obszaru roboczego są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="9b932-273">Verify that the workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="9b932-274">404</span><span class="sxs-lookup"><span data-stu-id="9b932-274">404</span></span> |<span data-ttu-id="9b932-275">Nie można odnaleźć</span><span class="sxs-lookup"><span data-stu-id="9b932-275">Not Found</span></span> | | <span data-ttu-id="9b932-276">Podany adres URL jest nieprawidłowy albo żądania jest za duży.</span><span class="sxs-lookup"><span data-stu-id="9b932-276">Either the URL provided is incorrect, or the request is too large.</span></span> |
| <span data-ttu-id="9b932-277">429</span><span class="sxs-lookup"><span data-stu-id="9b932-277">429</span></span> |<span data-ttu-id="9b932-278">Zbyt wiele żądań</span><span class="sxs-lookup"><span data-stu-id="9b932-278">Too Many Requests</span></span> | | <span data-ttu-id="9b932-279">Usługa napotkała dużą liczbę dane z Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="9b932-279">The service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="9b932-280">Ponów żądanie później.</span><span class="sxs-lookup"><span data-stu-id="9b932-280">Please retry the request later.</span></span> |
| <span data-ttu-id="9b932-281">500</span><span class="sxs-lookup"><span data-stu-id="9b932-281">500</span></span> |<span data-ttu-id="9b932-282">Wewnętrzny błąd serwera</span><span class="sxs-lookup"><span data-stu-id="9b932-282">Internal Server Error</span></span> |<span data-ttu-id="9b932-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="9b932-283">UnspecifiedError</span></span> |<span data-ttu-id="9b932-284">Usługa napotkała błąd wewnętrzny.</span><span class="sxs-lookup"><span data-stu-id="9b932-284">The service encountered an internal error.</span></span> <span data-ttu-id="9b932-285">Ponów żądanie.</span><span class="sxs-lookup"><span data-stu-id="9b932-285">Please retry the request.</span></span> |
| <span data-ttu-id="9b932-286">503</span><span class="sxs-lookup"><span data-stu-id="9b932-286">503</span></span> |<span data-ttu-id="9b932-287">Usługa jest niedostępna</span><span class="sxs-lookup"><span data-stu-id="9b932-287">Service Unavailable</span></span> |<span data-ttu-id="9b932-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="9b932-288">ServiceUnavailable</span></span> |<span data-ttu-id="9b932-289">Usługa jest obecnie odbierać żądań.</span><span class="sxs-lookup"><span data-stu-id="9b932-289">The service currently is unavailable to receive requests.</span></span> <span data-ttu-id="9b932-290">Ponów żądanie.</span><span class="sxs-lookup"><span data-stu-id="9b932-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="9b932-291">Zapytania o dane</span><span class="sxs-lookup"><span data-stu-id="9b932-291">Query data</span></span>
<span data-ttu-id="9b932-292">Aby danych zapytań przesyłanych przez analityka HTTP danych modułu zbierającego interfejs API dziennika, Wyszukaj rekordy z **typu** jest równa **LogType** wartość, która została określona, dołączony **_CL**.</span><span class="sxs-lookup"><span data-stu-id="9b932-292">To query data submitted by the Log Analytics HTTP Data Collector API, search for records with **Type** that is equal to the **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="9b932-293">Na przykład jeśli użyto **MyCustomLog**, a następnie zwróci wszystkie rekordy z **typu = MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="9b932-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="9b932-294">Jeśli obszaru roboczego został uaktualniony do [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), a następnie zmienić powyższym zapytaniu następujące.</span><span class="sxs-lookup"><span data-stu-id="9b932-294">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="9b932-295">Próbki żądań</span><span class="sxs-lookup"><span data-stu-id="9b932-295">Sample requests</span></span>
<span data-ttu-id="9b932-296">W kolejnych sekcjach znajdują się przykłady sposobu przesyłania danych do interfejsu API dziennika analizy HTTP danych moduł zbierający przy użyciu różnych języków programowania.</span><span class="sxs-lookup"><span data-stu-id="9b932-296">In the next sections, you'll find samples of how to submit data to the Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="9b932-297">Dla każdej próbki wykonaj następujące kroki, aby ustawić zmienne dla nagłówka autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="9b932-297">For each sample, do these steps to set the variables for the authorization header:</span></span>

1. <span data-ttu-id="9b932-298">W portalu usługi Operations Management Suite wybierz **ustawienia** Kafelek, a następnie wybierz **połączonych źródeł** kartę.</span><span class="sxs-lookup"><span data-stu-id="9b932-298">In the Operations Management Suite portal, select the **Settings** tile, and then select the **Connected Sources** tab.</span></span>
2. <span data-ttu-id="9b932-299">Po prawej stronie **identyfikator obszaru roboczego**, wybierz ikonę kopiowania, a następnie wklej identyfikator jako wartość **identyfikator klienta** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="9b932-299">To the right of **Workspace ID**, select the copy icon, and then paste the ID as the value of the **Customer ID** variable.</span></span>
3. <span data-ttu-id="9b932-300">Po prawej stronie **klucza podstawowego**, wybierz ikonę kopiowania, a następnie wklej identyfikator jako wartość **klucz wstępny** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="9b932-300">To the right of **Primary Key**, select the copy icon, and then paste the ID as the value of the **Shared Key** variable.</span></span>

<span data-ttu-id="9b932-301">Można również zmienić zmienne typu dziennika i dane JSON.</span><span class="sxs-lookup"><span data-stu-id="9b932-301">Alternatively, you can change the variables for the log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="9b932-302">Przykładowe programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b932-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify the name of the record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with the created time for the records
$TimeStampField = "DateValue"


# Create two records with the same set of properties to create
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

# Create the function to create the authorization signature
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


# Create the function to create and post the request
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

# Submit the data to the API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="9b932-303">Przykład w języku C#</span><span class="sxs-lookup"><span data-stu-id="9b932-303">C# sample</span></span>
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

        // Update customerId to your Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either the primary or the secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of the event type that is being submitted to Log Analytics
        static string LogName = "DemoExample";

        // You can use an optional field to specify the timestamp from the data. If the time field is not specified, Log Analytics assumes the time is the message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for the API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build the API signature
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

        // Send a request to the POST API endpoint
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

### <a name="python-sample"></a><span data-ttu-id="9b932-304">Przykładowe Python</span><span class="sxs-lookup"><span data-stu-id="9b932-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update the customer ID to your Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For the shared key, use either the primary or the secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# The log type is the name of the event that is being submitted
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

# Build the API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request to the POST API
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

## <a name="next-steps"></a><span data-ttu-id="9b932-305">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9b932-305">Next steps</span></span>
- <span data-ttu-id="9b932-306">Użyj [interfejs API dziennika wyszukiwania](log-analytics-log-search-api.md) do pobierania danych z repozytorium analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="9b932-306">Use the [Log Search API](log-analytics-log-search-api.md) to retrieve data from the Log Analytics repository.</span></span>
