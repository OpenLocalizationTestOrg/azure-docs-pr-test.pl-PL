---
title: "Jak używać magazynu kolejek w języku Ruby | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać usługi kolejek platformy Azure do tworzenia i usuwania kolejki, Wstaw, Pobierz i usunąć wiadomości. Przykłady napisany w języku Ruby."
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: b1a7dd36af6c45bf085342cdf9c1c926a5040792
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-ruby"></a><span data-ttu-id="3f6dc-104">Jak używać Magazynu kolejek w języku Ruby</span><span class="sxs-lookup"><span data-stu-id="3f6dc-104">How to use Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="3f6dc-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3f6dc-105">Overview</span></span>
<span data-ttu-id="3f6dc-106">W tym przewodniku przedstawiono sposób wykonywania typowych scenariuszy przy użyciu usługi Microsoft Azure Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="3f6dc-107">Przykłady są napisane przy użyciu interfejsu API Azure Ruby.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-107">The samples are written using the Ruby Azure API.</span></span>
<span data-ttu-id="3f6dc-108">Omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także **tworzenie i usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="3f6dc-109">Tworzenie aplikacji Ruby</span><span class="sxs-lookup"><span data-stu-id="3f6dc-109">Create a Ruby Application</span></span>
<span data-ttu-id="3f6dc-110">Utwórz aplikację dopisków fonetycznych.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-110">Create a Ruby application.</span></span> <span data-ttu-id="3f6dc-111">Aby uzyskać instrukcje, zobacz [dopisków fonetycznych w aplikacji sieci Web szyny na maszynie Wirtualnej platformy Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="3f6dc-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="3f6dc-112">Konfigurowanie aplikacji na dostęp do magazynu</span><span class="sxs-lookup"><span data-stu-id="3f6dc-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="3f6dc-113">Aby korzystać z usługi Azure storage, konieczne pobranie i użycie dopisków fonetycznych pakiet azure zawiera zestaw wygody bibliotek, które komunikują się z magazynu usługi REST.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-113">To use Azure storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="3f6dc-114">Umożliwia uzyskanie pakietu RubyGems</span><span class="sxs-lookup"><span data-stu-id="3f6dc-114">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="3f6dc-115">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="3f6dc-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="3f6dc-116">Wpisz "azure gem instalacji" w oknie wiersza polecenia, aby zainstalować gem i zależności.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-116">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="3f6dc-117">Importowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="3f6dc-117">Import the package</span></span>
<span data-ttu-id="3f6dc-118">Użyj edytora tekstu, Dodaj następujący element do góry pliku dopisków fonetycznych, których zamierzasz używać magazynu:</span><span class="sxs-lookup"><span data-stu-id="3f6dc-118">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="3f6dc-119">Ustawienia połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="3f6dc-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="3f6dc-120">Moduł azure odczyta zmiennych środowiskowych **AZURE\_MAGAZYNU\_konta** i **AZURE\_MAGAZYNU\_ACCESS_KEY** informacji wymagane do łączenia się z kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-120">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="3f6dc-121">Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie przed użyciem **Azure::QueueService** następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="3f6dc-121">If these environment variables are not set, you must specify the account information before using **Azure::QueueService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="3f6dc-122">Aby uzyskać te wartości z klasyczny lub Menedżera zasobów konta magazynu w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="3f6dc-122">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="3f6dc-123">Zaloguj się do witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3f6dc-123">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3f6dc-124">Przejdź do konta magazynu, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-124">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="3f6dc-125">W bloku ustawienia po prawej stronie, kliknij przycisk **klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-125">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="3f6dc-126">W bloku klucze dostępu pojawia się zostanie wyświetlony klucz dostępu 1 i klucz dostępu 2.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-126">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="3f6dc-127">Można użyć jednego z tych.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-127">You can use either of these.</span></span> 
5. <span data-ttu-id="3f6dc-128">Kliknij ikonę kopiowania, aby skopiować klucz do Schowka.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-128">Click the copy icon to copy the key to the clipboard.</span></span> 

## <a name="how-to-create-a-queue"></a><span data-ttu-id="3f6dc-129">Porady: Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="3f6dc-129">How To: Create a Queue</span></span>
<span data-ttu-id="3f6dc-130">Poniższy kod tworzy **Azure::QueueService** obiektu, który umożliwia pracę z kolejki.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-130">The following code creates a **Azure::QueueService** object, which enables you to work with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="3f6dc-131">Użyj **create_queue()** metodę, aby utworzyć kolejkę o określonej nazwie.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-131">Use the **create_queue()** method to create a queue with the specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="3f6dc-132">Porady: Wstawianie komunikatu do kolejki</span><span class="sxs-lookup"><span data-stu-id="3f6dc-132">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="3f6dc-133">Aby wstawić komunikat do kolejki, użyj **create_message()** metodę, aby utworzyć nową wiadomość i dodaj go do kolejki.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-133">To insert a message into a queue, use the **create_message()** method to create a new message and add it to the queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="3f6dc-134">Porady: Podgląd kolejnego komunikatu</span><span class="sxs-lookup"><span data-stu-id="3f6dc-134">How To: Peek at the Next Message</span></span>
<span data-ttu-id="3f6dc-135">Możesz uzyskać wgląd w komunikat z przodu kolejki bez jego usuwania z kolejki, wywołując **peek\_messages()** metody.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-135">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages()** method.</span></span> <span data-ttu-id="3f6dc-136">Domyślnie **peek\_messages()** wglądu w pojedynczym komunikacie.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-136">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="3f6dc-137">Można również określić, ile komunikatów, aby Podgląd.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-137">You can also specify how many messages you want to peek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="3f6dc-138">Porady: Następny komunikat usuwania z kolejki</span><span class="sxs-lookup"><span data-stu-id="3f6dc-138">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="3f6dc-139">Można usunąć wiadomości z kolejki w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-139">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="3f6dc-140">Podczas wywoływania **listy\_messages()**, Pobierz następnej wiadomości w kolejce domyślnie.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-140">When you call **list\_messages()**, you get the next message in a queue by default.</span></span> <span data-ttu-id="3f6dc-141">Można również określić, ile komunikatów, które chcesz pobrać.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-141">You can also specify how many messages you want to get.</span></span> <span data-ttu-id="3f6dc-142">Komunikaty zwracane z **listy\_messages()** staje się niewidoczny dla innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-142">The messages returned from **list\_messages()** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="3f6dc-143">Przekaż widoczność limit czasu w sekundach jako parametr.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-143">You pass in the visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="3f6dc-144">Aby zakończyć usuwanie komunikatu z kolejki, musisz również wywołać **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-144">To finish removing the message from the queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="3f6dc-145">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że gdy kodu nie może przetworzyć komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu można uzyskać ten sam komunikat i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-145">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="3f6dc-146">Twój kod wywołuje **usunąć\_message()** natychmiast po przetworzeniu komunikatu.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-146">Your code calls **delete\_message()** right after the message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="3f6dc-147">Porady: Zmiana zawartości komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="3f6dc-147">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="3f6dc-148">Możesz zmienić zawartość komunikatu w kolejce.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-148">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="3f6dc-149">Kod poniżej używa **update_message()** metodę aktualizowania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-149">The code below uses the **update_message()** method to update a message.</span></span> <span data-ttu-id="3f6dc-150">Metoda zwraca spójną kolekcję zawierającą pop odbieranie komunikatu w kolejce i UTC wartość daty i godziny reprezentujące komunikat będzie widoczny w kolejce.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-150">The method will return a tuple which contains the pop receipt of the queue message and a UTC date time value that represents when the message will be visible on the queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="3f6dc-151">Porady: Dodatkowych opcji usuwania komunikatów</span><span class="sxs-lookup"><span data-stu-id="3f6dc-151">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="3f6dc-152">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-152">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="3f6dc-153">Możesz uzyskać partii komunikatu.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-153">You can get a batch of message.</span></span>
2. <span data-ttu-id="3f6dc-154">Można ustawić limitu czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie bardziej lub mniej czasu na pełne przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-154">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="3f6dc-155">Poniższy przykład kodu wykorzystuje **listy\_messages()** metodę, aby pobrać 15 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-155">The following code example uses the **list\_messages()** method to get 15 messages in one call.</span></span> <span data-ttu-id="3f6dc-156">Następnie wyświetla i usuwa każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-156">Then it prints and deletes each message.</span></span> <span data-ttu-id="3f6dc-157">Ustawia również limitu czasu niewidoczności na pięć minut dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-157">It also sets the invisibility timeout to five minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="3f6dc-158">Porady: Pobieranie długości kolejki</span><span class="sxs-lookup"><span data-stu-id="3f6dc-158">How To: Get the Queue Length</span></span>
<span data-ttu-id="3f6dc-159">Możesz uzyskać oszacowanie liczbę wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-159">You can get an estimation of the number of messages in the queue.</span></span> <span data-ttu-id="3f6dc-160">**Uzyskać\_kolejki\_metadata()** metody prosi usługę kolejki, aby przekazać przybliżone wiadomości i metadane dotyczące kolejki.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-160">The **get\_queue\_metadata()** method asks the queue service to return the approximate message count and metadata about the queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="3f6dc-161">Porady: Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="3f6dc-161">How To: Delete a Queue</span></span>
<span data-ttu-id="3f6dc-162">Aby usunąć kolejkę i wszystkie zawarte w niej komunikaty, wywołaj **usunąć\_queue()** metody dla obiekt kolejki.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-162">To delete a queue and all the messages contained in it, call the **delete\_queue()** method on the queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="3f6dc-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3f6dc-163">Next Steps</span></span>
<span data-ttu-id="3f6dc-164">Teraz, kiedy znasz już podstawy magazynu kolejek, skorzystaj z poniższych linków, aby dowiedzieć się więcej o bardziej skomplikowanych zadaniach magazynu.</span><span class="sxs-lookup"><span data-stu-id="3f6dc-164">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="3f6dc-165">Odwiedź stronę [Blog zespołu usługi Magazyn Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="3f6dc-165">Visit the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="3f6dc-166">Odwiedź stronę [zestawu Azure SDK dla środowiska Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repozytorium w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="3f6dc-166">Visit the [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="3f6dc-167">Porównanie między omówione w tym artykule usługi kolejek platformy Azure i Azure kolejek usługi Service Bus omówione w [jak używać kolejek usługi Service Bus](/develop/ruby/how-to-guides/service-bus-queues/) artykułu, zobacz [kolejek Azure i kolejek usługi Service Bus - porównaniu i Odróżniające](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="3f6dc-167">For a comparison between the Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in the [How to use Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>