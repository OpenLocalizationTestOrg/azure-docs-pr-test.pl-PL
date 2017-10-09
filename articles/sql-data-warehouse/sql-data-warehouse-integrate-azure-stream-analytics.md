---
title: "aaaUse Azure Stream Analytics z usługą Magazyn danych SQL | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="97aa0-103">Użyj usługi Azure Stream Analytics z usługą Magazyn danych SQL</span><span class="sxs-lookup"><span data-stu-id="97aa0-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="97aa0-104">Usługa Azure Stream Analytics to w pełni zarządzana usługa dostarczanie przetwarzanie złożonych zdarzeń małe opóźnienia, skalowalne, wysoko dostępne za pośrednictwem przesyłania strumieniowego danych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="97aa0-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="97aa0-105">Dowiedz się podstawy hello odczytując [tooAzure wprowadzenie Stream Analytics][Introduction tooAzure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="97aa0-105">You can learn hello basics by reading [Introduction tooAzure Stream Analytics][Introduction tooAzure Stream Analytics].</span></span> <span data-ttu-id="97aa0-106">Można następnie Dowiedz się jak hello toocreate rozwiązanie end-to-end z Stream Analytics, wykonując [rozpocząć korzystanie z usługi Azure Stream Analytics] [ Get started using Azure Stream Analytics] samouczka.</span><span class="sxs-lookup"><span data-stu-id="97aa0-106">You can then learn how toocreate an end-to-end solution with Stream Analytics by following hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="97aa0-107">W tym artykule dowiesz się, jak toouse Azure SQL Data Warehouse bazy danych dla zadań para analiza ujściem danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="97aa0-107">In this article, you will learn how toouse your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97aa0-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="97aa0-108">Prerequisites</span></span>
<span data-ttu-id="97aa0-109">Najpierw uruchom za pomocą hello następujące kroki w hello [rozpocząć korzystanie z usługi Azure Stream Analytics] [ Get started using Azure Stream Analytics] samouczka.</span><span class="sxs-lookup"><span data-stu-id="97aa0-109">First, run through hello following steps in hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="97aa0-110">Tworzenie Centrum zdarzeń dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="97aa0-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="97aa0-111">Skonfiguruj i uruchom aplikację generator zdarzeń</span><span class="sxs-lookup"><span data-stu-id="97aa0-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="97aa0-112">Zainicjuj obsługę zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="97aa0-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="97aa0-113">Określ dane wejściowe zadania i zapytanie</span><span class="sxs-lookup"><span data-stu-id="97aa0-113">Specify job input and query</span></span>

<span data-ttu-id="97aa0-114">Następnie utwórz bazę danych magazynu danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="97aa0-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="97aa0-115">Określ dane wyjściowe zadania: baza danych Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="97aa0-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="97aa0-116">Krok 1</span><span class="sxs-lookup"><span data-stu-id="97aa0-116">Step 1</span></span>
<span data-ttu-id="97aa0-117">W przypadku zadania Stream Analytics kliknij **dane wyjściowe** od góry hello hello strony, a następnie kliknij przycisk **dodać danych wyjściowych**.</span><span class="sxs-lookup"><span data-stu-id="97aa0-117">In your Stream Analytics job click **OUTPUT** from hello top of hello page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="97aa0-118">Krok 2</span><span class="sxs-lookup"><span data-stu-id="97aa0-118">Step 2</span></span>
<span data-ttu-id="97aa0-119">Wybierz bazę danych SQL, a następnie kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="97aa0-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="97aa0-120">Krok 3</span><span class="sxs-lookup"><span data-stu-id="97aa0-120">Step 3</span></span>
<span data-ttu-id="97aa0-121">Wprowadź następujące wartości na następnej stronie powitania hello:</span><span class="sxs-lookup"><span data-stu-id="97aa0-121">Enter hello following values on hello next page:</span></span>

* <span data-ttu-id="97aa0-122">*Dane wyjściowe Alias*: Wprowadź przyjazną nazwę dla danych wyjściowych tego zadania.</span><span class="sxs-lookup"><span data-stu-id="97aa0-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="97aa0-123">*Subskrypcja*:</span><span class="sxs-lookup"><span data-stu-id="97aa0-123">*Subscription*:</span></span>
  * <span data-ttu-id="97aa0-124">Jeśli w bazie danych magazynu danych SQL jest w hello tej samej subskrypcji co zadanie usługi Stream Analytics hello, wybierz opcję użycia bazy danych SQL z bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="97aa0-124">If your SQL Data Warehouse database is in hello same subscription as hello Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="97aa0-125">Jeśli baza danych jest w innej subskrypcji, wybierz Użyj bazy danych SQL z innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="97aa0-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="97aa0-126">*Baza danych*: należy określić nazwę hello docelowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="97aa0-126">*Database*: Specify hello name of a destination database.</span></span>
* <span data-ttu-id="97aa0-127">*Nazwa serwera*: Określ nazwę serwera hello bazy danych hello właśnie zostało określone.</span><span class="sxs-lookup"><span data-stu-id="97aa0-127">*Server Name*: Specify hello server name for hello database you just specified.</span></span> <span data-ttu-id="97aa0-128">Możesz użyć hello toofind klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="97aa0-128">You can use hello Azure Classic Portal toofind this.</span></span>

![][server-name]

* <span data-ttu-id="97aa0-129">*Nazwa użytkownika*: Określ nazwę użytkownika konta, które ma uprawnienia do zapisu dla bazy danych hello hello.</span><span class="sxs-lookup"><span data-stu-id="97aa0-129">*User Name*: Specify hello user name of an account that has write permissions for hello database.</span></span>
* <span data-ttu-id="97aa0-130">*Hasło*: Podaj hasło hello hello określone konto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="97aa0-130">*Password*: Provide hello password for hello specified user account.</span></span>
* <span data-ttu-id="97aa0-131">*Tabela*: Określ nazwę tabeli docelowej hello hello w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="97aa0-131">*Table*: Specify hello name of hello target table in hello database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="97aa0-132">Krok 4</span><span class="sxs-lookup"><span data-stu-id="97aa0-132">Step 4</span></span>
<span data-ttu-id="97aa0-133">Kliknij przycisk tooadd przycisk wyboru hello, to dane wyjściowe zadania i tooverify, że analiza strumienia może pomyślnie połączyć toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="97aa0-133">Click hello check button tooadd this job output and tooverify that Stream Analytics can successfully connect toohello database.</span></span>

![][test-connection]

<span data-ttu-id="97aa0-134">Baza danych toohello połączenia hello zakończy się powodzeniem, zobaczysz powiadomienie u dołu hello hello portalu.</span><span class="sxs-lookup"><span data-stu-id="97aa0-134">When hello connection toohello database succeeds, you will see a notification at hello bottom of hello portal.</span></span> <span data-ttu-id="97aa0-135">W dolnej hello tootest połączenia hello toohello bazy danych można kliknij przycisk Testuj połączenie.</span><span class="sxs-lookup"><span data-stu-id="97aa0-135">You can click Test Connection at hello bottom tootest hello connection toohello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97aa0-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="97aa0-136">Next steps</span></span>
<span data-ttu-id="97aa0-137">Omówienie integracji, zobacz [Omówienie integracji usługi SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="97aa0-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="97aa0-138">Więcej porad dla deweloperów znajduje się w artykule [Omówienie programowania w usłudze SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="97aa0-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
