---
title: "Użyj usługi Azure Stream Analytics z usługą Magazyn danych SQL | Dokumentacja firmy Microsoft"
description: "Porady dotyczące korzystania z usługi Azure Stream Analytics z usługą Magazyn danych SQL Azure związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 14783f0464764a11d7f03a5db1c2d63728a4cb50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="9ffa4-103">Użyj usługi Azure Stream Analytics z usługą Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="9ffa4-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="9ffa4-104">Usługa Azure Stream Analytics to w pełni zarządzana usługa dostarczanie przetwarzanie złożonych zdarzeń małe opóźnienia, skalowalne, wysoko dostępne za pośrednictwem przesyłania strumieniowego danych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="9ffa4-105">Dowiedz się podstawy odczytując [wprowadzenie do usługi Azure Stream Analytics][Introduction to Azure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="9ffa4-105">You can learn the basics by reading [Introduction to Azure Stream Analytics][Introduction to Azure Stream Analytics].</span></span> <span data-ttu-id="9ffa4-106">Następnie Dowiedz się jak utworzyć rozwiązanie end-to-end z usługi Stream Analytics, postępując [rozpocząć korzystanie z usługi Azure Stream Analytics] [ Get started using Azure Stream Analytics] samouczka.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-106">You can then learn how to create an end-to-end solution with Stream Analytics by following the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="9ffa4-107">W tym artykule dowiesz się, jak używać bazy danych Azure SQL Data Warehouse ujściem danych wyjściowych dla zadań para analiza.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-107">In this article, you will learn how to use your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ffa4-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9ffa4-108">Prerequisites</span></span>
<span data-ttu-id="9ffa4-109">Najpierw uruchom poniższe kroki w [rozpocząć korzystanie z usługi Azure Stream Analytics] [ Get started using Azure Stream Analytics] samouczka.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-109">First, run through the following steps in the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="9ffa4-110">Tworzenie Centrum zdarzeń dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="9ffa4-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="9ffa4-111">Skonfiguruj i uruchom aplikację generator zdarzeń</span><span class="sxs-lookup"><span data-stu-id="9ffa4-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="9ffa4-112">Zainicjuj obsługę zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="9ffa4-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="9ffa4-113">Określ dane wejściowe zadania i zapytanie</span><span class="sxs-lookup"><span data-stu-id="9ffa4-113">Specify job input and query</span></span>

<span data-ttu-id="9ffa4-114">Następnie utwórz bazę danych magazynu danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9ffa4-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="9ffa4-115">Określ dane wyjściowe zadania: baza danych Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9ffa4-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="9ffa4-116">Krok 1</span><span class="sxs-lookup"><span data-stu-id="9ffa4-116">Step 1</span></span>
<span data-ttu-id="9ffa4-117">W przypadku zadania Stream Analytics kliknij **dane wyjściowe** w górnej części strony, a następnie kliknij przycisk **dodać danych wyjściowych**.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-117">In your Stream Analytics job click **OUTPUT** from the top of the page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="9ffa4-118">Krok 2</span><span class="sxs-lookup"><span data-stu-id="9ffa4-118">Step 2</span></span>
<span data-ttu-id="9ffa4-119">Wybierz bazę danych SQL, a następnie kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="9ffa4-120">Krok 3</span><span class="sxs-lookup"><span data-stu-id="9ffa4-120">Step 3</span></span>
<span data-ttu-id="9ffa4-121">Na następnej stronie, wprowadź następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-121">Enter the following values on the next page:</span></span>

* <span data-ttu-id="9ffa4-122">*Dane wyjściowe Alias*: Wprowadź przyjazną nazwę dla danych wyjściowych tego zadania.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="9ffa4-123">*Subskrypcja*:</span><span class="sxs-lookup"><span data-stu-id="9ffa4-123">*Subscription*:</span></span>
  * <span data-ttu-id="9ffa4-124">Jeśli w bazie danych magazynu danych SQL jest w tej samej subskrypcji co zadanie usługi Stream Analytics, wybierz opcję Użyj bazy danych SQL z bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-124">If your SQL Data Warehouse database is in the same subscription as the Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="9ffa4-125">Jeśli baza danych jest w innej subskrypcji, wybierz Użyj bazy danych SQL z innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="9ffa4-126">*Baza danych*: Określ nazwę docelowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-126">*Database*: Specify the name of a destination database.</span></span>
* <span data-ttu-id="9ffa4-127">*Nazwa serwera*: Określ nazwę serwera bazy danych, właśnie zostało określone.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-127">*Server Name*: Specify the server name for the database you just specified.</span></span> <span data-ttu-id="9ffa4-128">Aby znaleźć tę wartość, można użyć klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-128">You can use the Azure Classic Portal to find this.</span></span>

![][server-name]

* <span data-ttu-id="9ffa4-129">*Nazwa użytkownika*: Określ nazwę użytkownika konta, które ma uprawnienia do zapisu dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-129">*User Name*: Specify the user name of an account that has write permissions for the database.</span></span>
* <span data-ttu-id="9ffa4-130">*Hasło*: Podaj hasło dla określonego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-130">*Password*: Provide the password for the specified user account.</span></span>
* <span data-ttu-id="9ffa4-131">*Tabela*: Określ nazwę tabeli docelowej w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-131">*Table*: Specify the name of the target table in the database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="9ffa4-132">Krok 4</span><span class="sxs-lookup"><span data-stu-id="9ffa4-132">Step 4</span></span>
<span data-ttu-id="9ffa4-133">Kliknij przycisk wyboru, aby dodać te dane wyjściowe zadania i sprawdzić, czy analiza strumienia może pomyślnie połączyć z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-133">Click the check button to add this job output and to verify that Stream Analytics can successfully connect to the database.</span></span>

![][test-connection]

<span data-ttu-id="9ffa4-134">Podczas połączenia z bazą danych zakończy się pomyślnie, zostanie wyświetlone powiadomienie w dolnej części portalu.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-134">When the connection to the database succeeds, you will see a notification at the bottom of the portal.</span></span> <span data-ttu-id="9ffa4-135">Możesz kliknąć Testuj połączenie na dole, aby przetestować połączenie z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="9ffa4-135">You can click Test Connection at the bottom to test the connection to the database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ffa4-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9ffa4-136">Next steps</span></span>
<span data-ttu-id="9ffa4-137">Omówienie integracji, zobacz [Omówienie integracji usługi SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="9ffa4-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="9ffa4-138">Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="9ffa4-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction to Azure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
