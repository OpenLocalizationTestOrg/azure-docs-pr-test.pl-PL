---
title: "Jak używać magazynu kolejek w języku Python | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać usługi kolejek platformy Azure w języku Python do tworzenia i usuwania kolejki, Wstaw, Pobierz i usunąć wiadomości."
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
ms.openlocfilehash: 963c11acb7939993568a774cd281145a8059b5a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-python"></a><span data-ttu-id="f21fb-103">Jak używać Magazynu kolejek w języku Python</span><span class="sxs-lookup"><span data-stu-id="f21fb-103">How to use Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="f21fb-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f21fb-104">Overview</span></span>
<span data-ttu-id="f21fb-105">W tym przewodniku przedstawiono sposób wykonywania typowych scenariuszy przy użyciu usługi magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="f21fb-105">This guide shows you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="f21fb-106">Próbki są napisane w języku Python i użyj [Microsoft Azure magazynu SDK dla języka Python].</span><span class="sxs-lookup"><span data-stu-id="f21fb-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="f21fb-107">Omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także **tworzenie i usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="f21fb-107">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="f21fb-108">Aby uzyskać więcej informacji dotyczących kolejek można znaleźć w sekcji [następne kroki].</span><span class="sxs-lookup"><span data-stu-id="f21fb-108">For more information on queues, refer to the [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="f21fb-109">Porady: Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="f21fb-109">How To: Create a Queue</span></span>
<span data-ttu-id="f21fb-110">**QueueService** obiektu umożliwia pracę z kolejki.</span><span class="sxs-lookup"><span data-stu-id="f21fb-110">The **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="f21fb-111">Poniższy kod tworzy **QueueService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="f21fb-111">The following code creates a **QueueService** object.</span></span> <span data-ttu-id="f21fb-112">Dodaj następujący kod w górnej części każdego pliku Python, w którym chcesz uzyskania programowego dostępu do magazynu Azure:</span><span class="sxs-lookup"><span data-stu-id="f21fb-112">Add the following near the top of any Python file in which you wish to programmatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="f21fb-113">Poniższy kod tworzy **QueueService** przy użyciu klucza nazwy i konta konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f21fb-113">The following code creates a **QueueService** object using the storage account name and account key.</span></span> <span data-ttu-id="f21fb-114">Zamień "myaccount" i "klucze" Nazwa konta i klucz.</span><span class="sxs-lookup"><span data-stu-id="f21fb-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="f21fb-115">Porady: Wstawianie komunikatu do kolejki</span><span class="sxs-lookup"><span data-stu-id="f21fb-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="f21fb-116">Aby wstawić komunikat do kolejki, użyj **put\_komunikat** metodę, aby utworzyć nową wiadomość i dodaj go do kolejki.</span><span class="sxs-lookup"><span data-stu-id="f21fb-116">To insert a message into a queue, use the **put\_message** method to create a new message and add it to the queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="f21fb-117">Porady: Podgląd kolejnego komunikatu</span><span class="sxs-lookup"><span data-stu-id="f21fb-117">How To: Peek at the Next Message</span></span>
<span data-ttu-id="f21fb-118">Możesz uzyskać wgląd w komunikat z przodu kolejki bez jego usuwania z kolejki, wywołując **peek\_wiadomości** metody.</span><span class="sxs-lookup"><span data-stu-id="f21fb-118">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages** method.</span></span> <span data-ttu-id="f21fb-119">Domyślnie **peek\_wiadomości** wglądu w pojedynczym komunikacie.</span><span class="sxs-lookup"><span data-stu-id="f21fb-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="f21fb-120">Porady: Usuwania z kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="f21fb-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="f21fb-121">Twój kod usuwa komunikat z kolejki w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="f21fb-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="f21fb-122">Podczas wywoływania **uzyskać\_wiadomości**, Pobierz następnej wiadomości w kolejce domyślnie.</span><span class="sxs-lookup"><span data-stu-id="f21fb-122">When you call **get\_messages**, you get the next message in a queue by default.</span></span> <span data-ttu-id="f21fb-123">Komunikat zwrócony z **uzyskać\_wiadomości** staje się niewidoczny dla innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="f21fb-123">A message returned from **get\_messages** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="f21fb-124">Domyślnie komunikat pozostanie niewidoczny przez 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="f21fb-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="f21fb-125">Aby zakończyć usuwanie komunikatu z kolejki, musisz również wywołać **usunąć\_komunikat**.</span><span class="sxs-lookup"><span data-stu-id="f21fb-125">To finish removing the message from the queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="f21fb-126">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że gdy kodu nie może przetworzyć komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu można uzyskać ten sam komunikat i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="f21fb-126">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="f21fb-127">Twój kod wywołuje **usunąć\_komunikat** natychmiast po przetworzeniu komunikatu.</span><span class="sxs-lookup"><span data-stu-id="f21fb-127">Your code calls **delete\_message** right after the message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="f21fb-128">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="f21fb-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="f21fb-129">Po pierwsze można uzyskać komunikaty zbiorczo (do 32).</span><span class="sxs-lookup"><span data-stu-id="f21fb-129">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="f21fb-130">Po drugie można ustawić dłuższy lub krótszy limit czasu niewidoczności, dzięki czemu kod będzie mieć więcej lub mniej czasu na pełne przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="f21fb-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="f21fb-131">Poniższy przykład kodu wykorzystuje **uzyskać\_wiadomości** metodę, aby pobrać 16 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="f21fb-131">The following code example uses the **get\_messages** method to get 16 messages in one call.</span></span> <span data-ttu-id="f21fb-132">Następnie przetwarza każdy komunikat przy użyciu pętli for.</span><span class="sxs-lookup"><span data-stu-id="f21fb-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="f21fb-133">Ustawia również limitu czasu niewidoczności na pięć minut dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="f21fb-133">It also sets the invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="f21fb-134">Porady: Zmiana zawartości komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="f21fb-134">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="f21fb-135">Możesz zmienić zawartość komunikatu w kolejce.</span><span class="sxs-lookup"><span data-stu-id="f21fb-135">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="f21fb-136">Jeśli komunikat reprezentuje zadanie robocze, możesz użyć tej funkcji, aby zaktualizować stan zadania.</span><span class="sxs-lookup"><span data-stu-id="f21fb-136">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="f21fb-137">Kod poniżej używa **aktualizacji\_komunikat** metodę aktualizowania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f21fb-137">The code below uses the **update\_message** method to update a message.</span></span> <span data-ttu-id="f21fb-138">Limitu czasu widoczności jest równa 0, co oznacza komunikat jest wyświetlany natychmiast i aktualizacji zawartości.</span><span class="sxs-lookup"><span data-stu-id="f21fb-138">The visibility timeout is set to 0, meaning the message appears immediately and the content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="f21fb-139">Porady: Pobieranie długości kolejki</span><span class="sxs-lookup"><span data-stu-id="f21fb-139">How To: Get the Queue Length</span></span>
<span data-ttu-id="f21fb-140">Możesz uzyskać szacunkową liczbę komunikatów w kolejce.</span><span class="sxs-lookup"><span data-stu-id="f21fb-140">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="f21fb-141">**Uzyskać\_kolejki\_metadanych** metody prosi usługę kolejki do zwracania metadanych dotyczących kolejki oraz **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="f21fb-141">The **get\_queue\_metadata** method asks the queue service to return metadata about the queue, and the **approximate_message_count**.</span></span> <span data-ttu-id="f21fb-142">Wynik jest tylko przybliżoną, ponieważ komunikaty mogą dodane lub usunięte po usługa kolejki odpowiada na żądania.</span><span class="sxs-lookup"><span data-stu-id="f21fb-142">The result is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="f21fb-143">Porady: Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="f21fb-143">How To: Delete a Queue</span></span>
<span data-ttu-id="f21fb-144">Aby usunąć kolejkę i wszystkie zawarte w niej komunikaty, wywołaj **usunąć\_kolejki** metody.</span><span class="sxs-lookup"><span data-stu-id="f21fb-144">To delete a queue and all the messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="f21fb-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f21fb-145">Next Steps</span></span>
<span data-ttu-id="f21fb-146">Teraz, kiedy znasz już podstawy magazynu kolejek, skorzystaj z poniższych linków, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="f21fb-146">Now that you've learned the basics of Queue storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="f21fb-147">Centrum deweloperów języka Python</span><span class="sxs-lookup"><span data-stu-id="f21fb-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="f21fb-148">Interfejs API REST usług Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f21fb-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="f21fb-149">[Blog zespołu odpowiedzialnego za usługę Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="f21fb-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="f21fb-150">[Microsoft Azure magazynu SDK dla języka Python]</span><span class="sxs-lookup"><span data-stu-id="f21fb-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog zespołu odpowiedzialnego za usługę Azure Storage]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure magazynu SDK dla języka Python]: https://github.com/Azure/azure-storage-python