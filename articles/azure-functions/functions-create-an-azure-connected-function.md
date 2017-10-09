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
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a>Użyj usługi Azure Functions toocreate funkcję, która łączy tooother Azure usługi

W tym temacie pokazano, jak toocreate funkcji w funkcji Azure, która nasłuchuje toomessages na hello Azure Storage kolejki, jak i kopie komunikatów toorows w tabeli magazynu Azure. Funkcja czasomierza wyzwalane jest używane tooload wiadomości w kolejce hello. Druga funkcja odczytuje hello kolejki i zapisuje komunikaty toohello tabeli. Zarówno kolejka hello, jak i tabela hello są tworzone przez usługi Azure Functions, na podstawie definicji powiązania hello. 

bardziej interesujące elementy toomake, jedna funkcja została napisana w języku JavaScript i hello innych napisano w języku C# skrypt. To pokazuje, w jaki sposób aplikacja funkcji może mieć funkcje w różnych językach. 

Ten scenariusz pokazano w [wideo w witrynie Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).

## <a name="create-a-function-that-writes-toohello-queue"></a>Tworzy funkcję, która zapisuje toohello kolejki

Zanim będzie można połączyć tooa kolejki magazynu, należy toocreate funkcję, która ładuje kolejki wiadomości powitania. Ta funkcja JavaScript korzysta z wyzwalacza bazującego na czasomierzu zapisującej kolejki komunikatów toohello co 10 sekund. Jeśli nie masz jeszcze konta platformy Azure, zapoznaj się hello [spróbuj usługi Azure Functions](https://functions.azure.com/try) występują, lub [utworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/free/).

1. Przejdź toohello portalu Azure i Znajdź aplikację funkcji.

2. Kliknij pozycje **Nowa funkcja** > **TimerTrigger-JavaScript**. 

3. Nazwa funkcji hello **FunctionsBindingsDemo1**, wprowadź wartość wyrażenia cron `0/10 * * * * *` dla **harmonogram**, a następnie kliknij przycisk **Utwórz**.
   
    ![Dodawanie funkcji wyzwalanej czasomierzem](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    W ten sposób została utworzona funkcja wyzwalana czasomierzem, uruchamiana co 10 sekund.

5. Na powitania **opracowanie** , kliknij pozycję **dzienniki** i wyświetlać informacje w dzienniku hello aktywności hello. Zobaczysz wpisy dziennika zapisywane co 10 sekund.
   
    ![Widok hello dziennika tooverify hello funkcja działa](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a>Dodawanie powiązania wyjściowego kolejki komunikatów

1. Na powitania **integracji** , wybierz pozycję **nowe dane wyjściowe** > **Azure Queue Storage** > **wybierz**.

    ![Dodawanie funkcji czasomierza wyzwalacza](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. Wprowadź `myQueueItem` dla **Nazwa parametru komunikatu** i `functions-bindings` dla **Nazwa kolejki**, wybierz istniejący **połączenia konta magazynu** lub kliknij przycisk **nowe** toocreate konta połączenia magazynu, a następnie kliknij przycisk **zapisać**.  

    ![Utwórz kolejkę toohello powiązania hello danych wyjściowych w pamięci masowej](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. Po powrocie do hello **opracowanie** karcie, Dołącz hello następującego kodu toohello funkcji:
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. Zlokalizuj hello *Jeśli* instrukcji wiersz około 9 hello funkcji i Wstaw hello poniższy kod po tej instrukcji.
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    Ten kod tworzy **myQueueItem** i ustawia jej **czasu** bieżącą sygnaturę czasową toohello właściwości. Następnie dodaje hello nowej kolejki elementu toohello kontekstu **myQueueItem** powiązania.

3. Kliknij pozycję **Zapisz i uruchom**.

## <a name="view-storage-updates-by-using-storage-explorer"></a>Wyświetlanie aktualizacji magazynu za pomocą programu Storage Explorer
Możesz sprawdzić, czy funkcja działa przez wyświetlanie wiadomości w kolejce hello, który został utworzony.  Możesz połączyć tooyour kolejki magazynu przy użyciu Eksplorator chmury w programie Visual Studio. Jednak hello portal umożliwia konta magazynu tooyour łatwe tooconnect za pomocą Eksploratora usługi Microsoft Azure Storage.

1. W hello **integracji** , kliknij pozycję kolejki powiązania wyjściowego > **dokumentacji**, odkryć hello parametry połączenia dla konta magazynu i skopiuj wartość hello. Możesz użyć tego konta magazynu tooyour tooconnect wartość.

    ![Pobieranie programu Azure Storage Explorer](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. Jeśli jeszcze tego nie zrobiono, pobierz i zainstaluj program [Microsoft Azure Storage Explorer](http://storageexplorer.com). 
 
3. W Eksploratorze usługi Storage, kliknij przycisk hello połączenia magazynu tooAzure, Wklej parametry połączenia hello w polu hello i ukończyć powitalnych kreatora.

    ![Program Storage Explorer dodaje połączenie](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. W obszarze **lokalne i podłączone**, rozwiń węzeł **kont magazynu** > konta magazynu > **kolejek** > **funkcji powiązania**i sprawdź, czy komunikaty są zapisywane toohello kolejki.

    ![Widok komunikatów w kolejce hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    Jeśli hello kolejka nie istnieje lub jest pusta, prawdopodobnie problem jest powiązanie funkcji lub kodu.

## <a name="create-a-function-that-reads-from-hello-queue"></a>Tworzy funkcję, która odczytuje z kolejki hello

Teraz, gdy masz dodawany toohello kolejki wiadomości, można utworzyć inną funkcję, która odczytuje z kolejki hello i hello zapisy trwale wiadomości tooan tabeli magazynu Azure.

1. Kliknij pozycje **Nowa funkcja** > **QueueTrigger-CSharp**. 
 
2. Nazwa funkcji hello `FunctionsBindingsDemo2`, wprowadź **powiązania funkcji** w hello **Nazwa kolejki** pola, wybrać istniejące konto magazynu lub utworzyć, a następnie kliknij **Utwórz**.

    ![Dodawanie funkcji czasomierza kolejki danych wyjściowych](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. (Opcjonalnie) Możesz sprawdzić, czy hello nowa funkcja działa wyświetlając hello nową kolejkę w Eksploratorze usługi Storage jako przed. Możesz także użyć programu Cloud Explorer w programie Visual Studio.  

4. (Opcjonalnie) Odśwież hello **powiązania funkcji** kolejki i zwróć uwagę, że elementy zostały usunięte z kolejki hello. Hello usuwania występuje, ponieważ funkcja hello jest powiązane toohello **powiązania funkcji** kolejka wejściowe funkcji wyzwalacza i hello odczyt hello kolejki. 
 
## <a name="add-a-table-output-binding"></a>Dodawanie powiązania wyjściowego tabeli

1. W obszarze FunctionsBindingsDemo2 kliknij pozycje **Integracja** > **Nowe dane wyjściowe** > **Azure Table Storage** > **Wybierz**.

    ![Dodaj tabelę powiązania tooan usługi Azure Storage](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. Wprowadź wartość `functionbindings` w polu **Nazwa tabeli** i `myTable` w polu **Nazwa parametru tabeli**, wybierz **Połączenie konta magazynu** lub utwórz nowe, a następnie kliknij przycisk **Zapisz**.

    ![Skonfiguruj powiązanie tabeli hello magazynu](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. W hello **opracowanie** karcie, Zamień istniejący kod funkcji hello hello poniżej:
   
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
    Hello **TableItem** klasy reprezentuje wiersz w tabeli magazynu hello i dodać hello elementu toohello `myTable` zbiór **TableItem** obiektów. Należy ustawić hello **PartitionKey** i **RowKey** tooinsert stanie toobe właściwości do tabeli hello.

4. Kliknij pozycję **Zapisz**.  Na koniec można sprawdzić działa funkcja hello, wyświetlając hello tabeli w Eksploratora magazynu lub programu Visual Studio Cloud Explorer.

5. (Opcjonalnie) Na koncie magazynu w Eksploratorze usługi Storage, rozwiń węzeł **tabel** > **functionsbindings** i upewnij się, że wiersze są dodawane toohello tabeli. Możesz zrobić hello takie same w Eksploratorze chmury w programie Visual Studio.

    ![Widok wierszy w tabeli hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    Jeśli hello tabela nie istnieje lub jest pusty, prawdopodobnie problem jest powiązanie funkcji lub kodu. 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat usługi Azure Functions zobacz następujące tematy hello:

* [Dokumentacja usługi Azure Functions dla deweloperów](functions-reference.md)  
  Dokumentacja dla programistów dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.
* [Testowanie usługi Azure Functions](functions-test-a-function.md)  
  Opis różnych narzędzi i technik testowania funkcji.
* [Jak tooscale usługi Azure Functions](functions-scale.md)  
  Omówienie planów usług dostępnych w środowisku Azure Functions: plan hostingu zużycie hello i jak toochoose hello właściwego planu. 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

