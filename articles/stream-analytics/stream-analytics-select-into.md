---
title: "Azure Stream Analytics aaaDebug zapytania przy użyciu SELECT INTO | Dokumentacja firmy Microsoft"
description: "Przykładowe zapytanie pośredniej danych przy użyciu instrukcji SELECT INTO w analiza strumienia"
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="f6af2-103">Debugowania zapytania przy użyciu instrukcji SELECT INTO</span><span class="sxs-lookup"><span data-stu-id="f6af2-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="f6af2-104">Podczas przetwarzania danych w czasie rzeczywistym wiedząc, jakie dane hello wygląda w środku hello hello zapytania mogą być pomocne.</span><span class="sxs-lookup"><span data-stu-id="f6af2-104">In real-time data processing, knowing what hello data looks like in hello middle of hello query can be helpful.</span></span> <span data-ttu-id="f6af2-105">Ponieważ dane wejściowe lub kroki zadanie usługi analiza strumienia Azure może zostać odczytany wiele razy, można napisać dodatkowy instrukcji SELECT INTO.</span><span class="sxs-lookup"><span data-stu-id="f6af2-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="f6af2-106">Dzięki temu generuje pośrednich danych do magazynu i można sprawdzić poprawności hello hello danych, podobnie jak *Obejrzyj zmienne* czy podczas debugowania programu.</span><span class="sxs-lookup"><span data-stu-id="f6af2-106">Doing so outputs intermediate data into storage and lets you inspect hello correctness of hello data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-toocheck-hello-data-stream"></a><span data-ttu-id="f6af2-107">Użyj SELECT INTO toocheck hello strumienia danych</span><span class="sxs-lookup"><span data-stu-id="f6af2-107">Use SELECT INTO toocheck hello data stream</span></span>

<span data-ttu-id="f6af2-108">Hello następujące przykładowe zapytanie do zadania usługi analiza strumienia Azure ma jednego strumienia danych wejściowych, dwóch parametrów wejściowych danych odwołania, a dane wyjściowe tooAzure magazynu tabel.</span><span class="sxs-lookup"><span data-stu-id="f6af2-108">hello following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output tooAzure Table Storage.</span></span> <span data-ttu-id="f6af2-109">Zapytanie Hello łączy dane z Centrum zdarzeń hello i dwa obiekty BLOB tooget hello nazwą i kategorią informacje:</span><span class="sxs-lookup"><span data-stu-id="f6af2-109">hello query joins data from hello event hub and two reference blobs tooget hello name and category information:</span></span>

![Przykładowe zapytanie SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="f6af2-111">Należy pamiętać, że hello zadanie jest uruchomione, ale żadne zdarzenia nie są tworzonym w danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="f6af2-111">Note that hello job is running, but no events are being produced in hello output.</span></span> <span data-ttu-id="f6af2-112">Na powitania **monitorowanie** kafelka, w tym miejscu pokazano widać, że dane wejściowe hello jest zwracające dane, ale nie wiadomo, który krok hello **JOIN** spowodowane hello wszystkie zdarzenia toobe porzucony.</span><span class="sxs-lookup"><span data-stu-id="f6af2-112">On hello **Monitoring** tile, shown here, you can see that hello input is producing data, but you don’t know which step of hello **JOIN** caused all hello events toobe dropped.</span></span>

![Kafelek monitorowanie Hello](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="f6af2-114">W takiej sytuacji można dodać kilka dodatkowych instrukcji SELECT INTO zbyt "" hello pośrednich wyników sprzężenia i dziennika hello dane, które są odczytywane z danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="f6af2-114">In this situation, you can add a few extra SELECT INTO statements too“log” hello intermediate JOIN results and hello data that's read from hello input.</span></span>

<span data-ttu-id="f6af2-115">W tym przykładzie dodano dwa nowe "tymczasowego danych wyjściowych."</span><span class="sxs-lookup"><span data-stu-id="f6af2-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="f6af2-116">Mogą to być wszystkie zbiornika, który chcesz.</span><span class="sxs-lookup"><span data-stu-id="f6af2-116">They can be any sink you like.</span></span> <span data-ttu-id="f6af2-117">W tym miejscu używamy usługi Azure Storage, na przykład:</span><span class="sxs-lookup"><span data-stu-id="f6af2-117">Here we use Azure Storage as an example:</span></span>

![Dodawanie dodatkowych instrukcji SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="f6af2-119">Następnie można ponownie napisać zapytanie hello następująco:</span><span class="sxs-lookup"><span data-stu-id="f6af2-119">You can then rewrite hello query like this:</span></span>

![Ponownie zapisane zapytanie SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="f6af2-121">Teraz ponownie uruchomić zadanie hello i pozwól mu Uruchom kilka minut.</span><span class="sxs-lookup"><span data-stu-id="f6af2-121">Now start hello job again, and let it run for a few minutes.</span></span> <span data-ttu-id="f6af2-122">Następnie zbadać temp1 i temp2 za pomocą programu Visual Studio Cloud Explorer tooproduce hello następujących tabel:</span><span class="sxs-lookup"><span data-stu-id="f6af2-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer tooproduce hello following tables:</span></span>

<span data-ttu-id="f6af2-123">**Tabela temp1**
![SELECT INTO tabeli temp1](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="f6af2-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="f6af2-124">**Tabela temp2**
![SELECT INTO tabeli temp2](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="f6af2-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="f6af2-125">Jak widać, temp1 i temp2 znajdują się dane, a w temp2 hello w kolumnie Nazwa została wpisana poprawnie.</span><span class="sxs-lookup"><span data-stu-id="f6af2-125">As you can see, temp1 and temp2 both have data, and hello name column is populated correctly in temp2.</span></span> <span data-ttu-id="f6af2-126">Jednak ponieważ nie jeszcze żadnych danych w danych wyjściowych, element jest nieprawidłowy:</span><span class="sxs-lookup"><span data-stu-id="f6af2-126">However, because there is still no data in output, something is wrong:</span></span>

![Wybierz do tabeli output1 bez danych](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="f6af2-128">Poprzez próbkowanie hello danych, można prawie pewność, że problem hello jest z hello drugie sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="f6af2-128">By sampling hello data, you can be almost certain that hello issue is with hello second JOIN.</span></span> <span data-ttu-id="f6af2-129">Można pobrać danych referencyjnych hello z obiektu blob hello i zapoznaj się z:</span><span class="sxs-lookup"><span data-stu-id="f6af2-129">You can download hello reference data from hello blob and take a look:</span></span>

![Wybierz do tabeli referencyjnej](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="f6af2-131">Jak widać, format hello hello identyfikator GUID w tym danych referencyjnych różni się od formatu hello hello [z] kolumny temp2.</span><span class="sxs-lookup"><span data-stu-id="f6af2-131">As you can see, hello format of hello GUID in this reference data is different from hello format of hello [from] column in temp2.</span></span> <span data-ttu-id="f6af2-132">Dlatego hello danych nie zostało dostarczone w output1 zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="f6af2-132">That’s why hello data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="f6af2-133">Można rozwiązać hello format danych, przekaż go tooreference obiektów blob i spróbuj ponownie:</span><span class="sxs-lookup"><span data-stu-id="f6af2-133">You can fix hello data format, upload it tooreference blob, and try again:</span></span>

![Wybierz do tabeli tymczasowej](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="f6af2-135">Ten czas danych hello w danych wyjściowych hello jest sformatowany i wypełniane zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="f6af2-135">This time, hello data in hello output is formatted and populated as expected.</span></span>

![Wybierz do tabeli końcowej](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="f6af2-137">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="f6af2-137">Get help</span></span>

<span data-ttu-id="f6af2-138">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="f6af2-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6af2-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6af2-139">Next steps</span></span>

* [<span data-ttu-id="f6af2-140">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="f6af2-140">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f6af2-141">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f6af2-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f6af2-142">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f6af2-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f6af2-143">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f6af2-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f6af2-144">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f6af2-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

