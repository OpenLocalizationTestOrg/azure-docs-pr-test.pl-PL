---
title: "aaaConstructing filtru ciągów dla projektanta tabel hello | Dokumentacja firmy Microsoft"
description: "Utworzenie filtru ciągów dla projektanta tabel hello"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a><span data-ttu-id="7da42-103">Konstruowanie ciągach filtru dla hello projektanta tabel</span><span class="sxs-lookup"><span data-stu-id="7da42-103">Constructing Filter Strings for hello Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="7da42-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7da42-104">Overview</span></span>
<span data-ttu-id="7da42-105">Visual Studio hello toofilter dane w tabeli platformy Azure, która jest wyświetlana w **projektanta tabel**, utworzyć ciąg filtru i wprowadzić go w polu filtru hello.</span><span class="sxs-lookup"><span data-stu-id="7da42-105">toofilter data in an Azure table that is displayed in hello Visual Studio **Table Designer**, you construct a filter string and enter it into hello filter field.</span></span> <span data-ttu-id="7da42-106">Składnia ciągu filtru Hello jest definiowana za pomocą hello usługi danych WCF i jest podobne tooa klauzuli SQL WHERE, ale są wysyłane toohello usługi tabel za pomocą żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="7da42-106">hello filter string syntax is defined by hello WCF Data Services and is similar tooa SQL WHERE clause, but is sent toohello Table service via an HTTP request.</span></span> <span data-ttu-id="7da42-107">Witaj **projektanta tabel** dojść hello kodowanie odpowiednie dla Ciebie tak toofilter na wartość żądanej właściwości, należy wprowadzić tylko nazwa właściwości hello, operator porównania wartości kryteriów i opcjonalnie można filtrować operator logiczny w hello pole.</span><span class="sxs-lookup"><span data-stu-id="7da42-107">hello **Table Designer** handles hello proper encoding for you, so toofilter on a desired property value, you need only enter hello property name, comparison operator, criteria value, and optionally, Boolean operator in hello filter field.</span></span> <span data-ttu-id="7da42-108">Nie ma potrzeby opcji zapytania hello $filter tooinclude, jak w przypadku, jeśli zostały tworzenia tabeli hello tooquery adresu URL za pośrednictwem hello [dokumentacja interfejsu API REST usług magazynu](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span><span class="sxs-lookup"><span data-stu-id="7da42-108">You do not need tooinclude hello $filter query option as you would if you were constructing a URL tooquery hello table via hello [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="7da42-109">Usługi danych WCF Hello są oparte na powitania [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span><span class="sxs-lookup"><span data-stu-id="7da42-109">hello WCF Data Services are based on hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="7da42-110">Szczegółowe informacje na temat opcji zapytania system filtru hello (**$filter**), zobacz hello [specyfikacji Konwencji identyfikatora URI OData](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span><span class="sxs-lookup"><span data-stu-id="7da42-110">For details on hello filter system query option (**$filter**), see hello [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="7da42-111">Operatory porównania</span><span class="sxs-lookup"><span data-stu-id="7da42-111">Comparison Operators</span></span>
<span data-ttu-id="7da42-112">Witaj następujące operatory logiczne są obsługiwane dla wszystkich typów właściwości:</span><span class="sxs-lookup"><span data-stu-id="7da42-112">hello following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="7da42-113">Operator logiczny</span><span class="sxs-lookup"><span data-stu-id="7da42-113">Logical operator</span></span> | <span data-ttu-id="7da42-114">Opis</span><span class="sxs-lookup"><span data-stu-id="7da42-114">Description</span></span> | <span data-ttu-id="7da42-115">Przykład ciąg filtru</span><span class="sxs-lookup"><span data-stu-id="7da42-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7da42-116">EQ</span><span class="sxs-lookup"><span data-stu-id="7da42-116">eq</span></span> |<span data-ttu-id="7da42-117">Równości</span><span class="sxs-lookup"><span data-stu-id="7da42-117">Equal</span></span> |<span data-ttu-id="7da42-118">Eq Miasto "Redmond"</span><span class="sxs-lookup"><span data-stu-id="7da42-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="7da42-119">gt</span><span class="sxs-lookup"><span data-stu-id="7da42-119">gt</span></span> |<span data-ttu-id="7da42-120">Więcej niż</span><span class="sxs-lookup"><span data-stu-id="7da42-120">Greater than</span></span> |<span data-ttu-id="7da42-121">Cena gt 20</span><span class="sxs-lookup"><span data-stu-id="7da42-121">Price gt 20</span></span> |
| <span data-ttu-id="7da42-122">GE</span><span class="sxs-lookup"><span data-stu-id="7da42-122">ge</span></span> |<span data-ttu-id="7da42-123">Większe lub równe zbyt</span><span class="sxs-lookup"><span data-stu-id="7da42-123">Greater than or equal too</span></span>|<span data-ttu-id="7da42-124">Cena ge 10</span><span class="sxs-lookup"><span data-stu-id="7da42-124">Price ge 10</span></span> |
| <span data-ttu-id="7da42-125">lt</span><span class="sxs-lookup"><span data-stu-id="7da42-125">lt</span></span> |<span data-ttu-id="7da42-126">Mniej niż</span><span class="sxs-lookup"><span data-stu-id="7da42-126">Less than</span></span> |<span data-ttu-id="7da42-127">Cena lt 20</span><span class="sxs-lookup"><span data-stu-id="7da42-127">Price lt 20</span></span> |
| <span data-ttu-id="7da42-128">le</span><span class="sxs-lookup"><span data-stu-id="7da42-128">le</span></span> |<span data-ttu-id="7da42-129">Mniejsze niż lub równe</span><span class="sxs-lookup"><span data-stu-id="7da42-129">Less than or equal</span></span> |<span data-ttu-id="7da42-130">Cena le 100</span><span class="sxs-lookup"><span data-stu-id="7da42-130">Price le 100</span></span> |
| <span data-ttu-id="7da42-131">ne</span><span class="sxs-lookup"><span data-stu-id="7da42-131">ne</span></span> |<span data-ttu-id="7da42-132">Nie ma wartości</span><span class="sxs-lookup"><span data-stu-id="7da42-132">Not equal</span></span> |<span data-ttu-id="7da42-133">Ne Miasto "Londyn"</span><span class="sxs-lookup"><span data-stu-id="7da42-133">City ne 'London'</span></span> |
| <span data-ttu-id="7da42-134">i</span><span class="sxs-lookup"><span data-stu-id="7da42-134">and</span></span> |<span data-ttu-id="7da42-135">I</span><span class="sxs-lookup"><span data-stu-id="7da42-135">And</span></span> |<span data-ttu-id="7da42-136">Cena le 200 i cen gt 3.5</span><span class="sxs-lookup"><span data-stu-id="7da42-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="7da42-137">lub</span><span class="sxs-lookup"><span data-stu-id="7da42-137">or</span></span> |<span data-ttu-id="7da42-138">Lub</span><span class="sxs-lookup"><span data-stu-id="7da42-138">Or</span></span> |<span data-ttu-id="7da42-139">Cena le 3.5 lub gt cen 200</span><span class="sxs-lookup"><span data-stu-id="7da42-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="7da42-140">nie</span><span class="sxs-lookup"><span data-stu-id="7da42-140">not</span></span> |<span data-ttu-id="7da42-141">nie</span><span class="sxs-lookup"><span data-stu-id="7da42-141">Not</span></span> |<span data-ttu-id="7da42-142">nie isAvailable</span><span class="sxs-lookup"><span data-stu-id="7da42-142">not isAvailable</span></span> |

<span data-ttu-id="7da42-143">Podczas konstruowania ciąg filtru, hello następujące reguły są ważne:</span><span class="sxs-lookup"><span data-stu-id="7da42-143">When constructing a filter string, hello following rules are important:</span></span>

* <span data-ttu-id="7da42-144">Użyj hello operatorów logicznych toocompare tooa wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="7da42-144">Use hello logical operators toocompare a property tooa value.</span></span> <span data-ttu-id="7da42-145">Należy pamiętać, że nie jest możliwe toocompare wartość dynamiczna tooa właściwości; po jednej stronie powitania wyrażenie musi być stałą.</span><span class="sxs-lookup"><span data-stu-id="7da42-145">Note that it is not possible toocompare a property tooa dynamic value; one side of hello expression must be a constant.</span></span>
* <span data-ttu-id="7da42-146">Wszystkie części hello ciąg filtru jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="7da42-146">All parts of hello filter string are case-sensitive.</span></span>
* <span data-ttu-id="7da42-147">musi być wartością stałą Hello hello tych samych danych typu jako właściwość hello aby hello filtru tooreturn prawidłowe wyniki.</span><span class="sxs-lookup"><span data-stu-id="7da42-147">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="7da42-148">Aby uzyskać więcej informacji na temat typów obsługiwanych właściwości zobacz [hello opis modelu danych usługi tabel](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span><span class="sxs-lookup"><span data-stu-id="7da42-148">For more information about supported property types, see [Understanding hello Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="7da42-149">Filtrowanie właściwości ciągu</span><span class="sxs-lookup"><span data-stu-id="7da42-149">Filtering on String Properties</span></span>
<span data-ttu-id="7da42-150">Podczas filtrowania na właściwości ciągów, ujmij stała ciąg hello w pojedynczy cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="7da42-150">When you filter on string properties, enclose hello string constant in single quotation marks.</span></span>

<span data-ttu-id="7da42-151">następujące przykładowe filtry na powitania Hello **PartitionKey** i **RowKey** właściwości; dodatkowe niekluczowych właściwości można również dodawać ciąg filtru toohello:</span><span class="sxs-lookup"><span data-stu-id="7da42-151">hello following example filters on hello **PartitionKey** and **RowKey** properties; additional non-key properties could also be added toohello filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="7da42-152">Każde wyrażenie filtru można ująć w nawiasach, chociaż nie jest to wymagane:</span><span class="sxs-lookup"><span data-stu-id="7da42-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="7da42-153">Zauważ, że hello usługi tabel nie obsługuje symboli wieloznacznych zapytań, i nie są obsługiwane w hello projektanta tabel albo.</span><span class="sxs-lookup"><span data-stu-id="7da42-153">Note that hello Table service does not support wildcard queries, and they are not supported in hello Table Designer either.</span></span> <span data-ttu-id="7da42-154">Można jednak wykonać Dopasowywanie przy użyciu operatorów na prefiksie żądaną hello prefiksów.</span><span class="sxs-lookup"><span data-stu-id="7da42-154">However, you can perform prefix matching by using comparison operators on hello desired prefix.</span></span> <span data-ttu-id="7da42-155">Witaj poniższy przykład zwraca jednostki z nazwisko właściwość rozpoczynająca się od litery hello "A":</span><span class="sxs-lookup"><span data-stu-id="7da42-155">hello following example returns entities with a LastName property beginning with hello letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="7da42-156">Filtrowanie właściwości liczbowych</span><span class="sxs-lookup"><span data-stu-id="7da42-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="7da42-157">toofilter na liczbą całkowitą lub liczba zmiennoprzecinkowa, określ numer hello bez znaków cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="7da42-157">toofilter on an integer or floating-point number, specify hello number without quotation marks.</span></span>

<span data-ttu-id="7da42-158">W tym przykładzie zwraca wszystkie jednostki z właściwością wieku, którego wartość jest większa niż 30:</span><span class="sxs-lookup"><span data-stu-id="7da42-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="7da42-159">W tym przykładzie zwraca wszystkie jednostki z właściwością AmountDue, którego wartość jest mniejsza niż lub równa too100.25:</span><span class="sxs-lookup"><span data-stu-id="7da42-159">This example returns all entities with an AmountDue property whose value is less than or equal too100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="7da42-160">Filtrowanie operatory logiczne</span><span class="sxs-lookup"><span data-stu-id="7da42-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="7da42-161">Określ toofilter na wartość logiczną **true** lub **false** bez znaków cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="7da42-161">toofilter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="7da42-162">Witaj poniższy przykład zwraca wszystkie jednostki którym hello IsActive właściwości ustawiono zbyt**true**:</span><span class="sxs-lookup"><span data-stu-id="7da42-162">hello following example returns all entities where hello IsActive property is set too**true**:</span></span>

    IsActive eq true

<span data-ttu-id="7da42-163">Można również napisać tego wyrażenia filtru bez hello operatora logicznego.</span><span class="sxs-lookup"><span data-stu-id="7da42-163">You can also write this filter expression without hello logical operator.</span></span> <span data-ttu-id="7da42-164">W hello poniższy przykład, hello usługi tabel zwrócone zostaną również wszystkie jednostki w przypadku IsActive **true**:</span><span class="sxs-lookup"><span data-stu-id="7da42-164">In hello following example, hello Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="7da42-165">wszystkie jednostki, w którym IsActive ma wartość false, można użyć hello nie tooreturn operator:</span><span class="sxs-lookup"><span data-stu-id="7da42-165">tooreturn all entities where IsActive is false, you can use hello not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="7da42-166">Filtrowanie właściwości daty i godziny</span><span class="sxs-lookup"><span data-stu-id="7da42-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="7da42-167">toofilter na wartość daty i godziny, określ hello **datetime** — słowo kluczowe, następuje hello Stała daty/godziny w pojedynczy cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="7da42-167">toofilter on a DateTime value, specify hello **datetime** keyword, followed by hello date/time constant in single quotation marks.</span></span> <span data-ttu-id="7da42-168">Stała daty/godziny Hello musi być w formacie UTC połączone, zgodnie z opisem w [formatowania wartości właściwości data/godzina](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span><span class="sxs-lookup"><span data-stu-id="7da42-168">hello date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="7da42-169">Hello poniższy przykład zwraca jednostki, w których właściwość CustomerSince hello jest tooJuly równy 10, 2008:</span><span class="sxs-lookup"><span data-stu-id="7da42-169">hello following example returns entities where hello CustomerSince property is equal tooJuly 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
