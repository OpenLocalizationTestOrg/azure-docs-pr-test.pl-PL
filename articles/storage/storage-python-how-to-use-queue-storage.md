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
# <a name="how-toouse-queue-storage-from-python"></a>Jak toouse magazynu kolejek w języku Python
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Omówienie
Ten przewodnik przedstawia, jak tooperform typowych scenariuszy przy użyciu hello usługi magazynu kolejek Azure. Witaj przykłady są napisane w języku Python i używają hello [Microsoft Azure magazynu SDK dla języka Python]. Hello omówione scenariusze obejmują **wstawianie**, **wybierania**, **pobierania**, i **usuwanie** kolejki komunikatów, a także  **Tworzenie i usuwanie kolejek**. Więcej informacji dotyczących kolejek można znaleźć w sekcji toohello [następne kroki].

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a>Porady: Tworzenie kolejki
Witaj **QueueService** obiektu umożliwia pracę z kolejki. Witaj poniższy kod tworzy **QueueService** obiektu. Dodaj następujące hello górze hello dowolny plik Python, w którym chcesz tooprogrammatically dostępu do magazynu Azure:

```python
from azure.storage.queue import QueueService
```

Witaj poniższy kod tworzy **QueueService** obiektu przy użyciu hello magazynu konta nazwy i klucza konta. Zamień "myaccount" i "klucze" Nazwa konta i klucz.

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Porady: Wstawianie komunikatu do kolejki
tooinsert wiadomości do kolejki, użyj hello **put\_komunikat** metodę, aby utworzyć nową wiadomość i dodać go toohello kolejki.

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a>Porady: Podgląd hello następny komunikat
Można wglądu wiadomość hello hello przodu kolejki bez jego usuwania z kolejki hello przez wywołanie hello **peek\_wiadomości** metody. Domyślnie **peek\_wiadomości** wglądu w pojedynczym komunikacie.

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a>Porady: Usuwania z kolejki komunikatów
Twój kod usuwa komunikat z kolejki w dwóch etapach. Podczas wywoływania **uzyskać\_wiadomości**, Pobierz hello następnej wiadomości w kolejce domyślnie. Komunikat zwrócony z **uzyskać\_wiadomości** staje się niewidoczny tooany innego kodu odczytującego komunikaty z tej kolejki. Domyślnie komunikat pozostanie niewidoczny przez 30 sekund. toofinish usuwania wiadomość hello z kolejki hello, musisz również wywołać **usunąć\_komunikat**. Ten dwuetapowy proces usuwania komunikatów gwarantuje, że gdy kodu nie powiedzie się tooprocess komunikatu z powodu awarii sprzętu lub oprogramowania, inne wystąpienie kodu można uzyskać ten sam komunikat i spróbuj ponownie. Twój kod wywołuje **usunąć\_komunikat** natychmiast po przetworzeniu wiadomość hello.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

Istnieją dwa sposoby dostosowania pobierania komunikatów z kolejki.
Po pierwsze można uzyskać partię komunikatów (w górę too32). Po drugie można ustawić limit czasu niewidoczności dłuższy lub krótszy, dzięki czemu kod będzie więcej lub mniej czasu toofully przetworzenie każdego komunikatu. następujące Hello przykład kodu wykorzystuje **uzyskać\_wiadomości** metody tooget 16 komunikatów w jednym wywołaniu. Następnie przetwarza każdy komunikat przy użyciu pętli for. Ustawia również hello limitu czasu niewidoczności na pięć minut dla każdego komunikatu.

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Porady: Zmiana zawartości hello wiadomości w kolejce
Można zmienić zawartość komunikatu w miejscu w kolejce hello hello. Jeśli komunikat reprezentuje zadanie robocze, możesz użyć tej funkcji tooupdate stan hello zadania. Poniższy kod Hello używa hello **aktualizacji\_komunikat** tooupdate metody wiadomość. limit czasu widoczności Hello ustawiono too0, co oznacza komunikat jest wyświetlany natychmiast i aktualizowania zawartości hello.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a>Porady: Uzyskiwanie hello długość kolejki
Możesz uzyskać szacunkową hello liczbę wiadomości w kolejce. **Uzyskać\_kolejki\_metadanych** metody zapyta hello kolejki usługi tooreturn metadane dotyczące hello kolejki i hello **approximate_message_count**. wynik Hello jest tylko przybliżonej, ponieważ komunikaty mogą dodane lub usunięte po usługa kolejki odpowiada tooyour żądania.

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a>Porady: Usuwanie kolejki
toodelete kolejkę i wszystkie wiadomości powitania zawartych w nim, należy wywołać **usunąć\_kolejki** metody.

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy magazynu kolejek hello, wykonaj te więcej toolearn łącza.

* [Centrum deweloperów języka Python](/develop/python/)
* [Interfejs API REST usług Azure Storage](http://msdn.microsoft.com/library/azure/dd179355)
* [Blog zespołu odpowiedzialnego za usługę Azure Storage]
* [Microsoft Azure magazynu SDK dla języka Python]

[Blog zespołu odpowiedzialnego za usługę Azure Storage]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure magazynu SDK dla języka Python]: https://github.com/Azure/azure-storage-python