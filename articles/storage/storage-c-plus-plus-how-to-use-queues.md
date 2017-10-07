---
title: magazyn kolejek toouse aaaHow (C++) | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello kolejki usługi magazynu platformy Azure. Przykłady są napisane w języku C++."
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
ms.openlocfilehash: 755380824890ad83774e14d258975915e10cfede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a><span data-ttu-id="8fbe2-104">Jak toouse magazynu kolejek w języku C++</span><span class="sxs-lookup"><span data-stu-id="8fbe2-104">How toouse Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="8fbe2-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8fbe2-105">Overview</span></span>
<span data-ttu-id="8fbe2-106">W tym przewodniku opisano sposób tooperform typowych scenariuszy przy użyciu hello usługi magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="8fbe2-107">Hello przykłady są napisane w języku C++ i używają hello [biblioteki klienta usługi Azure Storage dla języka C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="8fbe2-107">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="8fbe2-108">Hello omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także  **Tworzenie i usuwanie kolejek**.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="8fbe2-109">Cele tego przewodnika hello biblioteki klienta magazynu Azure dla języka C++ w wersji 1.0.0 i powyżej.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-109">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="8fbe2-110">Hello zalecana jest wersja biblioteki klienta usługi Storage 2.2.0, który jest dostępny za pośrednictwem [NuGet](http://www.nuget.org/packages/wastorage) lub [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="8fbe2-110">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="8fbe2-111">Tworzenie aplikacji C++</span><span class="sxs-lookup"><span data-stu-id="8fbe2-111">Create a C++ application</span></span>
<span data-ttu-id="8fbe2-112">W tym przewodniku użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji C++.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="8fbe2-113">toodo tak, konieczne będzie tooinstall hello biblioteki klienta magazynu Azure dla języka C++ i Utwórz konto magazynu Azure w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-113">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="8fbe2-114">Witaj tooinstall biblioteki klienta magazynu Azure dla języka C++, można użyć hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="8fbe2-114">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="8fbe2-115">**Linux:** postępuj zgodnie z instrukcjami hello w hello [biblioteki klienta usługi Azure Storage dla języka C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) strony.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-115">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="8fbe2-116">**System Windows:** w programie Visual Studio, kliknij przycisk **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="8fbe2-117">Typ hello następujące polecenie na powitania [Konsola Menedżera pakietów NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) i naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-117">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="8fbe2-118">Konfigurowanie sieci tooaccess aplikacji magazynu kolejek</span><span class="sxs-lookup"><span data-stu-id="8fbe2-118">Configure your application tooaccess Queue Storage</span></span>
<span data-ttu-id="8fbe2-119">Dodaj następujące hello wlicza się instrukcje toohello górnej części pliku C++ hello miejscu toouse hello magazynu Azure API tooaccess kolejki:</span><span class="sxs-lookup"><span data-stu-id="8fbe2-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="8fbe2-120">Konfigurowanie parametrów połączenia usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="8fbe2-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="8fbe2-121">Klienta usługi Azure storage używa punkty końcowe magazynu połączenia ciąg toostore i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="8fbe2-122">Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu hello w hello zgodny z formatem, używając hello nazwę konta i hello magazynu klucz dostępu do magazynu dla konta magazynu hello na liście hello [Azure Portal](https://portal.azure.com)dla hello *AccountName* i *AccountKey* wartości.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="8fbe2-123">Aby uzyskać informacje dotyczące kont magazynu i klucze dostępu, zobacz [o kontach magazynu Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8fbe2-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="8fbe2-124">Ten przykład przedstawia, jak można zadeklarować ciąg połączenia pola statycznego toohold hello:</span><span class="sxs-lookup"><span data-stu-id="8fbe2-124">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="8fbe2-125">tootest aplikacji w lokalnym komputerze z systemem Windows, można użyć hello Microsoft Azure [emulatora magazynu](storage-use-emulator.md) zainstalowane z hello [zestawu Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8fbe2-125">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="8fbe2-126">emulator magazynu Hello jest narzędziem, która symuluje hello dostępnej na platformie Azure na komputerze deweloperskim lokalnych usług obiektów Blob, kolejki i tabeli.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-126">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="8fbe2-127">Witaj poniższym przykładzie pokazano, jak można zadeklarować pola statycznego toohold hello połączenia ciąg tooyour lokalnym emulatorze magazynu:</span><span class="sxs-lookup"><span data-stu-id="8fbe2-127">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="8fbe2-128">emulatora magazynu Azure hello toostart, wybierz opcję hello **Start** hello przycisk lub naciśnij przycisk **Windows** klucza.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-128">toostart hello Azure storage emulator, select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="8fbe2-129">Rozpocznij wpisywanie **emulatora magazynu Azure**i wybierz **emulatora magazynu Azure Microsoft** z hello listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>

<span data-ttu-id="8fbe2-130">Hello następujące przykłady założono, że użyto jednego z tych parametrów połączenia magazynu Witaj dwie metody tooget.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-130">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="8fbe2-131">Pobranie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="8fbe2-131">Retrieve your connection string</span></span>
<span data-ttu-id="8fbe2-132">Można użyć hello **cloud_storage_account** klasy toorepresent informacje o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-132">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="8fbe2-133">tooretrieve informacji z parametrów połączenia magazynu hello konta magazynu, możesz użyć hello **przeanalizować** metody.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-133">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="8fbe2-134">Porady: Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="8fbe2-134">How to: Create a queue</span></span>
<span data-ttu-id="8fbe2-135">A **cloud_queue_client** obiektu pozwala pobierać obiekty odwołań do kolejki.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="8fbe2-136">Witaj poniższy kod tworzy **cloud_queue_client** obiektu.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-136">hello following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="8fbe2-137">Użyj hello **cloud_queue_client** tooget kolejki toohello odwołanie ma toouse obiektu.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-137">Use hello **cloud_queue_client** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="8fbe2-138">Można utworzyć kolejki hello, jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-138">You can create hello queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="8fbe2-139">Porady: wstawianie komunikatu do kolejki</span><span class="sxs-lookup"><span data-stu-id="8fbe2-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="8fbe2-140">tooinsert komunikat do istniejącej kolejki, najpierw utwórz nową **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-140">tooinsert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="8fbe2-141">Następnie wywołaj hello **add_message** metody.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-141">Next, call hello **add_message** method.</span></span> <span data-ttu-id="8fbe2-142">A **cloud_queue_message** można tworzyć przy użyciu dowolnego ciągu lub **bajtów** tablicy.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="8fbe2-143">Oto kod, który tworzy kolejkę (Jeśli nie istnieje) i wstawia wiadomości powitania "Hello, World":</span><span class="sxs-lookup"><span data-stu-id="8fbe2-143">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it toohello queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="8fbe2-144">Porady: Podgląd przy następnej wiadomości powitania</span><span class="sxs-lookup"><span data-stu-id="8fbe2-144">How to: Peek at hello next message</span></span>
<span data-ttu-id="8fbe2-145">Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **peek_message** metody.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-145">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at hello next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output hello message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="8fbe2-146">Porady: Zmienianie hello zawartość komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="8fbe2-146">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="8fbe2-147">Można zmienić zawartość komunikatu w miejscu w kolejce hello hello.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-147">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="8fbe2-148">Jeśli wiadomość hello reprezentuje zadanie robocze, można użyć zadania hello tego stanu hello tooupdate funkcji.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-148">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="8fbe2-149">powitania po kod aktualizuje komunikat kolejki hello o nową zawartość i zestawy hello tooextend limitu czasu widoczności o kolejne 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-149">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="8fbe2-150">Zapisuje stan pracy związanej z wiadomość hello hello i zapewnia inny toocontinue minuty pracy na wiadomość powitania powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-150">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="8fbe2-151">Ta technika tootrack wieloetapowych przepływów pracy można użyć w wiadomości w kolejce, bez konieczności toostart za pośrednictwem od początku hello, jeśli dany etap nie powiedzie się powodu awarii toohardware lub oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-151">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="8fbe2-152">Zazwyczaj zachowa również liczbę ponownych prób, a jeśli hello komunikat zostanie ponowiony więcej niż n razy, zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-152">Typically, you would keep a retry count as well, and if hello message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="8fbe2-153">Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello message from hello queue and update hello message contents.
// hello visibility timeout "0" means make it visible immediately.
// hello visibility timeout "60" means hello client can get another minute toocontinue
// working on hello message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output hello message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-hello-next-message"></a><span data-ttu-id="8fbe2-154">Porady: kolejka do następnej wiadomości powitania</span><span class="sxs-lookup"><span data-stu-id="8fbe2-154">How to: De-queue hello next message</span></span>
<span data-ttu-id="8fbe2-155">Twój kod usuwa komunikat z kolejki w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="8fbe2-156">Podczas wywoływania **get_message**, Pobierz hello następnej wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-156">When you call **get_message**, you get hello next message in a queue.</span></span> <span data-ttu-id="8fbe2-157">Komunikat zwrócony z **get_message** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-157">A message returned from **get_message** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="8fbe2-158">toofinish usuwania wiadomość hello z kolejki hello, musisz również wywołać **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-158">toofinish removing hello message from hello queue, you must also call **delete_message**.</span></span> <span data-ttu-id="8fbe2-159">Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie powiedzie się tooprocess, który można uzyskać komunikatu powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu tę samą wiadomość hello i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-159">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="8fbe2-160">Twój kod wywołuje **delete_message** natychmiast po przetworzeniu wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-160">Your code calls **delete_message** right after hello message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete hello message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="8fbe2-161">Porady: wykorzystanie dodatkowych opcji do usuwania komunikatów z kolejek</span><span class="sxs-lookup"><span data-stu-id="8fbe2-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="8fbe2-162">Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="8fbe2-163">Po pierwsze można uzyskać partię komunikatów (w górę too32).</span><span class="sxs-lookup"><span data-stu-id="8fbe2-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="8fbe2-164">Po drugie można ustawić limit czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="8fbe2-165">Witaj poniższy przykład kodu wykorzystuje hello **get_messages** metody tooget 20 komunikatów w jednym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-165">hello following code example uses hello **get_messages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="8fbe2-166">Następnie przetwarza każdy komunikat przy użyciu **dla** pętli.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="8fbe2-167">Ustawia również minut toofive limitu czasu niewidoczności powitania dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="8fbe2-168">Należy pamiętać, że hello 5 minut rozpoczyna się dla wszystkich wiadomości na powitania sam czasu, po 5 minut od wywołania hello zbyt**get_messages**, wszystkie komunikaty, które nie zostały usunięte, będą widoczne ponownie.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-168">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display hello contents of hello message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="8fbe2-169">Porady: pobieranie długości kolejki hello</span><span class="sxs-lookup"><span data-stu-id="8fbe2-169">How to: Get hello queue length</span></span>
<span data-ttu-id="8fbe2-170">Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-170">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="8fbe2-171">Witaj **download_attributes** metody zapyta hello kolejki usługi tooretrieve hello kolejki atrybutów, w tym liczbę wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-171">hello **download_attributes** method asks hello Queue service tooretrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="8fbe2-172">Witaj **approximate_message_count** metoda pobiera hello przybliżoną liczbę wiadomości w kolejce hello.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-172">hello **approximate_message_count** method gets hello approximate number of messages in hello queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch hello queue attributes.
queue.download_attributes();

// Retrieve hello cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="8fbe2-173">Porady: Usuwanie kolejki</span><span class="sxs-lookup"><span data-stu-id="8fbe2-173">How to: Delete a queue</span></span>
<span data-ttu-id="8fbe2-174">toodelete kolejkę i wszystkie wiadomości powitania zawarte w niej, wywołanie hello **delete_queue_if_exists** metody dla obiekt kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-174">toodelete a queue and all hello messages contained in it, call hello **delete_queue_if_exists** method on hello queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If hello queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="8fbe2-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8fbe2-175">Next steps</span></span>
<span data-ttu-id="8fbe2-176">Teraz, kiedy znasz już podstawy magazynu kolejek hello, wykonaj te toolearn łącza więcej informacji na temat usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8fbe2-176">Now that you've learned hello basics of Queue storage, follow these links toolearn more about Azure Storage.</span></span>

* [<span data-ttu-id="8fbe2-177">Jak toouse magazynu obiektów Blob w języku C++</span><span class="sxs-lookup"><span data-stu-id="8fbe2-177">How toouse Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="8fbe2-178">Jak toouse magazynu tabel w języku C++</span><span class="sxs-lookup"><span data-stu-id="8fbe2-178">How toouse Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="8fbe2-179">Lista zasobów magazynu Azure w języku C++</span><span class="sxs-lookup"><span data-stu-id="8fbe2-179">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="8fbe2-180">Biblioteka klienta usługi Storage for C++ — dokumentacja</span><span class="sxs-lookup"><span data-stu-id="8fbe2-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="8fbe2-181">Dokumentacja usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8fbe2-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)