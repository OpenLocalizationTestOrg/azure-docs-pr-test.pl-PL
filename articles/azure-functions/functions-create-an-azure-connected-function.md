---
title: "Tworzenie funkcji nawiązującej połączenie z usługami Azure | Microsoft Docs"
description: "Tworzenie nieużywającej serwera aplikacji, która nawiązuje połączenie z innymi usługami Azure, za pomocą usługi Azure Functions."
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
ms.openlocfilehash: 65964a322f0adab4f648fb350bedb77b46bf9054
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-functions-to-create-a-function-that-connects-to-other-azure-services"></a><span data-ttu-id="fe16b-104">Tworzenie funkcji nawiązującej połączenie z innymi usługami Azure za pomocą usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fe16b-104">Use Azure Functions to create a function that connects to other Azure services</span></span>

<span data-ttu-id="fe16b-105">W tym temacie opisano sposób tworzenia funkcji w usłudze Azure Functions, która nasłuchuje komunikatów w kolejce usługi Azure Storage i kopiuje je do wierszy w tabeli usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fe16b-105">This topic shows you how to create a function in Azure Functions that listens to messages on an Azure Storage queue and copies the messages to rows in an Azure Storage table.</span></span> <span data-ttu-id="fe16b-106">Funkcja wyzwalana przez czasomierz służy do ładowania komunikatów do kolejki.</span><span class="sxs-lookup"><span data-stu-id="fe16b-106">A timer triggered function is used to load messages into the queue.</span></span> <span data-ttu-id="fe16b-107">Druga funkcja odczytuje komunikaty z kolejki i zapisuje je do tabeli.</span><span class="sxs-lookup"><span data-stu-id="fe16b-107">A second function reads from the queue and writes messages to the table.</span></span> <span data-ttu-id="fe16b-108">Zarówno kolejka, jak i tabela są tworzone przez usługę Azure Functions na podstawie definicji powiązania.</span><span class="sxs-lookup"><span data-stu-id="fe16b-108">Both the queue and the table are created for you by Azure Functions based on the binding definitions.</span></span> 

<span data-ttu-id="fe16b-109">Aby było ciekawiej, jedna funkcja została napisana w języku JavaScript, a druga w języku C#.</span><span class="sxs-lookup"><span data-stu-id="fe16b-109">To make things more interesting, one function is written in JavaScript and the other is written in C# script.</span></span> <span data-ttu-id="fe16b-110">To pokazuje, w jaki sposób aplikacja funkcji może mieć funkcje w różnych językach.</span><span class="sxs-lookup"><span data-stu-id="fe16b-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="fe16b-111">Ten scenariusz pokazano w [wideo w witrynie Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span><span class="sxs-lookup"><span data-stu-id="fe16b-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-to-the-queue"></a><span data-ttu-id="fe16b-112">Tworzenie funkcji, która zapisuje do kolejki</span><span class="sxs-lookup"><span data-stu-id="fe16b-112">Create a function that writes to the queue</span></span>

<span data-ttu-id="fe16b-113">Przed połączeniem się z kolejką magazynu należy utworzyć funkcję, która ładuje kolejkę komunikatów.</span><span class="sxs-lookup"><span data-stu-id="fe16b-113">Before you can connect to a storage queue, you need to create a function that loads the message queue.</span></span> <span data-ttu-id="fe16b-114">Ta funkcja JavaScript korzysta z wyzwalacza czasomierza, który zapisuje komunikat do kolejki co 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="fe16b-114">This JavaScript function uses a timer trigger that writes a message to the queue every 10 seconds.</span></span> <span data-ttu-id="fe16b-115">Jeśli nie masz jeszcze konta platformy Azure, zapoznaj się ze środowiskiem [Wypróbuj usługę Azure Functions](https://functions.azure.com/try) lub [utwórz bezpłatne konto platformy Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fe16b-115">If you don't already have an Azure account, check out the [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="fe16b-116">Przejdź do witryny Azure Portal i wyszukaj aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="fe16b-116">Go to the Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="fe16b-117">Kliknij pozycje **Nowa funkcja** > **TimerTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="fe16b-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="fe16b-118">Nadaj funkcji nazwę **FunctionsBindingsDemo1**, wprowadź wartość wyrażenia cron `0/10 * * * * *` w polu **Harmonogram**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fe16b-118">Name the function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Dodawanie funkcji wyzwalanej czasomierzem](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="fe16b-120">W ten sposób została utworzona funkcja wyzwalana czasomierzem, uruchamiana co 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="fe16b-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="fe16b-121">Na karcie **Programowanie** kliknij przycisk **Dzienniki**, aby wyświetlić aktywność w dzienniku.</span><span class="sxs-lookup"><span data-stu-id="fe16b-121">On the **Develop** tab, click **Logs** and view the activity in the log.</span></span> <span data-ttu-id="fe16b-122">Zobaczysz wpisy dziennika zapisywane co 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="fe16b-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Wyświetlanie dziennika w celu sprawdzenia, czy funkcja działa](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="fe16b-124">Dodawanie powiązania wyjściowego kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="fe16b-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="fe16b-125">Na karcie **Integracja** wybierz elementy **Nowe dane wyjściowe** > **Azure Queue Storage** > **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="fe16b-125">On the **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Dodawanie funkcji czasomierza wyzwalacza](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="fe16b-127">Wprowadź wartość `myQueueItem` w polu **Nazwa parametru komunikatu** i `functions-bindings` w polu **Nazwa kolejki**, wybierz istniejące **Połączenie konta magazynu** lub kliknij pozycję **nowe**, aby utworzyć nowe połączenie konta magazynu, a następnie kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="fe16b-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** to create a storage account connection, and then click **Save**.</span></span>  

    ![Tworzenie powiązania wyjściowego do kolejki magazynu](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="fe16b-129">Po powrocie na kartę **Programowanie** dołącz następujący kod do funkcji:</span><span class="sxs-lookup"><span data-stu-id="fe16b-129">Back in the **Develop** tab, append the following code to the function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="fe16b-130">Znajdź instrukcję *if* około wiersza 9 funkcji i wstaw następujący kod po tej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="fe16b-130">Locate the *if* statement around line 9 of the function, and insert the following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="fe16b-131">Ten kod powoduje utworzenie elementu **myQueueItem** i ustawienie jego właściwości **time** na bieżącą sygnaturę czasową.</span><span class="sxs-lookup"><span data-stu-id="fe16b-131">This code creates a **myQueueItem** and sets its **time** property to the current timeStamp.</span></span> <span data-ttu-id="fe16b-132">Następnie nowy element kolejki jest dodawany do powiązania **myQueueItem** kontekstu.</span><span class="sxs-lookup"><span data-stu-id="fe16b-132">It then adds the new queue item to the context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="fe16b-133">Kliknij pozycję **Zapisz i uruchom**.</span><span class="sxs-lookup"><span data-stu-id="fe16b-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="fe16b-134">Wyświetlanie aktualizacji magazynu za pomocą programu Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="fe16b-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="fe16b-135">Aby sprawdzić, czy funkcja działa, wyświetl komunikaty w utworzonej kolejce.</span><span class="sxs-lookup"><span data-stu-id="fe16b-135">You can verify that your function is working by viewing messages in the queue you created.</span></span>  <span data-ttu-id="fe16b-136">Z kolejką magazynu można połączyć się za pomocą programu Cloud Explorer w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe16b-136">You can connect to your storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="fe16b-137">Jednak portal ułatwia łączenie się z kontem magazynu za pomocą programu Microsoft Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="fe16b-137">However, the portal makes it easy to connect to your storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="fe16b-138">Na karcie **Integracja** kliknij powiązanie wyjściowe kolejki i pozycję **Dokumentacja**, a następnie wyświetl parametry połączenia dla konta magazynu i skopiuj tę wartość.</span><span class="sxs-lookup"><span data-stu-id="fe16b-138">In the **Integrate** tab, click your queue output binding > **Documentation**, then unhide the Connection String for your storage account and copy the value.</span></span> <span data-ttu-id="fe16b-139">Ta wartość służy do łączenia się z kontem magazynu.</span><span class="sxs-lookup"><span data-stu-id="fe16b-139">You use this value to connect to your storage account.</span></span>

    ![Pobieranie programu Azure Storage Explorer](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="fe16b-141">Jeśli jeszcze tego nie zrobiono, pobierz i zainstaluj program [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="fe16b-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="fe16b-142">W programie Storage Explorer kliknij ikonę Połącz z usługą Azure Storage, wklej parametry połączenia w polu i zakończ pracę kreatora.</span><span class="sxs-lookup"><span data-stu-id="fe16b-142">In Storage Explorer, click the connect to Azure Storage icon, paste the connection string in the field, and complete the wizard.</span></span>

    ![Program Storage Explorer dodaje połączenie](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="fe16b-144">W obszarze **Local and attached** (Lokalne i dołączone) rozwiń pozycje **Konta magazynu** > Twoje konto magazynu > **Kolejki** > **functions-bindings** i sprawdź, czy komunikaty są zapisywane do kolejki.</span><span class="sxs-lookup"><span data-stu-id="fe16b-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written to the queue.</span></span>

    ![Wyświetlanie komunikatów w kolejce](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="fe16b-146">Jeśli kolejka nie istnieje lub jest pusta, prawdopodobnie występuje problem z powiązaniem lub kodem funkcji.</span><span class="sxs-lookup"><span data-stu-id="fe16b-146">If the queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-the-queue"></a><span data-ttu-id="fe16b-147">Tworzenie funkcji, która odczytuje z kolejki</span><span class="sxs-lookup"><span data-stu-id="fe16b-147">Create a function that reads from the queue</span></span>

<span data-ttu-id="fe16b-148">Teraz, gdy komunikaty są dodawane do kolejki, możesz utworzyć inną funkcję, która odczytuje z kolejki i zapisuje komunikaty trwale do tabeli usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fe16b-148">Now that you have messages being added to the queue, you can create another function that reads from the queue and writes the messages permanently to an Azure Storage table.</span></span>

1. <span data-ttu-id="fe16b-149">Kliknij pozycje **Nowa funkcja** > **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="fe16b-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="fe16b-150">Nadaj funkcji nazwę `FunctionsBindingsDemo2`, wprowadź wartość **functions-bindings** w polu **Nazwa kolejki**, wybierz istniejące konto magazynu lub utwórz nowe, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fe16b-150">Name the function `FunctionsBindingsDemo2`, enter **functions-bindings** in the **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Dodawanie funkcji czasomierza kolejki danych wyjściowych](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="fe16b-152">(Opcjonalnie) Możesz sprawdzić, czy nowa funkcja działa, poprzez wyświetlenie nowej kolejki w programie Storage Explorer, tak jak poprzednio.</span><span class="sxs-lookup"><span data-stu-id="fe16b-152">(Optional) You can verify that the new function works by viewing the new queue in Storage Explorer as before.</span></span> <span data-ttu-id="fe16b-153">Możesz także użyć programu Cloud Explorer w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe16b-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="fe16b-154">(Opcjonalnie) Odśwież kolejkę **functions-bindings** i zwróć uwagę, że elementy zostały usunięte z kolejki.</span><span class="sxs-lookup"><span data-stu-id="fe16b-154">(Optional) Refresh the **functions-bindings** queue and notice that items have been removed from the queue.</span></span> <span data-ttu-id="fe16b-155">Usuwanie występuje, ponieważ funkcja jest powiązana z kolejką **functions-bindings** jako wyzwalacz wejściowy i funkcja odczytuje kolejkę.</span><span class="sxs-lookup"><span data-stu-id="fe16b-155">The removal occurs because the function is bound to the **functions-bindings** queue as an input trigger and the function reads the queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="fe16b-156">Dodawanie powiązania wyjściowego tabeli</span><span class="sxs-lookup"><span data-stu-id="fe16b-156">Add a table output binding</span></span>

1. <span data-ttu-id="fe16b-157">W obszarze FunctionsBindingsDemo2 kliknij pozycje **Integracja** > **Nowe dane wyjściowe** > **Azure Table Storage** > **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="fe16b-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Dodawanie powiązania do tabeli usługi Azure Storage](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="fe16b-159">Wprowadź wartość `functionbindings` w polu **Nazwa tabeli** i `myTable` w polu **Nazwa parametru tabeli**, wybierz **Połączenie konta magazynu** lub utwórz nowe, a następnie kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="fe16b-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Konfigurowanie powiązania tabeli magazynu](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="fe16b-161">Na karcie **Programowanie** zastąp istniejący kod funkcji następującym:</span><span class="sxs-lookup"><span data-stu-id="fe16b-161">In the **Develop** tab, replace the existing function code with the following:</span></span>
   
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
        
        // Add the item to the table binding collection.
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
    <span data-ttu-id="fe16b-162">Klasa **TableItem** reprezentuje wiersz w tabeli magazynu i element jest dodawany do kolekcji `myTable` obiektów **TableItem**.</span><span class="sxs-lookup"><span data-stu-id="fe16b-162">The **TableItem** class represents a row in the storage table, and you add the item to the `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="fe16b-163">Należy ustawić właściwości **PartitionKey** i **RowKey**, aby umożliwić wstawienie do tabeli.</span><span class="sxs-lookup"><span data-stu-id="fe16b-163">You must set the **PartitionKey** and **RowKey** properties to be able to insert into the table.</span></span>

4. <span data-ttu-id="fe16b-164">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="fe16b-164">Click **Save**.</span></span>  <span data-ttu-id="fe16b-165">Na koniec można sprawdzić działanie funkcji, wyświetlając tabelę w programie Storage Explorer lub programie Cloud Explorer programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe16b-165">Finally, you can verify the function works by viewing the table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="fe16b-166">(Opcjonalnie) W swoim koncie magazynu w programie Storage Explorer rozwiń pozycje **Tabele** > **functionsbindings** i sprawdź, czy wiersze są dodawane do tabeli.</span><span class="sxs-lookup"><span data-stu-id="fe16b-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added to the table.</span></span> <span data-ttu-id="fe16b-167">To samo można zrobić w programie Cloud Explorer programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe16b-167">You can do the same in Cloud Explorer in Visual Studio.</span></span>

    ![Widok wierszy w tabeli](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="fe16b-169">Jeśli tabela nie istnieje lub jest pusta, prawdopodobnie występuje problem z powiązaniem lub kodem funkcji.</span><span class="sxs-lookup"><span data-stu-id="fe16b-169">If the table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="fe16b-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe16b-170">Next steps</span></span>
<span data-ttu-id="fe16b-171">Aby uzyskać więcej informacji na temat usługi Azure Functions, zobacz poniższe tematy:</span><span class="sxs-lookup"><span data-stu-id="fe16b-171">For more information about Azure Functions, see the following topics:</span></span>

* [<span data-ttu-id="fe16b-172">Dokumentacja usługi Azure Functions dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="fe16b-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="fe16b-173">Dokumentacja dla programistów dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.</span><span class="sxs-lookup"><span data-stu-id="fe16b-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="fe16b-174">Testowanie usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fe16b-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="fe16b-175">Opis różnych narzędzi i technik testowania funkcji.</span><span class="sxs-lookup"><span data-stu-id="fe16b-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="fe16b-176">Jak skalować usługę Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fe16b-176">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="fe16b-177">Omówienie planów usług dostępnych w środowisku Azure Functions, w tym planu hostingowego zużycia, oraz sposobu wybierania właściwego planu.</span><span class="sxs-lookup"><span data-stu-id="fe16b-177">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

