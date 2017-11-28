---
title: "toouse aaaHow magazynu kolejek w języku Ruby | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate usługi kolejek platformy Azure hello toouse i usuwania kolejki oraz insert, Pobierz i usunąć wiadomości. Przykłady napisany w języku Ruby."
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
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a><span data-ttu-id="43ef9-104">Jak toouse magazynu kolejek w języku Ruby</span><span class="sxs-lookup"><span data-stu-id="43ef9-104">How toouse Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="43ef9-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="43ef9-105">Overview</span></span>
<span data-ttu-id="43ef9-106">Ten przewodnik przedstawia, jak tooperform typowych scenariuszy przy użyciu hello usługi Microsoft Azure Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="43ef9-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="43ef9-107">Hello przykłady są napisane przy użyciu hello Ruby interfejsu API Azure.</span><span class="sxs-lookup"><span data-stu-id="43ef9-107">hello samples are written using hello Ruby Azure API.</span></span>
<span data-ttu-id="43ef9-108">Hello omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także  **Tworzenie i usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="43ef9-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="43ef9-109">Tworzenie aplikacji Ruby</span><span class="sxs-lookup"><span data-stu-id="43ef9-109">Create a Ruby Application</span></span>
<span data-ttu-id="43ef9-110">Utwórz aplikację dopisków fonetycznych.</span><span class="sxs-lookup"><span data-stu-id="43ef9-110">Create a Ruby application.</span></span> <span data-ttu-id="43ef9-111">Aby uzyskać instrukcje, zobacz [dopisków fonetycznych w aplikacji sieci Web szyny na maszynie Wirtualnej platformy Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="43ef9-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="43ef9-112">Skonfiguruj tooAccess Twoja aplikacja magazynu</span><span class="sxs-lookup"><span data-stu-id="43ef9-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="43ef9-113">toouse magazynu Azure, należy toodownload i użyj hello dopisków fonetycznych azure pakiet, który zawiera zestaw wygody bibliotek, które komunikują się z usługi REST magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="43ef9-113">toouse Azure storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="43ef9-114">Użyj RubyGems tooobtain hello pakietu</span><span class="sxs-lookup"><span data-stu-id="43ef9-114">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="43ef9-115">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="43ef9-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="43ef9-116">Wpisz "gem zainstalować program azure" hello polecenia okna tooinstall hello gem i zależności.</span><span class="sxs-lookup"><span data-stu-id="43ef9-116">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="43ef9-117">Importowanie pakietu hello</span><span class="sxs-lookup"><span data-stu-id="43ef9-117">Import hello package</span></span>
<span data-ttu-id="43ef9-118">Użyj edytora tekstu, Dodaj powitania od góry toohello hello dopisków fonetycznych pliku, w którym ma toouse magazynu:</span><span class="sxs-lookup"><span data-stu-id="43ef9-118">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="43ef9-119">Ustawienia połączenia z magazynem Azure</span><span class="sxs-lookup"><span data-stu-id="43ef9-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="43ef9-120">Moduł Hello azure odczyta zmiennych środowiskowych hello **AZURE\_MAGAZYNU\_konta** i **AZURE\_MAGAZYNU\_ACCESS_KEY** dla Konto magazynu Azure tooyour tooconnect wymaganych informacji.</span><span class="sxs-lookup"><span data-stu-id="43ef9-120">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="43ef9-121">Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello przed użyciem **Azure::QueueService** z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="43ef9-121">If these environment variables are not set, you must specify hello account information before using **Azure::QueueService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="43ef9-122">tooobtain te wartości z klasyczny lub Menedżera zasobów magazynu konta w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="43ef9-122">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="43ef9-123">Zaloguj się za toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43ef9-123">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="43ef9-124">Przejdź toohello konta magazynu, które chcesz toouse.</span><span class="sxs-lookup"><span data-stu-id="43ef9-124">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="43ef9-125">W bloku ustawienia hello na powitania prawo, kliknij przycisk **klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="43ef9-125">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="43ef9-126">W bloku klucze dostępu hello, który pojawia się zostanie wyświetlony klucz dostępu hello 1 i klucz dostępu 2.</span><span class="sxs-lookup"><span data-stu-id="43ef9-126">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="43ef9-127">Można użyć jednego z tych.</span><span class="sxs-lookup"><span data-stu-id="43ef9-127">You can use either of these.</span></span> 
5. <span data-ttu-id="43ef9-128">Kliknij przycisk hello Kopiuj ikona toocopy hello klucza toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="43ef9-128">Click hello copy icon toocopy hello key toohello clipboard.</span></span> 

<span data-ttu-id="43ef9-129">tooobtain te wartości z klasycznym magazynu konta w klasycznym portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="43ef9-129">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="43ef9-130">Zaloguj się za toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="43ef9-130">Log in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="43ef9-131">Przejdź toohello konta magazynu, które chcesz toouse.</span><span class="sxs-lookup"><span data-stu-id="43ef9-131">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="43ef9-132">Kliknij przycisk **ZARZĄDZAJ KLUCZAMI dostępu** u dołu okienka nawigacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="43ef9-132">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="43ef9-133">W hello wyskakujące okno dialogowe zostanie wyświetlona nazwa konta magazynu hello, podstawowy klucz dostępu i pomocniczy klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="43ef9-133">In hello pop up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="43ef9-134">Klucz dostępu można użyć hello główną lub hello jednej dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="43ef9-134">For access key, you can use either hello primary one or hello secondary one.</span></span> 
5. <span data-ttu-id="43ef9-135">Kliknij przycisk hello Kopiuj ikona toocopy hello klucza toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="43ef9-135">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="43ef9-136">Porady: Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="43ef9-136">How To: Create a Queue</span></span>
<span data-ttu-id="43ef9-137">Witaj poniższy kod tworzy **Azure::QueueService** obiektu, który pozwala toowork z kolejki.</span><span class="sxs-lookup"><span data-stu-id="43ef9-137">hello following code creates a **Azure::QueueService** object, which enables you toowork with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="43ef9-138">Użyj hello **create_queue()** toocreate metody kolejki z hello określona nazwa.</span><span class="sxs-lookup"><span data-stu-id="43ef9-138">Use hello **create_queue()** method toocreate a queue with hello specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="43ef9-139">Porady: Wstawianie komunikatu do kolejki</span><span class="sxs-lookup"><span data-stu-id="43ef9-139">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="43ef9-140">tooinsert wiadomości do kolejki, użyj hello **create_message()** toocreate metody nową wiadomość i dodaj go toohello kolejki.</span><span class="sxs-lookup"><span data-stu-id="43ef9-140">tooinsert a message into a queue, use hello **create_message()** method toocreate a new message and add it toohello queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="43ef9-141">Porady: Podgląd hello następny komunikat</span><span class="sxs-lookup"><span data-stu-id="43ef9-141">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="43ef9-142">Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **peek\_messages()** metody.</span><span class="sxs-lookup"><span data-stu-id="43ef9-142">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages()** method.</span></span> <span data-ttu-id="43ef9-143">Domyślnie **peek\_messages()** wglądu w pojedynczym komunikacie.</span><span class="sxs-lookup"><span data-stu-id="43ef9-143">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="43ef9-144">Można również określić, ile komunikatów ma toopeek.</span><span class="sxs-lookup"><span data-stu-id="43ef9-144">You can also specify how many messages you want toopeek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="43ef9-145">Porady: Hello następny komunikat usuwania z kolejki</span><span class="sxs-lookup"><span data-stu-id="43ef9-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="43ef9-146">Można usunąć wiadomości z kolejki w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="43ef9-146">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="43ef9-147">Podczas wywoływania **listy\_messages()**, Pobierz hello następnej wiadomości w kolejce domyślnie.</span><span class="sxs-lookup"><span data-stu-id="43ef9-147">When you call **list\_messages()**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="43ef9-148">Można również określić, ile komunikatów ma tooget.</span><span class="sxs-lookup"><span data-stu-id="43ef9-148">You can also specify how many messages you want tooget.</span></span> <span data-ttu-id="43ef9-149">Witaj komunikaty zwracane z **listy\_messages()** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="43ef9-149">hello messages returned from **list\_messages()** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="43ef9-150">Przekaż limitu czasu widoczności hello w sekundach jako parametr.</span><span class="sxs-lookup"><span data-stu-id="43ef9-150">You pass in hello visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="43ef9-151">toofinish usuwania wiadomość hello z kolejki hello, musisz również wywołać **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="43ef9-151">toofinish removing hello message from hello queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="43ef9-152">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że gdy tooprocess kończy się niepowodzeniem z kodu, przypisywany komunikat powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu hello sam komunikat i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="43ef9-152">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="43ef9-153">Twój kod wywołuje **usunąć\_message()** natychmiast po przetworzeniu wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="43ef9-153">Your code calls **delete\_message()** right after hello message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="43ef9-154">Porady: Zmiana zawartości hello wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="43ef9-154">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="43ef9-155">Można zmienić zawartość komunikatu w miejscu w kolejce hello hello.</span><span class="sxs-lookup"><span data-stu-id="43ef9-155">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="43ef9-156">Poniższy kod Hello używa hello **update_message()** tooupdate metody wiadomość.</span><span class="sxs-lookup"><span data-stu-id="43ef9-156">hello code below uses hello **update_message()** method tooupdate a message.</span></span> <span data-ttu-id="43ef9-157">Metoda Hello zwróci spójnych kolekcji zawierający pop odebranie hello kolejki wiadomości powitania i reprezentujące wiadomość hello będą widoczne w kolejce hello wartość czasu daty UTC.</span><span class="sxs-lookup"><span data-stu-id="43ef9-157">hello method will return a tuple which contains hello pop receipt of hello queue message and a UTC date time value that represents when hello message will be visible on hello queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="43ef9-158">Porady: Dodatkowych opcji usuwania komunikatów</span><span class="sxs-lookup"><span data-stu-id="43ef9-158">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="43ef9-159">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="43ef9-159">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="43ef9-160">Możesz uzyskać partii komunikatu.</span><span class="sxs-lookup"><span data-stu-id="43ef9-160">You can get a batch of message.</span></span>
2. <span data-ttu-id="43ef9-161">Można ustawić limitu czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="43ef9-161">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="43ef9-162">Witaj poniższy przykład kodu wykorzystuje hello **listy\_messages()** metody tooget 15 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="43ef9-162">hello following code example uses hello **list\_messages()** method tooget 15 messages in one call.</span></span> <span data-ttu-id="43ef9-163">Następnie wyświetla i usuwa każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="43ef9-163">Then it prints and deletes each message.</span></span> <span data-ttu-id="43ef9-164">Ustawia również minut toofive limitu czasu niewidoczności powitania dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="43ef9-164">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="43ef9-165">Porady: Uzyskiwanie hello długość kolejki</span><span class="sxs-lookup"><span data-stu-id="43ef9-165">How To: Get hello Queue Length</span></span>
<span data-ttu-id="43ef9-166">Możesz uzyskać oszacowanie hello liczbę wiadomości w kolejce hello.</span><span class="sxs-lookup"><span data-stu-id="43ef9-166">You can get an estimation of hello number of messages in hello queue.</span></span> <span data-ttu-id="43ef9-167">Witaj **uzyskać\_kolejki\_metadata()** — metoda zadaje licznika przybliżonej wiadomości powitania tooreturn hello kolejki usługi i metadane dotyczące hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="43ef9-167">hello **get\_queue\_metadata()** method asks hello queue service tooreturn hello approximate message count and metadata about hello queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="43ef9-168">Porady: Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="43ef9-168">How To: Delete a Queue</span></span>
<span data-ttu-id="43ef9-169">toodelete kolejkę i wszystkie wiadomości powitania zawarte w niej hello wywołania **usunąć\_queue()** metody dla obiekt kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="43ef9-169">toodelete a queue and all hello messages contained in it, call hello **delete\_queue()** method on hello queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="43ef9-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43ef9-170">Next Steps</span></span>
<span data-ttu-id="43ef9-171">Teraz, kiedy znasz już podstawy magazynu kolejek hello, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu.</span><span class="sxs-lookup"><span data-stu-id="43ef9-171">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="43ef9-172">Odwiedź hello [Blog zespołu usługi Magazyn Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="43ef9-172">Visit hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="43ef9-173">Odwiedź hello [zestawu Azure SDK dla środowiska Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repozytorium w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="43ef9-173">Visit hello [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="43ef9-174">Porównanie między hello Azure kolejki usługi omówione w tym artykule i Azure kolejek usługi Service Bus omówione w hello [jak toouse kolejek usługi Service Bus](/develop/ruby/how-to-guides/service-bus-queues/) artykułu, zobacz [kolejek Azure i kolejek usługi Service Bus - porównaniu i Odróżniające](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="43ef9-174">For a comparison between hello Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in hello [How toouse Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>
