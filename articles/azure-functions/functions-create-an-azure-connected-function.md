---
title: "aaaCreate funkcję, która łączy się z usługami tooAzure | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Functions toocreate aplikację niekorzystającą, który łączy tooother Azure usługi."
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "usługa Azure Functions, funkcje, przetwarzanie zdarzeń, elementy webhook, obliczanie dynamiczne, architektura bez serwera"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a><span data-ttu-id="3f6eb-104">Użyj usługi Azure Functions toocreate funkcję, która łączy tooother Azure usługi</span><span class="sxs-lookup"><span data-stu-id="3f6eb-104">Use Azure Functions toocreate a function that connects tooother Azure services</span></span>

<span data-ttu-id="3f6eb-105">W tym temacie pokazano, jak toocreate funkcji w funkcji Azure, która nasłuchuje toomessages na hello Azure Storage kolejki, jak i kopie komunikatów toorows w tabeli magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-105">This topic shows you how toocreate a function in Azure Functions that listens toomessages on an Azure Storage queue and copies hello messages toorows in an Azure Storage table.</span></span> <span data-ttu-id="3f6eb-106">Funkcja czasomierza wyzwalane jest używane tooload wiadomości w kolejce hello.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-106">A timer triggered function is used tooload messages into hello queue.</span></span> <span data-ttu-id="3f6eb-107">Druga funkcja odczytuje hello kolejki i zapisuje komunikaty toohello tabeli.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-107">A second function reads from hello queue and writes messages toohello table.</span></span> <span data-ttu-id="3f6eb-108">Zarówno kolejka hello, jak i tabela hello są tworzone przez usługi Azure Functions, na podstawie definicji powiązania hello.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-108">Both hello queue and hello table are created for you by Azure Functions based on hello binding definitions.</span></span> 

<span data-ttu-id="3f6eb-109">bardziej interesujące elementy toomake, jedna funkcja została napisana w języku JavaScript i hello innych napisano w języku C# skrypt.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-109">toomake things more interesting, one function is written in JavaScript and hello other is written in C# script.</span></span> <span data-ttu-id="3f6eb-110">To pokazuje, w jaki sposób aplikacja funkcji może mieć funkcje w różnych językach.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="3f6eb-111">Ten scenariusz pokazano w [wideo w witrynie Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span><span class="sxs-lookup"><span data-stu-id="3f6eb-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-toohello-queue"></a><span data-ttu-id="3f6eb-112">Tworzy funkcję, która zapisuje toohello kolejki</span><span class="sxs-lookup"><span data-stu-id="3f6eb-112">Create a function that writes toohello queue</span></span>

<span data-ttu-id="3f6eb-113">Zanim będzie można połączyć tooa kolejki magazynu, należy toocreate funkcję, która ładuje kolejki wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-113">Before you can connect tooa storage queue, you need toocreate a function that loads hello message queue.</span></span> <span data-ttu-id="3f6eb-114">Ta funkcja JavaScript korzysta z wyzwalacza bazującego na czasomierzu zapisującej kolejki komunikatów toohello co 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-114">This JavaScript function uses a timer trigger that writes a message toohello queue every 10 seconds.</span></span> <span data-ttu-id="3f6eb-115">Jeśli nie masz jeszcze konta platformy Azure, zapoznaj się hello [spróbuj usługi Azure Functions](https://functions.azure.com/try) występują, lub [utworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="3f6eb-115">If you don't already have an Azure account, check out hello [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="3f6eb-116">Przejdź toohello portalu Azure i Znajdź aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-116">Go toohello Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="3f6eb-117">Kliknij pozycje **Nowa funkcja** > **TimerTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="3f6eb-118">Nazwa funkcji hello **FunctionsBindingsDemo1**, wprowadź wartość wyrażenia cron `0/10 * * * * *` dla **harmonogram**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-118">Name hello function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Dodawanie funkcji wyzwalanej czasomierzem](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="3f6eb-120">W ten sposób została utworzona funkcja wyzwalana czasomierzem, uruchamiana co 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="3f6eb-121">Na powitania **opracowanie** , kliknij pozycję **dzienniki** i wyświetlać informacje w dzienniku hello aktywności hello.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-121">On hello **Develop** tab, click **Logs** and view hello activity in hello log.</span></span> <span data-ttu-id="3f6eb-122">Zobaczysz wpisy dziennika zapisywane co 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Widok hello dziennika tooverify hello funkcja działa](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="3f6eb-124">Dodawanie powiązania wyjściowego kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="3f6eb-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="3f6eb-125">Na powitania **integracji** , wybierz pozycję **nowe dane wyjściowe** > **Azure Queue Storage** > **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-125">On hello **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Dodawanie funkcji czasomierza wyzwalacza](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="3f6eb-127">Wprowadź `myQueueItem` dla **Nazwa parametru komunikatu** i `functions-bindings` dla **Nazwa kolejki**, wybierz istniejący **połączenia konta magazynu** lub kliknij przycisk **nowe** toocreate konta połączenia magazynu, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** toocreate a storage account connection, and then click **Save**.</span></span>  

    ![Utwórz kolejkę toohello powiązania hello danych wyjściowych w pamięci masowej](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="3f6eb-129">Po powrocie do hello **opracowanie** karcie, Dołącz hello następującego kodu toohello funkcji:</span><span class="sxs-lookup"><span data-stu-id="3f6eb-129">Back in hello **Develop** tab, append hello following code toohello function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="3f6eb-130">Zlokalizuj hello *Jeśli* instrukcji wiersz około 9 hello funkcji i Wstaw hello poniższy kod po tej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-130">Locate hello *if* statement around line 9 of hello function, and insert hello following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="3f6eb-131">Ten kod tworzy **myQueueItem** i ustawia jej **czasu** bieżącą sygnaturę czasową toohello właściwości.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-131">This code creates a **myQueueItem** and sets its **time** property toohello current timeStamp.</span></span> <span data-ttu-id="3f6eb-132">Następnie dodaje hello nowej kolejki elementu toohello kontekstu **myQueueItem** powiązania.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-132">It then adds hello new queue item toohello context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="3f6eb-133">Kliknij pozycję **Zapisz i uruchom**.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="3f6eb-134">Wyświetlanie aktualizacji magazynu za pomocą programu Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="3f6eb-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="3f6eb-135">Możesz sprawdzić, czy funkcja działa przez wyświetlanie wiadomości w kolejce hello, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-135">You can verify that your function is working by viewing messages in hello queue you created.</span></span>  <span data-ttu-id="3f6eb-136">Możesz połączyć tooyour kolejki magazynu przy użyciu Eksplorator chmury w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-136">You can connect tooyour storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="3f6eb-137">Jednak hello portal umożliwia konta magazynu tooyour łatwe tooconnect za pomocą Eksploratora usługi Microsoft Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-137">However, hello portal makes it easy tooconnect tooyour storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="3f6eb-138">W hello **integracji** , kliknij pozycję kolejki powiązania wyjściowego > **dokumentacji**, odkryć hello parametry połączenia dla konta magazynu i skopiuj wartość hello.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-138">In hello **Integrate** tab, click your queue output binding > **Documentation**, then unhide hello Connection String for your storage account and copy hello value.</span></span> <span data-ttu-id="3f6eb-139">Możesz użyć tego konta magazynu tooyour tooconnect wartość.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-139">You use this value tooconnect tooyour storage account.</span></span>

    ![Pobieranie programu Azure Storage Explorer](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="3f6eb-141">Jeśli jeszcze tego nie zrobiono, pobierz i zainstaluj program [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="3f6eb-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="3f6eb-142">W Eksploratorze usługi Storage, kliknij przycisk hello połączenia magazynu tooAzure, Wklej parametry połączenia hello w polu hello i ukończyć powitalnych kreatora.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-142">In Storage Explorer, click hello connect tooAzure Storage icon, paste hello connection string in hello field, and complete hello wizard.</span></span>

    ![Program Storage Explorer dodaje połączenie](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="3f6eb-144">W obszarze **lokalne i podłączone**, rozwiń węzeł **kont magazynu** > konta magazynu > **kolejek** > **funkcji powiązania**i sprawdź, czy komunikaty są zapisywane toohello kolejki.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written toohello queue.</span></span>

    ![Widok komunikatów w kolejce hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="3f6eb-146">Jeśli hello kolejka nie istnieje lub jest pusta, prawdopodobnie problem jest powiązanie funkcji lub kodu.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-146">If hello queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-hello-queue"></a><span data-ttu-id="3f6eb-147">Tworzy funkcję, która odczytuje z kolejki hello</span><span class="sxs-lookup"><span data-stu-id="3f6eb-147">Create a function that reads from hello queue</span></span>

<span data-ttu-id="3f6eb-148">Teraz, gdy masz dodawany toohello kolejki wiadomości, można utworzyć inną funkcję, która odczytuje z kolejki hello i hello zapisy trwale wiadomości tooan tabeli magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-148">Now that you have messages being added toohello queue, you can create another function that reads from hello queue and writes hello messages permanently tooan Azure Storage table.</span></span>

1. <span data-ttu-id="3f6eb-149">Kliknij pozycje **Nowa funkcja** > **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="3f6eb-150">Nazwa funkcji hello `FunctionsBindingsDemo2`, wprowadź **powiązania funkcji** w hello **Nazwa kolejki** pola, wybrać istniejące konto magazynu lub utworzyć, a następnie kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-150">Name hello function `FunctionsBindingsDemo2`, enter **functions-bindings** in hello **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Dodawanie funkcji czasomierza kolejki danych wyjściowych](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="3f6eb-152">(Opcjonalnie) Możesz sprawdzić, czy hello nowa funkcja działa wyświetlając hello nową kolejkę w Eksploratorze usługi Storage jako przed.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-152">(Optional) You can verify that hello new function works by viewing hello new queue in Storage Explorer as before.</span></span> <span data-ttu-id="3f6eb-153">Możesz także użyć programu Cloud Explorer w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="3f6eb-154">(Opcjonalnie) Odśwież hello **powiązania funkcji** kolejki i zwróć uwagę, że elementy zostały usunięte z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-154">(Optional) Refresh hello **functions-bindings** queue and notice that items have been removed from hello queue.</span></span> <span data-ttu-id="3f6eb-155">Hello usuwania występuje, ponieważ funkcja hello jest powiązane toohello **powiązania funkcji** kolejka wejściowe funkcji wyzwalacza i hello odczyt hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-155">hello removal occurs because hello function is bound toohello **functions-bindings** queue as an input trigger and hello function reads hello queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="3f6eb-156">Dodawanie powiązania wyjściowego tabeli</span><span class="sxs-lookup"><span data-stu-id="3f6eb-156">Add a table output binding</span></span>

1. <span data-ttu-id="3f6eb-157">W obszarze FunctionsBindingsDemo2 kliknij pozycje **Integracja** > **Nowe dane wyjściowe** > **Azure Table Storage** > **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Dodaj tabelę powiązania tooan usługi Azure Storage](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="3f6eb-159">Wprowadź wartość `functionbindings` w polu **Nazwa tabeli** i `myTable` w polu **Nazwa parametru tabeli**, wybierz **Połączenie konta magazynu** lub utwórz nowe, a następnie kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Skonfiguruj powiązanie tabeli hello magazynu](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="3f6eb-161">W hello **opracowanie** karcie, Zamień istniejący kod funkcji hello hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="3f6eb-161">In hello **Develop** tab, replace hello existing function code with hello following:</span></span>
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    <span data-ttu-id="3f6eb-162">Hello **TableItem** klasy reprezentuje wiersz w tabeli magazynu hello i dodać hello elementu toohello `myTable` zbiór **TableItem** obiektów.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-162">hello **TableItem** class represents a row in hello storage table, and you add hello item toohello `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="3f6eb-163">Należy ustawić hello **PartitionKey** i **RowKey** tooinsert stanie toobe właściwości do tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-163">You must set hello **PartitionKey** and **RowKey** properties toobe able tooinsert into hello table.</span></span>

4. <span data-ttu-id="3f6eb-164">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-164">Click **Save**.</span></span>  <span data-ttu-id="3f6eb-165">Na koniec można sprawdzić działa funkcja hello, wyświetlając hello tabeli w Eksploratora magazynu lub programu Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-165">Finally, you can verify hello function works by viewing hello table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="3f6eb-166">(Opcjonalnie) Na koncie magazynu w Eksploratorze usługi Storage, rozwiń węzeł **tabel** > **functionsbindings** i upewnij się, że wiersze są dodawane toohello tabeli.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added toohello table.</span></span> <span data-ttu-id="3f6eb-167">Możesz zrobić hello takie same w Eksploratorze chmury w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-167">You can do hello same in Cloud Explorer in Visual Studio.</span></span>

    ![Widok wierszy w tabeli hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="3f6eb-169">Jeśli hello tabela nie istnieje lub jest pusty, prawdopodobnie problem jest powiązanie funkcji lub kodu.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-169">If hello table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="3f6eb-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3f6eb-170">Next steps</span></span>
<span data-ttu-id="3f6eb-171">Aby uzyskać więcej informacji na temat usługi Azure Functions zobacz następujące tematy hello:</span><span class="sxs-lookup"><span data-stu-id="3f6eb-171">For more information about Azure Functions, see hello following topics:</span></span>

* [<span data-ttu-id="3f6eb-172">Dokumentacja usługi Azure Functions dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="3f6eb-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="3f6eb-173">Dokumentacja dla programistów dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="3f6eb-174">Testowanie usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3f6eb-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="3f6eb-175">Opis różnych narzędzi i technik testowania funkcji.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="3f6eb-176">Jak tooscale usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3f6eb-176">How tooscale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="3f6eb-177">Omówienie planów usług dostępnych w środowisku Azure Functions: plan hostingu zużycie hello i jak toochoose hello właściwego planu.</span><span class="sxs-lookup"><span data-stu-id="3f6eb-177">Discusses service plans available with Azure Functions, including hello Consumption hosting plan, and how toochoose hello right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

