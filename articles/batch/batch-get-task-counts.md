---
title: "postęp zadania poprzez zliczanie zadań według stanu - partii zadań Azure aaaMonitor | Dokumentacja firmy Microsoft"
description: "Monitorować postęp hello zadania, wywołując operację Get liczby zadań hello toocount zadań dla zadania. Możesz uzyskać liczby aktywnych, uruchomione i zakończonych zadań i zadań, które zakończyło się pomyślnie lub nie powiodło się."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/02/2017
ms.author: tamram
ms.openlocfilehash: 03957d8a3d678bf44587f3bc7f988a76885c2af0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="count-tasks-by-state-toomonitor-a-jobs-progress-preview"></a>Liczba zadań według stanu toomonitor postępu zadania (wersja zapoznawcza)

Partia zadań Azure umożliwia efektywną toomonitor hello postępu zadania podczas jego wykonywania swoich zadań. Możesz wywołać program hello [pobrać liczby zadań] [ rest_get_task_counts] toofind operacji jak wielu zadań, które są w stanie active, uruchomione lub zostało zakończone i ma liczbę powodzeniem lub niepowodzeniem. Poprzez zliczanie hello liczba zadań w każdym stanie, można łatwiej wyświetlanie użytkownika tooa postępu zadania hello lub wykrywania nieoczekiwane opóźnienia lub błędy, które mogą wpłynąć na powitania zadania.

> [!IMPORTANT]
> Hello operacji Get liczby zadań jest obecnie w wersji zapoznawczej i nie jest jeszcze dostępna w Azure dla instytucji rządowych, chińskiej wersji platformy Azure i platformy Azure w Niemczech. 
>
>

## <a name="how-tasks-are-counted"></a>Jak zliczane są zadania

Witaj operacji Get liczby zadań liczby zadań według stanu, w następujący sposób:

- Zadanie jest traktowane jako **active** po jest toorun umieszczonych w kolejce i może, ale nie jest aktualnie przypisany tooa węźle obliczeń. Zadanie również jest traktowane jako **active** Jeśli jest on zależny od zadaniem nadrzędnym, które nie zostało jeszcze zakończone. Aby uzyskać więcej informacji o zależnościach zadań, zobacz [utworzyć zależności zadań toorun zadania, które są zależne od innych zadań](batch-task-dependencies.md). 
- Zadanie jest traktowane jako **systemem** po jego przypisano tooa węźle obliczeń, ale nie zostało jeszcze zakończone. Zadanie jest traktowane jako **systemem** po jej stan to `preparing` lub `running`, wskazywany przez hello [uzyskać informacje o zadaniu] [ rest_get_task] operacji.
- Zadanie jest traktowane jako **ukończone** gdy nie jest już toorun kwalifikujących się. Zadania są liczone jako **ukończone** ma zazwyczaj albo zakończyło się pomyślnie, lub zakończy się niepowodzeniem i również Przekroczono limit ponownych prób. 

Witaj operacji Get liczby zadań udostępnia również ile zadań ma powodzeniem lub niepowodzeniem. Partii określa, czy zadanie zakończyło się pomyślnie lub nie powiodło się, sprawdzając hello **wynik** właściwości hello [executionInfo] [https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo] Właściwości:

    - Zadanie jest traktowane jako **zakończyło się pomyślnie** Jeśli hello wynikiem wykonania zadania jest `success`.
    - Zadanie jest traktowane jako **nie powiodło się** Jeśli hello wynikiem wykonania zadania jest `failure`.

Aby uzyskać więcej informacji na temat stanów zadań, zobacz [uzyskać informacje o zadaniu][rest_get_task].

Hello poniższy przykład kodu .NET przedstawia sposób liczby tooretrieve zadań według stanu: 

```csharp
var taskCounts = await batchClient.JobOperations.GetTaskCountsAsync("job-1");

Console.WriteLine("Task count in active state: {0}", taskCounts.Active);
Console.WriteLine("Task count in preparing or running state: {0}", taskCounts.Running);
Console.WriteLine("Task count in completed state: {0}", taskCounts.Completed);
Console.WriteLine("Succeeded task count: {0}", taskCounts.Succeeded);
Console.WriteLine("Failed task count: {0}", taskCounts.Failed);
Console.WriteLine("ValidationStatus: {0}", taskCounts.ValidationStatus);
```

> [!NOTE]
> Można użyć tego samego typu dla REST i innych obsługiwanych języków, które zlicza tooget zadań dla zadania. 
> 
> 

## <a name="consistency-checking-for-task-counts"></a>Sprawdzanie liczby zadań spójności

Usługa partia zadań Hello agreguje liczby zadań przez zbieranie danych z wielu części asynchroniczne Rozproszony system. tooensure, który liczby zadań są poprawne, partii zapewnia dodatkowe sprawdzenie poprawności stanu liczby, wykonując sprawdzenie spójności względem systemu hello przez kilka składników. Partii wykonuje te sprawdzenia spójności tak długo, jak w zadaniu hello jest krótsza niż 200 000 zadań. W przypadku mało prawdopodobnego hello czy sprawdzanie spójności hello znajdzie błędy partii poprawia hello wynik operacji Get liczby zadań hello oparte na wynikach hello hello Sprawdzanie spójności. Witaj Kontrola spójności jest tooensure dodatkowe miary, która klientów, którzy korzystają na powitania pobrać liczby zadań operacji get hello właściwe informacje, które są im niezbędne do ich rozwiązania.

Witaj **stan** właściwość w odpowiedzi hello wskazuje, czy partii ma przeprowadzić sprawdzanie spójności hello. Jeśli nie zostanie toocheck stanie stanu liczby przed hello stanów rzeczywiste przechowywanych w systemie hello partii, następnie hello **stan** właściwość jest ustawiona zbyt`unvalidated`. Ze względu na wydajność wsadu nie będzie wykonywać sprawdzanie spójności hello, jeśli zadanie hello zawiera więcej niż 200 000 zadań, tak hello **stan** właściwości można ustawić zbyt`unvalidated` w takim przypadku. Jednak liczba zadań hello nie jest zawsze niewłaściwy w takim przypadku nawet utraty bardzo ograniczoną ilość danych jest wysoce nieprawdopodobne. 

Po zmianie stanu zadania potoku agregacji hello przetwarza hello zmiany w ciągu kilku sekund. Witaj operacji Get liczby zadań odzwierciedla hello zaktualizować liczby zadań w tym okresie. Jednak jeśli potoku agregacji hello chybień zmianę stanu zadań, następnie zmiany nie jest zarejestrowany do hello następny przebieg sprawdzania poprawności. W tym czasie liczby zadań mogą być nieco niedokładne powodu toohello brakujących zdarzeń, ale są one usunąć na powitania następny przebieg sprawdzania poprawności.

## <a name="best-practices-for-counting-a-jobs-tasks"></a>Najlepsze rozwiązania dotyczące inwentaryzacji zadania podrzędne zadania

Podczas wywoływania operacji Get liczby zadań hello jest hello najbardziej efektywny sposób tooreturn podstawowe liczba zadania według stanu. Jeśli używasz wersji usługi partii 2017-06-01.5.1, zaleca się zapisywania lub aktualizowanie Twojej toouse kodu pobrać liczby zadań.

Hello operacji Get liczby zadań nie jest starszy niż 2017-06-01.5.1 dostępne w wersjach usługi partii. Jeśli używasz starszej wersji usługi hello, następnie użyć listy zadań toocount zapytania w ramach zadania. Aby uzyskać więcej informacji, zobacz [tworzenie zapytań wydajnie zasobów partii toolist](batch-efficient-list-queries.md).

## <a name="next-steps"></a>Następne kroki

* Zobacz hello [Przegląd funkcji partii](batch-api-basics.md) toolearn więcej informacji na temat partii pojęcia dotyczące usługi i funkcje. Witaj artykule omówiono hello głównej partii zasobów takich jak pule, węzły obliczeniowe, zadań i zadań i zawiera omówienie funkcji hello usługi.
* Dowiedz się podstawy hello opracowanie aplikacji z obsługą usługi partia zadań przy użyciu hello [biblioteki klienta .NET partii](batch-dotnet-get-started.md) lub [Python](batch-python-tutorial.md). Te artykuły wprowadzające informacje pomocne przy działającą aplikację, która używa hello partii usługi tooexecute obciążenia na wielu węzłach obliczeniowych.


[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job
[rest_get_task]: https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task
[rest_list_tasks]: https://docs.microsoft.com/rest/api/batchservice/list-the-tasks-associated-with-a-job
