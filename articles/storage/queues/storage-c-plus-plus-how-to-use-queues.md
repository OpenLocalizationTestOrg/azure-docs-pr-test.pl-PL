---
title: "Jak używać magazynu kolejek (C++) | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie korzystania z usługi magazyn kolejek na platformie Azure. Przykłady są napisane w języku C++."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 05/11/2017
ms.author: cbrooksmsft
ms.openlocfilehash: 5e81d5e0af9871099b7f921f355cf94249e4d30c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-c"></a><span data-ttu-id="8af52-104">Jak używać magazynu kolejek w języku C++</span><span class="sxs-lookup"><span data-stu-id="8af52-104">How to use Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="8af52-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8af52-105">Overview</span></span>
<span data-ttu-id="8af52-106">W tym przewodniku opisano sposób wykonywania typowych scenariuszy przy użyciu usługi magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="8af52-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="8af52-107">Przykłady są napisane w C++ i użyj [biblioteki klienta usługi Azure Storage dla języka C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="8af52-107">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="8af52-108">Omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także **tworzenie i usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="8af52-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="8af52-109">Ten przewodnik jest przeznaczony dla biblioteki klienta magazynu Azure dla języka C++ w wersji 1.0.0 i powyżej.</span><span class="sxs-lookup"><span data-stu-id="8af52-109">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="8af52-110">Zalecana wersja jest biblioteka klienta usługi Storage 2.2.0, który jest dostępny za pośrednictwem [NuGet](http://www.nuget.org/packages/wastorage) lub [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="8af52-110">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="8af52-111">Tworzenie aplikacji C++</span><span class="sxs-lookup"><span data-stu-id="8af52-111">Create a C++ application</span></span>
<span data-ttu-id="8af52-112">W tym przewodniku użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji C++.</span><span class="sxs-lookup"><span data-stu-id="8af52-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="8af52-113">Aby to zrobić, należy zainstalować bibliotekę klienta usługi Azure Storage dla języka C++ i Utwórz konto magazynu Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8af52-113">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="8af52-114">Aby zainstalować bibliotekę klienta usługi Azure Storage dla języka C++, można użyć następujących metod:</span><span class="sxs-lookup"><span data-stu-id="8af52-114">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="8af52-115">**Linux:** postępuj zgodnie z instrukcjami [biblioteki klienta usługi Azure Storage dla języka C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) strony.</span><span class="sxs-lookup"><span data-stu-id="8af52-115">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="8af52-116">**System Windows:** w programie Visual Studio, kliknij przycisk **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="8af52-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="8af52-117">Wpisz następujące polecenie w [Konsola Menedżera pakietów NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) i naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="8af52-117">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="8af52-118">Konfigurowanie aplikacji dostęp do kolejki magazynu</span><span class="sxs-lookup"><span data-stu-id="8af52-118">Configure your application to access Queue Storage</span></span>
<span data-ttu-id="8af52-119">Dodaj następujące instrukcje na początku pliku C++, których chcesz użyć interfejsów API magazynu Azure można uzyskać dostępu do kolejek obejmują:</span><span class="sxs-lookup"><span data-stu-id="8af52-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="8af52-120">Konfigurowanie parametrów połączenia usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="8af52-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="8af52-121">Klienta usługi Azure storage używa parametrów połączenia magazynu do przechowywania punktów końcowych i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="8af52-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="8af52-122">Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu w następującym formacie, przy użyciu nazwy konta magazynu i klucz dostępu do magazynu dla konta magazynu na liście [Azure Portal](https://portal.azure.com) dla *AccountName* i *AccountKey* wartości.</span><span class="sxs-lookup"><span data-stu-id="8af52-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="8af52-123">Aby uzyskać informacje dotyczące kont magazynu i klucze dostępu, zobacz [o kontach magazynu Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8af52-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span></span> <span data-ttu-id="8af52-124">Ten przykład przedstawia, jak można zadeklarować pola statycznego do przechowywania parametrów połączenia:</span><span class="sxs-lookup"><span data-stu-id="8af52-124">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="8af52-125">Aby przetestować aplikację w lokalnym komputerze z systemem Windows, można użyć Microsoft Azure [emulatora magazynu](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) zainstalowane z [zestawu Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8af52-125">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="8af52-126">Emulator magazynu jest narzędziem, która symuluje dostępnej na platformie Azure na komputerze deweloperskim lokalnych usług obiektów Blob, kolejki i tabeli.</span><span class="sxs-lookup"><span data-stu-id="8af52-126">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="8af52-127">W poniższym przykładzie pokazano, jak można zadeklarować pole statyczne, aby mógł pomieścić parametry połączenia z lokalnym emulatorze magazynu:</span><span class="sxs-lookup"><span data-stu-id="8af52-127">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="8af52-128">Aby uruchomić emulatora magazynu Azure, wybierz **Start** przycisk lub naciśnij przycisk **Windows** klucza.</span><span class="sxs-lookup"><span data-stu-id="8af52-128">To start the Azure storage emulator, select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="8af52-129">Rozpocznij wpisywanie **emulatora magazynu Azure**i wybierz **emulatora magazynu Azure Microsoft** z listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8af52-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>

<span data-ttu-id="8af52-130">Poniższe przykłady założono użycie jednej z tych dwóch metod można pobrać parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="8af52-130">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="8af52-131">Pobranie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="8af52-131">Retrieve your connection string</span></span>
<span data-ttu-id="8af52-132">Można użyć **cloud_storage_account** klasy do reprezentowania informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="8af52-132">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="8af52-133">Aby uzyskać informacje o koncie magazynu z parametrów połączenia magazynu, można użyć **przeanalizować** metody.</span><span class="sxs-lookup"><span data-stu-id="8af52-133">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="8af52-134">Porady: Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="8af52-134">How to: Create a queue</span></span>
<span data-ttu-id="8af52-135">A **cloud_queue_client** obiektu pozwala pobierać obiekty odwołań do kolejki.</span><span class="sxs-lookup"><span data-stu-id="8af52-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="8af52-136">Poniższy kod tworzy **cloud_queue_client** obiektu.</span><span class="sxs-lookup"><span data-stu-id="8af52-136">The following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="8af52-137">Użyj **cloud_queue_client** obiekt, aby pobrać odwołanie do kolejki, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="8af52-137">Use the **cloud_queue_client** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="8af52-138">Można utworzyć kolejkę, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="8af52-138">You can create the queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="8af52-139">Porady: wstawianie komunikatu do kolejki</span><span class="sxs-lookup"><span data-stu-id="8af52-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="8af52-140">Aby wstawić komunikat do istniejącej kolejki, najpierw utwórz nową **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="8af52-140">To insert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="8af52-141">Następnie wywołaj **add_message** metody.</span><span class="sxs-lookup"><span data-stu-id="8af52-141">Next, call the **add_message** method.</span></span> <span data-ttu-id="8af52-142">A **cloud_queue_message** można tworzyć przy użyciu dowolnego ciągu lub **bajtów** tablicy.</span><span class="sxs-lookup"><span data-stu-id="8af52-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="8af52-143">Oto kod, który tworzy kolejkę (jeśli kolejka nie istnieje) i wstawia komunikat „Hello, World”:</span><span class="sxs-lookup"><span data-stu-id="8af52-143">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it to the queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="8af52-144">Porady: Podgląd kolejnego komunikatu</span><span class="sxs-lookup"><span data-stu-id="8af52-144">How to: Peek at the next message</span></span>
<span data-ttu-id="8af52-145">Możesz uzyskać wgląd w komunikat z przodu kolejki bez jego usuwania z kolejki, wywołując **peek_message** metody.</span><span class="sxs-lookup"><span data-stu-id="8af52-145">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at the next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output the message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="8af52-146">Porady: zmiana zawartości komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="8af52-146">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="8af52-147">Możesz zmienić zawartość komunikatu w kolejce.</span><span class="sxs-lookup"><span data-stu-id="8af52-147">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="8af52-148">Jeśli komunikat reprezentuje zadanie robocze, możesz użyć tej funkcji, aby zaktualizować stan zadania.</span><span class="sxs-lookup"><span data-stu-id="8af52-148">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="8af52-149">Poniższy kod aktualizuje komunikat kolejki o nową zawartość i ustawia rozszerzenie limitu czasu widoczności o kolejne 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="8af52-149">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="8af52-150">Operacja ta zapisuje stan pracy powiązanej z komunikatem i daje klientowi kolejną minutę na kontynuowanie pracy nad komunikatem.</span><span class="sxs-lookup"><span data-stu-id="8af52-150">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="8af52-151">Możesz użyć tej metody do śledzenia wieloetapowych przepływów pracy związanych z komunikatami kolejek, bez konieczności rozpoczynania od nowa, gdy dany etap nie powiedzie się ze względu na awarię sprzętu lub oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="8af52-151">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="8af52-152">Zazwyczaj zachowa również liczbę ponownych prób, a jeśli komunikat zostanie ponowiony więcej niż n razy, zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="8af52-152">Typically, you would keep a retry count as well, and if the message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="8af52-153">Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="8af52-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the message from the queue and update the message contents.
// The visibility timeout "0" means make it visible immediately.
// The visibility timeout "60" means the client can get another minute to continue
// working on the message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output the message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-the-next-message"></a><span data-ttu-id="8af52-154">Porady: usuwanie następnego komunikatu z kolejki</span><span class="sxs-lookup"><span data-stu-id="8af52-154">How to: De-queue the next message</span></span>
<span data-ttu-id="8af52-155">Twój kod usuwa komunikat z kolejki w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="8af52-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="8af52-156">Podczas wywoływania **get_message**, Pobierz następnej wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="8af52-156">When you call **get_message**, you get the next message in a queue.</span></span> <span data-ttu-id="8af52-157">Komunikat zwrócony z **get_message** staje się niewidoczny dla innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="8af52-157">A message returned from **get_message** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="8af52-158">Aby zakończyć usuwanie komunikatu z kolejki, musisz również wywołać **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="8af52-158">To finish removing the message from the queue, you must also call **delete_message**.</span></span> <span data-ttu-id="8af52-159">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie będzie w stanie przetworzyć komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu będzie w stanie uzyskać ten sam komunikat i ponowić próbę.</span><span class="sxs-lookup"><span data-stu-id="8af52-159">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="8af52-160">Twój kod wywołuje **delete_message** natychmiast po przetworzeniu komunikatu.</span><span class="sxs-lookup"><span data-stu-id="8af52-160">Your code calls **delete_message** right after the message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete the message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="8af52-161">Porady: wykorzystanie dodatkowych opcji do usuwania komunikatów z kolejek</span><span class="sxs-lookup"><span data-stu-id="8af52-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="8af52-162">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="8af52-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="8af52-163">Po pierwsze można uzyskać komunikaty zbiorczo (do 32).</span><span class="sxs-lookup"><span data-stu-id="8af52-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="8af52-164">Po drugie można ustawić dłuższy lub krótszy limit czasu niewidoczności, dzięki czemu kod będzie mieć więcej lub mniej czasu na pełne przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="8af52-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="8af52-165">Poniższy przykład kodu wykorzystuje **get_messages** metodę, aby pobrać 20 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="8af52-165">The following code example uses the **get_messages** method to get 20 messages in one call.</span></span> <span data-ttu-id="8af52-166">Następnie przetwarza każdy komunikat przy użyciu **dla** pętli.</span><span class="sxs-lookup"><span data-stu-id="8af52-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="8af52-167">Ustawia również limitu czasu niewidoczności na pięć minut dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="8af52-167">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="8af52-168">Należy pamiętać, że 5 minut rozpoczyna się dla wszystkich wiadomości w tym samym czasie, więc po 5 minut przekazany od czasu wywołania **get_messages**, wszystkie komunikaty, które nie zostały usunięte, będą widoczne ponownie.</span><span class="sxs-lookup"><span data-stu-id="8af52-168">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display the contents of the message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="8af52-169">Porady: pobieranie długości kolejki</span><span class="sxs-lookup"><span data-stu-id="8af52-169">How to: Get the queue length</span></span>
<span data-ttu-id="8af52-170">Możesz uzyskać szacunkową liczbę komunikatów w kolejce.</span><span class="sxs-lookup"><span data-stu-id="8af52-170">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="8af52-171">**Download_attributes** metody prosi usługę kolejki o pobranie atrybutów kolejki, w tym liczby komunikatów.</span><span class="sxs-lookup"><span data-stu-id="8af52-171">The **download_attributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="8af52-172">**Approximate_message_count** metoda pobiera przybliżoną liczbę wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="8af52-172">The **approximate_message_count** method gets the approximate number of messages in the queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch the queue attributes.
queue.download_attributes();

// Retrieve the cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="8af52-173">Porady: Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="8af52-173">How to: Delete a queue</span></span>
<span data-ttu-id="8af52-174">Aby usunąć kolejkę i wszystkie zawarte w niej komunikaty, wywołaj **delete_queue_if_exists** metody dla obiekt kolejki.</span><span class="sxs-lookup"><span data-stu-id="8af52-174">To delete a queue and all the messages contained in it, call the **delete_queue_if_exists** method on the queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If the queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="8af52-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8af52-175">Next steps</span></span>
<span data-ttu-id="8af52-176">Teraz, kiedy znasz już podstawy magazynu kolejek, skorzystaj z poniższych linków, aby dowiedzieć się więcej na temat usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8af52-176">Now that you've learned the basics of Queue storage, follow these links to learn more about Azure Storage.</span></span>

* [<span data-ttu-id="8af52-177">Jak używać magazynu obiektów Blob w języku C++</span><span class="sxs-lookup"><span data-stu-id="8af52-177">How to use Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="8af52-178">Jak używać magazynu tabel w języku C++</span><span class="sxs-lookup"><span data-stu-id="8af52-178">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="8af52-179">Lista zasobów magazynu Azure w języku C++</span><span class="sxs-lookup"><span data-stu-id="8af52-179">List Azure Storage Resources in C++</span></span>](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="8af52-180">Biblioteka klienta usługi Storage for C++ — dokumentacja</span><span class="sxs-lookup"><span data-stu-id="8af52-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="8af52-181">Dokumentacja usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8af52-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)