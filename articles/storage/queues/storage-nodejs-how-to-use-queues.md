---
title: "Jak używać magazynu kolejek w oprogramowaniu Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać usługi kolejek platformy Azure do tworzenia i usuwania kolejki, Wstaw, Pobierz i usunąć wiadomości. Przykłady zapisywane w środowisku Node.js."
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
ms.openlocfilehash: 15c1d3cb6eac8fc14837277c4a4275dea91701cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-nodejs"></a><span data-ttu-id="a04f9-104">Jak używać Magazynu kolejek w oprogramowaniu Node.js</span><span class="sxs-lookup"><span data-stu-id="a04f9-104">How to use Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="a04f9-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a04f9-105">Overview</span></span>
<span data-ttu-id="a04f9-106">W tym przewodniku przedstawiono sposób wykonywania typowych scenariuszy przy użyciu usługi Microsoft Azure kolejki.</span><span class="sxs-lookup"><span data-stu-id="a04f9-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue service.</span></span> <span data-ttu-id="a04f9-107">Przykłady są napisane przy użyciu interfejsu API środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="a04f9-107">The samples are written using the Node.js API.</span></span> <span data-ttu-id="a04f9-108">Omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także **tworzenie i usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="a04f9-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="a04f9-109">Tworzenie aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="a04f9-109">Create a Node.js Application</span></span>
<span data-ttu-id="a04f9-110">Utwórz pustą aplikację Node.js.</span><span class="sxs-lookup"><span data-stu-id="a04f9-110">Create a blank Node.js application.</span></span> <span data-ttu-id="a04f9-111">Instrukcje dotyczące tworzenia aplikacji programu Node.js znajdują się [tworzenie aplikacji sieci web Node.js w usłudze Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md), [tworzenia i wdrażania aplikacji Node.js do usługi w chmurze platformy Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) przy użyciu programu Windows PowerShell lub [tworzenie i wdrażanie aplikacji sieci web Node.js na platformie Azure przy użyciu Web Matrix](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="a04f9-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md), [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="a04f9-112">Konfigurowanie aplikacji na dostęp do magazynu</span><span class="sxs-lookup"><span data-stu-id="a04f9-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="a04f9-113">Korzystanie z usługi Azure storage, wymaga zestawu SDK usługi Magazyn Azure dla środowiska Node.js, w tym zestaw wygody bibliotek, które komunikują się z magazynu usługi REST.</span><span class="sxs-lookup"><span data-stu-id="a04f9-113">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="a04f9-114">Umożliwia uzyskanie pakietu węzeł Menedżera pakietów (NPM)</span><span class="sxs-lookup"><span data-stu-id="a04f9-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="a04f9-115">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix), przejdź do folderu, w którym utworzono przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a04f9-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="a04f9-116">Typ **magazyn azure instalacji narzędzia npm** w oknie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a04f9-116">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="a04f9-117">Dane wyjściowe polecenia jest podobny do poniższego przykładu.</span><span class="sxs-lookup"><span data-stu-id="a04f9-117">Output from the command is similar to the following example.</span></span>
 
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

3. <span data-ttu-id="a04f9-118">Możesz ręcznie uruchomić **ls** polecenie, aby sprawdzić, czy **węzła\_modułów** folder został utworzony.</span><span class="sxs-lookup"><span data-stu-id="a04f9-118">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="a04f9-119">Wewnątrz tego folderu znajdują się **magazyn azure** pakiet, który zawiera biblioteki muszą uzyskać dostęp do magazynu.</span><span class="sxs-lookup"><span data-stu-id="a04f9-119">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="a04f9-120">Importowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="a04f9-120">Import the package</span></span>
<span data-ttu-id="a04f9-121">Za pomocą Notatnika lub innego edytora tekstu, Dodaj następujący element do góry **server.js** pliku aplikacji, których zamierzasz używać magazynu:</span><span class="sxs-lookup"><span data-stu-id="a04f9-121">Using Notepad or another text editor, add the following to the top the **server.js** file of the application where you intend to use storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="a04f9-122">Ustawienia połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="a04f9-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="a04f9-123">Moduł azure odczyta zmiennych środowiskowych AZURE\_MAGAZYNU\_konto i AZURE\_MAGAZYNU\_dostępu\_klucz lub AZURE\_MAGAZYNU\_połączenia\_ciąg informacje wymagane do łączenia się z kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a04f9-123">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="a04f9-124">Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie podczas wywoływania metody **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="a04f9-124">If these environment variables are not set, you must specify the account information when calling **createQueueService**.</span></span>

<span data-ttu-id="a04f9-125">Ustawianie zmiennych środowiskowych, na przykład [Azure Portal](https://portal.azure.com) dla witryny sieci Web Azure, zobacz [aplikacji sieci web Node.js przy użyciu usługi Azure tabeli].</span><span class="sxs-lookup"><span data-stu-id="a04f9-125">For an example of setting the environment variables in the [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="a04f9-126">Porady: Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="a04f9-126">How To: Create a Queue</span></span>
<span data-ttu-id="a04f9-127">Poniższy kod tworzy **QueueService** obiektu, który umożliwia pracę z kolejki.</span><span class="sxs-lookup"><span data-stu-id="a04f9-127">The following code creates a **QueueService** object, which enables you to work with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="a04f9-128">Użyj **createQueueIfNotExists** metody, która zwraca określoną kolejkę, jeśli już istnieje lub tworzy nową kolejkę o określonej nazwie, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="a04f9-128">Use the **createQueueIfNotExists** method, which returns the specified queue if it already exists or creates a new queue with the specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="a04f9-129">Jeśli kolejka została utworzona, `result.created` ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="a04f9-129">If the queue is created, `result.created` is true.</span></span> <span data-ttu-id="a04f9-130">Jeśli kolejka istnieje, `result.created` ma wartość false.</span><span class="sxs-lookup"><span data-stu-id="a04f9-130">If the queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="a04f9-131">Filtry</span><span class="sxs-lookup"><span data-stu-id="a04f9-131">Filters</span></span>
<span data-ttu-id="a04f9-132">Opcjonalne operacjach filtrowania może odnosić się do operacji wykonywanych przy użyciu **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="a04f9-132">Optional filtering operations can be applied to operations performed using **QueueService**.</span></span> <span data-ttu-id="a04f9-133">Filtrowanie operacje mogą obejmować rejestrowania, Automatyczne ponawianie próby itp. Obiekty, które implementują metodę o sygnaturze są następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="a04f9-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="a04f9-134">Po wykonaniu przetwarzanie wstępne opcje żądania, metoda musi wywołać "dalej" przekazywanie wywołania zwrotnego z następującą sygnaturą:</span><span class="sxs-lookup"><span data-stu-id="a04f9-134">After doing its preprocessing on the request options, the method needs to call "next" passing a callback with the following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="a04f9-135">W tym wywołania zwrotnego, a po przetworzeniu returnObject (odpowiedź z żądania do serwera) wywołania zwrotnego musi wywołać obok, jeśli istnieje kontynuować przetwarzanie inne filtry lub po prostu Wywołaj finalCallback inaczej tworzyć wywołania usługi.</span><span class="sxs-lookup"><span data-stu-id="a04f9-135">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end up the service invocation.</span></span>

<span data-ttu-id="a04f9-136">Dwa filtry, które implementują logikę ponawiania wchodzą w skład zestawu Azure SDK dla środowiska Node.js, **ExponentialRetryPolicyFilter** i **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="a04f9-136">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="a04f9-137">Tworzy następujące **QueueService** obiekt, który używa **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="a04f9-137">The following creates a **QueueService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="a04f9-138">Porady: Wstawianie komunikatu do kolejki</span><span class="sxs-lookup"><span data-stu-id="a04f9-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="a04f9-139">Aby wstawić komunikat do kolejki, użyj **polecenie createMessage** metodę, aby utworzyć nową wiadomość i dodaj go do kolejki.</span><span class="sxs-lookup"><span data-stu-id="a04f9-139">To insert a message into a queue, use the **createMessage** method to create a new message and add it to the queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="a04f9-140">Porady: Podgląd kolejnego komunikatu</span><span class="sxs-lookup"><span data-stu-id="a04f9-140">How To: Peek at the Next Message</span></span>
<span data-ttu-id="a04f9-141">Możesz uzyskać wgląd w komunikat z przodu kolejki bez jego usuwania z kolejki, wywołując **peekMessages** metody.</span><span class="sxs-lookup"><span data-stu-id="a04f9-141">You can peek at the message in the front of a queue without removing it from the queue by calling the **peekMessages** method.</span></span> <span data-ttu-id="a04f9-142">Domyślnie **peekMessages** wglądu w pojedynczym komunikacie.</span><span class="sxs-lookup"><span data-stu-id="a04f9-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="a04f9-143">`result` Zawiera komunikat.</span><span class="sxs-lookup"><span data-stu-id="a04f9-143">The `result` contains the message.</span></span>

> [!NOTE]
> <span data-ttu-id="a04f9-144">Przy użyciu **peekMessages** gdy nie ma żadnych komunikatów w kolejce nie zwróci błąd, jednak zostanie zwrócony żaden komunikat.</span><span class="sxs-lookup"><span data-stu-id="a04f9-144">Using **peekMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="a04f9-145">Porady: Następny komunikat usuwania z kolejki</span><span class="sxs-lookup"><span data-stu-id="a04f9-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="a04f9-146">Przetwarza komunikat jest procesem dwuetapowym:</span><span class="sxs-lookup"><span data-stu-id="a04f9-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="a04f9-147">Usuwania z kolejki wiadomości.</span><span class="sxs-lookup"><span data-stu-id="a04f9-147">Dequeue the message.</span></span>
2. <span data-ttu-id="a04f9-148">Usunięcie wiadomości.</span><span class="sxs-lookup"><span data-stu-id="a04f9-148">Delete the message.</span></span>

<span data-ttu-id="a04f9-149">Aby usunąć wiadomości z kolejki, użyj **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="a04f9-149">To dequeue a message, use **getMessages**.</span></span> <span data-ttu-id="a04f9-150">Dzięki temu wiadomości niewidoczne w kolejce, więc może je przetwarzać żadnych innych klientów.</span><span class="sxs-lookup"><span data-stu-id="a04f9-150">This makes the messages invisible in the queue, so no other clients can process them.</span></span> <span data-ttu-id="a04f9-151">Po przetworzeniu komunikatu aplikacji wywołać **deleteMessage** go usunąć z kolejki.</span><span class="sxs-lookup"><span data-stu-id="a04f9-151">Once your application has processed a message, call **deleteMessage** to delete it from the queue.</span></span> <span data-ttu-id="a04f9-152">Poniższy przykład pobiera komunikat, a następnie usuwa je:</span><span class="sxs-lookup"><span data-stu-id="a04f9-152">The following example gets a message, then deletes it:</span></span>

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
> <span data-ttu-id="a04f9-153">Domyślnie komunikat jest ukryty tylko przez 30 sekund, po którym jest widoczny dla innych klientów.</span><span class="sxs-lookup"><span data-stu-id="a04f9-153">By default, a message is only hidden for 30 seconds, after which it is visible to other clients.</span></span> <span data-ttu-id="a04f9-154">Określ inną wartość, przy użyciu `options.visibilityTimeout` z **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="a04f9-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="a04f9-155">Przy użyciu **getMessages** gdy nie ma żadnych komunikatów w kolejce nie zwróci błąd, jednak zostanie zwrócony żaden komunikat.</span><span class="sxs-lookup"><span data-stu-id="a04f9-155">Using **getMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="a04f9-156">Porady: Zmiana zawartości komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="a04f9-156">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="a04f9-157">Można zmienić zawartość komunikatu w miejscu przy użyciu kolejki **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="a04f9-157">You can change the contents of a message in-place in the queue using **updateMessage**.</span></span> <span data-ttu-id="a04f9-158">Poniższy przykład aktualizuje tekst wiadomości:</span><span class="sxs-lookup"><span data-stu-id="a04f9-158">The following example updates the text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got the message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="a04f9-159">Porady: Dodatkowych opcji usuwania komunikatów</span><span class="sxs-lookup"><span data-stu-id="a04f9-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="a04f9-160">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki:</span><span class="sxs-lookup"><span data-stu-id="a04f9-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="a04f9-161">`options.numOfMessages`-Pobrać partii wiadomości (do 32).</span><span class="sxs-lookup"><span data-stu-id="a04f9-161">`options.numOfMessages` - Retrieve a batch of messages (up to 32.)</span></span>
* <span data-ttu-id="a04f9-162">`options.visibilityTimeout`-Ustawienia limit czasu niewidoczności dłuższy lub krótszy.</span><span class="sxs-lookup"><span data-stu-id="a04f9-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="a04f9-163">W poniższym przykładzie użyto **getMessages** metodę, aby pobrać 15 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="a04f9-163">The following example uses the **getMessages** method to get 15 messages in one call.</span></span> <span data-ttu-id="a04f9-164">Następnie przetwarza każdy komunikat przy użyciu pętli for.</span><span class="sxs-lookup"><span data-stu-id="a04f9-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="a04f9-165">Ustawia również limitu czasu niewidoczności na pięć minut dla wszystkich wiadomości zwracane przez tę metodę.</span><span class="sxs-lookup"><span data-stu-id="a04f9-165">It also sets the invisibility timeout to five minutes for all messages returned by this method.</span></span>

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

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="a04f9-166">Porady: Pobieranie długości kolejki</span><span class="sxs-lookup"><span data-stu-id="a04f9-166">How To: Get the Queue Length</span></span>
<span data-ttu-id="a04f9-167">**GetQueueMetadata** zwraca metadane dotyczące kolejki, w tym przybliżoną liczbę komunikatów oczekujących w kolejce.</span><span class="sxs-lookup"><span data-stu-id="a04f9-167">The **getQueueMetadata** returns metadata about the queue, including the approximate number of messages waiting in the queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="a04f9-168">Porady: Lista kolejek</span><span class="sxs-lookup"><span data-stu-id="a04f9-168">How To: List Queues</span></span>
<span data-ttu-id="a04f9-169">Aby uzyskać listę kolejek, użyj **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="a04f9-169">To retrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="a04f9-170">Aby uzyskać listę filtrowane według określonego prefiksu, użyj **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="a04f9-170">To retrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains the list of queues
  }
});
```

<span data-ttu-id="a04f9-171">Jeśli nie można zwrócić wszystkich kolejek, `result.continuationToken` może być używany jako pierwszy parametr **listQueuesSegmented** lub drugi parametr funkcji **listQueuesSegmentedWithPrefix** można pobrać więcej wyników.</span><span class="sxs-lookup"><span data-stu-id="a04f9-171">If all queues cannot be returned, `result.continuationToken` can be used as the first parameter of **listQueuesSegmented** or the second parameter of **listQueuesSegmentedWithPrefix** to retrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="a04f9-172">Porady: Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="a04f9-172">How To: Delete a Queue</span></span>
<span data-ttu-id="a04f9-173">Aby usunąć kolejkę i wszystkie zawarte w niej komunikaty, wywołaj **deleteQueue** metody dla obiekt kolejki.</span><span class="sxs-lookup"><span data-stu-id="a04f9-173">To delete a queue and all the messages contained in it, call the **deleteQueue** method on the queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="a04f9-174">Aby wyczyścić wszystkie komunikaty z kolejki bez jego usuwania, należy użyć **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="a04f9-174">To clear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="a04f9-175">Porady: Praca z sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="a04f9-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="a04f9-176">Udostępniony sygnatur dostępu (SAS) to bezpieczny sposób zapewnienia szczegółowej dostępu do kolejek bez podawania Twojej nazwy konta magazynu i klucze.</span><span class="sxs-lookup"><span data-stu-id="a04f9-176">Shared Access Signatures (SAS) are a secure way to provide granular access to queues without providing your storage account name or keys.</span></span> <span data-ttu-id="a04f9-177">Skojarzenia zabezpieczeń są często używane do udzielany ograniczony dostęp do kolejek, na przykład pozwala aplikacji mobilnej do przesyłania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="a04f9-177">SAS are often used to provide limited access to your queues, such as allowing a mobile app to submit messages.</span></span>

<span data-ttu-id="a04f9-178">Generuje zaufanych aplikacji, takich jak jest usługą opartą na chmurze przy użyciu sygnatury dostępu Współdzielonego **generateSharedAccessSignature** z **QueueService**i udostępnia go do niezaufanych lub częściowo zaufanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a04f9-178">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **QueueService**, and provides it to an untrusted or semi-trusted application.</span></span> <span data-ttu-id="a04f9-179">Na przykład aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="a04f9-179">For example, a mobile app.</span></span> <span data-ttu-id="a04f9-180">Sygnatury dostępu Współdzielonego jest generowany przy użyciu zasad, opisujący daty rozpoczęcia i zakończenia, w których sygnatury dostępu Współdzielonego jest prawidłowy, a także poziom dostępu przyznane posiadacz sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="a04f9-180">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="a04f9-181">Poniższy przykład generuje nowe zasady dostępu współdzielonego, które umożliwia właścicielowi SAS dodać wiadomości do kolejki i wygasa 100 minut po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="a04f9-181">The following example generates a new shared access policy that will allow the SAS holder to add messages to the queue, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="a04f9-182">Należy pamiętać, że informacji o hoście należy podać także jako jest wymagana podczas próby dostępu do kolejki posiadacz sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="a04f9-182">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the queue.</span></span>

<span data-ttu-id="a04f9-183">Następnie aplikacja kliencka używa SAS z **QueueServiceWithSAS** wykonywanie operacji względem kolejki.</span><span class="sxs-lookup"><span data-stu-id="a04f9-183">The client application then uses the SAS with **QueueServiceWithSAS** to perform operations against the queue.</span></span> <span data-ttu-id="a04f9-184">Poniższy przykład łączy do kolejki i tworzy komunikat.</span><span class="sxs-lookup"><span data-stu-id="a04f9-184">The following example connects to the queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="a04f9-185">Od czasu skojarzenia zabezpieczeń został wygenerowany z Dodawanie dostępu, jeśli podjęta odczytywać, aktualizować lub usuwać wiadomości, czy zwracany błąd.</span><span class="sxs-lookup"><span data-stu-id="a04f9-185">Since the SAS was generated with add access, if an attempt were made to read, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="a04f9-186">Listy kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="a04f9-186">Access control lists</span></span>
<span data-ttu-id="a04f9-187">Listy kontroli dostępu (ACL) umożliwia także ustawić zasady dostępu dla sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="a04f9-187">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="a04f9-188">Jest to przydatne, jeśli chcesz umożliwić wielu klientów dostępu do kolejki, ale zawiera różne zasady dostępu dla każdego klienta.</span><span class="sxs-lookup"><span data-stu-id="a04f9-188">This is useful if you wish to allow multiple clients to access the queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="a04f9-189">Listy ACL jest zaimplementowana przy użyciu tablicy zasad dostępu w usłudze identyfikator skojarzony z każdej zasady.</span><span class="sxs-lookup"><span data-stu-id="a04f9-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="a04f9-190">W poniższym przykładzie zdefiniowano dwie zasady; jeden dla "Użytkownik1" i jeden dla "uzytkownik2":</span><span class="sxs-lookup"><span data-stu-id="a04f9-190">The  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="a04f9-191">Poniższy przykład pobiera bieżącej listy ACL dla **Moja_kolejka**, następnie dodaje nowe zasady przy użyciu **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="a04f9-191">The following example gets the current ACL for **myqueue**, then adds the new policies using **setQueueAcl**.</span></span> <span data-ttu-id="a04f9-192">Takie podejście umożliwia:</span><span class="sxs-lookup"><span data-stu-id="a04f9-192">This approach allows:</span></span>

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

<span data-ttu-id="a04f9-193">Po ustawieniu listy ACL następnie można utworzyć na podstawie Identyfikatora zasady sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="a04f9-193">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="a04f9-194">Poniższy przykład tworzy nowe sygnatury dostępu Współdzielonego dla "uzytkownik2":</span><span class="sxs-lookup"><span data-stu-id="a04f9-194">The following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="a04f9-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a04f9-195">Next Steps</span></span>
<span data-ttu-id="a04f9-196">Teraz, kiedy znasz już podstawy magazynu kolejek, skorzystaj z poniższych linków, aby dowiedzieć się więcej o bardziej skomplikowanych zadaniach magazynu.</span><span class="sxs-lookup"><span data-stu-id="a04f9-196">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="a04f9-197">Odwiedź [Blog zespołu usługi Azure Storage] [Blog zespołu usługi Magazyn Azure].</span><span class="sxs-lookup"><span data-stu-id="a04f9-197">Visit the [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="a04f9-198">Odwiedź stronę [zestawu SDK usługi Magazyn Azure dla węzła] [ Azure Storage SDK for Node] repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="a04f9-198">Visit the [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com<span data-ttu-id="a04f9-199">
[Tworzenie aplikacji sieci web Node.js w usłudze Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md) </span><span class="sxs-lookup"><span data-stu-id="a04f9-199">
[Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md) </span></span>  
<span data-ttu-id="a04f9-200">[Aplikacja sieci web node.js przy użyciu usługi Azure tabeli](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span><span class="sxs-lookup"><span data-stu-id="a04f9-200">[Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span></span>  


<span data-ttu-id="a04f9-201">[Tworzenie i wdrażanie aplikacji Node.js do usługi w chmurze platformy Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span><span class="sxs-lookup"><span data-stu-id="a04f9-201">[Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span></span>  
<span data-ttu-id="a04f9-202">[Azure Blog zespołu usługi Magazyn]: http://blogs.msdn.com/b/windowsazurestorage/ [tworzenie i wdrażanie aplikacji sieci web Node.js na platformie Azure przy użyciu macierzy sieci Web]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="a04f9-202">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Build and deploy a Node.js web app to Azure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>   
