---
title: "Zasady usługi Azure CDN aparat wyrażeń warunkowych | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 57e56c38e003cb83dcf44f455c4451d159db8a59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="f922b-103">Zasady usługi Azure CDN aparat wyrażeń warunkowych</span><span class="sxs-lookup"><span data-stu-id="f922b-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="f922b-104">Ten temat zawiera szczegółowe opisy wyrażeń warunkowych dla usługi Azure sieci dostarczania zawartości (CDN) [aparatu reguł](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="f922b-104">This topic lists detailed descriptions of the Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="f922b-105">Pierwsza część reguły jest wyrażenia warunkowego.</span><span class="sxs-lookup"><span data-stu-id="f922b-105">The first part of a rule is the Conditional Expression.</span></span>

<span data-ttu-id="f922b-106">Wyrażenie warunkowe</span><span class="sxs-lookup"><span data-stu-id="f922b-106">Conditional Expression</span></span> | <span data-ttu-id="f922b-107">Opis</span><span class="sxs-lookup"><span data-stu-id="f922b-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="f922b-108">JEŚLI</span><span class="sxs-lookup"><span data-stu-id="f922b-108">IF</span></span> | <span data-ttu-id="f922b-109">Jeśli wyrażenie jest zawsze część pierwszą instrukcją w regule.</span><span class="sxs-lookup"><span data-stu-id="f922b-109">An IF expression is always a part of the first statement in a rule.</span></span> <span data-ttu-id="f922b-110">Podobnie jak wszystkie inne wyrażenia warunkowego tej instrukcji IF musi być skojarzony z dopasowania.</span><span class="sxs-lookup"><span data-stu-id="f922b-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="f922b-111">Jeśli są zdefiniowane nie dodatkowe wyrażenia warunkowego, tego dopasowania Określa kryterium, które muszą zostać spełnione przed zestaw funkcji można stosować na żądanie.</span><span class="sxs-lookup"><span data-stu-id="f922b-111">If no additional conditional expressions are defined, then this match determines the criterion that must be met before a set of features may be applied to a request.</span></span>
<span data-ttu-id="f922b-112">A JEŚLI</span><span class="sxs-lookup"><span data-stu-id="f922b-112">AND IF</span></span> | <span data-ttu-id="f922b-113">Wyrażenie IF i mogą być dodane tylko po następujących typów wyrażenia warunkowe: IF, i jeśli.</span><span class="sxs-lookup"><span data-stu-id="f922b-113">An AND IF expression may only be added after the following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="f922b-114">Wskazuje on, istnieje inny warunek, które muszą zostać spełnione dla początkowego instrukcji IF.</span><span class="sxs-lookup"><span data-stu-id="f922b-114">It indicates that there is another condition that must be met for the initial IF statement.</span></span>
<span data-ttu-id="f922b-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="f922b-115">ELSE IF</span></span>| <span data-ttu-id="f922b-116">Wyrażenia ELSE IF określa warunek alternatywną, na którym muszą zostać spełnione przed dokonaniem zestaw funkcji specyficznych dla tej instrukcji ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="f922b-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific to this ELSE IF statement takes place.</span></span> <span data-ttu-id="f922b-117">Obecność instrukcji ELSE IF wskazuje koniec poprzednią instrukcję.</span><span class="sxs-lookup"><span data-stu-id="f922b-117">The presence of an ELSE IF statement indicates the end of the previous statement.</span></span> <span data-ttu-id="f922b-118">Wyrażenie warunkowe tylko może być umieszczany po instrukcji ELSE IF innej instrukcji ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="f922b-118">The only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="f922b-119">Oznacza to, że instrukcji ELSE IF tylko można użyć do określenia jednego warunku dodatkowe, który ma zostać spełnione.</span><span class="sxs-lookup"><span data-stu-id="f922b-119">This means that an ELSE IF statement may only be used to specify a single additional condition that has to be met.</span></span>

<span data-ttu-id="f922b-120">**Przykład**: ![CDN zgodne z warunkiem](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="f922b-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="f922b-121">Kolejne reguły mogą zastąpić akcje określone przez poprzednie reguły.</span><span class="sxs-lookup"><span data-stu-id="f922b-121">A subsequent rule may override the actions specified by a previous rule.</span></span> <span data-ttu-id="f922b-122">Przykład: Reguła wychwytywania chroni wszystkie żądania przy użyciu uwierzytelniania opartego na tokenie.</span><span class="sxs-lookup"><span data-stu-id="f922b-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="f922b-123">Inną regułę można tworzyć bezpośrednio poniżej, aby utworzyć wyjątek dla niektórych typów żądań.</span><span class="sxs-lookup"><span data-stu-id="f922b-123">Another rule may be created directly below it to make an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="f922b-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f922b-124">Next steps</span></span>
* [<span data-ttu-id="f922b-125">Omówienie usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f922b-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="f922b-126">Odwołanie do aparatu reguł</span><span class="sxs-lookup"><span data-stu-id="f922b-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="f922b-127">Warunki uzgadniania aparatu reguł</span><span class="sxs-lookup"><span data-stu-id="f922b-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="f922b-128">Funkcje aparatu reguł</span><span class="sxs-lookup"><span data-stu-id="f922b-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="f922b-129">Zastępowanie domyślnego zachowania HTTP przy użyciu aparatu reguł</span><span class="sxs-lookup"><span data-stu-id="f922b-129">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
