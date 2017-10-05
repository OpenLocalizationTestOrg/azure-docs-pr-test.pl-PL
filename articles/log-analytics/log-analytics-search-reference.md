---
title: "Odwołanie wyszukiwania Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Analiza dzienników odwołanie wyszukiwania opisuje język wyszukiwania i udostępnia opcje ogólne składnię służy do wyszukiwania danych i filtrowania wyrażenia, aby zawęzić kryteria wyszukiwania."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc9c9b0a6292dab256997a86a6db16367fc48cd3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-search-reference"></a><span data-ttu-id="36902-103">Odwołanie wyszukiwania analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="36902-103">Log Analytics search reference</span></span>

>[!NOTE]
> <span data-ttu-id="36902-104">W tym artykule opisano dziennik wyszukiwania przy użyciu bieżącego języka zapytań w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="36902-104">This article describes log searches using the current query language in Log Analytics.</span></span>  <span data-ttu-id="36902-105">Jeśli obszaru roboczego został uaktualniony do [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), a następnie należy zapoznać się [odwołanie językowe dla nowego języka](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="36902-105">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer to [the language reference for the new language](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="36902-106">W poniższej sekcji odwołania dotyczące języków wyszukiwania opisano opcje składni zapytania ogólne, można użyć podczas wyszukiwania danych i filtrowania wyrażenia, aby zawęzić kryteria wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="36902-106">The following reference section about search language describes the general query syntax options you can use when searching for data and filtering expressions to help narrow your search.</span></span> <span data-ttu-id="36902-107">Omówiono także używane do wykonania akcji na dane pobrane polecenia.</span><span class="sxs-lookup"><span data-stu-id="36902-107">It also describes commands that you can use to take action on the data retrieved.</span></span>

<span data-ttu-id="36902-108">Informacje o polach zwracane w wynikach wyszukiwania i aspektów, które ułatwiają Dowiedz się więcej o kategoriach podobne danych, w [pola wyszukiwania i aspekt odwoływać sekcji](#search-field-and-facet-reference).</span><span class="sxs-lookup"><span data-stu-id="36902-108">You can read about the fields returned in searches, and the facets that help you discover more about similar categories of data, in the [Search field and facet reference section](#search-field-and-facet-reference).</span></span>

## <a name="general-query-syntax"></a><span data-ttu-id="36902-109">Składnia zapytania ogólne</span><span class="sxs-lookup"><span data-stu-id="36902-109">General query syntax</span></span>
<span data-ttu-id="36902-110">Składnia kwerendy ogólne wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="36902-110">The syntax for general querying is as follows:</span></span>

```
filterExpression | command1 | command2 …
```

<span data-ttu-id="36902-111">Wyrażenie filtru (`filterExpression`) definiuje "where" warunku dla zapytania.</span><span class="sxs-lookup"><span data-stu-id="36902-111">The filter expression (`filterExpression`) defines the "where" condition for the query.</span></span> <span data-ttu-id="36902-112">Polecenia dotyczą wyników zwróconych przez kwerendę.</span><span class="sxs-lookup"><span data-stu-id="36902-112">The commands apply to the results returned by the query.</span></span> <span data-ttu-id="36902-113">Wiele poleceń muszą być oddzielone znaku kreski pionowej (|).</span><span class="sxs-lookup"><span data-stu-id="36902-113">Multiple commands must be separated by the pipe character ( | ).</span></span>

### <a name="general-syntax-examples"></a><span data-ttu-id="36902-114">Przykłady składni ogólnej</span><span class="sxs-lookup"><span data-stu-id="36902-114">General syntax examples</span></span>
<span data-ttu-id="36902-115">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="36902-115">Examples:</span></span>

```
system
```

<span data-ttu-id="36902-116">Ta kwerenda zwraca wyniki zawierające słowo *systemu* w każde pole, które zostały zindeksowane dla pełnotekstowego lub warunki wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="36902-116">This query returns results that contain the word *system* in any field that has been indexed for full text or terms searching.</span></span>

> [!NOTE]
> <span data-ttu-id="36902-117">Nie wszystkie pola są indeksowane w ten sposób, ale najbardziej typowe tekstowej pola (na przykład nazwy i opisy) zazwyczaj są.</span><span class="sxs-lookup"><span data-stu-id="36902-117">Not all fields are indexed this way, but the most common textual fields (such as descriptions and names) usually are.</span></span>
>
>

```
system error
```

<span data-ttu-id="36902-118">Ta kwerenda zwraca wyniki zawierające słowa *systemu* i *błąd*.</span><span class="sxs-lookup"><span data-stu-id="36902-118">This query returns results that contain the words *system* and *error*.</span></span>

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

<span data-ttu-id="36902-119">Ta kwerenda zwraca wyniki zawierające słowa *systemu* i *błąd*.</span><span class="sxs-lookup"><span data-stu-id="36902-119">This query returns results that contain the words *system* and *error*.</span></span> <span data-ttu-id="36902-120">Następnie sortujące wyniki według *ManagementGroupName* pola (rosnąco), a następnie według *TimeGenerated* (w kolejności malejącej).</span><span class="sxs-lookup"><span data-stu-id="36902-120">It then sorts the results by the *ManagementGroupName* field (in ascending order), and then by the *TimeGenerated* field (in descending order).</span></span> <span data-ttu-id="36902-121">Trwa tylko 10 pierwszych wyników.</span><span class="sxs-lookup"><span data-stu-id="36902-121">It takes only the first 10 results.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36902-122">Wszystkie nazwy pól i wartości dla pola string i tekst jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="36902-122">All the field names and the values for the string and text fields are case sensitive.</span></span>
>
>

## <a name="filter-expressions"></a><span data-ttu-id="36902-123">Wyrażenia filtru</span><span class="sxs-lookup"><span data-stu-id="36902-123">Filter expressions</span></span>
<span data-ttu-id="36902-124">Poniższe podpunkty opisują wyrażenia filtru.</span><span class="sxs-lookup"><span data-stu-id="36902-124">The following subsections explain the filter expressions.</span></span>

### <a name="string-literals"></a><span data-ttu-id="36902-125">Literały ciągu</span><span class="sxs-lookup"><span data-stu-id="36902-125">String literals</span></span>
<span data-ttu-id="36902-126">Literał ciągu jest dowolny ciąg, który nie jest rozpoznawany przez parser jako słowo kluczowe lub typu danych wstępnie zdefiniowane (na przykład, liczby lub daty).</span><span class="sxs-lookup"><span data-stu-id="36902-126">A string literal is any string that is not recognized by the parser as a keyword or a predefined data type (for example, a number or date).</span></span>

<span data-ttu-id="36902-127">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="36902-127">Examples:</span></span>

```
These all are string literals
```

<span data-ttu-id="36902-128">To zapytanie szuka wyniki zawierające wystąpienia wszystkich pięciu wyrazów.</span><span class="sxs-lookup"><span data-stu-id="36902-128">This query searches for results that contain occurrences of all five words.</span></span> <span data-ttu-id="36902-129">Aby wykonać wyszukiwanie ciągu złożonych, ujmij literał w znaki cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="36902-129">To perform a complex string search, enclose the string literal in quotation marks.</span></span> <span data-ttu-id="36902-130">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36902-130">For example:</span></span>

```
"Windows Server"
```

<span data-ttu-id="36902-131">To polecenie zwróci tylko wyniki z dokładne dopasowania dla *systemu Windows Server*.</span><span class="sxs-lookup"><span data-stu-id="36902-131">This only returns results with exact matches for *Windows Server*.</span></span>

### <a name="numbers"></a><span data-ttu-id="36902-132">Numery</span><span class="sxs-lookup"><span data-stu-id="36902-132">Numbers</span></span>
<span data-ttu-id="36902-133">Analizator obsługuje dziesiętną liczbą całkowitą i składni liczb zmiennoprzecinkowych pola liczbowego.</span><span class="sxs-lookup"><span data-stu-id="36902-133">The parser supports the decimal integer and floating-point number syntax for numerical fields.</span></span>

<span data-ttu-id="36902-134">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="36902-134">Examples:</span></span>

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a><span data-ttu-id="36902-135">Daty i godziny</span><span class="sxs-lookup"><span data-stu-id="36902-135">Dates and times</span></span>
<span data-ttu-id="36902-136">Każdy element danych w systemie ma *TimeGenerated* właściwość, która reprezentuje oryginalnego Data i godzina rekordu.</span><span class="sxs-lookup"><span data-stu-id="36902-136">Every piece of data in the system has a *TimeGenerated* property, which represents the original date and time of the record.</span></span> <span data-ttu-id="36902-137">Niektóre typy danych mogą mieć dodatkowe Data i godzina (na przykład *LastModified*).</span><span class="sxs-lookup"><span data-stu-id="36902-137">Some types of data can have additional date and time fields (for example, *LastModified*).</span></span>

<span data-ttu-id="36902-138">Oś czasu **wykresu/godzina** selektora w Analiza dzienników Azure zawiera dystrybucji wyników wraz z upływem czasu (w zależności od bieżącego zapytania uruchamiane).</span><span class="sxs-lookup"><span data-stu-id="36902-138">The timeline **Chart/Time** selector in Azure Log Analytics shows a distribution of results over time (according to the current query being run).</span></span> <span data-ttu-id="36902-139">To jest oparta na *TimeGenerated* pola.</span><span class="sxs-lookup"><span data-stu-id="36902-139">This is based on the *TimeGenerated* field.</span></span> <span data-ttu-id="36902-140">Data i godzina pola mają określony ciąg formatu, który może być używane w zapytaniach Aby ograniczyć zapytanie do określonego przedziału czasu.</span><span class="sxs-lookup"><span data-stu-id="36902-140">Date and time fields have a specific string format that can be used in queries to restrict the query to a particular timeframe.</span></span> <span data-ttu-id="36902-141">Umożliwia także składni w odwołaniu do przedziały czasu względną (na przykład "między 3 dni temu i 2 godz. temu").</span><span class="sxs-lookup"><span data-stu-id="36902-141">You can also use syntax to refer to relative time intervals (for example, "between 3 days ago and 2 hours ago").</span></span>

<span data-ttu-id="36902-142">Poniżej przedstawiono prawidłowe formularze składnię daty i godziny:</span><span class="sxs-lookup"><span data-stu-id="36902-142">The following are valid forms of syntax for dates and times:</span></span>

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


<span data-ttu-id="36902-143">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36902-143">For example:</span></span>

```
TimeGenerated:2013-10-01T12:20
```

<span data-ttu-id="36902-144">Poprzednie polecenie zwraca tylko rekordy z *TimeGenerated* wartości dokładnie 12:20 na 1 października 2013.</span><span class="sxs-lookup"><span data-stu-id="36902-144">The previous command returns only records with a *TimeGenerated* value of exactly 12:20 on October 1, 2013.</span></span>

<span data-ttu-id="36902-145">Analizator obsługuje również skrótu wartości daty/godziny, teraz.</span><span class="sxs-lookup"><span data-stu-id="36902-145">The parser also supports the mnemonic Date/Time value, NOW.</span></span> <span data-ttu-id="36902-146">(Jest mało prawdopodobne, że da żadnych wyników, ponieważ nie była danych za pośrednictwem systemu to szybkie.)</span><span class="sxs-lookup"><span data-stu-id="36902-146">(It is unlikely that this will yield any results, because data doesn’t make it through the system that fast.)</span></span>

<span data-ttu-id="36902-147">Te przykłady są blokami konstrukcyjnymi do użycia dla dat względnych i bezwzględnych.</span><span class="sxs-lookup"><span data-stu-id="36902-147">These examples are building blocks to use for relative and absolute dates.</span></span> <span data-ttu-id="36902-148">W trzech kolejnych podsekcjach pojawi się, jak ich używać w filtrach bardziej zaawansowanych, wraz z przykładami, korzystających z zakresów względnej daty.</span><span class="sxs-lookup"><span data-stu-id="36902-148">In the next three subsections, you'll see how to use them in more advanced filters, with examples that use relative date ranges.</span></span>

### <a name="datetime-math"></a><span data-ttu-id="36902-149">Data/Godzina matematyczne</span><span class="sxs-lookup"><span data-stu-id="36902-149">Date/Time math</span></span>
<span data-ttu-id="36902-150">Operatory matematyczne daty i godziny umożliwia przesunięcie lub zaokrąglanie wartości daty/godziny przy użyciu prostych obliczeń daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="36902-150">Use the Date/Time math operators to offset or round the Date/Time value, by using simple Date/Time calculations.</span></span>

<span data-ttu-id="36902-151">Składnia:</span><span class="sxs-lookup"><span data-stu-id="36902-151">Syntax:</span></span>

```
datetime/unit
```

```
datetime[+|-]count unit
```

| <span data-ttu-id="36902-152">Operator</span><span class="sxs-lookup"><span data-stu-id="36902-152">Operator</span></span> | <span data-ttu-id="36902-153">Opis</span><span class="sxs-lookup"><span data-stu-id="36902-153">Description</span></span> |
| --- | --- |
| / |<span data-ttu-id="36902-154">Zaokrągla wartość daty i godziny do określonej jednostki.</span><span class="sxs-lookup"><span data-stu-id="36902-154">Rounds Date/Time to the specified unit.</span></span> <span data-ttu-id="36902-155">Na przykład teraz / dzień zaokrągla bieżącej daty/godziny północy bieżącego dnia.</span><span class="sxs-lookup"><span data-stu-id="36902-155">For example, NOW/DAY rounds the current Date/Time to midnight of the current day.</span></span> |
| <span data-ttu-id="36902-156">+ lub -</span><span class="sxs-lookup"><span data-stu-id="36902-156">+ or -</span></span> |<span data-ttu-id="36902-157">Powoduje przesunięcie daty/godziny, o określoną liczbę jednostek.</span><span class="sxs-lookup"><span data-stu-id="36902-157">Offsets Date/Time by the specified number of units.</span></span> <span data-ttu-id="36902-158">Na przykład teraz + 1 godzina powoduje przesunięcie bieżącej daty/godziny o godzinę wyprzedzeniem.</span><span class="sxs-lookup"><span data-stu-id="36902-158">For example, NOW+1HOUR offsets the current Date/Time by one hour ahead.</span></span> <span data-ttu-id="36902-159">2013-10-01T12:00-10-DNIOWĄ przesunięcia wartości typu Date przez 10 dni.</span><span class="sxs-lookup"><span data-stu-id="36902-159">2013-10-01T12:00-10DAYS offsets the Date value back by 10 days.</span></span> |

<span data-ttu-id="36902-160">Operatory matematyczne daty i godziny mogą powiązane ze sobą.</span><span class="sxs-lookup"><span data-stu-id="36902-160">You can chain the Date/Time math operators together.</span></span> <span data-ttu-id="36902-161">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36902-161">For example:</span></span>

```
NOW+1HOUR-10MONTHS/MINUTE
```

<span data-ttu-id="36902-162">W poniższej tabeli wymieniono obsługiwane jednostek daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="36902-162">The following table lists the supported Date/Time units.</span></span>

| <span data-ttu-id="36902-163">Jednostka daty/godziny</span><span class="sxs-lookup"><span data-stu-id="36902-163">Date/Time unit</span></span> | <span data-ttu-id="36902-164">Opis</span><span class="sxs-lookup"><span data-stu-id="36902-164">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36902-165">YEAR, YEARS</span><span class="sxs-lookup"><span data-stu-id="36902-165">YEAR, YEARS</span></span> |<span data-ttu-id="36902-166">Zaokrągla liczbę do bieżącego roku, lub przesunięcia przez określoną liczbę lat.</span><span class="sxs-lookup"><span data-stu-id="36902-166">Rounds to current year, or offsets by the specified number of years.</span></span> |
| <span data-ttu-id="36902-167">MIESIĄC, MIESIĘCY</span><span class="sxs-lookup"><span data-stu-id="36902-167">MONTH, MONTHS</span></span> |<span data-ttu-id="36902-168">Zaokrągla liczbę do bieżącego miesiąca lub przesunięcia przez określoną liczbę miesięcy.</span><span class="sxs-lookup"><span data-stu-id="36902-168">Rounds to current month, or offsets by the specified number of months.</span></span> |
| <span data-ttu-id="36902-169">DZIEŃ, DNI, DATA</span><span class="sxs-lookup"><span data-stu-id="36902-169">DAY, DAYS, DATE</span></span> |<span data-ttu-id="36902-170">Powoduje zaokrąglenie do bieżącego dnia, miesiąca lub przesunięcia przez określoną liczbę dni.</span><span class="sxs-lookup"><span data-stu-id="36902-170">Rounds to current day of the month, or offsets by the specified number of days.</span></span> |
| <span data-ttu-id="36902-171">GODZINA, GODZINY</span><span class="sxs-lookup"><span data-stu-id="36902-171">HOUR, HOURS</span></span> |<span data-ttu-id="36902-172">Zaokrągla liczbę do bieżącej godziny lub przesunięcia przez określoną liczbę godzin.</span><span class="sxs-lookup"><span data-stu-id="36902-172">Rounds to current hour, or offsets by the specified number of hours.</span></span> |
| <span data-ttu-id="36902-173">MINUTA, MINUT</span><span class="sxs-lookup"><span data-stu-id="36902-173">MINUTE, MINUTES</span></span> |<span data-ttu-id="36902-174">Zaokrągla liczbę do bieżącej minuty lub przesunięcia przez określoną liczbę minut.</span><span class="sxs-lookup"><span data-stu-id="36902-174">Rounds to current minute, or offsets by the specified number of minutes.</span></span> |
| <span data-ttu-id="36902-175">SECOND, SECONDS,</span><span class="sxs-lookup"><span data-stu-id="36902-175">SECOND, SECONDS</span></span> |<span data-ttu-id="36902-176">Drugi powoduje zaokrąglenie do bieżącej lub przesunięcia przez określoną liczbę sekund.</span><span class="sxs-lookup"><span data-stu-id="36902-176">Rounds to current second, or offsets by the specified number of seconds.</span></span> |
| <span data-ttu-id="36902-177">MILISEKUNDY MILISEKUND, MILLI, MILLIS</span><span class="sxs-lookup"><span data-stu-id="36902-177">MILLISECOND, MILLISECONDS, MILLI, MILLIS</span></span> |<span data-ttu-id="36902-178">Zaokrągla liczbę do bieżącego milisekund lub przesunięcia przez określoną liczbę milisekund.</span><span class="sxs-lookup"><span data-stu-id="36902-178">Rounds to current millisecond, or offsets by the specified number of milliseconds.</span></span> |

### <a name="field-facets"></a><span data-ttu-id="36902-179">Aspekty pola</span><span class="sxs-lookup"><span data-stu-id="36902-179">Field facets</span></span>
<span data-ttu-id="36902-180">Za pomocą pola aspektów, można określić warunku wyszukiwania dla określonych pól i ich dokładne wartości.</span><span class="sxs-lookup"><span data-stu-id="36902-180">By using field facets, you can specify the search condition for specific fields and their exact values.</span></span> <span data-ttu-id="36902-181">To różni się od Pisanie zapytań "wolne tekst" dla różnych warunków w całym indeksie.</span><span class="sxs-lookup"><span data-stu-id="36902-181">This differs from writing "free text" queries for various terms throughout the index.</span></span> <span data-ttu-id="36902-182">Ta technika w poprzednich przykładach kilka ma już widoczne.</span><span class="sxs-lookup"><span data-stu-id="36902-182">You have already seen this technique in several previous examples.</span></span> <span data-ttu-id="36902-183">Poniżej przedstawiono bardziej skomplikowane.</span><span class="sxs-lookup"><span data-stu-id="36902-183">The following are more complex examples.</span></span>

<span data-ttu-id="36902-184">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="36902-184">**Syntax**</span></span>

```
field:value
```

```
field=value
```

<span data-ttu-id="36902-185">**Opis**</span><span class="sxs-lookup"><span data-stu-id="36902-185">**Description**</span></span>

<span data-ttu-id="36902-186">Wyszukuje określoną wartość w polu.</span><span class="sxs-lookup"><span data-stu-id="36902-186">Searches the field for the specific value.</span></span> <span data-ttu-id="36902-187">Wartość może być literał ciągu, numer, lub Data i godzina.</span><span class="sxs-lookup"><span data-stu-id="36902-187">The value can be a string literal, number, or date and time.</span></span>

<span data-ttu-id="36902-188">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36902-188">For example:</span></span>

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

<span data-ttu-id="36902-189">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="36902-189">**Syntax**</span></span>

<span data-ttu-id="36902-190">*pole > wartość*</span><span class="sxs-lookup"><span data-stu-id="36902-190">*field>value*</span></span>

<span data-ttu-id="36902-191">*pole < wartość*</span><span class="sxs-lookup"><span data-stu-id="36902-191">*field<value*</span></span>

<span data-ttu-id="36902-192">*pole > = wartość*</span><span class="sxs-lookup"><span data-stu-id="36902-192">*field>=value*</span></span>

<span data-ttu-id="36902-193">*pole < = wartość*</span><span class="sxs-lookup"><span data-stu-id="36902-193">*field<=value*</span></span>

<span data-ttu-id="36902-194">*pole! = wartość*</span><span class="sxs-lookup"><span data-stu-id="36902-194">*field!=value*</span></span>

<span data-ttu-id="36902-195">**Opis**</span><span class="sxs-lookup"><span data-stu-id="36902-195">**Description**</span></span>

<span data-ttu-id="36902-196">Udostępnia porównania.</span><span class="sxs-lookup"><span data-stu-id="36902-196">Provides comparisons.</span></span>

<span data-ttu-id="36902-197">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36902-197">For example:</span></span>

```
TimeGenerated>NOW+2HOURS
```

<span data-ttu-id="36902-198">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="36902-198">**Syntax**</span></span>

```
field:[from..to]
```

<span data-ttu-id="36902-199">**Opis**</span><span class="sxs-lookup"><span data-stu-id="36902-199">**Description**</span></span>

<span data-ttu-id="36902-200">Umożliwia tworzenie aspektów zakresu.</span><span class="sxs-lookup"><span data-stu-id="36902-200">Provides range faceting.</span></span>

<span data-ttu-id="36902-201">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="36902-201">For example:</span></span>

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a><span data-ttu-id="36902-202">W</span><span class="sxs-lookup"><span data-stu-id="36902-202">IN</span></span>
<span data-ttu-id="36902-203">**IN** — słowo kluczowe można wybrać z listy wartości.</span><span class="sxs-lookup"><span data-stu-id="36902-203">The **IN** keyword allows you to select from a list of values.</span></span> <span data-ttu-id="36902-204">W zależności od składni, którego używasz może to być prosta lista wartości, który podasz lub listę wartości z agregacji.</span><span class="sxs-lookup"><span data-stu-id="36902-204">Depending on the syntax you use, this can be a simple list of values you provide, or a list of values from an aggregation.</span></span>

<span data-ttu-id="36902-205">Składnia 1:</span><span class="sxs-lookup"><span data-stu-id="36902-205">Syntax 1:</span></span>

```
field IN {value1,value2,value3,...}
```

<span data-ttu-id="36902-206">Ta składnia umożliwia obejmują wszystkie wartości na liście proste.</span><span class="sxs-lookup"><span data-stu-id="36902-206">This syntax allows you to include all values in a simple list.</span></span>



<span data-ttu-id="36902-207">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="36902-207">Examples:</span></span>

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

<span data-ttu-id="36902-208">Składnia 2:</span><span class="sxs-lookup"><span data-stu-id="36902-208">Syntax 2:</span></span>

```
(Outer query) (Field to use with inner query results) IN {Inner query | measure count() by (Field to send to outer query)} (rest  of outer query)  
```

<span data-ttu-id="36902-209">Ta składnia umożliwia tworzenie agregacji.</span><span class="sxs-lookup"><span data-stu-id="36902-209">This syntax allows you to create an aggregation.</span></span> <span data-ttu-id="36902-210">Lista wartości może następnie dostarczyć z tym agregacji w innym zewnętrzne wyszukiwania (podstawowe), sprawdzający zdarzenia z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="36902-210">You can then feed the list of values from that aggregation into another outer (primary) search that looks for events with those value.</span></span> <span data-ttu-id="36902-211">W tym celu otaczającej wewnętrzny wyszukiwania w nawiasach klamrowych i skierowanie wyniki jako możliwe wartości dla pola w zewnętrznym wyszukiwania za pomocą operatora IN.</span><span class="sxs-lookup"><span data-stu-id="36902-211">You do this by enclosing the inner search in braces, and feeding its results as possible values for a field in the outer search by using the IN operator.</span></span>

<span data-ttu-id="36902-212">Przykład wewnętrzny zapytania: *komputerów obecnie brakujących aktualizacji zabezpieczeń* z następującej kwerendy agregacji:</span><span class="sxs-lookup"><span data-stu-id="36902-212">Inner query example: *computers currently missing security updates* with the following aggregation query:</span></span>

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

<span data-ttu-id="36902-213">Końcowe kwerendę, która wyszukuje *wszystkie zdarzenia systemu Windows dla komputerów, w obecnie brakujących aktualizacji zabezpieczeń* jest podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="36902-213">The final query that finds *all Windows events for computers currently missing security updates* resembles the following:</span></span>

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a><span data-ttu-id="36902-214">Contains</span><span class="sxs-lookup"><span data-stu-id="36902-214">Contains</span></span>
<span data-ttu-id="36902-215">**Zawiera** — słowo kluczowe umożliwia filtrowanie rekordów z polem, który zawiera określony ciąg.</span><span class="sxs-lookup"><span data-stu-id="36902-215">The **Contains** keyword allows you to filter for records with a field that contains a specified string.</span></span> <span data-ttu-id="36902-216">To jest rozróżniana wielkość liter, działa tylko w przypadku pól ciągów i nie może zawierać żadnych znaków ucieczki.</span><span class="sxs-lookup"><span data-stu-id="36902-216">This is case sensitive, works only with string fields, and may not include any escape characters.</span></span>

<span data-ttu-id="36902-217">Składnia:</span><span class="sxs-lookup"><span data-stu-id="36902-217">Syntax:</span></span>

```
field:contains("string")
```

<span data-ttu-id="36902-218">Przykład:</span><span class="sxs-lookup"><span data-stu-id="36902-218">Example:</span></span>

```
Type:contains("Event")
```

<span data-ttu-id="36902-219">To polecenie zwróci rekordy z typem, który zawiera ciąg "Event".</span><span class="sxs-lookup"><span data-stu-id="36902-219">This returns records with a type that contains the string "Event".</span></span> <span data-ttu-id="36902-220">Przykłady obejmują **zdarzeń**, **SecurityEvent**, i **ServiceFabricOperationEvent**.</span><span class="sxs-lookup"><span data-stu-id="36902-220">Examples include **Event**, **SecurityEvent**, and **ServiceFabricOperationEvent**.</span></span>



### <a name="regular-expressions"></a><span data-ttu-id="36902-221">Wyrażenia regularne</span><span class="sxs-lookup"><span data-stu-id="36902-221">Regular expressions</span></span>
<span data-ttu-id="36902-222">Można określić warunku wyszukiwania dla pola z wyrażeniem regularnym, za pomocą **Regex** — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="36902-222">You can specify a search condition for a field with a regular expression, by using the **Regex** keyword.</span></span> <span data-ttu-id="36902-223">Pełny opis można używać w wyrażeniach regularnych składni, zobacz [za pomocą wyrażeń regularnych do filtrowania dziennika wyszukiwania analizy dzienników](log-analytics-log-searches-regex.md).</span><span class="sxs-lookup"><span data-stu-id="36902-223">For a complete description of the syntax you can use in regular expressions, see [Using regular expressions to filter log searches in Log Analytics](log-analytics-log-searches-regex.md).</span></span>

<span data-ttu-id="36902-224">Składnia:</span><span class="sxs-lookup"><span data-stu-id="36902-224">Syntax:</span></span>

```
field:Regex("Regular Expression")
```

<span data-ttu-id="36902-225">Przykład:</span><span class="sxs-lookup"><span data-stu-id="36902-225">Example:</span></span>

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a><span data-ttu-id="36902-226">Operatory logiczne</span><span class="sxs-lookup"><span data-stu-id="36902-226">Logical operators</span></span>
<span data-ttu-id="36902-227">Języki zapytań obsługuje operatory logiczne (*i*, *lub*, i *nie*) i ich aliasy w stylu języka C (*&&*,  *||* , i *!*odpowiednio).</span><span class="sxs-lookup"><span data-stu-id="36902-227">The query languages support the logical operators (*AND*, *OR*, and *NOT*) and their C-style aliases (*&&*, *||*, and *!*, respectively).</span></span> <span data-ttu-id="36902-228">Można użyć nawiasów do grupowania tych operatorów.</span><span class="sxs-lookup"><span data-stu-id="36902-228">You can use parentheses to group these operators.</span></span>

<span data-ttu-id="36902-229">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="36902-229">Examples:</span></span>

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

<span data-ttu-id="36902-230">Operator logiczny dla argumentów filtru najwyższego poziomu można pominąć.</span><span class="sxs-lookup"><span data-stu-id="36902-230">You can omit the logical operator for the top-level filter arguments.</span></span> <span data-ttu-id="36902-231">W takim przypadku AND operator zakłada, że.</span><span class="sxs-lookup"><span data-stu-id="36902-231">In this case, the AND operator is assumed.</span></span>

| <span data-ttu-id="36902-232">Wyrażenie filtru</span><span class="sxs-lookup"><span data-stu-id="36902-232">Filter expression</span></span> | <span data-ttu-id="36902-233">Wartość równoważna wartości</span><span class="sxs-lookup"><span data-stu-id="36902-233">Equivalent to</span></span> |
| --- | --- |
| <span data-ttu-id="36902-234">Błąd systemu:</span><span class="sxs-lookup"><span data-stu-id="36902-234">system error</span></span> |<span data-ttu-id="36902-235">System i błędów</span><span class="sxs-lookup"><span data-stu-id="36902-235">system AND error</span></span> |
| <span data-ttu-id="36902-236">System "Windows Server" lub ważność: 1</span><span class="sxs-lookup"><span data-stu-id="36902-236">system "Windows Server" OR Severity:1</span></span> |<span data-ttu-id="36902-237">System i ("Windows Server" lub ważność: 1)</span><span class="sxs-lookup"><span data-stu-id="36902-237">system AND ("Windows Server" OR Severity:1)</span></span> |

### <a name="wildcarding"></a><span data-ttu-id="36902-238">Symbole wieloznaczne</span><span class="sxs-lookup"><span data-stu-id="36902-238">Wildcarding</span></span>
<span data-ttu-id="36902-239">Język zapytań obsługuje korzystanie z ( \* ) znaku do reprezentowania jeden lub więcej znaków wartości w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="36902-239">The query language supports using the ( \* ) character to  represent one or more characters for a value in a query.</span></span>

<span data-ttu-id="36902-240">Przykład:</span><span class="sxs-lookup"><span data-stu-id="36902-240">Example:</span></span>

 <span data-ttu-id="36902-241">Znajdź wszystkie komputery z "SQL" w nazwie, takie jak "Redmond SQL".</span><span class="sxs-lookup"><span data-stu-id="36902-241">Find all computers with "SQL" in the name, such as "Redmond-SQL".</span></span>

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> <span data-ttu-id="36902-242">W tej chwili nie można używać symboli wieloznacznych w cudzysłowach.</span><span class="sxs-lookup"><span data-stu-id="36902-242">At this time, wildcards cannot be used within quotations.</span></span> <span data-ttu-id="36902-243">Na przykład komunikat `"*This text*"` uwzględnia (\*) używane jako literału (\*) znaków.</span><span class="sxs-lookup"><span data-stu-id="36902-243">For example, the message `"*This text*"` considers the (\*) used as a literal (\*) character.</span></span>


## <a name="commands"></a><span data-ttu-id="36902-244">Polecenia</span><span class="sxs-lookup"><span data-stu-id="36902-244">Commands</span></span>


<span data-ttu-id="36902-245">Polecenia dotyczą wyników zwróconych przez kwerendę.</span><span class="sxs-lookup"><span data-stu-id="36902-245">The commands apply to the results that are returned by the query.</span></span> <span data-ttu-id="36902-246">Umożliwia zastosowanie polecenia do wyników pobrane znaku kreski pionowej (|).</span><span class="sxs-lookup"><span data-stu-id="36902-246">Use the pipe character ( | ) to apply a command to the retrieved results.</span></span> <span data-ttu-id="36902-247">Wiele poleceń muszą być oddzielone znaku kreski pionowej.</span><span class="sxs-lookup"><span data-stu-id="36902-247">Multiple commands must be separated by the pipe character.</span></span>

> [!NOTE]
> <span data-ttu-id="36902-248">Nazwy poleceń można pisać w wielkie lub małe litery, w odróżnieniu od nazwy pól i danych.</span><span class="sxs-lookup"><span data-stu-id="36902-248">Command names can be written in upper case or lower case, unlike the field names and the data.</span></span>
>
>

### <a name="sort"></a><span data-ttu-id="36902-249">Sortuj</span><span class="sxs-lookup"><span data-stu-id="36902-249">Sort</span></span>
<span data-ttu-id="36902-250">Składnia:</span><span class="sxs-lookup"><span data-stu-id="36902-250">Syntax:</span></span>

    sort field1 asc|desc, field2 asc|desc, …

<span data-ttu-id="36902-251">Sortuj wyniki według określonego pola.</span><span class="sxs-lookup"><span data-stu-id="36902-251">Sorts the results by particular fields.</span></span> <span data-ttu-id="36902-252">Sufiks asc/desc sortować wyniki w kolejności rosnącej lub malejącej jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="36902-252">The asc/desc suffix to sort the results in ascending or descending order is optional.</span></span> <span data-ttu-id="36902-253">Jeśli zostanie pominięty, *asc* zakłada, że kolejność sortowania.</span><span class="sxs-lookup"><span data-stu-id="36902-253">If it is omitted, the *asc* sort order is assumed.</span></span> <span data-ttu-id="36902-254">Dla **TimeGenerated** pola *desc* zakłada się porządek sortowania, więc najpierw zwraca najnowsze wyniki domyślnie.</span><span class="sxs-lookup"><span data-stu-id="36902-254">For the **TimeGenerated** field, *desc* sort order is assumed, so it returns the most recent results first by default.</span></span>

### <a name="toplimit"></a><span data-ttu-id="36902-255">TOP/Limit</span><span class="sxs-lookup"><span data-stu-id="36902-255">Top/Limit</span></span>
<span data-ttu-id="36902-256">Składnia:</span><span class="sxs-lookup"><span data-stu-id="36902-256">Syntax:</span></span>

    top number


    limit number
<span data-ttu-id="36902-257">Ogranicza odpowiedź na pierwsze N wyników.</span><span class="sxs-lookup"><span data-stu-id="36902-257">Limits the response to the top N results.</span></span>

<span data-ttu-id="36902-258">Przykład:</span><span class="sxs-lookup"><span data-stu-id="36902-258">Example:</span></span>

    Type:Alert errors detected | top 10

<span data-ttu-id="36902-259">Zwraca górny 10 pasujących wyników.</span><span class="sxs-lookup"><span data-stu-id="36902-259">Returns the top 10 matching results.</span></span>

### <a name="skip"></a><span data-ttu-id="36902-260">Pomiń</span><span class="sxs-lookup"><span data-stu-id="36902-260">Skip</span></span>
<span data-ttu-id="36902-261">Składnia:</span><span class="sxs-lookup"><span data-stu-id="36902-261">Syntax:</span></span>

    skip number

<span data-ttu-id="36902-262">Pomija liczbę wyników na liście.</span><span class="sxs-lookup"><span data-stu-id="36902-262">Skips the number of results listed.</span></span>

<span data-ttu-id="36902-263">Przykład:</span><span class="sxs-lookup"><span data-stu-id="36902-263">Example:</span></span>

    Type:Alert errors detected | top 10 | skip 200

<span data-ttu-id="36902-264">Zwraca górny 10 pasujących wyników zaczynając od wyniku 200.</span><span class="sxs-lookup"><span data-stu-id="36902-264">Returns top 10 matching results starting at result 200.</span></span>

### <a name="select"></a><span data-ttu-id="36902-265">Wybierz pozycję</span><span class="sxs-lookup"><span data-stu-id="36902-265">Select</span></span>
<span data-ttu-id="36902-266">Składnia:</span><span class="sxs-lookup"><span data-stu-id="36902-266">Syntax:</span></span>

    select field1, field2, ...

<span data-ttu-id="36902-267">Ogranicza wyniki do pola, które można wybrać.</span><span class="sxs-lookup"><span data-stu-id="36902-267">Limits results to the fields you choose.</span></span>

<span data-ttu-id="36902-268">Przykład:</span><span class="sxs-lookup"><span data-stu-id="36902-268">Example:</span></span>

    Type:Alert errors detected | select Name, Severity

<span data-ttu-id="36902-269">Ogranicza pola zwrócone wyniki *nazwa* i *ważność*.</span><span class="sxs-lookup"><span data-stu-id="36902-269">Limits the returned results fields to *Name* and *Severity*.</span></span>

### <a name="measure"></a><span data-ttu-id="36902-270">Miary</span><span class="sxs-lookup"><span data-stu-id="36902-270">Measure</span></span>
<span data-ttu-id="36902-271">*Miary* polecenie służy do stosowania funkcji statystycznych do wyników wyszukiwania raw.</span><span class="sxs-lookup"><span data-stu-id="36902-271">The *measure* command is used to apply statistical functions to the raw search results.</span></span> <span data-ttu-id="36902-272">Jest to bardzo przydatne uzyskać *Grupuj według* widoków danych.</span><span class="sxs-lookup"><span data-stu-id="36902-272">This is very useful to get *group-by* views over the data.</span></span> <span data-ttu-id="36902-273">Po użyciu polecenia miary, analizy dzienników zostanie wyświetlona tabela z wyników zagregowany.</span><span class="sxs-lookup"><span data-stu-id="36902-273">When you use the measure command, Log Analytics search displays a table with aggregated results.</span></span>

<span data-ttu-id="36902-274">**Składnia:**</span><span class="sxs-lookup"><span data-stu-id="36902-274">**Syntax:**</span></span>

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



<span data-ttu-id="36902-275">Agreguje wyniki według *groupField*i oblicza wartości zagregowane miary za pomocą *aggregatedField*.</span><span class="sxs-lookup"><span data-stu-id="36902-275">Aggregates the results by *groupField*, and calculates the aggregated measure values by using *aggregatedField*.</span></span>

| <span data-ttu-id="36902-276">Funkcja statystyczne miary</span><span class="sxs-lookup"><span data-stu-id="36902-276">Measure statistical function</span></span> | <span data-ttu-id="36902-277">Opis</span><span class="sxs-lookup"><span data-stu-id="36902-277">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36902-278">*Funkcja aggregateFunction*</span><span class="sxs-lookup"><span data-stu-id="36902-278">*aggregateFunction*</span></span> |<span data-ttu-id="36902-279">Nazwa funkcji agregującej (bez uwzględniania wielkości liter).</span><span class="sxs-lookup"><span data-stu-id="36902-279">The name of the aggregate function (case insensitive).</span></span> <span data-ttu-id="36902-280">Obsługiwane są następujące funkcje agregujące: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, percentyl ## lub PCT ## (## jest liczbą zakresu od 1 do 99).</span><span class="sxs-lookup"><span data-stu-id="36902-280">The following aggregate functions are supported: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> |
| <span data-ttu-id="36902-281">*aggregatedField*</span><span class="sxs-lookup"><span data-stu-id="36902-281">*aggregatedField*</span></span> |<span data-ttu-id="36902-282">Pole jest agregowanie.</span><span class="sxs-lookup"><span data-stu-id="36902-282">The field that is being aggregated.</span></span> <span data-ttu-id="36902-283">To pole jest opcjonalne dla funkcji agregującej COUNT, ale musi być istniejącym polem liczbowe SUM, MAX, MIN, AVG, STDDEV, percentyl ## lub PCT ## (## jest liczbą zakresu od 1 do 99).</span><span class="sxs-lookup"><span data-stu-id="36902-283">This field is optional for the COUNT aggregate function, but has to be an existing numeric field for SUM, MAX, MIN, AVG, STDDEV, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> <span data-ttu-id="36902-284">AggregatedField mogą również być **Rozszerz** obsługiwanych funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-284">The aggregatedField can also be any of the **Extend** supported functions.</span></span> |
| <span data-ttu-id="36902-285">*fieldAlias*</span><span class="sxs-lookup"><span data-stu-id="36902-285">*fieldAlias*</span></span> |<span data-ttu-id="36902-286">(Opcjonalnie) alias dla obliczonej wartości zagregowanej.</span><span class="sxs-lookup"><span data-stu-id="36902-286">The (optional) alias for the calculated aggregated value.</span></span> <span data-ttu-id="36902-287">Jeśli nie zostanie określony, nazwa pola jest **AggregatedValue**.</span><span class="sxs-lookup"><span data-stu-id="36902-287">If not specified, the field name is **AggregatedValue**.</span></span> |
| <span data-ttu-id="36902-288">*groupField*</span><span class="sxs-lookup"><span data-stu-id="36902-288">*groupField*</span></span> |<span data-ttu-id="36902-289">Nazwa pola, które zestaw wyników są grupowane według.</span><span class="sxs-lookup"><span data-stu-id="36902-289">The name of the field that the result set is grouped by.</span></span> |
| <span data-ttu-id="36902-290">*Interwał*</span><span class="sxs-lookup"><span data-stu-id="36902-290">*Interval*</span></span> |<span data-ttu-id="36902-291">Przedział czasu, w formacie:**nnnNAME**.</span><span class="sxs-lookup"><span data-stu-id="36902-291">The time interval, in the format:**nnnNAME**.</span></span> <span data-ttu-id="36902-292">**nnn**jest to liczba dodatnia liczba całkowita.</span><span class="sxs-lookup"><span data-stu-id="36902-292">**nnn** is the positive integer number.</span></span> <span data-ttu-id="36902-293">**Nazwa** jest nazwą interwału.</span><span class="sxs-lookup"><span data-stu-id="36902-293">**NAME** is the interval name.</span></span> <span data-ttu-id="36902-294">Nazwy obsługiwany interwał jest uwzględniana wielkość liter i obejmują: MILISEKUNDY [S] sekundy [S] MINUTĘ [S] z godziny [S] dnia [S] [S] miesiąca i roku [S].</span><span class="sxs-lookup"><span data-stu-id="36902-294">Supported interval names are case sensitive, and include:MILLISECOND[S], SECOND[S], MINUTE[S], HOUR[S], DAY[S], MONTH[S], and YEAR[S].</span></span> |

<span data-ttu-id="36902-295">Opcja zakresu jest możliwe tylko w polach grupy daty/godziny (takich jak *TimeGenerated* i *TimeCreated*).</span><span class="sxs-lookup"><span data-stu-id="36902-295">The interval option can only be used in Date/Time group fields (such as *TimeGenerated* and *TimeCreated*).</span></span> <span data-ttu-id="36902-296">Obecnie ta wartość nie jest wymuszana przez usługę, ale pole bez daty i godziny przekazywane do wewnętrznej powoduje błąd w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="36902-296">Currently, this is not enforced by the service, but a field without Date/Time that is passed to the back end causes a runtime error.</span></span> <span data-ttu-id="36902-297">Po zaimplementowaniu sprawdzanie poprawności schematu interfejsu API usługi odrzuca zapytań, które pola bez daty/godziny na użytek interwał agregacji.</span><span class="sxs-lookup"><span data-stu-id="36902-297">When the schema validation is implemented, the service API rejects queries that use fields without Date/Time for interval aggregation.</span></span> <span data-ttu-id="36902-298">Bieżący *miary* implementacja obsługuje grupowania interwał funkcji agregacji.</span><span class="sxs-lookup"><span data-stu-id="36902-298">The current *Measure* implementation supports interval grouping for any aggregate function.</span></span>

<span data-ttu-id="36902-299">Jeśli w klauzuli BY zostanie pominięty, ale podano interwału (jako drugi składni), *TimeGenerated* pola przyjęto, że domyślnie.</span><span class="sxs-lookup"><span data-stu-id="36902-299">If the BY clause is omitted, but an interval is specified (as a second syntax), the *TimeGenerated* field is assumed by default.</span></span>

<span data-ttu-id="36902-300">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="36902-300">Examples:</span></span>

<span data-ttu-id="36902-301">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="36902-301">**Example 1**</span></span>

    Type:Alert | measure count() as Count by ObjectId

<span data-ttu-id="36902-302">Grupuje alertów według *ObjectID*i oblicza liczbę alertów dla każdej grupy.</span><span class="sxs-lookup"><span data-stu-id="36902-302">Groups the alerts by *ObjectID*, and calculates the number of alerts for each group.</span></span> <span data-ttu-id="36902-303">Wartości zagregowane są zwracane jako *liczba* pola (alias).</span><span class="sxs-lookup"><span data-stu-id="36902-303">The aggregated value is returned as the *Count* field (alias).</span></span>

<span data-ttu-id="36902-304">**Przykład 2**</span><span class="sxs-lookup"><span data-stu-id="36902-304">**Example 2**</span></span>

    Type:Alert | measure count() interval 1HOUR

<span data-ttu-id="36902-305">Grupy alerty przez 1 godzinę za pomocą *TimeGenerated* pól i zwraca liczbę alertów w każdym interwale.</span><span class="sxs-lookup"><span data-stu-id="36902-305">Groups the alerts by 1-hour intervals by using the *TimeGenerated* field, and returns the number of alerts in each interval.</span></span>

<span data-ttu-id="36902-306">**Przykład 3**</span><span class="sxs-lookup"><span data-stu-id="36902-306">**Example 3**</span></span>

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

<span data-ttu-id="36902-307">Co w poprzednim przykładzie, ale z aliasem pola zagregowane (*AlertsPerHour*).</span><span class="sxs-lookup"><span data-stu-id="36902-307">Same as the previous example, but with an aggregated field alias (*AlertsPerHour*).</span></span>

<span data-ttu-id="36902-308">**Przykład 4**</span><span class="sxs-lookup"><span data-stu-id="36902-308">**Example 4**</span></span>

    * <span data-ttu-id="36902-309">| Miara count() przez 5DAYS interwał TimeCreated</span><span class="sxs-lookup"><span data-stu-id="36902-309">| measure count() by TimeCreated interval 5DAYS</span></span>

<span data-ttu-id="36902-310">Grupuje wyniki według 5 dni przy użyciu *TimeCreated* pól i zwraca liczbę wyników w każdym interwale.</span><span class="sxs-lookup"><span data-stu-id="36902-310">Groups the results by 5-day intervals by using the *TimeCreated* field, and returns the number of results in each interval.</span></span>

<span data-ttu-id="36902-311">**Przykład 5**</span><span class="sxs-lookup"><span data-stu-id="36902-311">**Example 5**</span></span>

    Type:Alert | measure max(Severity) by WorkflowName

<span data-ttu-id="36902-312">Grupuje alerty według nazwy obciążenie i zwraca wartość maksymalną alert o ważności dla każdego przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="36902-312">Groups the alerts by workload name, and returns the maximum alert severity value for each workflow.</span></span>

<span data-ttu-id="36902-313">**Przykład 6**</span><span class="sxs-lookup"><span data-stu-id="36902-313">**Example 6**</span></span>

    Type:Alert | measure min(Severity) by WorkflowName

<span data-ttu-id="36902-314">Co w poprzednim przykładzie, ale z *min* zagregowane funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-314">Same as the previous example, but with the *min* aggregated function.</span></span>

<span data-ttu-id="36902-315">**Przykład 7**</span><span class="sxs-lookup"><span data-stu-id="36902-315">**Example 7**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer

<span data-ttu-id="36902-316">Grupuje wydajności przez komputer, a następnie oblicza średnią (średni).</span><span class="sxs-lookup"><span data-stu-id="36902-316">Groups Perf by computer, and calculates the average (avg).</span></span>

<span data-ttu-id="36902-317">**Przykład 8**</span><span class="sxs-lookup"><span data-stu-id="36902-317">**Example 8**</span></span>

    Type:Perf | measure sum(CounterValue) by Computer

<span data-ttu-id="36902-318">Takie same, co w poprzednim przykładzie, ale używa *suma*.</span><span class="sxs-lookup"><span data-stu-id="36902-318">Same as the previous example, but uses *sum*.</span></span>

<span data-ttu-id="36902-319">**Przykład 9**</span><span class="sxs-lookup"><span data-stu-id="36902-319">**Example 9**</span></span>

    Type:Perf | measure stddev(CounterValue) by Computer

<span data-ttu-id="36902-320">Takie same, co w poprzednim przykładzie, ale używa *stddev*.</span><span class="sxs-lookup"><span data-stu-id="36902-320">Same as the previous example, but uses *stddev*.</span></span>

<span data-ttu-id="36902-321">**Przykład 10**</span><span class="sxs-lookup"><span data-stu-id="36902-321">**Example 10**</span></span>

    Type:Perf | measure percentile70(CounterValue) by Computer

<span data-ttu-id="36902-322">Takie same, co w poprzednim przykładzie, ale używa *percentile70*.</span><span class="sxs-lookup"><span data-stu-id="36902-322">Same as the previous example, but uses *percentile70*.</span></span>

<span data-ttu-id="36902-323">**Przykład 11**</span><span class="sxs-lookup"><span data-stu-id="36902-323">**Example 11**</span></span>

    Type:Perf | measure pct70(CounterValue) by Computer

<span data-ttu-id="36902-324">Takie same, co w poprzednim przykładzie, ale używa *pct70*.</span><span class="sxs-lookup"><span data-stu-id="36902-324">Same as the previous example, but uses *pct70*.</span></span> <span data-ttu-id="36902-325">Należy pamiętać, że *PCT ##* jest tylko aliasu dla *percentyl ##* funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-325">Note that *PCT##* is only an alias for *PERCENTILE##* function.</span></span>

<span data-ttu-id="36902-326">**Przykład 12**</span><span class="sxs-lookup"><span data-stu-id="36902-326">**Example 12**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

<span data-ttu-id="36902-327">Grupuje wydajności najpierw przez komputer, a następnie CounterName i oblicza średnią (średni).</span><span class="sxs-lookup"><span data-stu-id="36902-327">Groups Perf first by Computer and then CounterName, and calculates the average (avg).</span></span>

<span data-ttu-id="36902-328">**Przykład 13**</span><span class="sxs-lookup"><span data-stu-id="36902-328">**Example 13**</span></span>

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

<span data-ttu-id="36902-329">Pobiera top pięć przepływy pracy z maksymalną liczbę alertów.</span><span class="sxs-lookup"><span data-stu-id="36902-329">Gets the top five workflows with the maximum number of alerts.</span></span>

<span data-ttu-id="36902-330">**Przykład 14**</span><span class="sxs-lookup"><span data-stu-id="36902-330">**Example 14**</span></span>

    * <span data-ttu-id="36902-331">| Miara countdistinct(Computer) według typu</span><span class="sxs-lookup"><span data-stu-id="36902-331">| measure countdistinct(Computer) by Type</span></span>

<span data-ttu-id="36902-332">Liczy unikatowe komputery raportowania dla każdego typu.</span><span class="sxs-lookup"><span data-stu-id="36902-332">Counts the number of unique computers reporting for each Type.</span></span>

<span data-ttu-id="36902-333">**Przykład 15**</span><span class="sxs-lookup"><span data-stu-id="36902-333">**Example 15**</span></span>

    * <span data-ttu-id="36902-334">| Miara countdistinct(Computer) interwał 1 godzina</span><span class="sxs-lookup"><span data-stu-id="36902-334">| measure countdistinct(Computer) Interval 1HOUR</span></span>

<span data-ttu-id="36902-335">Liczy unikatowe komputery raportowania co godzinę.</span><span class="sxs-lookup"><span data-stu-id="36902-335">Counts the number of unique computers reporting for every hour.</span></span>

<span data-ttu-id="36902-336">**Przykład 16**</span><span class="sxs-lookup"><span data-stu-id="36902-336">**Example 16**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

<span data-ttu-id="36902-337">Grupuje % czasu procesora przez komputer i zwraca średnią dla każdej godziny.</span><span class="sxs-lookup"><span data-stu-id="36902-337">Groups % Processor Time by Computer, and returns the average for every hour.</span></span>

<span data-ttu-id="36902-338">**Przykład 17**</span><span class="sxs-lookup"><span data-stu-id="36902-338">**Example 17**</span></span>

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

<span data-ttu-id="36902-339">Grupuje W3CIISLog przez metodę i zwraca maksymalny co 5 minut.</span><span class="sxs-lookup"><span data-stu-id="36902-339">Groups W3CIISLog by method, and returns the maximum for every 5 minutes.</span></span>

<span data-ttu-id="36902-340">**Przykład 18**</span><span class="sxs-lookup"><span data-stu-id="36902-340">**Example 18**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

<span data-ttu-id="36902-341">Grupuje czas procesora (%) na komputerze i zwraca, średnia, 75 percentyl maksymalne i minimalne dla każdej godziny.</span><span class="sxs-lookup"><span data-stu-id="36902-341">Groups % Processor Time by computer, and returns the minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="36902-342">**Przykład 19**</span><span class="sxs-lookup"><span data-stu-id="36902-342">**Example 19**</span></span>

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

<span data-ttu-id="36902-343">Grupuje % czasu procesora najpierw przez komputer, a następnie według nazwy wystąpienia i zwraca, średnia, 75 percentyl maksymalne i minimalne dla każdej godziny.</span><span class="sxs-lookup"><span data-stu-id="36902-343">Groups % Processor Time first by computer and then by Instance name, and returns the minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="36902-344">**Przykład 20**</span><span class="sxs-lookup"><span data-stu-id="36902-344">**Example 20**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

<span data-ttu-id="36902-345">Oblicza maksymalną na minutę dla każdego dysku operacji zapisu na dysku na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="36902-345">Calculates the maximum of disk writes per minute for every disk on your computer.</span></span>

### <a name="where"></a><span data-ttu-id="36902-346">gdzie</span><span class="sxs-lookup"><span data-stu-id="36902-346">Where</span></span>
<span data-ttu-id="36902-347">Składnia:</span><span class="sxs-lookup"><span data-stu-id="36902-347">Syntax:</span></span>

```
**where** AggregatedValue>20
```

<span data-ttu-id="36902-348">Można używać tylko po *miary* polecenie, aby dokładniej przefiltrować zagregowane powoduje, że *miary* opracowała funkcji agregacji.</span><span class="sxs-lookup"><span data-stu-id="36902-348">Can only be used after a *Measure* command to further filter the aggregated results that the *Measure* aggregation function has produced.</span></span>

<span data-ttu-id="36902-349">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="36902-349">Examples:</span></span>

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a><span data-ttu-id="36902-350">Funkcja deduplikacji</span><span class="sxs-lookup"><span data-stu-id="36902-350">Dedup</span></span>
<span data-ttu-id="36902-351">Składnia:</span><span class="sxs-lookup"><span data-stu-id="36902-351">Syntax:</span></span>

    Dedup FieldName

<span data-ttu-id="36902-352">Zwraca pierwszy dokument znaleziono dla każdej unikatowej wartości tego pola.</span><span class="sxs-lookup"><span data-stu-id="36902-352">Returns the first document found for every unique value of the given field.</span></span>

<span data-ttu-id="36902-353">Przykład:</span><span class="sxs-lookup"><span data-stu-id="36902-353">Example:</span></span>

    Type=Event | Dedup EventID | sort TimeGenerated DESC

<span data-ttu-id="36902-354">W tym przykładzie zwraca jedno zdarzenie (najnowsze zdarzenie) na identyfikator zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="36902-354">This example returns one event (the latest event) per EventID.</span></span>

### <a name="join"></a><span data-ttu-id="36902-355">Join</span><span class="sxs-lookup"><span data-stu-id="36902-355">Join</span></span>
<span data-ttu-id="36902-356">Dołącza wyniki dwa zapytania do utworzenia pojedynczy zestaw wyników.</span><span class="sxs-lookup"><span data-stu-id="36902-356">Joins the results of two queries to form a single result set.</span></span>  <span data-ttu-id="36902-357">Obsługuje wiele typów sprzężeń opisane w tabeli poniżej.</span><span class="sxs-lookup"><span data-stu-id="36902-357">Supports multiple join types described in the follow table.</span></span>

| <span data-ttu-id="36902-358">Typ sprzężenia</span><span class="sxs-lookup"><span data-stu-id="36902-358">Join type</span></span> | <span data-ttu-id="36902-359">Opis</span><span class="sxs-lookup"><span data-stu-id="36902-359">Description</span></span> |
|:--|:--|
| <span data-ttu-id="36902-360">wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="36902-360">inner</span></span> | <span data-ttu-id="36902-361">Zwraca tylko rekordów o pasującej wartości w obu zapytania.</span><span class="sxs-lookup"><span data-stu-id="36902-361">Return only records with a matching value in both queries.</span></span> |
| <span data-ttu-id="36902-362">zewnętrzne</span><span class="sxs-lookup"><span data-stu-id="36902-362">outer</span></span> | <span data-ttu-id="36902-363">Zwraca wszystkie rekordy z obu zapytań.</span><span class="sxs-lookup"><span data-stu-id="36902-363">Return all records from both queries.</span></span>  |
| <span data-ttu-id="36902-364">Po lewej</span><span class="sxs-lookup"><span data-stu-id="36902-364">left</span></span>  | <span data-ttu-id="36902-365">Zwraca wszystkie rekordy z lewym zapytań i pasujące rekordy z prawej zapytania.</span><span class="sxs-lookup"><span data-stu-id="36902-365">Return all records from left query and matching records from right query.</span></span> |


- <span data-ttu-id="36902-366">Sprzężenia nie obsługują aktualnie zapytań, które obejmują **IN** — słowo kluczowe, **miary** polecenia lub **Rozszerz** polecenia, jeśli elementem docelowym pola z prawej kwerendy.</span><span class="sxs-lookup"><span data-stu-id="36902-366">Joins do not currently support queries that include the **IN** keyword, the **Measure** command or the **Extend** command if it targets a field from the right query.</span></span>
- <span data-ttu-id="36902-367">Obecnie można uwzględnić tylko jedno pole sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="36902-367">You can currently include only a single field in a join.</span></span>
- <span data-ttu-id="36902-368">Pojedynczy wyszukiwania nie może zawierać więcej niż jedno połączenie.</span><span class="sxs-lookup"><span data-stu-id="36902-368">A single search may not include more than one join.</span></span>

<span data-ttu-id="36902-369">**Składnia**</span><span class="sxs-lookup"><span data-stu-id="36902-369">**Syntax**</span></span>

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

<span data-ttu-id="36902-370">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="36902-370">**Examples**</span></span>

<span data-ttu-id="36902-371">Aby zilustrować typów sprzężeń innego, należy rozważyć dołączenie typu danych zbieranych z dziennik niestandardowy o nazwie MyBackup_CL z pulsu dla każdego komputera.</span><span class="sxs-lookup"><span data-stu-id="36902-371">To illustrate the different join types, consider joining a data type collected from a custom log called MyBackup_CL with the heartbeat for each computer.</span></span>  <span data-ttu-id="36902-372">Te typy danych mają następujące dane.</span><span class="sxs-lookup"><span data-stu-id="36902-372">These datatypes have the following data.</span></span>

`Type = MyBackup_CL`

| <span data-ttu-id="36902-373">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="36902-373">TimeGenerated</span></span> | <span data-ttu-id="36902-374">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="36902-374">Computer</span></span> | <span data-ttu-id="36902-375">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="36902-375">LastBackupStatus</span></span> |
|:---|:---|:---|
| <span data-ttu-id="36902-376">2017-4/20 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="36902-376">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="36902-377">SRV01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-377">srv01.contoso.com</span></span> | <span data-ttu-id="36902-378">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="36902-378">Success</span></span> |
| <span data-ttu-id="36902-379">2017-4/20 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="36902-379">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="36902-380">SRV02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-380">srv02.contoso.com</span></span> | <span data-ttu-id="36902-381">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="36902-381">Success</span></span> |
| <span data-ttu-id="36902-382">2017-4/20 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="36902-382">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="36902-383">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-383">srv03.contoso.com</span></span> | <span data-ttu-id="36902-384">Niepowodzenie</span><span class="sxs-lookup"><span data-stu-id="36902-384">Failure</span></span> |

<span data-ttu-id="36902-385">`Type = Hearbeat`(Tylko podzestaw pokazane pola)</span><span class="sxs-lookup"><span data-stu-id="36902-385">`Type = Hearbeat` (Only a subset of fields shown)</span></span>

| <span data-ttu-id="36902-386">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="36902-386">TimeGenerated</span></span> | <span data-ttu-id="36902-387">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="36902-387">Computer</span></span> | <span data-ttu-id="36902-388">ComputerIP</span><span class="sxs-lookup"><span data-stu-id="36902-388">ComputerIP</span></span> |
|:---|:---|:---|
| <span data-ttu-id="36902-389">2017-4/21 12:01:34.482 PM.</span><span class="sxs-lookup"><span data-stu-id="36902-389">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="36902-390">SRV01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-390">srv01.contoso.com</span></span> | <span data-ttu-id="36902-391">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="36902-391">10.10.100.1</span></span> |
| <span data-ttu-id="36902-392">2017-4/21 12:02:21.916 PM.</span><span class="sxs-lookup"><span data-stu-id="36902-392">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="36902-393">SRV02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-393">srv02.contoso.com</span></span> | <span data-ttu-id="36902-394">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="36902-394">10.10.100.2</span></span> |
| <span data-ttu-id="36902-395">2017-4/21 12:01:47.373 PM.</span><span class="sxs-lookup"><span data-stu-id="36902-395">4/21/2017 12:01:47.373 PM</span></span> | <span data-ttu-id="36902-396">srv04.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-396">srv04.contoso.com</span></span> | <span data-ttu-id="36902-397">10.10.100.4</span><span class="sxs-lookup"><span data-stu-id="36902-397">10.10.100.4</span></span> |

#### <a name="inner-join"></a><span data-ttu-id="36902-398">sprzężenie wewnętrzne</span><span class="sxs-lookup"><span data-stu-id="36902-398">inner join</span></span>

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

<span data-ttu-id="36902-399">Zwraca następujące rekordy, jeśli pole komputera odpowiada dla obu typów danych.</span><span class="sxs-lookup"><span data-stu-id="36902-399">Returns the following records where the computer field matches for both datatypes.</span></span>

| <span data-ttu-id="36902-400">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="36902-400">Computer</span></span>| <span data-ttu-id="36902-401">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="36902-401">TimeGenerated</span></span> | <span data-ttu-id="36902-402">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="36902-402">LastBackupStatus</span></span> | <span data-ttu-id="36902-403">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="36902-403">TimeGenerated_joined</span></span> | <span data-ttu-id="36902-404">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="36902-404">ComputerIP_joined</span></span> | <span data-ttu-id="36902-405">Type_joined</span><span class="sxs-lookup"><span data-stu-id="36902-405">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="36902-406">SRV01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-406">srv01.contoso.com</span></span> | <span data-ttu-id="36902-407">2017-4/20 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="36902-407">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="36902-408">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="36902-408">Success</span></span> | <span data-ttu-id="36902-409">2017-4/21 12:01:34.482 PM.</span><span class="sxs-lookup"><span data-stu-id="36902-409">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="36902-410">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="36902-410">10.10.100.1</span></span> | <span data-ttu-id="36902-411">Pulsu</span><span class="sxs-lookup"><span data-stu-id="36902-411">Heartbeat</span></span> |
| <span data-ttu-id="36902-412">SRV02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-412">srv02.contoso.com</span></span> | <span data-ttu-id="36902-413">2017-4/20 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="36902-413">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="36902-414">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="36902-414">Success</span></span> | <span data-ttu-id="36902-415">2017-4/21 12:02:21.916 PM.</span><span class="sxs-lookup"><span data-stu-id="36902-415">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="36902-416">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="36902-416">10.10.100.2</span></span> | <span data-ttu-id="36902-417">Pulsu</span><span class="sxs-lookup"><span data-stu-id="36902-417">Heartbeat</span></span> |


#### <a name="outer-join"></a><span data-ttu-id="36902-418">sprzężenie zewnętrzne</span><span class="sxs-lookup"><span data-stu-id="36902-418">outer join</span></span>

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

<span data-ttu-id="36902-419">Zwraca następujące rekordy dla obu typów danych.</span><span class="sxs-lookup"><span data-stu-id="36902-419">Returns the following records for both datatypes.</span></span>

| <span data-ttu-id="36902-420">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="36902-420">Computer</span></span>| <span data-ttu-id="36902-421">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="36902-421">TimeGenerated</span></span> | <span data-ttu-id="36902-422">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="36902-422">LastBackupStatus</span></span> | <span data-ttu-id="36902-423">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="36902-423">TimeGenerated_joined</span></span> | <span data-ttu-id="36902-424">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="36902-424">ComputerIP_joined</span></span> | <span data-ttu-id="36902-425">Type_joined</span><span class="sxs-lookup"><span data-stu-id="36902-425">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="36902-426">SRV01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-426">srv01.contoso.com</span></span> | <span data-ttu-id="36902-427">2017-4/20 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="36902-427">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="36902-428">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="36902-428">Success</span></span>  | <span data-ttu-id="36902-429">2017-4/21 12:01:34.482 PM.</span><span class="sxs-lookup"><span data-stu-id="36902-429">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="36902-430">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="36902-430">10.10.100.1</span></span> | <span data-ttu-id="36902-431">Pulsu</span><span class="sxs-lookup"><span data-stu-id="36902-431">Heartbeat</span></span> |
| <span data-ttu-id="36902-432">SRV02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-432">srv02.contoso.com</span></span> | <span data-ttu-id="36902-433">2017-4/20 02:14:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="36902-433">4/20/2017 02:14:12.381 AM</span></span> | <span data-ttu-id="36902-434">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="36902-434">Success</span></span>  | <span data-ttu-id="36902-435">2017-4/21 12:02:21.916 PM.</span><span class="sxs-lookup"><span data-stu-id="36902-435">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="36902-436">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="36902-436">10.10.100.2</span></span> | <span data-ttu-id="36902-437">Pulsu</span><span class="sxs-lookup"><span data-stu-id="36902-437">Heartbeat</span></span> |
| <span data-ttu-id="36902-438">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-438">srv03.contoso.com</span></span> | <span data-ttu-id="36902-439">2017-4/20 01:33:35.974 AM</span><span class="sxs-lookup"><span data-stu-id="36902-439">4/20/2017 01:33:35.974 AM</span></span> | <span data-ttu-id="36902-440">Niepowodzenie</span><span class="sxs-lookup"><span data-stu-id="36902-440">Failure</span></span>  | <span data-ttu-id="36902-441">2017-4/21 12:01:47.373 PM.</span><span class="sxs-lookup"><span data-stu-id="36902-441">4/21/2017 12:01:47.373 PM</span></span> | | |
| <span data-ttu-id="36902-442">srv04.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-442">srv04.contoso.com</span></span> |                           |          | <span data-ttu-id="36902-443">2017-4/21 12:01:47.373 PM.</span><span class="sxs-lookup"><span data-stu-id="36902-443">4/21/2017 12:01:47.373 PM</span></span> | <span data-ttu-id="36902-444">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="36902-444">10.10.100.2</span></span> | <span data-ttu-id="36902-445">Pulsu</span><span class="sxs-lookup"><span data-stu-id="36902-445">Heartbeat</span></span> |



#### <a name="left-join"></a><span data-ttu-id="36902-446">Lewe sprzężenie</span><span class="sxs-lookup"><span data-stu-id="36902-446">left join</span></span>

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

<span data-ttu-id="36902-447">Zwraca następujące rekordy z MyBackup_CL żadnych pól zgodnych z pulsu.</span><span class="sxs-lookup"><span data-stu-id="36902-447">Returns the following records from MyBackup_CL with any matching fields from Heartbeat.</span></span>

| <span data-ttu-id="36902-448">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="36902-448">Computer</span></span>| <span data-ttu-id="36902-449">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="36902-449">TimeGenerated</span></span> | <span data-ttu-id="36902-450">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="36902-450">LastBackupStatus</span></span> | <span data-ttu-id="36902-451">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="36902-451">TimeGenerated_joined</span></span> | <span data-ttu-id="36902-452">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="36902-452">ComputerIP_joined</span></span> | <span data-ttu-id="36902-453">Type_joined</span><span class="sxs-lookup"><span data-stu-id="36902-453">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="36902-454">SRV01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-454">srv01.contoso.com</span></span> | <span data-ttu-id="36902-455">2017-4/20 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="36902-455">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="36902-456">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="36902-456">Success</span></span> | <span data-ttu-id="36902-457">2017-4/21 12:01:34.482 PM.</span><span class="sxs-lookup"><span data-stu-id="36902-457">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="36902-458">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="36902-458">10.10.100.1</span></span> | <span data-ttu-id="36902-459">Pulsu</span><span class="sxs-lookup"><span data-stu-id="36902-459">Heartbeat</span></span> |
| <span data-ttu-id="36902-460">SRV02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-460">srv02.contoso.com</span></span> | <span data-ttu-id="36902-461">2017-4/20 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="36902-461">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="36902-462">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="36902-462">Success</span></span> | <span data-ttu-id="36902-463">2017-4/21 12:02:21.916 PM.</span><span class="sxs-lookup"><span data-stu-id="36902-463">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="36902-464">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="36902-464">10.10.100.2</span></span> | <span data-ttu-id="36902-465">Pulsu</span><span class="sxs-lookup"><span data-stu-id="36902-465">Heartbeat</span></span> |
| <span data-ttu-id="36902-466">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="36902-466">srv03.contoso.com</span></span> | <span data-ttu-id="36902-467">2017-4/20 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="36902-467">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="36902-468">Niepowodzenie</span><span class="sxs-lookup"><span data-stu-id="36902-468">Failure</span></span> | | | |


### <a name="extend"></a><span data-ttu-id="36902-469">Rozszerzanie</span><span class="sxs-lookup"><span data-stu-id="36902-469">Extend</span></span>
<span data-ttu-id="36902-470">Służy do tworzenia środowiska wykonawczego pola w zapytaniach.</span><span class="sxs-lookup"><span data-stu-id="36902-470">Allows you to create run-time fields in queries.</span></span> <span data-ttu-id="36902-471">Należy pamiętać, że czasu wykonywania nie można używać pól przy użyciu polecenia miary do wykonania agregacji.</span><span class="sxs-lookup"><span data-stu-id="36902-471">Note that run-time fields cannot be used with the measure command to perform aggregation.</span></span>

<span data-ttu-id="36902-472">**Przykład 1**</span><span class="sxs-lookup"><span data-stu-id="36902-472">**Example 1**</span></span>

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
<span data-ttu-id="36902-473">Pokazuje ważone wynik zalecenie zalecenia SQL do oceny.</span><span class="sxs-lookup"><span data-stu-id="36902-473">Shows weighted recommendation score for SQL Assessment recommendations.</span></span>

<span data-ttu-id="36902-474">**Przykład 2**</span><span class="sxs-lookup"><span data-stu-id="36902-474">**Example 2**</span></span>

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
<span data-ttu-id="36902-475">Zawiera wartość licznika w KB/s, zamiast bajtów.</span><span class="sxs-lookup"><span data-stu-id="36902-475">Shows counter value in KBs instead of bytes.</span></span>

<span data-ttu-id="36902-476">**Przykład 3**</span><span class="sxs-lookup"><span data-stu-id="36902-476">**Example 3**</span></span>

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
<span data-ttu-id="36902-477">Skaluje wartość WireData TotalBytes w taki sposób, że wszystkie wyniki należą do zakresu od 0 do 100.</span><span class="sxs-lookup"><span data-stu-id="36902-477">Scales the value of WireData TotalBytes, such that all results are between 0 and 100.</span></span>

<span data-ttu-id="36902-478">**Przykład 4**</span><span class="sxs-lookup"><span data-stu-id="36902-478">**Example 4**</span></span>

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
<span data-ttu-id="36902-479">Znaczniki wartości liczników wydajności mniej niż 50 procent jako niski, a inne jako wysoki.</span><span class="sxs-lookup"><span data-stu-id="36902-479">Tags Perf Counter Values less than 50 percent as LOW, and others as HIGH.</span></span>

<span data-ttu-id="36902-480">**Przykład 5**</span><span class="sxs-lookup"><span data-stu-id="36902-480">**Example 5**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
<span data-ttu-id="36902-481">Oblicza maksymalną na minutę dla każdego dysku operacji zapisu na dysku na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="36902-481">Calculates the maximum of disk writes per minute for every disk on your computer.</span></span>

<span data-ttu-id="36902-482">**Obsługiwane funkcje**</span><span class="sxs-lookup"><span data-stu-id="36902-482">**Supported functions**</span></span>

| <span data-ttu-id="36902-483">Funkcja</span><span class="sxs-lookup"><span data-stu-id="36902-483">Function</span></span> | <span data-ttu-id="36902-484">Opis</span><span class="sxs-lookup"><span data-stu-id="36902-484">Description</span></span> | <span data-ttu-id="36902-485">Przykłady składni</span><span class="sxs-lookup"><span data-stu-id="36902-485">Syntax examples</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36902-486">ABS</span><span class="sxs-lookup"><span data-stu-id="36902-486">abs</span></span> |<span data-ttu-id="36902-487">Zwraca wartość bezwzględną liczby określonej wartości lub funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-487">Returns the absolute value of the specified value or function.</span></span> |`abs(x)` <br> `abs(-5)` |
| <span data-ttu-id="36902-488">ACOS</span><span class="sxs-lookup"><span data-stu-id="36902-488">acos</span></span> |<span data-ttu-id="36902-489">Zwraca arcus cosinus wartości lub funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-489">Returns arc cosine of a value or a function.</span></span> |`acos(x)` |
| <span data-ttu-id="36902-490">i</span><span class="sxs-lookup"><span data-stu-id="36902-490">and</span></span> |<span data-ttu-id="36902-491">Zwraca wartość true tylko wtedy, gdy wszystkich argumentów zwrócić wartość true.</span><span class="sxs-lookup"><span data-stu-id="36902-491">Returns a value of true if and only if all of its operands evaluate to true.</span></span> |`and(not(exists(popularity)),exists(price))` |
| <span data-ttu-id="36902-492">ASIN</span><span class="sxs-lookup"><span data-stu-id="36902-492">asin</span></span> |<span data-ttu-id="36902-493">Zwraca arcus sinus wartości lub funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-493">Returns arc sine of a value or a function.</span></span> |`asin(x)` |
| <span data-ttu-id="36902-494">ATAN</span><span class="sxs-lookup"><span data-stu-id="36902-494">atan</span></span> |<span data-ttu-id="36902-495">Zwraca arcus tangens wartości lub funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-495">Returns arc tangent of a value or a function.</span></span> |`atan(x)` |
| <span data-ttu-id="36902-496">ATAN2</span><span class="sxs-lookup"><span data-stu-id="36902-496">atan2</span></span> |<span data-ttu-id="36902-497">Zwraca kąt, wynikające z konwersję prostokątna współrzędne x, y na Współrzędne biegunowe.</span><span class="sxs-lookup"><span data-stu-id="36902-497">Returns the angle resulting from the conversion of the rectangular coordinates x,y to polar coordinates.</span></span> |`atan2(x,y)` |
| <span data-ttu-id="36902-498">cbrt —</span><span class="sxs-lookup"><span data-stu-id="36902-498">cbrt</span></span> |<span data-ttu-id="36902-499">Główny moduł.</span><span class="sxs-lookup"><span data-stu-id="36902-499">Cube root.</span></span> |`cbrt(x)` |
| <span data-ttu-id="36902-500">ceil</span><span class="sxs-lookup"><span data-stu-id="36902-500">ceil</span></span> |<span data-ttu-id="36902-501">Zaokrągla w górę do liczby całkowitej.</span><span class="sxs-lookup"><span data-stu-id="36902-501">Rounds up to an integer.</span></span> |`ceil(x)`  <br> <span data-ttu-id="36902-502">`ceil(5.6)`Zwraca 6</span><span class="sxs-lookup"><span data-stu-id="36902-502">`ceil(5.6)` Returns 6</span></span> |
| <span data-ttu-id="36902-503">COS</span><span class="sxs-lookup"><span data-stu-id="36902-503">cos</span></span> |<span data-ttu-id="36902-504">Zwraca cosinus kąta.</span><span class="sxs-lookup"><span data-stu-id="36902-504">Returns cosine of an angle.</span></span> |`cos(x)` |
| <span data-ttu-id="36902-505">COSH</span><span class="sxs-lookup"><span data-stu-id="36902-505">cosh</span></span> |<span data-ttu-id="36902-506">Zwraca cosinus hiperboliczny kąta.</span><span class="sxs-lookup"><span data-stu-id="36902-506">Returns hyperbolic cosine of an angle.</span></span> |`cosh(x)` |
| <span data-ttu-id="36902-507">DEF</span><span class="sxs-lookup"><span data-stu-id="36902-507">def</span></span> |<span data-ttu-id="36902-508">Skrót dla domyślnego.</span><span class="sxs-lookup"><span data-stu-id="36902-508">Abbreviation for default.</span></span> <span data-ttu-id="36902-509">Zwraca wartość "pola".</span><span class="sxs-lookup"><span data-stu-id="36902-509">Returns the value of field "field".</span></span> <span data-ttu-id="36902-510">Jeśli pole nie istnieje, zwraca wartość domyślna określona i zwraca pierwszą wartość gdzie: `exists()==true`.</span><span class="sxs-lookup"><span data-stu-id="36902-510">If the field does not exist, returns the default value specified and yields the first value where: `exists()==true`.</span></span> |<span data-ttu-id="36902-511">`def(rating,5)`.</span><span class="sxs-lookup"><span data-stu-id="36902-511">`def(rating,5)`.</span></span> <span data-ttu-id="36902-512">Ta funkcja def() zwraca klasyfikacji lub jeśli klasyfikacji nie określono dokumentu, zwraca 5.</span><span class="sxs-lookup"><span data-stu-id="36902-512">This def() function returns the rating, or if no rating is specified in the document, returns 5.</span></span> <br> <span data-ttu-id="36902-513">`def(myfield, 1.0)`jest odpowiednikiem `if(exists(myfield),myfield,1.0)`.</span><span class="sxs-lookup"><span data-stu-id="36902-513">`def(myfield, 1.0)` is equivalent to `if(exists(myfield),myfield,1.0)`.</span></span> |
| <span data-ttu-id="36902-514">stopni</span><span class="sxs-lookup"><span data-stu-id="36902-514">deg</span></span> |<span data-ttu-id="36902-515">Konwertuje wartość w radianach stopni.</span><span class="sxs-lookup"><span data-stu-id="36902-515">Converts radians to degrees.</span></span> |`deg(x)` |
| <span data-ttu-id="36902-516">DIV</span><span class="sxs-lookup"><span data-stu-id="36902-516">div</span></span> |<span data-ttu-id="36902-517">`div(x,y)`dzieli x przez y.</span><span class="sxs-lookup"><span data-stu-id="36902-517">`div(x,y)` divides x by y.</span></span> |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| <span data-ttu-id="36902-518">dystr.</span><span class="sxs-lookup"><span data-stu-id="36902-518">dist</span></span> |<span data-ttu-id="36902-519">Zwraca odległość między dwoma wektorami, (punkty) w n wymiarowej miejsca.</span><span class="sxs-lookup"><span data-stu-id="36902-519">Returns the distance between two vectors, (points) in an n-dimensional space.</span></span> <span data-ttu-id="36902-520">Przejście w prawo, a także wystąpień ValueSource dwóch lub więcej i oblicza odległość między dwoma wektorami.</span><span class="sxs-lookup"><span data-stu-id="36902-520">Takes in the power, plus two or more, ValueSource instances, and calculates the distances between the two vectors.</span></span> <span data-ttu-id="36902-521">Każdy ValueSource musi być liczbą.</span><span class="sxs-lookup"><span data-stu-id="36902-521">Each ValueSource must be a number.</span></span> <span data-ttu-id="36902-522">Musi być parzystą liczbą wystąpień ValueSource przekazano, a metoda przyjęto założenie, że pierwszej połowy reprezentują wektor pierwszej i drugiej połowie reprezentują wektor drugiego.</span><span class="sxs-lookup"><span data-stu-id="36902-522">There must be an even number of ValueSource instances passed in, and the method assumes that the first half represent the first vector and the second half represent the second vector.</span></span> |<span data-ttu-id="36902-523">`dist(2, x, y, 0, 0)`Oblicza odległość euklidesowa między (0,0) i (x, y) dla każdego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="36902-523">`dist(2, x, y, 0, 0)` Calculates the Euclidean distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="36902-524">`dist(1, x, y, 0, 0)`Oblicza odległość Manhattan (taxicab) między (0,0) i (x, y) dla każdego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="36902-524">`dist(1, x, y, 0, 0)` Calculates the Manhattan (taxicab) distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="36902-525">`dist(2,,x,y,z,0,0,0)`Euklidesowa odległość między (0,0,0) i (x, y, z) dla każdego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="36902-525">`dist(2,,x,y,z,0,0,0)` Euclidean distance between (0,0,0) and (x,y,z) for each document.</span></span><br><span data-ttu-id="36902-526">`dist(1,x,y,z,e,f,g)`Manhattan odległość między (x, y, z) i (e, f, g), gdzie każda litera jest nazwą pola.</span><span class="sxs-lookup"><span data-stu-id="36902-526">`dist(1,x,y,z,e,f,g)` Manhattan distance between (x,y,z) and (e,f,g), where each letter is a field name.</span></span> |
| <span data-ttu-id="36902-527">istnieje</span><span class="sxs-lookup"><span data-stu-id="36902-527">exists</span></span> |<span data-ttu-id="36902-528">Zwraca wartość TRUE, jeśli element członkowski pola istnieje.</span><span class="sxs-lookup"><span data-stu-id="36902-528">Returns TRUE if any member of the field exists.</span></span> |<span data-ttu-id="36902-529">`exists(author)`Zwraca wartość TRUE dla każdego dokumentu, który ma wartość w polu "Autor".</span><span class="sxs-lookup"><span data-stu-id="36902-529">`exists(author)` Returns TRUE for any document that has a value in the "author" field.</span></span><br><span data-ttu-id="36902-530">`exists(query(price:5.00))`Zwraca wartość TRUE, jeśli pasuje do "cena", "5.00".</span><span class="sxs-lookup"><span data-stu-id="36902-530">`exists(query(price:5.00))` Returns TRUE if "price" matches,"5.00".</span></span> |
| <span data-ttu-id="36902-531">EXP</span><span class="sxs-lookup"><span data-stu-id="36902-531">exp</span></span> |<span data-ttu-id="36902-532">Zwraca liczbę firmy Eulera podniesione do potęgi x.</span><span class="sxs-lookup"><span data-stu-id="36902-532">Returns Euler's number raised to power x.</span></span> |`exp(x)` |
| <span data-ttu-id="36902-533">FLOOR</span><span class="sxs-lookup"><span data-stu-id="36902-533">floor</span></span> |<span data-ttu-id="36902-534">Zaokrągla liczbę w dół do liczby całkowitej.</span><span class="sxs-lookup"><span data-stu-id="36902-534">Rounds down to an integer.</span></span> |`floor(x)`  <br> <span data-ttu-id="36902-535">`floor(5.6)`Zwraca 5</span><span class="sxs-lookup"><span data-stu-id="36902-535">`floor(5.6)` Returns 5</span></span> |
| <span data-ttu-id="36902-536">hypo</span><span class="sxs-lookup"><span data-stu-id="36902-536">hypo</span></span> |<span data-ttu-id="36902-537">Zwraca sqrt(sum(pow(x,2),pow(y,2))) bez pośredniego przepełnienie lub niedomiar.</span><span class="sxs-lookup"><span data-stu-id="36902-537">Returns sqrt(sum(pow(x,2),pow(y,2))) without intermediate overflow or underflow.</span></span> |`hypo(x,y)`  <br> ` |
| <span data-ttu-id="36902-538">Jeśli</span><span class="sxs-lookup"><span data-stu-id="36902-538">if</span></span> |<span data-ttu-id="36902-539">Umożliwia funkcja warunkowy zapytania.</span><span class="sxs-lookup"><span data-stu-id="36902-539">Enables conditional function queries.</span></span> <span data-ttu-id="36902-540">W `if(test,value1,value2)`, test jest lub odwołuje się do wartość logiczna lub wyrażenie, które zwraca wartość logiczną (TRUE lub FALSE).</span><span class="sxs-lookup"><span data-stu-id="36902-540">In `if(test,value1,value2)`, test is or refers to a logical value or expression that returns a logical value (TRUE or FALSE).</span></span> <span data-ttu-id="36902-541">`value1`jest zwracana wartość przez funkcję Jeśli test zwraca wartość TRUE.</span><span class="sxs-lookup"><span data-stu-id="36902-541">`value1` is the value returned by the function if test yields TRUE.</span></span> <span data-ttu-id="36902-542">`value2`jest zwracana wartość przez funkcję Jeśli test zwraca wartość FALSE.</span><span class="sxs-lookup"><span data-stu-id="36902-542">`value2` is the value returned by the function if test yields FALSE.</span></span> <span data-ttu-id="36902-543">Wyrażenie może być dowolnej funkcji, które generuje wartości logiczne.</span><span class="sxs-lookup"><span data-stu-id="36902-543">An expression can be any function which outputs boolean values.</span></span> <span data-ttu-id="36902-544">Można także funkcji zwracającej wartości liczbowe, w których wielkość wartość 0 jest interpretowana jako wartość false lub w których wielkość pustego ciągu zwracanie ciągów, jest interpretowany jako FAŁSZ.</span><span class="sxs-lookup"><span data-stu-id="36902-544">It can also be a function returning numeric values, in which case value 0 is interpreted as false, or returning strings, in which case empty string is interpreted as false.</span></span> |<span data-ttu-id="36902-545">`if(termfreq(cat,'electronics'),popularity,42)`Ta funkcja sprawdza każdego dokumentu, aby zobaczyć, czy zawiera termin "electronics" w polu cat.</span><span class="sxs-lookup"><span data-stu-id="36902-545">`if(termfreq(cat,'electronics'),popularity,42)` This function checks each document to see if it contains the term "electronics" in the cat field.</span></span> <span data-ttu-id="36902-546">Jeśli tak, jest zwracana wartość pola popularność.</span><span class="sxs-lookup"><span data-stu-id="36902-546">If it does, then the value of the popularity field is returned.</span></span> <span data-ttu-id="36902-547">W przeciwnym razie jest zwracana wartość 42.</span><span class="sxs-lookup"><span data-stu-id="36902-547">Otherwise, the value of 42 is returned.</span></span> |
| <span data-ttu-id="36902-548">liniowy</span><span class="sxs-lookup"><span data-stu-id="36902-548">linear</span></span> |<span data-ttu-id="36902-549">Implementuje `m*x+c`, gdzie m i c są stałe i x jest dowolną funkcją.</span><span class="sxs-lookup"><span data-stu-id="36902-549">Implements `m*x+c`, where m and c are constants, and x is an arbitrary function.</span></span> <span data-ttu-id="36902-550">Jest to równoważne `sum(product(m,x),c)`, ale nieco bardziej wydajne zaimplementowanego jako jednej funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-550">This is equivalent to `sum(product(m,x),c)`, but slightly more efficient as it is implemented as a single function.</span></span> |<span data-ttu-id="36902-551">`linear(x,m,c) linear(x,2,4)`Zwraca`2*x+4`</span><span class="sxs-lookup"><span data-stu-id="36902-551">`linear(x,m,c) linear(x,2,4)` returns `2*x+4`</span></span> |
| <span data-ttu-id="36902-552">ln</span><span class="sxs-lookup"><span data-stu-id="36902-552">ln</span></span> |<span data-ttu-id="36902-553">Zwraca logarytm naturalny określonej funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-553">Returns the natural log of the specified function.</span></span> |`ln(x)` |
| <span data-ttu-id="36902-554">Dziennik</span><span class="sxs-lookup"><span data-stu-id="36902-554">log</span></span> |<span data-ttu-id="36902-555">Zwraca dziennik określona funkcja o podstawie 10.</span><span class="sxs-lookup"><span data-stu-id="36902-555">Returns the log base 10 of the specified function.</span></span> |`log(x)   log(sum(x,100))` |
| <span data-ttu-id="36902-556">mapy</span><span class="sxs-lookup"><span data-stu-id="36902-556">map</span></span> |<span data-ttu-id="36902-557">Mapuje wartości wejściowe funkcji x, spełniających kryteria min i max, włącznie z określoną docelową.</span><span class="sxs-lookup"><span data-stu-id="36902-557">Maps any values of an input function x that fall within min and max, inclusive to the specified target.</span></span> <span data-ttu-id="36902-558">Argumenty min i max muszą być stałymi.</span><span class="sxs-lookup"><span data-stu-id="36902-558">The arguments min and max must be constants.</span></span> <span data-ttu-id="36902-559">Docelowy argumentów i domyślne może być stałe lub funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-559">The arguments target and default can be constants or functions.</span></span> <span data-ttu-id="36902-560">Jeśli wartość x nie należy do zakresu od min i max, następnie jest zwracana wartość x albo domyślną wartość zwracana, gdy określona jako 5. argument.</span><span class="sxs-lookup"><span data-stu-id="36902-560">If the value of x does not fall between min and max, then either the value of x is returned, or a default value is returned if specified as a 5th argument.</span></span> |<span data-ttu-id="36902-561">`map(x,min,max,target) map(x,0,0,1)`Zmienia wartości 0 lub 1.</span><span class="sxs-lookup"><span data-stu-id="36902-561">`map(x,min,max,target) map(x,0,0,1)` Changes any values of 0 to 1.</span></span> <span data-ttu-id="36902-562">Może to być przydatne podczas obsługi wartości domyślnej 0.</span><span class="sxs-lookup"><span data-stu-id="36902-562">This can be useful in handling default 0 values.</span></span><br> <span data-ttu-id="36902-563">`map(x,min,max,target,default)    map(x,0,100,1,-1)`Zmiany wartości zakresu od 0 do 1 do 100, a wszystkie inne wartości -1.</span><span class="sxs-lookup"><span data-stu-id="36902-563">`map(x,min,max,target,default)    map(x,0,100,1,-1)` Changes any values between 0 and 100 to 1, and all other values to -1.</span></span><br>  <span data-ttu-id="36902-564">`map(x,0,100,sum(x,599),docfreq(text,solr))`Zmiany wartości od 0 do 100 x + 599 oraz innych wartości częstotliwości termin "solr, w polu tekst.</span><span class="sxs-lookup"><span data-stu-id="36902-564">`map(x,0,100,sum(x,599),docfreq(text,solr))` Changes any values between 0 and 100 to x+599, and all other values to frequency of the term 'solr' in the field text.</span></span> |
| <span data-ttu-id="36902-565">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="36902-565">max</span></span> |<span data-ttu-id="36902-566">Zwraca maksymalną wartość liczbową wielu zagnieżdżonych funkcji lub stałe, które są określane jako argumenty: `max(x,y,...)`.</span><span class="sxs-lookup"><span data-stu-id="36902-566">Returns the maximum numeric value of multiple nested functions or constants, which are specified as arguments: `max(x,y,...)`.</span></span> <span data-ttu-id="36902-567">Max — funkcja może być przydatne przy "bottoming out" innej funkcji lub pola dla niektórych określone stała.</span><span class="sxs-lookup"><span data-stu-id="36902-567">The max function can also be useful for "bottoming out" another function or field at some specified constant.</span></span>  <span data-ttu-id="36902-568">Użyj `field(myfield,max)` składni wybierania maksymalną wartość jednego pola wielowartościowe.</span><span class="sxs-lookup"><span data-stu-id="36902-568">Use the `field(myfield,max)` syntax for selecting the maximum value of a single multivalued field.</span></span> |`max(myfield,myotherfield,0)` |
| <span data-ttu-id="36902-569">min.</span><span class="sxs-lookup"><span data-stu-id="36902-569">min</span></span> |<span data-ttu-id="36902-570">Zwraca minimalną wartość liczbową wiele funkcji zagnieżdżonych stałych, które są określane jako argumenty: `min(x,y,...)`.</span><span class="sxs-lookup"><span data-stu-id="36902-570">Returns the minimum numeric value of multiple nested functions of constants, which are specified as arguments: `min(x,y,...)`.</span></span> <span data-ttu-id="36902-571">Można też używany w celu tworzenia "górna granica" dla funkcji przy użyciu stałej funkcji min.</span><span class="sxs-lookup"><span data-stu-id="36902-571">The min function can also be useful for providing an "upper bound" on a function using a constant.</span></span> <span data-ttu-id="36902-572">Użyj `field(myfield,min)` składni wybierania minimalną wartość jednego pola wielowartościowe.</span><span class="sxs-lookup"><span data-stu-id="36902-572">Use the `field(myfield,min)` syntax for selecting the minimum value of a single multivalued field.</span></span> |`min(myfield,myotherfield,0)` |
| <span data-ttu-id="36902-573">mod</span><span class="sxs-lookup"><span data-stu-id="36902-573">mod</span></span> |<span data-ttu-id="36902-574">Oblicza resztę funkcja x t funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-574">Computes the modulus of the function x by the function y.</span></span> |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| <span data-ttu-id="36902-575">MS</span><span class="sxs-lookup"><span data-stu-id="36902-575">ms</span></span> |<span data-ttu-id="36902-576">Zwraca milisekund różnica między argumenty.</span><span class="sxs-lookup"><span data-stu-id="36902-576">Returns milliseconds of difference between its arguments.</span></span> <span data-ttu-id="36902-577">Daty są względem systemu Unix lub POSIX epoki czasu, północy, 1 stycznia 1970 UTC.</span><span class="sxs-lookup"><span data-stu-id="36902-577">Dates are relative to the Unix or POSIX time epoch, midnight, January 1, 1970 UTC.</span></span> <span data-ttu-id="36902-578">Argumenty może być nazwa indeksowanego TrieDateField lub matematyczne daty na podstawie daty stałej lub teraz.</span><span class="sxs-lookup"><span data-stu-id="36902-578">Arguments may be the name of an indexed TrieDateField, or date math based on a constant date or NOW .</span></span> <span data-ttu-id="36902-579">`ms()`jest odpowiednikiem `ms(NOW)`, liczba milisekund od epoka.</span><span class="sxs-lookup"><span data-stu-id="36902-579">`ms()` is equivalent to `ms(NOW)`, number of milliseconds since the epoch.</span></span> <span data-ttu-id="36902-580">`ms(a)`Zwraca liczbę milisekund od epoka reprezentujący argument.</span><span class="sxs-lookup"><span data-stu-id="36902-580">`ms(a)` returns the number of milliseconds since the epoch that the argument represents.</span></span> <span data-ttu-id="36902-581">`ms(a,b)`Zwraca liczbę milisekund, że b występuje przed, która jest `a - b`.</span><span class="sxs-lookup"><span data-stu-id="36902-581">`ms(a,b)` returns the number of milliseconds that b occurs before a, which is `a - b`.</span></span> |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| <span data-ttu-id="36902-582">nie</span><span class="sxs-lookup"><span data-stu-id="36902-582">not</span></span> |<span data-ttu-id="36902-583">Logicznie zanegowaną wartość opakowana funkcja.</span><span class="sxs-lookup"><span data-stu-id="36902-583">The logically negated value of the wrapped function.</span></span> |<span data-ttu-id="36902-584">`not(exists(author))`Wartość TRUE tylko wtedy, gdy `exists(author)` ma wartość false.</span><span class="sxs-lookup"><span data-stu-id="36902-584">`not(exists(author))` TRUE only when `exists(author)` is false.</span></span> |
| <span data-ttu-id="36902-585">lub</span><span class="sxs-lookup"><span data-stu-id="36902-585">or</span></span> |<span data-ttu-id="36902-586">Rozłączenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="36902-586">A logical disjunction.</span></span> |<span data-ttu-id="36902-587">`or(value1,value2)`Wartość TRUE, jeśli wartość1 lub wartość2 ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="36902-587">`or(value1,value2)` TRUE if either value1 or value2 is true.</span></span> |
| <span data-ttu-id="36902-588">Pow</span><span class="sxs-lookup"><span data-stu-id="36902-588">pow</span></span> |<span data-ttu-id="36902-589">Uruchamia określony podstawowy do określonej potęgi.</span><span class="sxs-lookup"><span data-stu-id="36902-589">Raises the specified base to the specified power.</span></span> <span data-ttu-id="36902-590">`pow(x,y)`zgłasza x do potęgi y.</span><span class="sxs-lookup"><span data-stu-id="36902-590">`pow(x,y)` raises x to the power of y.</span></span> |`pow(x,y)`<br>`pow(x,log(y))`<br><span data-ttu-id="36902-591">`pow(x,0.5)`Taki sam jak sqrt.</span><span class="sxs-lookup"><span data-stu-id="36902-591">`pow(x,0.5)` The same as sqrt.</span></span> |
| <span data-ttu-id="36902-592">Produktu</span><span class="sxs-lookup"><span data-stu-id="36902-592">product</span></span> |<span data-ttu-id="36902-593">Zwraca iloczyn wiele wartości lub funkcji, które są określone w postaci listy rozdzielanej przecinkami.</span><span class="sxs-lookup"><span data-stu-id="36902-593">Returns the product of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="36902-594">`mul(...)`może także służyć jako alias dla tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-594">`mul(...)` may also be used as an alias for this function.</span></span> |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| <span data-ttu-id="36902-595">recip</span><span class="sxs-lookup"><span data-stu-id="36902-595">recip</span></span> |<span data-ttu-id="36902-596">Wykonuje funkcję wzajemnego z `recip(x,m,a,b)` implementacja `a/(m*x+b)`, gdzie m,, b są stałe i x jest dowolną funkcję arbitralnie złożonych.</span><span class="sxs-lookup"><span data-stu-id="36902-596">Performs a reciprocal function with `recip(x,m,a,b)` implementing `a/(m*x+b)`, where m, a,and b are constants, and x is any arbitrarily complex function.</span></span> <span data-ttu-id="36902-597">Gdy i b są równe i x > = 0, ta funkcja posiada maksymalną wartość 1, wyeliminować x zwiększa.</span><span class="sxs-lookup"><span data-stu-id="36902-597">When a and b are equal, and x>=0, this function has a maximum value of 1 that drops as x increases.</span></span> <span data-ttu-id="36902-598">Zwiększenie wartości i b wyników razem w przepływie całą funkcję do płaska część krzywej.</span><span class="sxs-lookup"><span data-stu-id="36902-598">Increasing the value of a and b together results in a movement of the entire function to a flatter part of the curve.</span></span> <span data-ttu-id="36902-599">Te właściwości ułatwia tę funkcję nadaje się doskonale dla zwiększania nowych dokumentów, jeśli x to `rord(datefield)`.</span><span class="sxs-lookup"><span data-stu-id="36902-599">These properties can make this an ideal function for boosting more recent documents when x is `rord(datefield)`.</span></span> |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| <span data-ttu-id="36902-600">rad</span><span class="sxs-lookup"><span data-stu-id="36902-600">rad</span></span> |<span data-ttu-id="36902-601">Konwertuje stopnie na radiany.</span><span class="sxs-lookup"><span data-stu-id="36902-601">Converts degrees to radians.</span></span> |`rad(x)` |
| <span data-ttu-id="36902-602">Drukowanie</span><span class="sxs-lookup"><span data-stu-id="36902-602">rint</span></span> |<span data-ttu-id="36902-603">Zaokrąglenie do najbliższej liczby całkowitej.</span><span class="sxs-lookup"><span data-stu-id="36902-603">Rounds to the nearest integer.</span></span> |`rint(x)`  <br> <span data-ttu-id="36902-604">`rint(5.6)`Zwraca 6</span><span class="sxs-lookup"><span data-stu-id="36902-604">`rint(5.6)` Returns 6</span></span> |
| <span data-ttu-id="36902-605">SIN</span><span class="sxs-lookup"><span data-stu-id="36902-605">sin</span></span> |<span data-ttu-id="36902-606">Zwraca sinus kąta.</span><span class="sxs-lookup"><span data-stu-id="36902-606">Returns sine of an angle.</span></span> |`sin(x)` |
| <span data-ttu-id="36902-607">SINH</span><span class="sxs-lookup"><span data-stu-id="36902-607">sinh</span></span> |<span data-ttu-id="36902-608">Zwraca sinus hiperboliczny kąta.</span><span class="sxs-lookup"><span data-stu-id="36902-608">Returns hyperbolic sine of an angle.</span></span> |`sinh(x)` |
| <span data-ttu-id="36902-609">Skali</span><span class="sxs-lookup"><span data-stu-id="36902-609">scale</span></span> |<span data-ttu-id="36902-610">Skalowanie wartości funkcji x taki sposób, że należą one między określonym minTarget i maxTarget włącznie.</span><span class="sxs-lookup"><span data-stu-id="36902-610">Scales values of the function x, such that they fall between the specified minTarget and maxTarget inclusive.</span></span> <span data-ttu-id="36902-611">Bieżąca implementacja przechodzi przez wszystkie wartości funkcja uzyskanie min i max, więc można wybrać odpowiedniej skali.</span><span class="sxs-lookup"><span data-stu-id="36902-611">The current implementation traverses all of the function values to obtain the min and max, so it can pick the correct scale.</span></span> <span data-ttu-id="36902-612">Bieżąca implementacja nie rozróżnia po usunięciu dokumenty lub dokumenty, niezawierające wartości.</span><span class="sxs-lookup"><span data-stu-id="36902-612">The current implementation cannot distinguish when documents have been deleted, or documents that have no value.</span></span> <span data-ttu-id="36902-613">W tych przypadkach używa 0.0 wartości.</span><span class="sxs-lookup"><span data-stu-id="36902-613">It uses 0.0 values for these cases.</span></span> <span data-ttu-id="36902-614">Oznacza to, że jeśli wartości są zwykle wszystkie większa niż 0,0, co może nadal końcowa 0,0 jako minimalna wartość do zamapowania z.</span><span class="sxs-lookup"><span data-stu-id="36902-614">This means that if values are normally all greater than 0.0, one can still end up with 0.0 as the min value to map from.</span></span> <span data-ttu-id="36902-615">W takich przypadkach odpowiednie `map()` funkcji można jako obejście zmienić 0,0 wartość w zakresie prawdziwe, jak pokazano poniżej:`scale(map(x,0,0,5),1,2)`</span><span class="sxs-lookup"><span data-stu-id="36902-615">In these cases, an appropriate `map()` function could be used as a workaround to change 0.0 to a value in the real range, as shown here: `scale(map(x,0,0,5),1,2)`</span></span> |`scale(x,minTarget,maxTarget)`<br><span data-ttu-id="36902-616">`scale(x,1,2)`Skaluje wartości x, w taki sposób, że wszystkie wartości należą do zakresu od 1 i 2 włącznie.</span><span class="sxs-lookup"><span data-stu-id="36902-616">`scale(x,1,2)` Scales the values of x, such that all values are between 1 and 2 inclusive.</span></span> |
| <span data-ttu-id="36902-617">SQRT</span><span class="sxs-lookup"><span data-stu-id="36902-617">sqrt</span></span> |<span data-ttu-id="36902-618">Zwraca pierwiastek kwadratowy z określonej wartości lub funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-618">Returns the square root of the specified value or function.</span></span> |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| <span data-ttu-id="36902-619">strdist</span><span class="sxs-lookup"><span data-stu-id="36902-619">strdist</span></span> |<span data-ttu-id="36902-620">Oblicza odległość między dwa ciągi.</span><span class="sxs-lookup"><span data-stu-id="36902-620">Calculates the distance between two strings.</span></span> <span data-ttu-id="36902-621">Używa interfejsu StringDistance moduł sprawdzania pisowni Lucene i obsługuje wszystkie dostępne w tym pakiecie implementacji.</span><span class="sxs-lookup"><span data-stu-id="36902-621">Uses the Lucene spell checker StringDistance interface, and supports all of the implementations available in that package.</span></span> <span data-ttu-id="36902-622">Umożliwia również aplikacji w ich własnych za pośrednictwem zasobów w Solr możliwości ładowanie do.</span><span class="sxs-lookup"><span data-stu-id="36902-622">Also allows applications to plug in their own, via Solr's resource loading capabilities.</span></span> <span data-ttu-id="36902-623">przyjmuje strdist `(string1, string2, distance measure)`.</span><span class="sxs-lookup"><span data-stu-id="36902-623">strdist takes `(string1, string2, distance measure)`.</span></span> <span data-ttu-id="36902-624">Możliwe wartości dla miary odległości to:</span><span class="sxs-lookup"><span data-stu-id="36902-624">Possible values for distance measure are:</span></span><ul><li><span data-ttu-id="36902-625">jw: Winklera Jaro</span><span class="sxs-lookup"><span data-stu-id="36902-625">jw: Jaro-Winkler</span></span></li><li><span data-ttu-id="36902-626">Edytuj: Levenstein lub edycji odległości</span><span class="sxs-lookup"><span data-stu-id="36902-626">edit: Levenstein or Edit distance</span></span></li><li><span data-ttu-id="36902-627">ngram: NGramDistance, jeśli jest określony, można opcjonalnie Przekaż rozmiar ngram zbyt.</span><span class="sxs-lookup"><span data-stu-id="36902-627">ngram: The NGramDistance, if specified, can optionally pass in the ngram size too.</span></span> <span data-ttu-id="36902-628">Domyślna to 2.</span><span class="sxs-lookup"><span data-stu-id="36902-628">Default is 2.</span></span></li><li><span data-ttu-id="36902-629">FQN: W pełni kwalifikowaną nazwę implementację interfejsu StringDistance klasy.</span><span class="sxs-lookup"><span data-stu-id="36902-629">FQN: Fully Qualified class Name for an implementation of the StringDistance interface.</span></span> <span data-ttu-id="36902-630">Musi mieć konstruktora nie argumentu.</span><span class="sxs-lookup"><span data-stu-id="36902-630">Must have a no-arg constructor.</span></span></li></ul> |`strdist("SOLR",id,edit)` |
| <span data-ttu-id="36902-631">Sub</span><span class="sxs-lookup"><span data-stu-id="36902-631">sub</span></span> |<span data-ttu-id="36902-632">Zwraca x i y, z `sub(x,y)`.</span><span class="sxs-lookup"><span data-stu-id="36902-632">Returns x-y from `sub(x,y)`.</span></span> |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| <span data-ttu-id="36902-633">Suma</span><span class="sxs-lookup"><span data-stu-id="36902-633">sum</span></span> |<span data-ttu-id="36902-634">Zwraca sumę wiele wartości lub funkcji, które są określone w postaci listy rozdzielanej przecinkami.</span><span class="sxs-lookup"><span data-stu-id="36902-634">Returns the sum of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="36902-635">`add(...)`może być używany jako alias dla tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="36902-635">`add(...)` may be used as an alias for this function.</span></span> |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| <span data-ttu-id="36902-636">termfreq</span><span class="sxs-lookup"><span data-stu-id="36902-636">termfreq</span></span> |<span data-ttu-id="36902-637">Zwraca liczbę razy, termin zostanie wyświetlony w polu dla tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="36902-637">Returns the number of times the term appears in the field for that document.</span></span> |<span data-ttu-id="36902-638">termfreq(text,'memory')</span><span class="sxs-lookup"><span data-stu-id="36902-638">termfreq(text,'memory')</span></span> |
| <span data-ttu-id="36902-639">tan</span><span class="sxs-lookup"><span data-stu-id="36902-639">tan</span></span> |<span data-ttu-id="36902-640">Zwraca tangens kąta.</span><span class="sxs-lookup"><span data-stu-id="36902-640">Returns tangent of an angle.</span></span> |`tan(x)` |
| <span data-ttu-id="36902-641">TANH</span><span class="sxs-lookup"><span data-stu-id="36902-641">tanh</span></span> |<span data-ttu-id="36902-642">Zwraca tangens hiperboliczny kąta.</span><span class="sxs-lookup"><span data-stu-id="36902-642">Returns hyperbolic tangent of an angle.</span></span> |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a><span data-ttu-id="36902-643">Odwołanie wyszukiwania pola i aspektu</span><span class="sxs-lookup"><span data-stu-id="36902-643">Search field and facet reference</span></span>
<span data-ttu-id="36902-644">Korzystając z wyszukiwania dziennika można znaleźć dane, wyniki są wyświetlane różne pola i aspektami.</span><span class="sxs-lookup"><span data-stu-id="36902-644">When you use Log Search to find data, results display various field and facets.</span></span> <span data-ttu-id="36902-645">Niektóre informacje mogą być niewidoczne bardzo opisowy.</span><span class="sxs-lookup"><span data-stu-id="36902-645">Some of the information might not appear very descriptive.</span></span> <span data-ttu-id="36902-646">Skorzystaj z poniższych informacji, aby ułatwić zrozumienie wyników.</span><span class="sxs-lookup"><span data-stu-id="36902-646">Use the following information to help you understand the results.</span></span>

| <span data-ttu-id="36902-647">Pole</span><span class="sxs-lookup"><span data-stu-id="36902-647">Field</span></span> | <span data-ttu-id="36902-648">Typ wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="36902-648">Search type</span></span> | <span data-ttu-id="36902-649">Opis</span><span class="sxs-lookup"><span data-stu-id="36902-649">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36902-650">Dla identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="36902-650">TenantId</span></span> |<span data-ttu-id="36902-651">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="36902-651">All</span></span> |<span data-ttu-id="36902-652">Używane do danych partycji.</span><span class="sxs-lookup"><span data-stu-id="36902-652">Used to partition data.</span></span> |
| <span data-ttu-id="36902-653">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="36902-653">TimeGenerated</span></span> |<span data-ttu-id="36902-654">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="36902-654">All</span></span> |<span data-ttu-id="36902-655">Używana do osi czasu, timeselectors (wyszukiwania i w innych ekranów).</span><span class="sxs-lookup"><span data-stu-id="36902-655">Used to drive the timeline, timeselectors (in search and in other screens).</span></span> <span data-ttu-id="36902-656">Reprezentuje on, gdy element danych został wygenerowany (zwykle w agencie).</span><span class="sxs-lookup"><span data-stu-id="36902-656">It represents when the piece of data was generated (typically on the agent).</span></span> <span data-ttu-id="36902-657">Czas jest wyrażona w formacie ISO i jest zawsze UTC.</span><span class="sxs-lookup"><span data-stu-id="36902-657">The time is expressed in ISO format, and is always UTC.</span></span> <span data-ttu-id="36902-658">W przypadku typów, które są oparte na istniejących Instrumentacji (to znaczy zdarzenia w dzienniku) jest to zazwyczaj rejestrującej wpisu/wiersz/rekord dziennika w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="36902-658">In the case of types that are based on existing instrumentation (that is, events in a log), this is typically the real time that the log entry/line/record was logged.</span></span> <span data-ttu-id="36902-659">W przypadku niektórych typów, które są tworzone za pomocą pakietów administracyjnych lub w chmurze (na przykład zalecenia lub alerty) czas reprezentuje inną.</span><span class="sxs-lookup"><span data-stu-id="36902-659">For some of the other types that are produced either via management packs or in the cloud (for example, recommendations or alerts), the time represents something different.</span></span> <span data-ttu-id="36902-660">Jest to nowy element danych migawka konfiguracji pewnego rodzaju zostały zebrane, lub zalecenie/alert został utworzony na jego podstawie.</span><span class="sxs-lookup"><span data-stu-id="36902-660">This is the time when this new piece of data with a snapshot of a configuration of some sort was collected, or a recommendation/alert was produced based on it.</span></span> |
| <span data-ttu-id="36902-661">Identyfikator zdarzenia</span><span class="sxs-lookup"><span data-stu-id="36902-661">EventID</span></span> |<span data-ttu-id="36902-662">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="36902-662">Event</span></span> |<span data-ttu-id="36902-663">Identyfikator zdarzenia w dzienniku zdarzeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="36902-663">EventID in the Windows event log.</span></span> |
| <span data-ttu-id="36902-664">Dziennik zdarzeń</span><span class="sxs-lookup"><span data-stu-id="36902-664">EventLog</span></span> |<span data-ttu-id="36902-665">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="36902-665">Event</span></span> |<span data-ttu-id="36902-666">Dziennik zdarzeń, w którym zdarzenie zostało zarejestrowane przez system Windows.</span><span class="sxs-lookup"><span data-stu-id="36902-666">Event log where the event was logged by Windows.</span></span> |
| <span data-ttu-id="36902-667">EventLevelName</span><span class="sxs-lookup"><span data-stu-id="36902-667">EventLevelName</span></span> |<span data-ttu-id="36902-668">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="36902-668">Event</span></span> |<span data-ttu-id="36902-669">Krytyczne/ostrzeżenia/informacji/Powodzenie</span><span class="sxs-lookup"><span data-stu-id="36902-669">Critical/warning/information/success</span></span> |
| <span data-ttu-id="36902-670">eventLevel</span><span class="sxs-lookup"><span data-stu-id="36902-670">EventLevel</span></span> |<span data-ttu-id="36902-671">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="36902-671">Event</span></span> |<span data-ttu-id="36902-672">Wartości liczbowej dla krytycznych/ostrzeżenia/informacji/Powodzenie (Użyj EventLevelName łatwiejsze/bardziej czytelny zapytań).</span><span class="sxs-lookup"><span data-stu-id="36902-672">Numerical value for critical/warning/information/success (use EventLevelName instead for easier/more readable queries).</span></span> |
| <span data-ttu-id="36902-673">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="36902-673">SourceSystem</span></span> |<span data-ttu-id="36902-674">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="36902-674">All</span></span> |<span data-ttu-id="36902-675">Gdy dane pochodzą z (w postaci liczby dołączyć tryb do usługi).</span><span class="sxs-lookup"><span data-stu-id="36902-675">Where the data comes from (in terms of attach mode to the service).</span></span> <span data-ttu-id="36902-676">Przykłady programu Microsoft System Center Operations Manager i usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="36902-676">Examples include Microsoft System Center Operations Manager and Azure Storage.</span></span> |
| <span data-ttu-id="36902-677">Nazwa obiektu</span><span class="sxs-lookup"><span data-stu-id="36902-677">ObjectName</span></span> |<span data-ttu-id="36902-678">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="36902-678">PerfHourly</span></span> |<span data-ttu-id="36902-679">Nazwa obiektu wydajności systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="36902-679">Windows performance object name.</span></span> |
| <span data-ttu-id="36902-680">InstanceName</span><span class="sxs-lookup"><span data-stu-id="36902-680">InstanceName</span></span> |<span data-ttu-id="36902-681">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="36902-681">PerfHourly</span></span> |<span data-ttu-id="36902-682">Nazwa wystąpienia liczników wydajności systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="36902-682">Windows performance counter instance name.</span></span> |
| <span data-ttu-id="36902-683">CounteName</span><span class="sxs-lookup"><span data-stu-id="36902-683">CounteName</span></span> |<span data-ttu-id="36902-684">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="36902-684">PerfHourly</span></span> |<span data-ttu-id="36902-685">Nazwa licznika wydajności systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="36902-685">Windows performance counter name.</span></span> |
| <span data-ttu-id="36902-686">ObjectDisplayName</span><span class="sxs-lookup"><span data-stu-id="36902-686">ObjectDisplayName</span></span> |<span data-ttu-id="36902-687">PerfHourly, ConfigurationObjectProperty ConfigurationAlert, ConfigurationObject,</span><span class="sxs-lookup"><span data-stu-id="36902-687">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="36902-688">Nazwa wyświetlana obiektu objęci zasadę zbierania danych wydajności w programie Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="36902-688">Display name of the object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="36902-689">Mogą być również nazwę wyświetlaną obiektu wykrytych przez usługę Operational Insights lub względem został wygenerowany alert.</span><span class="sxs-lookup"><span data-stu-id="36902-689">Could also be the display name of the object discovered by Operational Insights, or against which the alert was generated.</span></span> |
| <span data-ttu-id="36902-690">RootObjectName</span><span class="sxs-lookup"><span data-stu-id="36902-690">RootObjectName</span></span> |<span data-ttu-id="36902-691">PerfHourly, ConfigurationObjectProperty ConfigurationAlert, ConfigurationObject,</span><span class="sxs-lookup"><span data-stu-id="36902-691">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="36902-692">Wyświetlana nazwa nadrzędnego elementu nadrzędnego obiektu objęci zasadę zbierania danych wydajności w programie Operations Manager (w relacji hostingu podwójny).</span><span class="sxs-lookup"><span data-stu-id="36902-692">Display name of the parent of the parent (in a double hosting relationship) of the object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="36902-693">Mogą być również nazwę wyświetlaną obiektu wykrytych przez usługę Operational Insights lub względem został wygenerowany alert.</span><span class="sxs-lookup"><span data-stu-id="36902-693">Could also be the display name of the object discovered by Operational Insights, or against which the alert was generated.</span></span> |
| <span data-ttu-id="36902-694">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="36902-694">Computer</span></span> |<span data-ttu-id="36902-695">Większość typów</span><span class="sxs-lookup"><span data-stu-id="36902-695">Most types</span></span> |<span data-ttu-id="36902-696">Nazwa komputera należącego do danych.</span><span class="sxs-lookup"><span data-stu-id="36902-696">Computer name that the data belongs to.</span></span> |
| <span data-ttu-id="36902-697">DeviceName</span><span class="sxs-lookup"><span data-stu-id="36902-697">DeviceName</span></span> |<span data-ttu-id="36902-698">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="36902-698">ProtectionStatus</span></span> |<span data-ttu-id="36902-699">Nazwa komputera danych należy do (tak samo, jak "Komputer").</span><span class="sxs-lookup"><span data-stu-id="36902-699">Computer name the data belongs to (same as "Computer").</span></span> |
| <span data-ttu-id="36902-700">DetectionId</span><span class="sxs-lookup"><span data-stu-id="36902-700">DetectionId</span></span> |<span data-ttu-id="36902-701">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="36902-701">ProtectionStatus</span></span> | |
| <span data-ttu-id="36902-702">ThreatStatusRank</span><span class="sxs-lookup"><span data-stu-id="36902-702">ThreatStatusRank</span></span> |<span data-ttu-id="36902-703">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="36902-703">ProtectionStatus</span></span> |<span data-ttu-id="36902-704">Pozycja stan zagrożenie jest numeryczna reprezentacja stanu zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="36902-704">Threat status rank is a numerical representation of the threat status.</span></span> <span data-ttu-id="36902-705">Podobnie jak kody odpowiedzi HTTP, klasyfikację ma luki pomiędzy numery (dlatego zagrożenia nie wynosi 150 i nie 100 lub 0), pozostawiając miejsca, aby dodać nowe stany.</span><span class="sxs-lookup"><span data-stu-id="36902-705">Similar to HTTP response codes, the ranking has gaps between the numbers (which is why no threats is 150 and not 100 or 0), leaving room to add new states.</span></span> <span data-ttu-id="36902-706">Dla zbiorczego stanu zagrożeń i stanu ochrony jest do wyświetlenia najgorszy stan, który komputer był w trakcie wybrany okres czasu.</span><span class="sxs-lookup"><span data-stu-id="36902-706">For a rollup of threat status and protection status, the intention is to show the worst state that the computer has been in during the selected time period.</span></span> <span data-ttu-id="36902-707">Numery rank różne stany, więc można wyszukać rekord o najwyższym numerze.</span><span class="sxs-lookup"><span data-stu-id="36902-707">The numbers rank the different states, so you can look for the record with the highest number.</span></span> |
| <span data-ttu-id="36902-708">ThreatStatus</span><span class="sxs-lookup"><span data-stu-id="36902-708">ThreatStatus</span></span> |<span data-ttu-id="36902-709">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="36902-709">ProtectionStatus</span></span> |<span data-ttu-id="36902-710">Opis ThreatStatus, mapuje 1:1 z ThreatStatusRank.</span><span class="sxs-lookup"><span data-stu-id="36902-710">Description of ThreatStatus, maps 1:1 with ThreatStatusRank.</span></span> |
| <span data-ttu-id="36902-711">TypeofProtection</span><span class="sxs-lookup"><span data-stu-id="36902-711">TypeofProtection</span></span> |<span data-ttu-id="36902-712">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="36902-712">ProtectionStatus</span></span> |<span data-ttu-id="36902-713">Produkt ochrony przed złośliwym kodem, który zostanie wykryty na komputerze: Brak, narzędzie do usuwania złośliwego oprogramowania firmy Microsoft, Forefront itd.</span><span class="sxs-lookup"><span data-stu-id="36902-713">Antimalware product that is detected in the computer: none, Microsoft Malware Removal tool, Forefront, and so on.</span></span> |
| <span data-ttu-id="36902-714">ScanDate</span><span class="sxs-lookup"><span data-stu-id="36902-714">ScanDate</span></span> |<span data-ttu-id="36902-715">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="36902-715">ProtectionStatus</span></span> | |
| <span data-ttu-id="36902-716">SourceHealthServiceId</span><span class="sxs-lookup"><span data-stu-id="36902-716">SourceHealthServiceId</span></span> |<span data-ttu-id="36902-717">ProtectionStatus, RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="36902-717">ProtectionStatus, RequiredUpdate</span></span> |<span data-ttu-id="36902-718">Identyfikator usługi badania kondycji agenta na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="36902-718">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="36902-719">HealthServiceId</span><span class="sxs-lookup"><span data-stu-id="36902-719">HealthServiceId</span></span> |<span data-ttu-id="36902-720">Większość typów</span><span class="sxs-lookup"><span data-stu-id="36902-720">Most types</span></span> |<span data-ttu-id="36902-721">Identyfikator usługi badania kondycji agenta na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="36902-721">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="36902-722">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="36902-722">ManagementGroupName</span></span> |<span data-ttu-id="36902-723">Większość typów</span><span class="sxs-lookup"><span data-stu-id="36902-723">Most types</span></span> |<span data-ttu-id="36902-724">Nazwa grupy zarządzania agentami dołączone do programu Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="36902-724">Management Group Name for Operations Manager-attached agents.</span></span> <span data-ttu-id="36902-725">W przeciwnym razie wartość jest równa null/puste.</span><span class="sxs-lookup"><span data-stu-id="36902-725">Otherwise, it is null/blank.</span></span> |
| <span data-ttu-id="36902-726">Typ obiektu</span><span class="sxs-lookup"><span data-stu-id="36902-726">ObjectType</span></span> |<span data-ttu-id="36902-727">ConfigurationObject</span><span class="sxs-lookup"><span data-stu-id="36902-727">ConfigurationObject</span></span> |<span data-ttu-id="36902-728">Typ (jak klasa/typu pakiet administracyjny programu Operations Manager) dla tego obiektu, wykryte przez oceny konfiguracji analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="36902-728">Type (as in Operations Manager management pack's type/class) for this object, discovered by Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="36902-729">UpdateTitle</span><span class="sxs-lookup"><span data-stu-id="36902-729">UpdateTitle</span></span> |<span data-ttu-id="36902-730">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="36902-730">RequiredUpdate</span></span> |<span data-ttu-id="36902-731">Nazwa znaleziono aktualizacji nie jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="36902-731">Name of the update that was found not installed.</span></span> |
| <span data-ttu-id="36902-732">PublishDate</span><span class="sxs-lookup"><span data-stu-id="36902-732">PublishDate</span></span> |<span data-ttu-id="36902-733">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="36902-733">RequiredUpdate</span></span> |<span data-ttu-id="36902-734">Jeśli aktualizacja została opublikowana w witrynie Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="36902-734">When the update was published on Microsoft Update.</span></span> |
| <span data-ttu-id="36902-735">Serwer</span><span class="sxs-lookup"><span data-stu-id="36902-735">Server</span></span> |<span data-ttu-id="36902-736">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="36902-736">RequiredUpdate</span></span> |<span data-ttu-id="36902-737">Nazwa komputera danych należy do (tak samo, jak "Komputer").</span><span class="sxs-lookup"><span data-stu-id="36902-737">Computer name the data belongs to (same as "Computer").</span></span> |
| <span data-ttu-id="36902-738">Product (Produkt)</span><span class="sxs-lookup"><span data-stu-id="36902-738">Product</span></span> |<span data-ttu-id="36902-739">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="36902-739">RequiredUpdate</span></span> |<span data-ttu-id="36902-740">Aktualizacja dotyczy produktu.</span><span class="sxs-lookup"><span data-stu-id="36902-740">Product that the update applies to.</span></span> |
| <span data-ttu-id="36902-741">UpdateClassification</span><span class="sxs-lookup"><span data-stu-id="36902-741">UpdateClassification</span></span> |<span data-ttu-id="36902-742">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="36902-742">RequiredUpdate</span></span> |<span data-ttu-id="36902-743">Typ aktualizacji (na przykład pakiet zbiorczy aktualizacji lub dodatek service pack).</span><span class="sxs-lookup"><span data-stu-id="36902-743">Type of update (for example, update rollup or service pack).</span></span> |
| <span data-ttu-id="36902-744">KBID</span><span class="sxs-lookup"><span data-stu-id="36902-744">KBID</span></span> |<span data-ttu-id="36902-745">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="36902-745">RequiredUpdate</span></span> |<span data-ttu-id="36902-746">Identyfikator artykułu KB, który opisuje najlepsze praktyki lub aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="36902-746">KB article ID that describes this best practice or update.</span></span> |
| <span data-ttu-id="36902-747">WorkflowName</span><span class="sxs-lookup"><span data-stu-id="36902-747">WorkflowName</span></span> |<span data-ttu-id="36902-748">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="36902-748">ConfigurationAlert</span></span> |<span data-ttu-id="36902-749">Nazwa reguły lub monitora wytworzonego alertu.</span><span class="sxs-lookup"><span data-stu-id="36902-749">Name of the rule or monitor that produced the alert.</span></span> |
| <span data-ttu-id="36902-750">Ważność</span><span class="sxs-lookup"><span data-stu-id="36902-750">Severity</span></span> |<span data-ttu-id="36902-751">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="36902-751">ConfigurationAlert</span></span> |<span data-ttu-id="36902-752">Ważność alertu.</span><span class="sxs-lookup"><span data-stu-id="36902-752">Severity of the alert.</span></span> |
| <span data-ttu-id="36902-753">Priorytet</span><span class="sxs-lookup"><span data-stu-id="36902-753">Priority</span></span> |<span data-ttu-id="36902-754">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="36902-754">ConfigurationAlert</span></span> |<span data-ttu-id="36902-755">Priorytet alertu.</span><span class="sxs-lookup"><span data-stu-id="36902-755">Priority of the alert.</span></span> |
| <span data-ttu-id="36902-756">IsMonitorAlert</span><span class="sxs-lookup"><span data-stu-id="36902-756">IsMonitorAlert</span></span> |<span data-ttu-id="36902-757">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="36902-757">ConfigurationAlert</span></span> |<span data-ttu-id="36902-758">Ten alert został wygenerowany przez monitor (true) czy zasadę (false)?</span><span class="sxs-lookup"><span data-stu-id="36902-758">Is this alert generated by a monitor (true) or a rule (false)?</span></span> |
| <span data-ttu-id="36902-759">AlertParameters</span><span class="sxs-lookup"><span data-stu-id="36902-759">AlertParameters</span></span> |<span data-ttu-id="36902-760">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="36902-760">ConfigurationAlert</span></span> |<span data-ttu-id="36902-761">Plik XML z parametrami alertu analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="36902-761">XML with the parameters of the Log Analytics alert.</span></span> |
| <span data-ttu-id="36902-762">Kontekst</span><span class="sxs-lookup"><span data-stu-id="36902-762">Context</span></span> |<span data-ttu-id="36902-763">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="36902-763">ConfigurationAlert</span></span> |<span data-ttu-id="36902-764">Kod XML w kontekście alertu analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="36902-764">XML with the context of the Log Analytics alert.</span></span> |
| <span data-ttu-id="36902-765">Obciążenie</span><span class="sxs-lookup"><span data-stu-id="36902-765">Workload</span></span> |<span data-ttu-id="36902-766">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="36902-766">ConfigurationAlert</span></span> |<span data-ttu-id="36902-767">Technologia lub obciążenia, którego alert dotyczy.</span><span class="sxs-lookup"><span data-stu-id="36902-767">Technology or workload that the alert refers to.</span></span> |
| <span data-ttu-id="36902-768">AdvisorWorkload</span><span class="sxs-lookup"><span data-stu-id="36902-768">AdvisorWorkload</span></span> |<span data-ttu-id="36902-769">Zalecenie</span><span class="sxs-lookup"><span data-stu-id="36902-769">Recommendation</span></span> |<span data-ttu-id="36902-770">Technologia lub obciążenia, odnoszący się do zalecenia.</span><span class="sxs-lookup"><span data-stu-id="36902-770">Technology or workload that the recommendation refers to.</span></span> |
| <span data-ttu-id="36902-771">Opis</span><span class="sxs-lookup"><span data-stu-id="36902-771">Description</span></span> |<span data-ttu-id="36902-772">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="36902-772">ConfigurationAlert</span></span> |<span data-ttu-id="36902-773">Opis alertu (short).</span><span class="sxs-lookup"><span data-stu-id="36902-773">Alert description (short).</span></span> |
| <span data-ttu-id="36902-774">DaysSinceLastUpdate</span><span class="sxs-lookup"><span data-stu-id="36902-774">DaysSinceLastUpdate</span></span> |<span data-ttu-id="36902-775">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="36902-775">UpdateAgent</span></span> |<span data-ttu-id="36902-776">Ile dni temu (względem TimeGenerated tego rekordu) tego agenta zainstalować aktualizację z usługi Windows Server Update Service (WSUS) lub Microsoft Update?</span><span class="sxs-lookup"><span data-stu-id="36902-776">How many days ago (relative to TimeGenerated of this record) did this agent install any update from Windows Server Update Service (WSUS) or Microsoft Update?</span></span> |
| <span data-ttu-id="36902-777">DaysSinceLastUpdateBucket</span><span class="sxs-lookup"><span data-stu-id="36902-777">DaysSinceLastUpdateBucket</span></span> |<span data-ttu-id="36902-778">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="36902-778">UpdateAgent</span></span> |<span data-ttu-id="36902-779">Oparte na DaysSinceLastUpdate, kategoryzacji w przedziałów czasu z jak dawno temu komputera ostatniej instalacji żadnych aktualizacji usług WSUS/usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="36902-779">Based on DaysSinceLastUpdate, a categorization in time buckets of how long ago a computer last installed any update from WSUS/Microsoft Update.</span></span> |
| <span data-ttu-id="36902-780">AutomaticUpdateEnabled</span><span class="sxs-lookup"><span data-stu-id="36902-780">AutomaticUpdateEnabled</span></span> |<span data-ttu-id="36902-781">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="36902-781">UpdateAgent</span></span> |<span data-ttu-id="36902-782">Sprawdzanie aktualizacji automatycznych włączone lub wyłączone dla tego agenta?</span><span class="sxs-lookup"><span data-stu-id="36902-782">Is automatic update checking enabled or disabled on this agent?</span></span> |
| <span data-ttu-id="36902-783">AutomaticUpdateValue</span><span class="sxs-lookup"><span data-stu-id="36902-783">AutomaticUpdateValue</span></span> |<span data-ttu-id="36902-784">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="36902-784">UpdateAgent</span></span> |<span data-ttu-id="36902-785">Automatyczna aktualizacja sprawdza, czy ustawiono automatycznie pobrać i zainstalować, tylko pobierania lub tylko sprawdzanie?</span><span class="sxs-lookup"><span data-stu-id="36902-785">Is automatic update checking set to automatically download and install, only download, or only check?</span></span> |
| <span data-ttu-id="36902-786">WindowsUpdateAgentVersion</span><span class="sxs-lookup"><span data-stu-id="36902-786">WindowsUpdateAgentVersion</span></span> |<span data-ttu-id="36902-787">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="36902-787">UpdateAgent</span></span> |<span data-ttu-id="36902-788">Numer wersji agenta usługi Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="36902-788">Version number of the Microsoft Update agent.</span></span> |
| <span data-ttu-id="36902-789">WSUSServer</span><span class="sxs-lookup"><span data-stu-id="36902-789">WSUSServer</span></span> |<span data-ttu-id="36902-790">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="36902-790">UpdateAgent</span></span> |<span data-ttu-id="36902-791">Serwer WSUS, który jest celem tej usługi Windows update agent</span><span class="sxs-lookup"><span data-stu-id="36902-791">Which WSUS server is this update agent targeting?</span></span> |
| <span data-ttu-id="36902-792">OSVersion</span><span class="sxs-lookup"><span data-stu-id="36902-792">OSVersion</span></span> |<span data-ttu-id="36902-793">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="36902-793">UpdateAgent</span></span> |<span data-ttu-id="36902-794">Wersja systemu operacyjnego tej usługi Windows update agent jest uruchomiony w.</span><span class="sxs-lookup"><span data-stu-id="36902-794">Version of the operating system this update agent is running on.</span></span> |
| <span data-ttu-id="36902-795">Nazwa</span><span class="sxs-lookup"><span data-stu-id="36902-795">Name</span></span> |<span data-ttu-id="36902-796">Zalecenie, ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="36902-796">Recommendation, ConfigurationObjectProperty</span></span> |<span data-ttu-id="36902-797">Nazwa/tytuł zalecenia lub nazwa właściwości z analizy dzienników konfiguracji oceny.</span><span class="sxs-lookup"><span data-stu-id="36902-797">Name/title of the recommendation, or name of the property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="36902-798">Wartość</span><span class="sxs-lookup"><span data-stu-id="36902-798">Value</span></span> |<span data-ttu-id="36902-799">ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="36902-799">ConfigurationObjectProperty</span></span> |<span data-ttu-id="36902-800">Wartość właściwości z analizy dzienników konfiguracji oceny.</span><span class="sxs-lookup"><span data-stu-id="36902-800">Value of a property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="36902-801">KBLink</span><span class="sxs-lookup"><span data-stu-id="36902-801">KBLink</span></span> |<span data-ttu-id="36902-802">Zalecenie</span><span class="sxs-lookup"><span data-stu-id="36902-802">Recommendation</span></span> |<span data-ttu-id="36902-803">Adres URL do artykułu bazy wiedzy, który opisuje najlepsze praktyki lub aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="36902-803">URL to the KB article that describes this best practice or update.</span></span> |
| <span data-ttu-id="36902-804">RecommendationStatus</span><span class="sxs-lookup"><span data-stu-id="36902-804">RecommendationStatus</span></span> |<span data-ttu-id="36902-805">Zalecenie</span><span class="sxs-lookup"><span data-stu-id="36902-805">Recommendation</span></span> |<span data-ttu-id="36902-806">Zalecenia są wśród kilka typów rekordów aktualizowany, nie tylko dodane do indeksu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="36902-806">Recommendations are among the few types whose records get updated, not just added to the search index.</span></span> <span data-ttu-id="36902-807">Ten stan zmieni się, czy zalecane jest aktywny lub open lub analizy dzienników wykryje, że został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="36902-807">This status changes whether the recommendation is active/open, or if Log Analytics detects that it has been resolved.</span></span> |
| <span data-ttu-id="36902-808">RenderedDescription</span><span class="sxs-lookup"><span data-stu-id="36902-808">RenderedDescription</span></span> |<span data-ttu-id="36902-809">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="36902-809">Event</span></span> |<span data-ttu-id="36902-810">Renderowane opis (ponownie tekst z parametrami wypełnione) zdarzeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="36902-810">Rendered description (reused text with populated parameters) of a Windows event.</span></span> |
| <span data-ttu-id="36902-811">ParameterXml</span><span class="sxs-lookup"><span data-stu-id="36902-811">ParameterXml</span></span> |<span data-ttu-id="36902-812">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="36902-812">Event</span></span> |<span data-ttu-id="36902-813">Plik XML z parametrami w sekcji danych zdarzenia systemu Windows (taki jak pokazano w Podglądzie zdarzeń).</span><span class="sxs-lookup"><span data-stu-id="36902-813">XML with the parameters in the data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="36902-814">EventData</span><span class="sxs-lookup"><span data-stu-id="36902-814">EventData</span></span> |<span data-ttu-id="36902-815">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="36902-815">Event</span></span> |<span data-ttu-id="36902-816">Plik XML z sekcji całego danych zdarzenia systemu Windows (taki jak pokazano w Podglądzie zdarzeń).</span><span class="sxs-lookup"><span data-stu-id="36902-816">XML with the whole data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="36902-817">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="36902-817">Source</span></span> |<span data-ttu-id="36902-818">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="36902-818">Event</span></span> |<span data-ttu-id="36902-819">Źródło dziennika zdarzeń, który wygenerował zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="36902-819">Event log source that generated the event.</span></span> |
| <span data-ttu-id="36902-820">EventCategory</span><span class="sxs-lookup"><span data-stu-id="36902-820">EventCategory</span></span> |<span data-ttu-id="36902-821">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="36902-821">Event</span></span> |<span data-ttu-id="36902-822">Kategoria zdarzenia, bezpośrednio z dziennika zdarzeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="36902-822">Category of the event, directly from the Windows event log.</span></span> |
| <span data-ttu-id="36902-823">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="36902-823">UserName</span></span> |<span data-ttu-id="36902-824">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="36902-824">Event</span></span> |<span data-ttu-id="36902-825">Nazwa użytkownika dla zdarzenia systemu Windows (zazwyczaj NT AUTHORITY\LOCALSYSTEM).</span><span class="sxs-lookup"><span data-stu-id="36902-825">User name of the Windows event (typically, NT AUTHORITY\LOCALSYSTEM).</span></span> |
| <span data-ttu-id="36902-826">SampleValue</span><span class="sxs-lookup"><span data-stu-id="36902-826">SampleValue</span></span> |<span data-ttu-id="36902-827">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="36902-827">PerfHourly</span></span> |<span data-ttu-id="36902-828">Średnia wartość dla agregacji godzinowej licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="36902-828">Average value for the hourly aggregation of a performance counter.</span></span> |
| <span data-ttu-id="36902-829">Min</span><span class="sxs-lookup"><span data-stu-id="36902-829">Min</span></span> |<span data-ttu-id="36902-830">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="36902-830">PerfHourly</span></span> |<span data-ttu-id="36902-831">Minimalna wartość godzinny interwał agregacji godzinowej licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="36902-831">Minimum value in the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="36902-832">Maks.</span><span class="sxs-lookup"><span data-stu-id="36902-832">Max</span></span> |<span data-ttu-id="36902-833">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="36902-833">PerfHourly</span></span> |<span data-ttu-id="36902-834">Maksymalna wartość godzinny interwał agregacji godzinowej licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="36902-834">Maximum value in the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="36902-835">Percentile95</span><span class="sxs-lookup"><span data-stu-id="36902-835">Percentile95</span></span> |<span data-ttu-id="36902-836">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="36902-836">PerfHourly</span></span> |<span data-ttu-id="36902-837">Wartość percentylu 95 godzinny interwał agregacji godzinowej licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="36902-837">The 95th percentile value for the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="36902-838">SampleCount</span><span class="sxs-lookup"><span data-stu-id="36902-838">SampleCount</span></span> |<span data-ttu-id="36902-839">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="36902-839">PerfHourly</span></span> |<span data-ttu-id="36902-840">Jak wiele próbek licznika wydajność pierwotna były używane do tworzenia tego rekordu agregacji godzinowej.</span><span class="sxs-lookup"><span data-stu-id="36902-840">How many raw performance counter samples were used to produce this hourly aggregate record.</span></span> |
| <span data-ttu-id="36902-841">Zagrożenia</span><span class="sxs-lookup"><span data-stu-id="36902-841">Threat</span></span> |<span data-ttu-id="36902-842">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="36902-842">ProtectionStatus</span></span> |<span data-ttu-id="36902-843">Nazwa wykrytego złośliwego oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="36902-843">Name of malware found.</span></span> |
| <span data-ttu-id="36902-844">Konto magazynu</span><span class="sxs-lookup"><span data-stu-id="36902-844">StorageAccount</span></span> |<span data-ttu-id="36902-845">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-845">W3CIISLog</span></span> |<span data-ttu-id="36902-846">Konto usługi Azure Storage dziennika została odczytana z.</span><span class="sxs-lookup"><span data-stu-id="36902-846">Azure Storage account the log was read from.</span></span> |
| <span data-ttu-id="36902-847">AzureDeploymentID</span><span class="sxs-lookup"><span data-stu-id="36902-847">AzureDeploymentID</span></span> |<span data-ttu-id="36902-848">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-848">W3CIISLog</span></span> |<span data-ttu-id="36902-849">Identyfikator Azure wdrożenia usługi w chmurze dziennika należy.</span><span class="sxs-lookup"><span data-stu-id="36902-849">Azure deployment ID of the cloud service the log belongs to.</span></span> |
| <span data-ttu-id="36902-850">Rola</span><span class="sxs-lookup"><span data-stu-id="36902-850">Role</span></span> |<span data-ttu-id="36902-851">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-851">W3CIISLog</span></span> |<span data-ttu-id="36902-852">Przynależność roli usługi w chmurze Azure dziennika.</span><span class="sxs-lookup"><span data-stu-id="36902-852">Role of the Azure cloud service the log belongs to.</span></span> |
| <span data-ttu-id="36902-853">RoleInstance</span><span class="sxs-lookup"><span data-stu-id="36902-853">RoleInstance</span></span> |<span data-ttu-id="36902-854">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-854">W3CIISLog</span></span> |<span data-ttu-id="36902-855">RoleInstance Azure dziennika należy do roli.</span><span class="sxs-lookup"><span data-stu-id="36902-855">RoleInstance of the Azure role that the log belongs to.</span></span> |
| <span data-ttu-id="36902-856">sSiteName</span><span class="sxs-lookup"><span data-stu-id="36902-856">sSiteName</span></span> |<span data-ttu-id="36902-857">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-857">W3CIISLog</span></span> |<span data-ttu-id="36902-858">Witryny sieci Web usług IIS, której dziennika należy (metabazy notacji); Pole s-sitename w oryginalnym dziennika.</span><span class="sxs-lookup"><span data-stu-id="36902-858">IIS website that the log belongs to (metabase notation); the s-sitename field in the original log.</span></span> |
| <span data-ttu-id="36902-859">sComputerName</span><span class="sxs-lookup"><span data-stu-id="36902-859">sComputerName</span></span> |<span data-ttu-id="36902-860">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-860">W3CIISLog</span></span> |<span data-ttu-id="36902-861">Pole s-computername w oryginalnym dziennika.</span><span class="sxs-lookup"><span data-stu-id="36902-861">The s-computername field in the original log.</span></span> |
| <span data-ttu-id="36902-862">sIP</span><span class="sxs-lookup"><span data-stu-id="36902-862">sIP</span></span> |<span data-ttu-id="36902-863">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-863">W3CIISLog</span></span> |<span data-ttu-id="36902-864">Żądanie HTTP adres IP serwera został skierowany do.</span><span class="sxs-lookup"><span data-stu-id="36902-864">Server IP address the HTTP request was addressed to.</span></span> <span data-ttu-id="36902-865">Pole s-ip w oryginalnym dziennika.</span><span class="sxs-lookup"><span data-stu-id="36902-865">The s-ip field in the original log.</span></span> |
| <span data-ttu-id="36902-866">csMethod</span><span class="sxs-lookup"><span data-stu-id="36902-866">csMethod</span></span> |<span data-ttu-id="36902-867">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-867">W3CIISLog</span></span> |<span data-ttu-id="36902-868">Metoda HTTP (na przykład GET/POST) używany przez klienta w żądaniu HTTP.</span><span class="sxs-lookup"><span data-stu-id="36902-868">HTTP method (for example, GET/POST) used by the client in the HTTP request.</span></span> <span data-ttu-id="36902-869">Cs metoda w dzienniku oryginalnego.</span><span class="sxs-lookup"><span data-stu-id="36902-869">The cs-method in the original log.</span></span> |
| <span data-ttu-id="36902-870">cIP</span><span class="sxs-lookup"><span data-stu-id="36902-870">cIP</span></span> |<span data-ttu-id="36902-871">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-871">W3CIISLog</span></span> |<span data-ttu-id="36902-872">Pochodzi żądanie HTTP adres IP klienta.</span><span class="sxs-lookup"><span data-stu-id="36902-872">Client IP address the HTTP request came from.</span></span> <span data-ttu-id="36902-873">Pole c-ip w oryginalnym dziennika.</span><span class="sxs-lookup"><span data-stu-id="36902-873">The c-ip field in the original log.</span></span> |
| <span data-ttu-id="36902-874">csUserAgent</span><span class="sxs-lookup"><span data-stu-id="36902-874">csUserAgent</span></span> |<span data-ttu-id="36902-875">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-875">W3CIISLog</span></span> |<span data-ttu-id="36902-876">Agent użytkownika HTTP zgłoszone przez klienta (przeglądarki lub w inny sposób).</span><span class="sxs-lookup"><span data-stu-id="36902-876">HTTP User-Agent declared by the client (browser or otherwise).</span></span> <span data-ttu-id="36902-877">Cs-user-agent w dzienniku oryginalnego.</span><span class="sxs-lookup"><span data-stu-id="36902-877">The cs-user-agent in the original log.</span></span> |
| <span data-ttu-id="36902-878">scStatus</span><span class="sxs-lookup"><span data-stu-id="36902-878">scStatus</span></span> |<span data-ttu-id="36902-879">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-879">W3CIISLog</span></span> |<span data-ttu-id="36902-880">Zwrócony przez serwer do klienta kod stanu HTTP (na przykład 200/403/500).</span><span class="sxs-lookup"><span data-stu-id="36902-880">HTTP Status code (for example, 200/403/500) returned by the server to the client.</span></span> <span data-ttu-id="36902-881">Cs-status w oryginalnym dziennika.</span><span class="sxs-lookup"><span data-stu-id="36902-881">The cs-status in the original log.</span></span> |
| <span data-ttu-id="36902-882">Właściwość timeTaken</span><span class="sxs-lookup"><span data-stu-id="36902-882">TimeTaken</span></span> |<span data-ttu-id="36902-883">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-883">W3CIISLog</span></span> |<span data-ttu-id="36902-884">Jak długo (w milisekundach), który realizacja żądania zajęła do wykonania.</span><span class="sxs-lookup"><span data-stu-id="36902-884">How long (in milliseconds) that the request took to complete.</span></span> <span data-ttu-id="36902-885">Pole właściwość timetaken w oryginalnym dziennika.</span><span class="sxs-lookup"><span data-stu-id="36902-885">The timetaken field in the original log.</span></span> |
| <span data-ttu-id="36902-886">csUriStem</span><span class="sxs-lookup"><span data-stu-id="36902-886">csUriStem</span></span> |<span data-ttu-id="36902-887">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-887">W3CIISLog</span></span> |<span data-ttu-id="36902-888">Względny identyfikator URI (bez adres hosta, który jest, / wyszukaj) który odebrał żądanie.</span><span class="sxs-lookup"><span data-stu-id="36902-888">Relative URI (without host address, that is, /search ) that was requested.</span></span> <span data-ttu-id="36902-889">Pola cs uristem w oryginalnej dziennika.</span><span class="sxs-lookup"><span data-stu-id="36902-889">The cs-uristem field in the original log.</span></span> |
| <span data-ttu-id="36902-890">csUriQuery</span><span class="sxs-lookup"><span data-stu-id="36902-890">csUriQuery</span></span> |<span data-ttu-id="36902-891">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-891">W3CIISLog</span></span> |<span data-ttu-id="36902-892">Zapytanie URI.</span><span class="sxs-lookup"><span data-stu-id="36902-892">URI query.</span></span> <span data-ttu-id="36902-893">Identyfikator URI zapytania są niezbędne tylko w przypadku stron dynamicznych, takich jak strony ASP, więc to pole zawiera zwykle łącznika dla strony statyczne.</span><span class="sxs-lookup"><span data-stu-id="36902-893">URI queries are necessary only for dynamic pages, such as ASP pages, so this field usually contains a hyphen for static pages.</span></span> |
| <span data-ttu-id="36902-894">sPort</span><span class="sxs-lookup"><span data-stu-id="36902-894">sPort</span></span> |<span data-ttu-id="36902-895">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-895">W3CIISLog</span></span> |<span data-ttu-id="36902-896">Port serwera, który żądanie HTTP zostało wysłane do (i który program IIS nasłuchuje, ponieważ jej pobrania go).</span><span class="sxs-lookup"><span data-stu-id="36902-896">Server port that the HTTP request was sent to (and that IIS listens to, since it picked it up).</span></span> |
| <span data-ttu-id="36902-897">csUserName</span><span class="sxs-lookup"><span data-stu-id="36902-897">csUserName</span></span> |<span data-ttu-id="36902-898">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-898">W3CIISLog</span></span> |<span data-ttu-id="36902-899">Uwierzytelnić nazwę użytkownika, jeśli żądanie jest uwierzytelniane i nie anonimowe.</span><span class="sxs-lookup"><span data-stu-id="36902-899">Authenticated user name, if the request is authenticated and not anonymous.</span></span> |
| <span data-ttu-id="36902-900">csVersion</span><span class="sxs-lookup"><span data-stu-id="36902-900">csVersion</span></span> |<span data-ttu-id="36902-901">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-901">W3CIISLog</span></span> |<span data-ttu-id="36902-902">Wersja protokołu HTTP użyty w żądaniu (na przykład HTTP/1.1).</span><span class="sxs-lookup"><span data-stu-id="36902-902">HTTP Protocol version used in the request (for example, HTTP/1.1).</span></span> |
| <span data-ttu-id="36902-903">csCookie</span><span class="sxs-lookup"><span data-stu-id="36902-903">csCookie</span></span> |<span data-ttu-id="36902-904">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-904">W3CIISLog</span></span> |<span data-ttu-id="36902-905">Informacje dotyczące pliku cookie.</span><span class="sxs-lookup"><span data-stu-id="36902-905">Cookie information.</span></span> |
| <span data-ttu-id="36902-906">csReferer</span><span class="sxs-lookup"><span data-stu-id="36902-906">csReferer</span></span> |<span data-ttu-id="36902-907">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-907">W3CIISLog</span></span> |<span data-ttu-id="36902-908">Witryna ostatnio odwiedzona przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="36902-908">Site that the user last visited.</span></span> <span data-ttu-id="36902-909">Ta witryna udostępniła link do bieżącej lokacji.</span><span class="sxs-lookup"><span data-stu-id="36902-909">This site provided a link to the current site.</span></span> |
| <span data-ttu-id="36902-910">csHost</span><span class="sxs-lookup"><span data-stu-id="36902-910">csHost</span></span> |<span data-ttu-id="36902-911">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-911">W3CIISLog</span></span> |<span data-ttu-id="36902-912">Nagłówek hosta (na przykład www.mysite.com) żądanego.</span><span class="sxs-lookup"><span data-stu-id="36902-912">Host header (for example, www.mysite.com) that was requested.</span></span> |
| <span data-ttu-id="36902-913">scSubStatus</span><span class="sxs-lookup"><span data-stu-id="36902-913">scSubStatus</span></span> |<span data-ttu-id="36902-914">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-914">W3CIISLog</span></span> |<span data-ttu-id="36902-915">Kod błędu podstanu.</span><span class="sxs-lookup"><span data-stu-id="36902-915">Substatus error code.</span></span> |
| <span data-ttu-id="36902-916">scWin32Status</span><span class="sxs-lookup"><span data-stu-id="36902-916">scWin32Status</span></span> |<span data-ttu-id="36902-917">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-917">W3CIISLog</span></span> |<span data-ttu-id="36902-918">Kod stanu systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="36902-918">Windows status code.</span></span> |
| <span data-ttu-id="36902-919">csBytes</span><span class="sxs-lookup"><span data-stu-id="36902-919">csBytes</span></span> |<span data-ttu-id="36902-920">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-920">W3CIISLog</span></span> |<span data-ttu-id="36902-921">Liczba bajtów wysłanych w żądaniu od klienta do serwera.</span><span class="sxs-lookup"><span data-stu-id="36902-921">Bytes sent in the request from the client to the server.</span></span> |
| <span data-ttu-id="36902-922">scBytes</span><span class="sxs-lookup"><span data-stu-id="36902-922">scBytes</span></span> |<span data-ttu-id="36902-923">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="36902-923">W3CIISLog</span></span> |<span data-ttu-id="36902-924">Liczba bajtów zwrócona w odpowiedzi z serwera do klienta.</span><span class="sxs-lookup"><span data-stu-id="36902-924">Bytes returned back in the response from the server to the client.</span></span> |
| <span data-ttu-id="36902-925">ConfigChangeType</span><span class="sxs-lookup"><span data-stu-id="36902-925">ConfigChangeType</span></span> |<span data-ttu-id="36902-926">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-926">ConfigurationChange</span></span> |<span data-ttu-id="36902-927">Typ zmiany (na przykład WindowsServices/oprogramowania).</span><span class="sxs-lookup"><span data-stu-id="36902-927">Type of change (for example, WindowsServices/Software).</span></span> |
| <span data-ttu-id="36902-928">ChangeCategory</span><span class="sxs-lookup"><span data-stu-id="36902-928">ChangeCategory</span></span> |<span data-ttu-id="36902-929">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-929">ConfigurationChange</span></span> |<span data-ttu-id="36902-930">Kategoria zmiany (zmodyfikowane Added/usunięte).</span><span class="sxs-lookup"><span data-stu-id="36902-930">Category of the change (Modified/Added/Removed).</span></span> |
| <span data-ttu-id="36902-931">SoftwareType</span><span class="sxs-lookup"><span data-stu-id="36902-931">SoftwareType</span></span> |<span data-ttu-id="36902-932">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-932">ConfigurationChange</span></span> |<span data-ttu-id="36902-933">Typ oprogramowania (aplikacja/aktualizacji).</span><span class="sxs-lookup"><span data-stu-id="36902-933">Type of software (Update/Application).</span></span> |
| <span data-ttu-id="36902-934">SoftwareName</span><span class="sxs-lookup"><span data-stu-id="36902-934">SoftwareName</span></span> |<span data-ttu-id="36902-935">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-935">ConfigurationChange</span></span> |<span data-ttu-id="36902-936">Nazwa oprogramowania (dotyczy tylko zmiany oprogramowania).</span><span class="sxs-lookup"><span data-stu-id="36902-936">Name of the software (only applicable to software changes).</span></span> |
| <span data-ttu-id="36902-937">Wydawca</span><span class="sxs-lookup"><span data-stu-id="36902-937">Publisher</span></span> |<span data-ttu-id="36902-938">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-938">ConfigurationChange</span></span> |<span data-ttu-id="36902-939">Dostawcy, który publikuje oprogramowania (dotyczy tylko zmiany oprogramowania).</span><span class="sxs-lookup"><span data-stu-id="36902-939">Vendor who publishes the software (only applicable to software changes).</span></span> |
| <span data-ttu-id="36902-940">SvcChangeType</span><span class="sxs-lookup"><span data-stu-id="36902-940">SvcChangeType</span></span> |<span data-ttu-id="36902-941">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-941">ConfigurationChange</span></span> |<span data-ttu-id="36902-942">Typ zmiany, która została zastosowana na usługi systemu Windows (stan/StartupType/ścieżka/konto_usługi).</span><span class="sxs-lookup"><span data-stu-id="36902-942">Type of change that was applied on a Windows service (State/StartupType/Path/ServiceAccount).</span></span> <span data-ttu-id="36902-943">To ma zastosowanie tylko do zmiany usług systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="36902-943">This is only applicable to Windows service changes.</span></span> |
| <span data-ttu-id="36902-944">SvcDisplayName</span><span class="sxs-lookup"><span data-stu-id="36902-944">SvcDisplayName</span></span> |<span data-ttu-id="36902-945">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-945">ConfigurationChange</span></span> |<span data-ttu-id="36902-946">Nazwa wyświetlana usługi, która została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="36902-946">Display name of the service that was changed.</span></span> |
| <span data-ttu-id="36902-947">SvcName</span><span class="sxs-lookup"><span data-stu-id="36902-947">SvcName</span></span> |<span data-ttu-id="36902-948">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-948">ConfigurationChange</span></span> |<span data-ttu-id="36902-949">Nazwa usługi, która została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="36902-949">Name of the service that was changed.</span></span> |
| <span data-ttu-id="36902-950">SvcState</span><span class="sxs-lookup"><span data-stu-id="36902-950">SvcState</span></span> |<span data-ttu-id="36902-951">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-951">ConfigurationChange</span></span> |<span data-ttu-id="36902-952">Nowy (bieżący) stan usługi.</span><span class="sxs-lookup"><span data-stu-id="36902-952">New (current) state of the service.</span></span> |
| <span data-ttu-id="36902-953">SvcPreviousState</span><span class="sxs-lookup"><span data-stu-id="36902-953">SvcPreviousState</span></span> |<span data-ttu-id="36902-954">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-954">ConfigurationChange</span></span> |<span data-ttu-id="36902-955">Poprzedni znane stanie usługi (dotyczy tylko po zmianie stanu usługi).</span><span class="sxs-lookup"><span data-stu-id="36902-955">Previous known state of the service (only applicable if service state changed).</span></span> |
| <span data-ttu-id="36902-956">SvcStartupType</span><span class="sxs-lookup"><span data-stu-id="36902-956">SvcStartupType</span></span> |<span data-ttu-id="36902-957">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-957">ConfigurationChange</span></span> |<span data-ttu-id="36902-958">Typ uruchomienia usługi.</span><span class="sxs-lookup"><span data-stu-id="36902-958">Service startup type.</span></span> |
| <span data-ttu-id="36902-959">SvcPreviousStartupType</span><span class="sxs-lookup"><span data-stu-id="36902-959">SvcPreviousStartupType</span></span> |<span data-ttu-id="36902-960">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-960">ConfigurationChange</span></span> |<span data-ttu-id="36902-961">Poprzedni typ uruchamiania usługi (dotyczy tylko po zmianie typ uruchomienia usługi).</span><span class="sxs-lookup"><span data-stu-id="36902-961">Previous service startup type (only applicable if service startup type changed).</span></span> |
| <span data-ttu-id="36902-962">SvcAccount</span><span class="sxs-lookup"><span data-stu-id="36902-962">SvcAccount</span></span> |<span data-ttu-id="36902-963">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-963">ConfigurationChange</span></span> |<span data-ttu-id="36902-964">Konto usługi.</span><span class="sxs-lookup"><span data-stu-id="36902-964">Service account.</span></span> |
| <span data-ttu-id="36902-965">SvcPreviousAccount</span><span class="sxs-lookup"><span data-stu-id="36902-965">SvcPreviousAccount</span></span> |<span data-ttu-id="36902-966">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-966">ConfigurationChange</span></span> |<span data-ttu-id="36902-967">Poprzedniego konta usługi (dotyczy tylko po zmianie konta usługi).</span><span class="sxs-lookup"><span data-stu-id="36902-967">Previous service account (only applicable if service account changed).</span></span> |
| <span data-ttu-id="36902-968">SvcPath</span><span class="sxs-lookup"><span data-stu-id="36902-968">SvcPath</span></span> |<span data-ttu-id="36902-969">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-969">ConfigurationChange</span></span> |<span data-ttu-id="36902-970">Ścieżka do pliku wykonywalnego usługi systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="36902-970">Path to the executable of the Windows service.</span></span> |
| <span data-ttu-id="36902-971">SvcPreviousPath</span><span class="sxs-lookup"><span data-stu-id="36902-971">SvcPreviousPath</span></span> |<span data-ttu-id="36902-972">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-972">ConfigurationChange</span></span> |<span data-ttu-id="36902-973">Poprzednia ścieżka pliku wykonywalnego usługi systemu Windows (dotyczy tylko jego zmiana).</span><span class="sxs-lookup"><span data-stu-id="36902-973">Previous path of the executable for the Windows service (only applicable if it changed).</span></span> |
| <span data-ttu-id="36902-974">SvcDescription</span><span class="sxs-lookup"><span data-stu-id="36902-974">SvcDescription</span></span> |<span data-ttu-id="36902-975">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-975">ConfigurationChange</span></span> |<span data-ttu-id="36902-976">Opis usługi.</span><span class="sxs-lookup"><span data-stu-id="36902-976">Description of the service.</span></span> |
| <span data-ttu-id="36902-977">Poprzednie</span><span class="sxs-lookup"><span data-stu-id="36902-977">Previous</span></span> |<span data-ttu-id="36902-978">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-978">ConfigurationChange</span></span> |<span data-ttu-id="36902-979">Poprzedni stan tego oprogramowania (nie zainstalowano zainstalowana/poprzedniej wersji).</span><span class="sxs-lookup"><span data-stu-id="36902-979">Previous state of this software (Installed/Not Installed/previous version).</span></span> |
| <span data-ttu-id="36902-980">Bieżący</span><span class="sxs-lookup"><span data-stu-id="36902-980">Current</span></span> |<span data-ttu-id="36902-981">Zmianakonfiguracji</span><span class="sxs-lookup"><span data-stu-id="36902-981">ConfigurationChange</span></span> |<span data-ttu-id="36902-982">Najnowszy stan tego oprogramowania (nie zainstalowano zainstalowana/bieżącej wersji).</span><span class="sxs-lookup"><span data-stu-id="36902-982">Latest state of this software (Installed/Not Installed/current version).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="36902-983">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36902-983">Next steps</span></span>
<span data-ttu-id="36902-984">Aby uzyskać dodatkowe informacje dziennika wyszukiwania:</span><span class="sxs-lookup"><span data-stu-id="36902-984">For additional information about log searches:</span></span>

* <span data-ttu-id="36902-985">Zapoznaj się z [wyszukiwaniem w dziennikach](log-analytics-log-searches.md), aby wyświetlić szczegółowe informacje zebrane przez rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="36902-985">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span></span>
* <span data-ttu-id="36902-986">Użyj [pola niestandardowe w analizy dzienników](log-analytics-custom-fields.md) rozszerzenie dziennik wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="36902-986">Use [custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span></span>
