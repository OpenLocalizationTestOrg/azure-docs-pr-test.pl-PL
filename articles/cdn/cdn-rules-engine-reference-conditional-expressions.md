---
title: "wyrażenia warunkowe aparatu reguł aaaAzure CDN | Dokumentacja firmy Microsoft"
description: "Dokumentacja referencyjna dla usługi Azure CDN zasady warunków dopasowania aparatu i funkcje."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="065f7-103">Zasady usługi Azure CDN aparat wyrażeń warunkowych</span><span class="sxs-lookup"><span data-stu-id="065f7-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="065f7-104">Ten temat zawiera szczegółowe opisy hello wyrażenia warunkowego dla usługi Azure sieci dostarczania zawartości (CDN) [aparatu reguł](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="065f7-104">This topic lists detailed descriptions of hello Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="065f7-105">Pierwsza część reguły Hello jest hello wyrażenia warunkowego.</span><span class="sxs-lookup"><span data-stu-id="065f7-105">hello first part of a rule is hello Conditional Expression.</span></span>

<span data-ttu-id="065f7-106">Wyrażenie warunkowe</span><span class="sxs-lookup"><span data-stu-id="065f7-106">Conditional Expression</span></span> | <span data-ttu-id="065f7-107">Opis</span><span class="sxs-lookup"><span data-stu-id="065f7-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="065f7-108">JEŚLI</span><span class="sxs-lookup"><span data-stu-id="065f7-108">IF</span></span> | <span data-ttu-id="065f7-109">Jeśli wyrażenie jest zawsze część hello pierwszą instrukcją w regule.</span><span class="sxs-lookup"><span data-stu-id="065f7-109">An IF expression is always a part of hello first statement in a rule.</span></span> <span data-ttu-id="065f7-110">Podobnie jak wszystkie inne wyrażenia warunkowego tej instrukcji IF musi być skojarzony z dopasowania.</span><span class="sxs-lookup"><span data-stu-id="065f7-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="065f7-111">Jeśli są zdefiniowane nie dodatkowe wyrażenia warunkowego, tego dopasowania określa hello kryterium, które muszą zostać spełnione przed zestawem funkcji mogą być zastosowane tooa żądania.</span><span class="sxs-lookup"><span data-stu-id="065f7-111">If no additional conditional expressions are defined, then this match determines hello criterion that must be met before a set of features may be applied tooa request.</span></span>
<span data-ttu-id="065f7-112">A JEŚLI</span><span class="sxs-lookup"><span data-stu-id="065f7-112">AND IF</span></span> | <span data-ttu-id="065f7-113">Wyrażenie IF i mogą być dodane tylko po hello następujące typy wyrażenia warunkowe: IF, i jeśli.</span><span class="sxs-lookup"><span data-stu-id="065f7-113">An AND IF expression may only be added after hello following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="065f7-114">Go wskazuje, że istnieje inny warunek, które należy spełnić, aby hello początkowego instrukcji IF.</span><span class="sxs-lookup"><span data-stu-id="065f7-114">It indicates that there is another condition that must be met for hello initial IF statement.</span></span>
<span data-ttu-id="065f7-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="065f7-115">ELSE IF</span></span>| <span data-ttu-id="065f7-116">Wyrażenia ELSE IF określa warunek alternatywną, na którym muszą zostać spełnione przed dokonaniem zestaw funkcji określonych toothis instrukcji ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="065f7-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific toothis ELSE IF statement takes place.</span></span> <span data-ttu-id="065f7-117">obecność Hello instrukcji ELSE IF wskazuje koniec hello hello poprzednią instrukcję.</span><span class="sxs-lookup"><span data-stu-id="065f7-117">hello presence of an ELSE IF statement indicates hello end of hello previous statement.</span></span> <span data-ttu-id="065f7-118">Witaj wyrażenia warunkowego tylko może być umieszczany po instrukcji ELSE IF innej instrukcji ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="065f7-118">hello only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="065f7-119">Oznacza to, że instrukcji ELSE IF mogą być tylko używana toospecify pojedynczy warunek dodatkowe ma toobe spełnione.</span><span class="sxs-lookup"><span data-stu-id="065f7-119">This means that an ELSE IF statement may only be used toospecify a single additional condition that has toobe met.</span></span>

<span data-ttu-id="065f7-120">**Przykład**: ![CDN zgodne z warunkiem](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="065f7-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="065f7-121">Kolejne reguły mogą zastąpić akcje hello określone przez poprzednie reguły.</span><span class="sxs-lookup"><span data-stu-id="065f7-121">A subsequent rule may override hello actions specified by a previous rule.</span></span> <span data-ttu-id="065f7-122">Przykład: Reguła wychwytywania chroni wszystkie żądania przy użyciu uwierzytelniania opartego na tokenie.</span><span class="sxs-lookup"><span data-stu-id="065f7-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="065f7-123">Można tworzyć bezpośrednio pod inną regułę toomake wyjątków dla określonych typów żądań.</span><span class="sxs-lookup"><span data-stu-id="065f7-123">Another rule may be created directly below it toomake an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="065f7-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="065f7-124">Next steps</span></span>
* [<span data-ttu-id="065f7-125">Omówienie usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="065f7-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="065f7-126">Odwołanie do aparatu reguł</span><span class="sxs-lookup"><span data-stu-id="065f7-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="065f7-127">Warunki uzgadniania aparatu reguł</span><span class="sxs-lookup"><span data-stu-id="065f7-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="065f7-128">Funkcje aparatu reguł</span><span class="sxs-lookup"><span data-stu-id="065f7-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="065f7-129">Zastępowanie domyślnego zachowania HTTP przy użyciu aparatu reguł hello</span><span class="sxs-lookup"><span data-stu-id="065f7-129">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
