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
# <a name="how-toouse-queue-storage-from-ruby"></a>Jak toouse magazynu kolejek w języku Ruby
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Omówienie
Ten przewodnik przedstawia, jak tooperform typowych scenariuszy przy użyciu hello usługi Microsoft Azure Queue Storage. Hello przykłady są napisane przy użyciu hello Ruby interfejsu API Azure.
Hello omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także  **Tworzenie i usuwanie kolejek**.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Tworzenie aplikacji Ruby
Utwórz aplikację dopisków fonetycznych. Aby uzyskać instrukcje, zobacz [dopisków fonetycznych w aplikacji sieci Web szyny na maszynie Wirtualnej platformy Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Skonfiguruj tooAccess Twoja aplikacja magazynu
toouse magazynu Azure, należy toodownload i użyj hello dopisków fonetycznych azure pakiet, który zawiera zestaw wygody bibliotek, które komunikują się z usługi REST magazynu hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Użyj RubyGems tooobtain hello pakietu
1. Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix).
2. Wpisz "gem zainstalować program azure" hello polecenia okna tooinstall hello gem i zależności.

### <a name="import-hello-package"></a>Importowanie pakietu hello
Użyj edytora tekstu, Dodaj powitania od góry toohello hello dopisków fonetycznych pliku, w którym ma toouse magazynu:

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a>Ustawienia połączenia z magazynem Azure
Moduł Hello azure odczyta zmiennych środowiskowych hello **AZURE\_MAGAZYNU\_konta** i **AZURE\_MAGAZYNU\_ACCESS_KEY** dla Konto magazynu Azure tooyour tooconnect wymaganych informacji. Jeśli te zmienne środowiskowe nie są skonfigurowane, należy określić informacje o koncie hello przed użyciem **Azure::QueueService** z hello następującego kodu:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

tooobtain te wartości z klasyczny lub Menedżera zasobów magazynu konta w portalu Azure hello:

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com).
2. Przejdź toohello konta magazynu, które chcesz toouse.
3. W bloku ustawienia hello na powitania prawo, kliknij przycisk **klucze dostępu**.
4. W bloku klucze dostępu hello, który pojawia się zostanie wyświetlony klucz dostępu hello 1 i klucz dostępu 2. Można użyć jednego z tych. 
5. Kliknij przycisk hello Kopiuj ikona toocopy hello klucza toohello Schowka. 

tooobtain te wartości z klasycznym magazynu konta w klasycznym portalu Azure hello:

1. Zaloguj się za toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Przejdź toohello konta magazynu, które chcesz toouse.
3. Kliknij przycisk **ZARZĄDZAJ KLUCZAMI dostępu** u dołu okienka nawigacji hello hello.
4. W hello wyskakujące okno dialogowe zostanie wyświetlona nazwa konta magazynu hello, podstawowy klucz dostępu i pomocniczy klucz dostępu. Klucz dostępu można użyć hello główną lub hello jednej dodatkowej. 
5. Kliknij przycisk hello Kopiuj ikona toocopy hello klucza toohello Schowka.

## <a name="how-to-create-a-queue"></a>Porady: Tworzenie kolejki
Witaj poniższy kod tworzy **Azure::QueueService** obiektu, który pozwala toowork z kolejki.

```ruby
azure_queue_service = Azure::QueueService.new
```

Użyj hello **create_queue()** toocreate metody kolejki z hello określona nazwa.

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Porady: Wstawianie komunikatu do kolejki
tooinsert wiadomości do kolejki, użyj hello **create_message()** toocreate metody nową wiadomość i dodaj go toohello kolejki.

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a>Porady: Podgląd hello następny komunikat
Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **peek\_messages()** metody. Domyślnie **peek\_messages()** wglądu w pojedynczym komunikacie. Można również określić, ile komunikatów ma toopeek.

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a>Porady: Hello następny komunikat usuwania z kolejki
Można usunąć wiadomości z kolejki w dwóch etapach.

1. Podczas wywoływania **listy\_messages()**, Pobierz hello następnej wiadomości w kolejce domyślnie. Można również określić, ile komunikatów ma tooget. Witaj komunikaty zwracane z **listy\_messages()** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki. Przekaż limitu czasu widoczności hello w sekundach jako parametr.
2. toofinish usuwania wiadomość hello z kolejki hello, musisz również wywołać **delete_message()**.

Ten dwuetapowy proces usuwania komunikatów gwarantuje, że gdy tooprocess kończy się niepowodzeniem z kodu, przypisywany komunikat powodu awarii toohardware lub oprogramowania, inne wystąpienie kodu hello sam komunikat i spróbuj ponownie. Twój kod wywołuje **usunąć\_message()** natychmiast po przetworzeniu wiadomość hello.

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Porady: Zmiana zawartości hello wiadomości w kolejce
Można zmienić zawartość komunikatu w miejscu w kolejce hello hello. Poniższy kod Hello używa hello **update_message()** tooupdate metody wiadomość. Metoda Hello zwróci spójnych kolekcji zawierający pop odebranie hello kolejki wiadomości powitania i reprezentujące wiadomość hello będą widoczne w kolejce hello wartość czasu daty UTC.

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Porady: Dodatkowych opcji usuwania komunikatów
Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.

1. Możesz uzyskać partii komunikatu.
2. Można ustawić limitu czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu.

Witaj poniższy przykład kodu wykorzystuje hello **listy\_messages()** metody tooget 15 komunikatów w jednym wywołaniu. Następnie wyświetla i usuwa każdego komunikatu. Ustawia również minut toofive limitu czasu niewidoczności powitania dla każdego komunikatu.

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a>Porady: Uzyskiwanie hello długość kolejki
Możesz uzyskać oszacowanie hello liczbę wiadomości w kolejce hello. Witaj **uzyskać\_kolejki\_metadata()** — metoda zadaje licznika przybliżonej wiadomości powitania tooreturn hello kolejki usługi i metadane dotyczące hello kolejki.

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a>Porady: Usuwanie kolejki
toodelete kolejkę i wszystkie wiadomości powitania zawarte w niej hello wywołania **usunąć\_queue()** metody dla obiekt kolejki hello.

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy magazynu kolejek hello, wykonaj te toolearn łącza o bardziej skomplikowanych zadaniach magazynu.

* Odwiedź hello [Blog zespołu usługi Magazyn Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* Odwiedź hello [zestawu Azure SDK dla środowiska Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repozytorium w witrynie GitHub

Porównanie między hello Azure kolejki usługi omówione w tym artykule i Azure kolejek usługi Service Bus omówione w hello [jak toouse kolejek usługi Service Bus](/develop/ruby/how-to-guides/service-bus-queues/) artykułu, zobacz [kolejek Azure i kolejek usługi Service Bus - porównaniu i Odróżniające](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)
