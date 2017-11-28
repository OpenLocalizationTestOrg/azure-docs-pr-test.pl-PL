---
title: "toouse aaaHow magazynu kolejek w języku Python | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello usługi kolejek platformy Azure z Python toocreate i usuwanie kolejek, wstawianie, Pobierz i usunąć wiadomości."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: ce8d999d9fafaef0dab48442560d004c034c0804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a><span data-ttu-id="e7537-103">Jak toouse magazynu kolejek w języku Python</span><span class="sxs-lookup"><span data-stu-id="e7537-103">How toouse Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="e7537-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e7537-104">Overview</span></span>
<span data-ttu-id="e7537-105">Ten przewodnik przedstawia, jak tooperform typowych scenariuszy przy użyciu hello usługi magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="e7537-105">This guide shows you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="e7537-106">Witaj przykłady są napisane w języku Python i używają hello [Microsoft Azure magazynu SDK dla języka Python].</span><span class="sxs-lookup"><span data-stu-id="e7537-106">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="e7537-107">Hello omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także  **Tworzenie i usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="e7537-107">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="e7537-108">Więcej informacji dotyczących kolejek można znaleźć w sekcji toohello [następne kroki].</span><span class="sxs-lookup"><span data-stu-id="e7537-108">For more information on queues, refer toohello [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="e7537-109">Porady: Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="e7537-109">How To: Create a Queue</span></span>
<span data-ttu-id="e7537-110">Witaj **QueueService** obiektu umożliwia pracę z kolejki.</span><span class="sxs-lookup"><span data-stu-id="e7537-110">hello **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="e7537-111">Witaj poniższy kod tworzy **QueueService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="e7537-111">hello following code creates a **QueueService** object.</span></span> <span data-ttu-id="e7537-112">Dodaj następujące hello górze hello dowolny plik Python, w którym chcesz tooprogrammatically dostępu do magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="e7537-112">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="e7537-113">Witaj poniższy kod tworzy **QueueService** obiektu przy użyciu hello magazynu konta nazwy i klucza konta.</span><span class="sxs-lookup"><span data-stu-id="e7537-113">hello following code creates a **QueueService** object using hello storage account name and account key.</span></span> <span data-ttu-id="e7537-114">Zamień "myaccount" i "klucze" Nazwa konta i klucz.</span><span class="sxs-lookup"><span data-stu-id="e7537-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="e7537-115">Porady: Wstawianie komunikatu do kolejki</span><span class="sxs-lookup"><span data-stu-id="e7537-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="e7537-116">tooinsert wiadomości do kolejki, użyj hello **put\_komunikat** metodę, aby utworzyć nową wiadomość i dodać go toohello kolejki.</span><span class="sxs-lookup"><span data-stu-id="e7537-116">tooinsert a message into a queue, use hello **put\_message** method to create a new message and add it toohello queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="e7537-117">Porady: Podgląd hello następny komunikat</span><span class="sxs-lookup"><span data-stu-id="e7537-117">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="e7537-118">Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **peek\_wiadomości** metody.</span><span class="sxs-lookup"><span data-stu-id="e7537-118">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages** method.</span></span> <span data-ttu-id="e7537-119">Domyślnie **peek\_wiadomości** wglądu w pojedynczym komunikacie.</span><span class="sxs-lookup"><span data-stu-id="e7537-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="e7537-120">Porady: Usuwania z kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="e7537-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="e7537-121">Twój kod usuwa komunikat z kolejki w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="e7537-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="e7537-122">Podczas wywoływania **uzyskać\_wiadomości**, Pobierz hello następnej wiadomości w kolejce domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e7537-122">When you call **get\_messages**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="e7537-123">Komunikat zwrócony z **uzyskać\_wiadomości** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="e7537-123">A message returned from **get\_messages** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="e7537-124">Domyślnie komunikat pozostanie niewidoczny przez 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="e7537-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="e7537-125">toofinish usuwania wiadomość hello z kolejki hello, musisz również wywołać **usunąć\_komunikat**.</span><span class="sxs-lookup"><span data-stu-id="e7537-125">toofinish removing hello message from hello queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="e7537-126">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że gdy kodu nie powiedzie się tooprocess komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu można uzyskać ten sam komunikat i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="e7537-126">This two-step process of removing a message assures that when your code fails tooprocess a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="e7537-127">Twój kod wywołuje **usunąć\_komunikat** natychmiast po przetworzeniu wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="e7537-127">Your code calls **delete\_message** right after hello message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="e7537-128">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="e7537-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="e7537-129">Po pierwsze można uzyskać partię komunikatów (w górę too32).</span><span class="sxs-lookup"><span data-stu-id="e7537-129">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="e7537-130">Po drugie można ustawić limit czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="e7537-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="e7537-131">następujące Hello przykład kodu wykorzystuje **uzyskać\_wiadomości** metody tooget 16 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="e7537-131">hello following code example uses the **get\_messages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="e7537-132">Następnie przetwarza każdy komunikat przy użyciu pętli for.</span><span class="sxs-lookup"><span data-stu-id="e7537-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="e7537-133">Ustawia również hello limitu czasu niewidoczności na pięć minut dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="e7537-133">It also sets hello invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="e7537-134">Porady: Zmiana zawartości hello wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="e7537-134">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="e7537-135">Można zmienić zawartość komunikatu w miejscu w kolejce hello hello.</span><span class="sxs-lookup"><span data-stu-id="e7537-135">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="e7537-136">Jeśli komunikat reprezentuje zadanie robocze, możesz użyć tej funkcji tooupdate stan hello zadania.</span><span class="sxs-lookup"><span data-stu-id="e7537-136">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="e7537-137">Poniższy kod Hello używa hello **aktualizacji\_komunikat** tooupdate metody wiadomość.</span><span class="sxs-lookup"><span data-stu-id="e7537-137">hello code below uses hello **update\_message** method tooupdate a message.</span></span> <span data-ttu-id="e7537-138">limit czasu widoczności Hello ustawiono too0, co oznacza komunikat jest wyświetlany natychmiast i aktualizowania zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="e7537-138">hello visibility timeout is set too0, meaning the message appears immediately and hello content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="e7537-139">Porady: Uzyskiwanie hello długość kolejki</span><span class="sxs-lookup"><span data-stu-id="e7537-139">How To: Get hello Queue Length</span></span>
<span data-ttu-id="e7537-140">Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="e7537-140">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="e7537-141">**Uzyskać\_kolejki\_metadanych** metody zapyta hello kolejki usługi tooreturn metadane dotyczące hello kolejki i hello **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="e7537-141">The **get\_queue\_metadata** method asks hello queue service tooreturn metadata about hello queue, and hello **approximate_message_count**.</span></span> <span data-ttu-id="e7537-142">wynik Hello jest tylko przybliżonej, ponieważ komunikaty mogą dodane lub usunięte po usługa kolejki odpowiada tooyour żądania.</span><span class="sxs-lookup"><span data-stu-id="e7537-142">hello result is only approximate because messages can be added or removed after the queue service responds tooyour request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="e7537-143">Porady: Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="e7537-143">How To: Delete a Queue</span></span>
<span data-ttu-id="e7537-144">toodelete kolejkę i wszystkie wiadomości powitania zawartych w nim, należy wywołać **usunąć\_kolejki** metody.</span><span class="sxs-lookup"><span data-stu-id="e7537-144">toodelete a queue and all hello messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="e7537-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e7537-145">Next Steps</span></span>
<span data-ttu-id="e7537-146">Teraz, kiedy znasz już podstawy magazynu kolejek hello, wykonaj te więcej toolearn łącza.</span><span class="sxs-lookup"><span data-stu-id="e7537-146">Now that you've learned hello basics of Queue storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="e7537-147">Centrum deweloperów języka Python</span><span class="sxs-lookup"><span data-stu-id="e7537-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="e7537-148">Interfejs API REST usług Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e7537-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="e7537-149">[Blog zespołu odpowiedzialnego za usługę Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="e7537-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="e7537-150">[Microsoft Azure magazynu SDK dla języka Python]</span><span class="sxs-lookup"><span data-stu-id="e7537-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog zespołu odpowiedzialnego za usługę Azure Storage]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure magazynu SDK dla języka Python]: https://github.com/Azure/azure-storage-python