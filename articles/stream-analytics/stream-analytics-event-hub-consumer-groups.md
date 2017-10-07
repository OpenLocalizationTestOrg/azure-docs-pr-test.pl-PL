---
title: "aaaDebug Azure Stream Analytics z odbiorników Centrum zdarzeń | Dokumentacja firmy Microsoft"
description: "Zapytanie najlepsze rozwiązania dotyczące uwzględnieniu grupy konsumentów centra zdarzeń w zadania usługi analiza strumienia."
keywords: "limit Centrum zdarzeń, grupy odbiorców"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="48282-104">Debugowanie Azure Stream Analytics przy użyciu odbiorcy Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="48282-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="48282-105">Można użyć usługi Azure Event Hubs w danych tooingest lub dane wyjściowe z zadania usługi analiza strumienia Azure.</span><span class="sxs-lookup"><span data-stu-id="48282-105">You can use Azure Event Hubs in Azure Stream Analytics tooingest or output data from a job.</span></span> <span data-ttu-id="48282-106">Najlepsze rozwiązanie dotyczące korzystania z usługi Event Hubs jest toouse wiele grup odbiorców, tooensure zadania skalowalności.</span><span class="sxs-lookup"><span data-stu-id="48282-106">A best practice for using Event Hubs is toouse multiple consumer groups, tooensure job scalability.</span></span> <span data-ttu-id="48282-107">Jedną z przyczyn jest to, że hello liczbę czytników w zadaniu Stream Analytics hello na określone dane wejściowe ma wpływ na powitania liczbę czytników w grupie jednego konsumenta.</span><span class="sxs-lookup"><span data-stu-id="48282-107">One reason is that hello number of readers in hello Stream Analytics job for a specific input affects hello number of readers in a single consumer group.</span></span> <span data-ttu-id="48282-108">Hello dokładna liczba odbiorcy jest oparta na szczegóły implementacji wewnętrzny hello logiki topologii skalowalnego w poziomie.</span><span class="sxs-lookup"><span data-stu-id="48282-108">hello precise number of receivers is based on internal implementation details for hello scale-out topology logic.</span></span> <span data-ttu-id="48282-109">numer Hello odbiorników nie był widoczny zewnętrznie.</span><span class="sxs-lookup"><span data-stu-id="48282-109">hello number of receivers is not exposed externally.</span></span> <span data-ttu-id="48282-110">podczas uruchamiania zadania hello lub podczas uaktualniania zadania, można zmienić Hello liczbę czytników.</span><span class="sxs-lookup"><span data-stu-id="48282-110">hello number of readers can change either at hello job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="48282-111">Po zmianie podczas uaktualniania zadania hello liczbę czytników przejściowej ostrzeżenia są zapisywane tooaudit dzienniki.</span><span class="sxs-lookup"><span data-stu-id="48282-111">When hello number of readers changes during a job upgrade, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="48282-112">Zadania usługi analiza strumienia automatycznie odzyskać te przejściowych problemów.</span><span class="sxs-lookup"><span data-stu-id="48282-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="48282-113">Liczba czytników dla każdej partycji przekracza limit usługi Event Hubs pięć</span><span class="sxs-lookup"><span data-stu-id="48282-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="48282-114">Scenariusze, w których hello liczbę czytników dla każdej partycji przekracza limit usługi Event Hubs hello pięć Uwzględnij hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="48282-114">Scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five include hello following:</span></span>

* <span data-ttu-id="48282-115">Wiele instrukcji "SELECT": użycie wielu instrukcji SELECT, które odwołują się zbyt**tego samego** wprowadzania Centrum zdarzeń, każda instrukcja SELECT powoduje, że nowe toobe odbiornika utworzony.</span><span class="sxs-lookup"><span data-stu-id="48282-115">Multiple SELECT statements: If you use multiple SELECT statements that refer too**same** event hub input, each SELECT statement causes a new receiver toobe created.</span></span>
* <span data-ttu-id="48282-116">Unia: Użycie Unii, jest możliwe toohave wielu danych wejściowych, które odwołują się toohello **tego samego** grupy koncentratora i odbiorców zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="48282-116">UNION: When you use a UNION, it's possible toohave multiple inputs that refer toohello **same** event hub and consumer group.</span></span>
* <span data-ttu-id="48282-117">SAMOSPRZĘŻENIE: Korzystając z operacją JOIN SAMOOBSŁUGOWEGO, jest możliwe toorefer toohello **tego samego** Centrum zdarzeń wiele razy.</span><span class="sxs-lookup"><span data-stu-id="48282-117">SELF JOIN: When you use a SELF JOIN operation, it's possible toorefer toohello **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="48282-118">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="48282-118">Solution</span></span>

<span data-ttu-id="48282-119">Witaj następujące najlepsze rozwiązania może pomóc ograniczyć scenariusze, w których hello liczbę czytników dla każdej partycji przekracza limit usługi Event Hubs hello pięć.</span><span class="sxs-lookup"><span data-stu-id="48282-119">hello following best practices can help mitigate scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="48282-120">Podziel zapytanie na wielu kroków przy użyciu klauzuli WITH</span><span class="sxs-lookup"><span data-stu-id="48282-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="48282-121">Klauzula WITH Hello Określa tymczasowy nazwany zestaw wyników, który może odwoływać się klauzuli FROM w kwerendzie hello.</span><span class="sxs-lookup"><span data-stu-id="48282-121">hello WITH clause specifies a temporary named result set that can be referenced by a FROM clause in hello query.</span></span> <span data-ttu-id="48282-122">Klauzula WITH hello należy zdefiniować w zakresie wykonywania hello jednej instrukcji SELECT.</span><span class="sxs-lookup"><span data-stu-id="48282-122">You define hello WITH clause in hello execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="48282-123">Na przykład zamiast tego zapytania:</span><span class="sxs-lookup"><span data-stu-id="48282-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="48282-124">Skorzystaj z tej kwerendy:</span><span class="sxs-lookup"><span data-stu-id="48282-124">Use this query:</span></span>

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a><span data-ttu-id="48282-125">Upewnij się, że dane wejściowe powiązać toodifferent grupy konsumentów</span><span class="sxs-lookup"><span data-stu-id="48282-125">Ensure that inputs bind toodifferent consumer groups</span></span>

<span data-ttu-id="48282-126">Dla zapytania, w których co najmniej trzech dane wejściowe są połączone toohello konsumenta centra zdarzeń w tej samej grupy, tworzyć grupy konsumentów oddzielne.</span><span class="sxs-lookup"><span data-stu-id="48282-126">For queries in which three or more inputs are connected toohello same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="48282-127">Wymaga to tworzenie hello dodatkowe usługi analiza strumienia danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="48282-127">This requires hello creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="48282-128">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="48282-128">Get help</span></span>
<span data-ttu-id="48282-129">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="48282-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="48282-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="48282-130">Next steps</span></span>
* [<span data-ttu-id="48282-131">Wprowadzenie tooStream analityka</span><span class="sxs-lookup"><span data-stu-id="48282-131">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="48282-132">Wprowadzenie do usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="48282-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="48282-133">Zadania usługi analiza strumienia skali</span><span class="sxs-lookup"><span data-stu-id="48282-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="48282-134">Dokumentacja języka zapytania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="48282-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="48282-135">Strumienia Analytics management REST API reference</span><span class="sxs-lookup"><span data-stu-id="48282-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
