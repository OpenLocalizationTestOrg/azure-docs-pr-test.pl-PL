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
# <a name="how-toouse-queue-storage-from-c"></a>Jak toouse magazynu kolejek w języku C++
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Omówienie
W tym przewodniku opisano sposób tooperform typowych scenariuszy przy użyciu hello usługi magazynu kolejek Azure. Hello przykłady są napisane w języku C++ i używają hello [biblioteki klienta usługi Azure Storage dla języka C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hello omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także  **Tworzenie i usuwanie kolejek**.

> [!NOTE]
> Cele tego przewodnika hello biblioteki klienta magazynu Azure dla języka C++ w wersji 1.0.0 i powyżej. Hello zalecana jest wersja biblioteki klienta usługi Storage 2.2.0, który jest dostępny za pośrednictwem [NuGet](http://www.nuget.org/packages/wastorage) lub [GitHub](http://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Tworzenie aplikacji C++
W tym przewodniku użyje funkcji magazynu, które mogą być uruchamiane w ramach aplikacji C++.

toodo tak, konieczne będzie tooinstall hello biblioteki klienta magazynu Azure dla języka C++ i Utwórz konto magazynu Azure w ramach subskrypcji platformy Azure.

Witaj tooinstall biblioteki klienta magazynu Azure dla języka C++, można użyć hello następujące metody:

* **Linux:** postępuj zgodnie z instrukcjami hello w hello [biblioteki klienta usługi Azure Storage dla języka C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) strony.
* **System Windows:** w programie Visual Studio, kliknij przycisk **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów**. Typ hello następujące polecenie na powitania [Konsola Menedżera pakietów NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) i naciśnij klawisz **ENTER**.

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a>Konfigurowanie sieci tooaccess aplikacji magazynu kolejek
Dodaj następujące hello wlicza się instrukcje toohello górnej części pliku C++ hello miejscu toouse hello magazynu Azure API tooaccess kolejki:  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Konfigurowanie parametrów połączenia usługi Azure storage
Klienta usługi Azure storage używa punkty końcowe magazynu połączenia ciąg toostore i poświadczeń do uzyskiwania dostępu do danych usługi zarządzania. Podczas uruchamiania w aplikacji klienckiej, należy podać parametry połączenia magazynu hello w hello zgodny z formatem, używając hello nazwę konta i hello magazynu klucz dostępu do magazynu dla konta magazynu hello na liście hello [Azure Portal](https://portal.azure.com)dla hello *AccountName* i *AccountKey* wartości. Aby uzyskać informacje dotyczące kont magazynu i klucze dostępu, zobacz [o kontach magazynu Azure](storage-create-storage-account.md). Ten przykład przedstawia, jak można zadeklarować ciąg połączenia pola statycznego toohold hello:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest aplikacji w lokalnym komputerze z systemem Windows, można użyć hello Microsoft Azure [emulatora magazynu](storage-use-emulator.md) zainstalowane z hello [zestawu Azure SDK](https://azure.microsoft.com/downloads/). emulator magazynu Hello jest narzędziem, która symuluje hello dostępnej na platformie Azure na komputerze deweloperskim lokalnych usług obiektów Blob, kolejki i tabeli. Witaj poniższym przykładzie pokazano, jak można zadeklarować pola statycznego toohold hello połączenia ciąg tooyour lokalnym emulatorze magazynu:  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

emulatora magazynu Azure hello toostart, wybierz opcję hello **Start** hello przycisk lub naciśnij przycisk **Windows** klucza. Rozpocznij wpisywanie **emulatora magazynu Azure**i wybierz **emulatora magazynu Azure Microsoft** z hello listy aplikacji.

Hello następujące przykłady założono, że użyto jednego z tych parametrów połączenia magazynu Witaj dwie metody tooget.

## <a name="retrieve-your-connection-string"></a>Pobranie parametrów połączenia
Można użyć hello **cloud_storage_account** klasy toorepresent informacje o koncie magazynu. tooretrieve informacji z parametrów połączenia magazynu hello konta magazynu, możesz użyć hello **przeanalizować** metody.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a>Porady: Tworzenie kolejki
A **cloud_queue_client** obiektu pozwala pobierać obiekty odwołań do kolejki. Witaj poniższy kod tworzy **cloud_queue_client** obiektu.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

Użyj hello **cloud_queue_client** tooget kolejki toohello odwołanie ma toouse obiektu. Można utworzyć kolejki hello, jeśli nie istnieje.

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Porady: wstawianie komunikatu do kolejki
tooinsert komunikat do istniejącej kolejki, najpierw utwórz nową **cloud_queue_message**. Następnie wywołaj hello **add_message** metody. A **cloud_queue_message** można tworzyć przy użyciu dowolnego ciągu lub **bajtów** tablicy. Oto kod, który tworzy kolejkę (Jeśli nie istnieje) i wstawia wiadomości powitania "Hello, World":

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

## <a name="how-to-peek-at-hello-next-message"></a>Porady: Podgląd przy następnej wiadomości powitania
Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **peek_message** metody.

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Porady: Zmienianie hello zawartość komunikatu w kolejce
Można zmienić zawartość komunikatu w miejscu w kolejce hello hello. Jeśli wiadomość hello reprezentuje zadanie robocze, można użyć zadania hello tego stanu hello tooupdate funkcji. powitania po kod aktualizuje komunikat kolejki hello o nową zawartość i zestawy hello tooextend limitu czasu widoczności o kolejne 60 sekund. Zapisuje stan pracy związanej z wiadomość hello hello i zapewnia inny toocontinue minuty pracy na wiadomość powitania powitania klienta. Ta technika tootrack wieloetapowych przepływów pracy można użyć w wiadomości w kolejce, bez konieczności toostart za pośrednictwem od początku hello, jeśli dany etap nie powiedzie się powodu awarii toohardware lub oprogramowania. Zazwyczaj zachowa również liczbę ponownych prób, a jeśli hello komunikat zostanie ponowiony więcej niż n razy, zostanie usunięty. Jest to zabezpieczenie przed komunikatami, które wyzwalają błąd aplikacji zawsze, gdy są przetwarzane.

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

## <a name="how-to-de-queue-hello-next-message"></a>Porady: kolejka do następnej wiadomości powitania
Twój kod usuwa komunikat z kolejki w dwóch etapach. Podczas wywoływania **get_message**, Pobierz hello następnej wiadomości w kolejce. Komunikat zwrócony z **get_message** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki. toofinish usuwania wiadomość hello z kolejki hello, musisz również wywołać **delete_message**. Ten dwuetapowy proces usuwania komunikatów gwarantuje, że jeśli kod nie powiedzie się tooprocess, który można uzyskać komunikatu powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu tę samą wiadomość hello i spróbuj ponownie. Twój kod wywołuje **delete_message** natychmiast po przetworzeniu wiadomość hello.

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

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a>Porady: wykorzystanie dodatkowych opcji do usuwania komunikatów z kolejek
Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki. Po pierwsze można uzyskać partię komunikatów (w górę too32). Po drugie można ustawić limit czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu. Witaj poniższy przykład kodu wykorzystuje hello **get_messages** metody tooget 20 komunikatów w jednym wywołaniu. Następnie przetwarza każdy komunikat przy użyciu **dla** pętli. Ustawia również minut toofive limitu czasu niewidoczności powitania dla każdego komunikatu. Należy pamiętać, że hello 5 minut rozpoczyna się dla wszystkich wiadomości na powitania sam czasu, po 5 minut od wywołania hello zbyt**get_messages**, wszystkie komunikaty, które nie zostały usunięte, będą widoczne ponownie.

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

## <a name="how-to-get-hello-queue-length"></a>Porady: pobieranie długości kolejki hello
Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce. Witaj **download_attributes** metody zapyta hello kolejki usługi tooretrieve hello kolejki atrybutów, w tym liczbę wiadomości powitania. Witaj **approximate_message_count** metoda pobiera hello przybliżoną liczbę wiadomości w kolejce hello.

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

## <a name="how-to-delete-a-queue"></a>Porady: Usuwanie kolejki
toodelete kolejkę i wszystkie wiadomości powitania zawarte w niej, wywołanie hello **delete_queue_if_exists** metody dla obiekt kolejki hello.

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

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy magazynu kolejek hello, wykonaj te toolearn łącza więcej informacji na temat usługi Azure Storage.

* [Jak toouse magazynu obiektów Blob w języku C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Jak toouse magazynu tabel w języku C++](storage-c-plus-plus-how-to-use-tables.md)
* [Lista zasobów magazynu Azure w języku C++](storage-c-plus-plus-enumeration.md)
* [Biblioteka klienta usługi Storage for C++ — dokumentacja](http://azure.github.io/azure-storage-cpp)
* [Dokumentacja usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/)