---
title: toouse aaaHow magazynu kolejek w oprogramowaniu Node.js | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate usługi kolejek platformy Azure hello toouse i usuwania kolejki oraz insert, Pobierz i usunąć wiadomości. Przykłady zapisywane w środowisku Node.js."
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 977e5994c0be1b5d71c60b7479698ccb694ab860
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a><span data-ttu-id="a35b5-104">Jak toouse magazynu kolejek w oprogramowaniu Node.js</span><span class="sxs-lookup"><span data-stu-id="a35b5-104">How toouse Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="a35b5-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a35b5-105">Overview</span></span>
<span data-ttu-id="a35b5-106">W tym przewodniku pokazano, jak tooperform typowych scenariuszy przy użyciu hello usługi Microsoft Azure kolejki.</span><span class="sxs-lookup"><span data-stu-id="a35b5-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue service.</span></span> <span data-ttu-id="a35b5-107">Hello przykłady są napisane przy użyciu hello interfejsu API środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="a35b5-107">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="a35b5-108">Hello omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także  **Tworzenie i usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="a35b5-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="a35b5-109">Tworzenie aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="a35b5-109">Create a Node.js Application</span></span>
<span data-ttu-id="a35b5-110">Utwórz pustą aplikację Node.js.</span><span class="sxs-lookup"><span data-stu-id="a35b5-110">Create a blank Node.js application.</span></span> <span data-ttu-id="a35b5-111">Aby uzyskać instrukcje tworzenia aplikacji Node.js, zobacz [tworzenie aplikacji sieci web Node.js w usłudze Azure App Service], [tworzenie i wdrażanie tooan aplikacji Node.js usługi w chmurze Azure] przy użyciu programu Windows PowerShell lub [ Tworzenie i wdrażanie tooAzure aplikacji sieci web Node.js za pomocą macierzy sieci Web].</span><span class="sxs-lookup"><span data-stu-id="a35b5-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service] using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix].</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="a35b5-112">Skonfiguruj tooAccess Twoja aplikacja magazynu</span><span class="sxs-lookup"><span data-stu-id="a35b5-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="a35b5-113">toouse magazynu Azure, należy hello zestawu SDK usługi Magazyn Azure dla środowiska Node.js, w tym zestaw wygody bibliotek, które komunikują się z usługi REST magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="a35b5-113">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="a35b5-114">Użyj pakietu hello tooobtain węzeł Menedżera pakietów (NPM)</span><span class="sxs-lookup"><span data-stu-id="a35b5-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="a35b5-115">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix), przejdź do folderu toohello, w której utworzono aplikację przykładową.</span><span class="sxs-lookup"><span data-stu-id="a35b5-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="a35b5-116">Typ **magazyn azure instalacji narzędzia npm** w oknie polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="a35b5-116">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="a35b5-117">Dane wyjściowe polecenia hello jest toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="a35b5-117">Output from hello command is similar toohello following example.</span></span>
 
    ```
    azure-storage@0.5.0 node_modules\azure-storage
    +-- extend@1.2.1
    +-- xmlbuilder@0.4.3
    +-- mime@1.2.11
    +-- node-uuid@1.4.3
    +-- validator@3.22.2
    +-- underscore@1.4.4
    +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
    +-- xml2js@0.2.7 (sax@0.5.2)
    +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    ```

3. <span data-ttu-id="a35b5-118">Możesz ręcznie uruchomić hello **ls** tooverify polecenia który **węzła\_modułów** folder został utworzony.</span><span class="sxs-lookup"><span data-stu-id="a35b5-118">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="a35b5-119">Wewnątrz tego folderu znajdują się hello **magazyn azure** pakiet, który zawiera biblioteki hello muszą uzyskać dostęp do magazynu.</span><span class="sxs-lookup"><span data-stu-id="a35b5-119">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need to access storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="a35b5-120">Importowanie pakietu hello</span><span class="sxs-lookup"><span data-stu-id="a35b5-120">Import hello package</span></span>
<span data-ttu-id="a35b5-121">Za pomocą Notatnika lub innego edytora tekstu, dodać powitania od góry toohello **server.js** pliku aplikacji hello, w którym ma toouse magazynu:</span><span class="sxs-lookup"><span data-stu-id="a35b5-121">Using Notepad or another text editor, add hello following toohello top the **server.js** file of hello application where you intend toouse storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="a35b5-122">Ustawienia połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="a35b5-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="a35b5-123">Moduł Hello azure odczyta zmiennych środowiskowych hello AZURE\_MAGAZYNU\_konto i AZURE\_MAGAZYNU\_dostępu\_klucz lub AZURE\_MAGAZYNU\_połączenia \_Ciąg tooyour tooconnect informacje wymagane konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="a35b5-123">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="a35b5-124">Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello podczas wywoływania metody **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="a35b5-124">If these environment variables are not set, you must specify hello account information when calling **createQueueService**.</span></span>

<span data-ttu-id="a35b5-125">Na przykład ustawienia zmiennych środowiskowych hello w hello [Azure Portal](https://portal.azure.com) dla witryny sieci Web Azure, zobacz [aplikacji sieci web Node.js w usłudze hello Azure usługa tabel].</span><span class="sxs-lookup"><span data-stu-id="a35b5-125">For an example of setting hello environment variables in hello [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="a35b5-126">Porady: Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="a35b5-126">How To: Create a Queue</span></span>
<span data-ttu-id="a35b5-127">Witaj poniższy kod tworzy **QueueService** obiektu, który pozwala toowork z kolejki.</span><span class="sxs-lookup"><span data-stu-id="a35b5-127">hello following code creates a **QueueService** object, which enables you toowork with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="a35b5-128">Użyj hello **createQueueIfNotExists** metody, która zwraca hello określoną kolejkę, jeśli już istnieje lub tworzy nową kolejkę o określonej nazwie hello, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="a35b5-128">Use hello **createQueueIfNotExists** method, which returns hello specified queue if it already exists or creates a new queue with hello specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="a35b5-129">Jeśli kolejka hello jest tworzona, `result.created` ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="a35b5-129">If hello queue is created, `result.created` is true.</span></span> <span data-ttu-id="a35b5-130">Jeśli istnieje kolejka hello, `result.created` ma wartość false.</span><span class="sxs-lookup"><span data-stu-id="a35b5-130">If hello queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="a35b5-131">Filtry</span><span class="sxs-lookup"><span data-stu-id="a35b5-131">Filters</span></span>
<span data-ttu-id="a35b5-132">Opcjonalne filtrowania operacje mogą być zastosowane toooperations wykonywane przy użyciu **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="a35b5-132">Optional filtering operations can be applied toooperations performed using **QueueService**.</span></span> <span data-ttu-id="a35b5-133">Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę podpisem hello są następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="a35b5-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="a35b5-134">Po wykonaniu przetwarzanie wstępne opcje żądania hello, metoda hello musi toocall przycisk Dalej, przekazywanie wywołania zwrotnego z powitania po podpisaniu:</span><span class="sxs-lookup"><span data-stu-id="a35b5-134">After doing its preprocessing on hello request options, hello method needs toocall "next" passing a callback with hello following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="a35b5-135">W tym wywołania zwrotnego, a po przetworzeniu hello returnObject (hello odpowiedź z serwera toohello żądania hello), wywołania zwrotnego hello musi tooeither obok wywołać, jeśli istnieje toocontinue przetwarzania inne filtry lub po prostu Wywołaj finalCallback w przeciwnym razie tooend się hello wywołania usługi.</span><span class="sxs-lookup"><span data-stu-id="a35b5-135">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend up hello service invocation.</span></span>

<span data-ttu-id="a35b5-136">Dwa filtry, które implementują logikę ponawiania są dołączone hello Azure SDK dla środowiska Node.js, **ExponentialRetryPolicyFilter** i **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="a35b5-136">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="a35b5-137">tworzy następujące Hello **QueueService** obiekt, który używa hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="a35b5-137">hello following creates a **QueueService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="a35b5-138">Porady: Wstawianie komunikatu do kolejki</span><span class="sxs-lookup"><span data-stu-id="a35b5-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="a35b5-139">tooinsert wiadomości do kolejki, użyj hello **polecenie createMessage** metodę, aby utworzyć nową wiadomość i dodać go toohello kolejki.</span><span class="sxs-lookup"><span data-stu-id="a35b5-139">tooinsert a message into a queue, use hello **createMessage** method to create a new message and add it toohello queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="a35b5-140">Porady: Podgląd hello następny komunikat</span><span class="sxs-lookup"><span data-stu-id="a35b5-140">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="a35b5-141">Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **peekMessages** metody.</span><span class="sxs-lookup"><span data-stu-id="a35b5-141">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peekMessages** method.</span></span> <span data-ttu-id="a35b5-142">Domyślnie **peekMessages** wglądu w pojedynczym komunikacie.</span><span class="sxs-lookup"><span data-stu-id="a35b5-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="a35b5-143">Witaj `result` zawiera wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="a35b5-143">hello `result` contains hello message.</span></span>

> [!NOTE]
> <span data-ttu-id="a35b5-144">Przy użyciu **peekMessages** gdy nie ma żadnych komunikatów w kolejce hello nie zwróci błąd, jednak zostanie zwrócony żaden komunikat.</span><span class="sxs-lookup"><span data-stu-id="a35b5-144">Using **peekMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="a35b5-145">Porady: Hello następny komunikat usuwania z kolejki</span><span class="sxs-lookup"><span data-stu-id="a35b5-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="a35b5-146">Przetwarza komunikat jest procesem dwuetapowym:</span><span class="sxs-lookup"><span data-stu-id="a35b5-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="a35b5-147">Wiadomości powitania usuwania z kolejki.</span><span class="sxs-lookup"><span data-stu-id="a35b5-147">Dequeue hello message.</span></span>
2. <span data-ttu-id="a35b5-148">Usuń wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="a35b5-148">Delete hello message.</span></span>

<span data-ttu-id="a35b5-149">Użyj toodequeue komunikat **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="a35b5-149">toodequeue a message, use **getMessages**.</span></span> <span data-ttu-id="a35b5-150">Dzięki temu wiadomości powitania niewidoczne w kolejce hello, więc może je przetwarzać żadnych innych klientów.</span><span class="sxs-lookup"><span data-stu-id="a35b5-150">This makes hello messages invisible in hello queue, so no other clients can process them.</span></span> <span data-ttu-id="a35b5-151">Po przetworzeniu komunikatu aplikacji wywołać **deleteMessage** toodelete ją z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="a35b5-151">Once your application has processed a message, call **deleteMessage** toodelete it from hello queue.</span></span> <span data-ttu-id="a35b5-152">Poniższy przykład Hello pobiera komunikat, a następnie usuwa je:</span><span class="sxs-lookup"><span data-stu-id="a35b5-152">hello following example gets a message, then deletes it:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> <span data-ttu-id="a35b5-153">Domyślnie komunikat jest ukryty tylko przez 30 sekund, po których jest widoczna tooother klientów.</span><span class="sxs-lookup"><span data-stu-id="a35b5-153">By default, a message is only hidden for 30 seconds, after which it is visible tooother clients.</span></span> <span data-ttu-id="a35b5-154">Określ inną wartość, przy użyciu `options.visibilityTimeout` z **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="a35b5-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="a35b5-155">Przy użyciu **getMessages** gdy nie ma żadnych komunikatów w kolejce hello nie zwróci błąd, jednak zostanie zwrócony żaden komunikat.</span><span class="sxs-lookup"><span data-stu-id="a35b5-155">Using **getMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="a35b5-156">Porady: Zmiana zawartości hello wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="a35b5-156">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="a35b5-157">Możesz zmienić zawartość komunikatu w miejscu przy użyciu kolejki hello hello **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="a35b5-157">You can change hello contents of a message in-place in hello queue using **updateMessage**.</span></span> <span data-ttu-id="a35b5-158">Poniższy przykład Hello aktualizuje tekst wiadomości powitania:</span><span class="sxs-lookup"><span data-stu-id="a35b5-158">hello following example updates hello text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="a35b5-159">Porady: Dodatkowych opcji usuwania komunikatów</span><span class="sxs-lookup"><span data-stu-id="a35b5-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="a35b5-160">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki:</span><span class="sxs-lookup"><span data-stu-id="a35b5-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="a35b5-161">`options.numOfMessages`-Pobrać partii komunikatów (w górę too32).</span><span class="sxs-lookup"><span data-stu-id="a35b5-161">`options.numOfMessages` - Retrieve a batch of messages (up too32.)</span></span>
* <span data-ttu-id="a35b5-162">`options.visibilityTimeout`-Ustawienia limit czasu niewidoczności dłuższy lub krótszy.</span><span class="sxs-lookup"><span data-stu-id="a35b5-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="a35b5-163">Witaj poniższym przykładzie użyto hello **getMessages** metody tooget 15 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="a35b5-163">hello following example uses hello **getMessages** method tooget 15 messages in one call.</span></span> <span data-ttu-id="a35b5-164">Następnie przetwarza każdy komunikat przy użyciu pętli for.</span><span class="sxs-lookup"><span data-stu-id="a35b5-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="a35b5-165">Ustawia również minut toofive limitu czasu niewidoczności hello wszystkie komunikaty zwracane przez tę metodę.</span><span class="sxs-lookup"><span data-stu-id="a35b5-165">It also sets hello invisibility timeout toofive minutes for all messages returned by this method.</span></span>

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="a35b5-166">Porady: Uzyskiwanie hello długość kolejki</span><span class="sxs-lookup"><span data-stu-id="a35b5-166">How To: Get hello Queue Length</span></span>
<span data-ttu-id="a35b5-167">Witaj **getQueueMetadata** zwraca metadane dotyczące kolejki hello, łącznie z hello przybliżoną liczbę komunikatów oczekujących w kolejce hello.</span><span class="sxs-lookup"><span data-stu-id="a35b5-167">hello **getQueueMetadata** returns metadata about hello queue, including hello approximate number of messages waiting in hello queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="a35b5-168">Porady: Lista kolejek</span><span class="sxs-lookup"><span data-stu-id="a35b5-168">How To: List Queues</span></span>
<span data-ttu-id="a35b5-169">Lista kolejek, użyj tooretrieve **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="a35b5-169">tooretrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="a35b5-170">tooretrieve listy filtrowane według określonego prefiksu, użyj **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="a35b5-170">tooretrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

<span data-ttu-id="a35b5-171">Jeśli nie można zwrócić wszystkich kolejek, `result.continuationToken` mogą służyć jako pierwszy parametr hello **listQueuesSegmented** lub hello drugi parametr funkcji **listQueuesSegmentedWithPrefix** tooretrieve więcej wyników.</span><span class="sxs-lookup"><span data-stu-id="a35b5-171">If all queues cannot be returned, `result.continuationToken` can be used as hello first parameter of **listQueuesSegmented** or hello second parameter of **listQueuesSegmentedWithPrefix** tooretrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="a35b5-172">Porady: Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="a35b5-172">How To: Delete a Queue</span></span>
<span data-ttu-id="a35b5-173">toodelete kolejkę i wszystkie wiadomości powitania zawartych w nim, należy wywołać **deleteQueue** metody dla obiekt kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="a35b5-173">toodelete a queue and all hello messages contained in it, call the **deleteQueue** method on hello queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="a35b5-174">Użyj wszystkich wiadomości z kolejki usuwając, tooclear **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="a35b5-174">tooclear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="a35b5-175">Porady: Praca z sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="a35b5-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="a35b5-176">Udostępniony sygnatur dostępu (SAS) są tooqueues szczegółowego dostępu tooprovide bezpieczny sposób, bez konieczności podawania Twojej nazwy konta magazynu lub kluczy.</span><span class="sxs-lookup"><span data-stu-id="a35b5-176">Shared Access Signatures (SAS) are a secure way tooprovide granular access tooqueues without providing your storage account name or keys.</span></span> <span data-ttu-id="a35b5-177">Skojarzenia zabezpieczeń są często używane tooprovide ograniczone dostępu tooyour kolejki, na przykład pozwala aplikacji mobilnej toosubmit wiadomości.</span><span class="sxs-lookup"><span data-stu-id="a35b5-177">SAS are often used tooprovide limited access tooyour queues, such as allowing a mobile app toosubmit messages.</span></span>

<span data-ttu-id="a35b5-178">Zaufanych aplikacji, takich jak jest usługą opartą na chmurze generuje sygnaturę dostępu Współdzielonego przy użyciu hello **generateSharedAccessSignature** z hello **QueueService**i udostępnia go tooan niezaufanych lub częściowo zaufanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a35b5-178">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **QueueService**, and provides it tooan untrusted or semi-trusted application.</span></span> <span data-ttu-id="a35b5-179">Na przykład aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="a35b5-179">For example, a mobile app.</span></span> <span data-ttu-id="a35b5-180">Hello sygnatury dostępu Współdzielonego jest generowany przy użyciu zasad, które opisano hello rozpoczęcia i daty zakończenia, podczas których hello SAS jest prawidłowy, a także hello posiadacz SAS toohello nadanego poziomu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a35b5-180">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="a35b5-181">Poniższy przykład Hello generuje nowe zasady dostępu współdzielonego, które umożliwią hello SAS posiadacz tooadd wiadomości toohello kolejki i wygasa 100 minut po uruchomieniu hello jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="a35b5-181">hello following example generates a new shared access policy that will allow hello SAS holder tooadd messages toohello queue, and expires 100 minutes after hello time it is created.</span></span>

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

<span data-ttu-id="a35b5-182">Należy pamiętać, że informacji o hoście hello należy dostarczyć także zgodnie z wymaganiami podczas posiadacz SAS hello prób tooaccess hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="a35b5-182">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello queue.</span></span>

<span data-ttu-id="a35b5-183">Witaj aplikacji klienckiej, a następnie używa hello SAS z **QueueServiceWithSAS** tooperform operacji względem hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="a35b5-183">hello client application then uses hello SAS with **QueueServiceWithSAS** tooperform operations against hello queue.</span></span> <span data-ttu-id="a35b5-184">Poniższy przykład Hello łączy toohello kolejki i tworzy komunikat.</span><span class="sxs-lookup"><span data-stu-id="a35b5-184">hello following example connects toohello queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="a35b5-185">Ponieważ hello SAS został wygenerowany z Dodawanie dostępu, jeśli próba wprowadzono tooread, aktualizowanie lub usuwanie wiadomości, czy zwracany błąd.</span><span class="sxs-lookup"><span data-stu-id="a35b5-185">Since hello SAS was generated with add access, if an attempt were made tooread, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="a35b5-186">Listy kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="a35b5-186">Access control lists</span></span>
<span data-ttu-id="a35b5-187">Umożliwia także zasad dostępu hello tooset listy kontroli dostępu (ACL) dla sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="a35b5-187">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="a35b5-188">Jest to przydatne, jeśli chcesz tooallow wielu klientów tooaccess hello kolejki, ale zawiera różne zasady dostępu dla każdego klienta.</span><span class="sxs-lookup"><span data-stu-id="a35b5-188">This is useful if you wish tooallow multiple clients tooaccess hello queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="a35b5-189">Listy ACL jest zaimplementowana przy użyciu tablicy zasad dostępu w usłudze identyfikator skojarzony z każdej zasady.</span><span class="sxs-lookup"><span data-stu-id="a35b5-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="a35b5-190">Poniższy przykład Hello definiuje dwie zasady; jeden dla "Użytkownik1" i jeden dla "uzytkownik2":</span><span class="sxs-lookup"><span data-stu-id="a35b5-190">hello  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="a35b5-191">powitania po pobiera przykład Witaj bieżącej listy ACL dla **Moja_kolejka**, następnie dodaje nowe zasady hello przy użyciu **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="a35b5-191">hello following example gets hello current ACL for **myqueue**, then adds hello new policies using **setQueueAcl**.</span></span> <span data-ttu-id="a35b5-192">Takie podejście umożliwia:</span><span class="sxs-lookup"><span data-stu-id="a35b5-192">This approach allows:</span></span>

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="a35b5-193">Raz hello ustawione listy ACL, następnie można utworzyć sygnatury dostępu Współdzielonego na podstawie Identyfikatora hello zasad.</span><span class="sxs-lookup"><span data-stu-id="a35b5-193">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="a35b5-194">Witaj poniższy przykład powoduje utworzenie nowej sygnatury dostępu Współdzielonego dla "uzytkownik2":</span><span class="sxs-lookup"><span data-stu-id="a35b5-194">hello following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="a35b5-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a35b5-195">Next Steps</span></span>
<span data-ttu-id="a35b5-196">Teraz, kiedy znasz już podstawy magazynu kolejek hello, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu.</span><span class="sxs-lookup"><span data-stu-id="a35b5-196">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="a35b5-197">Odwiedź hello [Blog zespołu usługi Magazyn Azure][Azure Storage Team Blog].</span><span class="sxs-lookup"><span data-stu-id="a35b5-197">Visit hello [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="a35b5-198">Odwiedź hello [zestawu SDK usługi Magazyn Azure dla węzła] [ Azure Storage SDK for Node] repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="a35b5-198">Visit hello [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[tworzenie aplikacji sieci web Node.js w usłudze Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md
[aplikacji sieci web Node.js w usłudze hello Azure usługa tabel]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md


[tworzenie i wdrażanie tooan aplikacji Node.js usługi w chmurze Azure]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[ Tworzenie i wdrażanie tooAzure aplikacji sieci web Node.js za pomocą macierzy sieci Web]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
