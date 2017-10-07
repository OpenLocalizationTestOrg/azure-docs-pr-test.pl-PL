---
title: "aaaDesign wydajne listy kwerend - partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Zwiększyć wydajność przez filtrowanie zapytania, gdy żąda informacji na temat zasobów usługi partia zadań, takich jak pule, zadań, zadań i węzły obliczeniowe."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7e554119ec9d0e9e8007ccfb1ca80fe142a5e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-queries-toolist-batch-resources-efficiently"></a>Tworzenie zapytań wydajnie toolist partii zasobów

Tutaj dowiesz się, jak tooincrease aplikacji partii zadań Azure wydajność dzięki zmniejszeniu hello ilość danych zwracanych przez usługę hello kwerendy zadania, zadania i węzły obliczeniowe z hello [partiami platformy .NET] [ api_net] biblioteki.

Prawie wszystkie aplikacje partii muszą tooperform pewien typ monitorowania lub innych operacji, który odpytuje hello usługa partia zadań, często w regularnych odstępach czasu. Na przykład toodetermine czy są dostępne w kolejce zadań pozostały w ramach zadania, dla każdego zadania w zadaniu hello musi pobrać dane. Stan hello toodetermine węzłów w puli, w każdym węźle w puli hello musi pobrać danych. W tym artykule opisano, jak tooexecute takie zapytania w programie hello najbardziej wydajny sposób.

> [!NOTE]
> Witaj usługa partia zadań zapewnia obsługę interfejsu API specjalne hello typowy scenariusz inwentaryzacji zadań w ramach zadania. Zamiast korzystać z zapytania listy tych, należy wywołać hello [pobrać liczby zadań] [ rest_get_task_counts] operacji. Liczby zadań Get wskazuje, ile zadań oczekujących, uruchomiona lub Zakończ i ile zadań ma powodzeniem lub niepowodzeniem. Liczba zadań Get jest bardziej efektywne niż zapytanie listy. Aby uzyskać więcej informacji, zobacz [liczba zadań dla zadania według stanu (wersja zapoznawcza)](batch-get-task-counts.md). 
>
> Hello operacji Get liczby zadań nie jest starszy niż 2017-06-01.5.1 dostępne w wersjach usługi partii. Jeśli używasz starszej wersji usługi hello, następnie użyć listy zadań toocount zapytania w ramach zadania.
>
> 

## <a name="meet-hello-detaillevel"></a>Spełnia hello atrybut DetailLevel
W środowisku produkcyjnym aplikacji partii jednostek, takich jak zadania, zadania i węzły obliczeniowe można numerów w hello tysięcy. Gdy użytkownik żąda informacji na temat tych zasobów, potencjalnie dużą ilość danych musi "przechodzą przewodowy hello" z aplikacji tooyour usługi partii hello w każdym zapytaniu. Ograniczając hello liczbę elementów i typ danych zwróconych przez zapytanie wykonywane jest przyspieszenie hello zapytań i w związku z tym hello wydajność aplikacji.

To [partiami platformy .NET] [ api_net] list fragment kodu interfejsu API *co* zadanie, które jest skojarzone z zadaniem, wraz z *wszystkie* hello właściwości każdego z nich zadania:

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

Jednak bardziej efektywnego zapytanie listy, można wykonać przez zastosowanie kwerendy tooyour "poziom szczegółów". Aby to zrobić, podając [ODATADetailLevel] [ odata] obiekt toohello [JobOperations.ListTasks] [ net_list_tasks] metody. Ta Wstawka kodu zwraca identyfikator hello, wiersz polecenia i właściwości informacji węzła obliczeń zakończonych zadań:

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties tooreturn
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply hello ODATADetailLevel toohello ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

W tym przykładowym scenariuszu, jeśli istnieją tysiące zadań w zadaniu hello hello wyniki z drugiego zapytania hello zwykle będą najpierw znacznie szybszy niż hello zwracane. Więcej informacji o używaniu ODATADetailLevel wśród elementów z hello interfejs API .NET partii jest dołączony [poniżej](#efficient-querying-in-batch-net).

> [!IMPORTANT]
> Zdecydowanie zalecamy, aby użytkownik *zawsze* dostawy ODATADetailLevel obiektu tooyour interfejs API .NET listy wywołuje tooensure maksymalnej wydajności i wydajność aplikacji. Umożliwia określenie poziomu szczegółowości, może pomóc toolower partii czasy odpowiedzi usługi, poprawić wykorzystanie sieci i zminimalizować użycie pamięci przez aplikacje klienckie.
> 
> 

## <a name="filter-select-and-expand"></a>Filtruj, wybierz i rozwiń węzeł
Witaj [partiami platformy .NET] [ api_net] i [REST partii] [ api_rest] API stanowią tooreduce możliwości hello zarówno hello liczba elementów, które są zwracane w postaci listy a także hello ilość informacji, która jest zwracana dla każdego. Możesz to zrobić, określając **filtru**, **wybierz**, i **rozwiń ciągów** podczas wykonywania zapytania z listy.

### <a name="filter"></a>Filtr
ciąg filtru Hello jest wyrażenie, które zmniejsza hello liczbę elementów, które są zwracane. Na przykład listy tylko hello uruchomionych zadań dla zadania lub listy tylko węzły obliczeniowe, które są gotowe toorun zadania.

* ciąg filtru Hello składa się z co najmniej jednego wyrażenia z wyrażeniem, które składa się z nazwy właściwości, operator i wartość. Witaj właściwości, które można określić są tooeach określonych typów jednostek, które można zbadać są hello operatory, które są obsługiwane dla każdej właściwości.
* Wiele wyrażeń można łączyć przy użyciu operatorów logicznych hello `and` i `or`.
* W tym przykładzie filtrowanie list ciągów tylko zadania hello uruchomiona "renderowania": `(state eq 'running') and startswith(id, 'renderTask')`.

### <a name="select"></a>Wybierz pozycję
Wybierz ciąg Hello ogranicza hello wartości właściwości, które są zwracane dla każdego elementu. Określ listę nazw właściwości, a dla elementów hello w wynikach zapytania hello są zwracane tylko wartości tych właściwości.

* Wybierz ciąg Hello składa się z listy rozdzielanej przecinkami nazw właściwości. Można określić właściwości powitania dla typu jednostki hello jest kwerenda.
* Ten ciąg wybierz przykład określa, że powinny być zwracane tylko trzy wartości właściwości dla każdego zadania: `id, state, stateTransitionTime`.

### <a name="expand"></a>Rozwiń
Witaj rozwiń ciąg zmniejsza hello liczbę wywołań interfejsu API, które są wymagane tooobtain pewne informacje. Korzystając z ciągu Rozwiń, można uzyskać więcej informacji o każdym elemencie przy użyciu jednego wywołania interfejsu API. Zamiast pierwszego uzyskania hello listę jednostek, a następnie podać informacje dla każdego elementu na liście hello, użyj ciągu rozwiń tooobtain hello tych samych informacji w jednym wywołaniu interfejsu API. Mniej wywołań interfejsu API oznaczają lepszą wydajność.

* Podobne toohello wybierz ciąg hello rozwiń formanty ciąg czy niektórych danych znajduje się w wynikach zapytania listy.
* ciąg rozwiń Hello jest obsługiwana tylko gdy jest używany w listę zadań, harmonogramy zadań, zadań i pul. Obecnie obsługuje on tylko informacje statystyczne.
* Gdy wszystkie właściwości są wymagane, a nie wybierz podano ciągu, hello rozwiń ciąg *musi* tooget używane statystyki informacje. Jeśli wybierz ciąg jest używany tooobtain podzbiór właściwości, następnie `stats` można określić w ciągu wybierz hello i hello rozwiń ciąg nie jest konieczne toobe określony.
* W tym przykładzie rozwiń ciąg Określa, że informacje statystyczne powinny być zwracane dla każdego elementu na liście hello: `stats`.

> [!NOTE]
> Podczas konstruowania żadnego hello trzy typy ciągów zapytań (filtrowanie, wybierz i rozwiń), należy upewnić się, że hello nazwy i właściwości przypadku odpowiadają ich odpowiedniki element interfejsu API REST. Na przykład podczas pracy z hello .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) klasy, należy określić **stanu** zamiast **stanu**, nawet jeśli jest hello właściwości platformy .NET [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state). Zobacz poniższych tabelach hello mapowania właściwości między hello .NET i interfejsów API REST.
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a>Reguły filtra wybierz i rozwiń ciągów
* Nazwy właściwości w filtrze, wybierz i rozwiń ciągi powinny być wyświetlane, tak jak w hello [REST partii] [ api_rest] interfejsu API — nawet wtedy, gdy używasz [partiami platformy .NET] [ api_net] lub jednego z hello innych zestawów SDK usługi partia zadań.
* Wszystkie nazwy właściwości jest rozróżniana wielkość liter, ale wartości właściwości są bez uwzględniania wielkości liter.
* Data i godzina ciągów może być jednym z dwóch formatów i musi być poprzedzony `DateTime`.
  
  * Przykładowy format W3C DTF:`creationTime gt DateTime'2011-05-08T08:49:37Z'`
  * RFC 1123 Przykładowy format:`creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`
* Logiczna ciągi są albo `true` lub `false`.
* Jeśli określono nieprawidłowe właściwości lub operatora `400 (Bad Request)` spowoduje błąd.

## <a name="efficient-querying-in-batch-net"></a>Efektywne wykonywania zapytania w partiami platformy .NET
W ramach hello [partiami platformy .NET] [ api_net] interfejsu API, hello [ODATADetailLevel] [ odata] klasa jest używana do podawania filtru, wybierz i rozwiń ciągów operacje toolist. Witaj ODataDetailLevel klasa ma trzy właściwości publicznych parametrów, które mogą być określony w Konstruktorze hello lub ustawić bezpośrednio dla obiekt hello. Można następnie przekazać hello ODataDetailLevel obiektu jako toohello parametru różne operacje listy takich jak [ListPools][net_list_pools], [ListJobs][net_list_jobs], i [ListTasks][net_list_tasks].

* [ODATADetailLevel][odata].[ FilterClause][odata_filter]: Ogranicz hello liczbę elementów, które są zwracane.
* [ODATADetailLevel][odata].[ SelectClause][odata_select]: Określ wartości właściwości, które są zwracane z każdym elementem.
* [ODATADetailLevel][odata].[ ExpandClause][odata_expand]: pobieranie danych dla wszystkich elementów w jeden interfejs API Wywołaj zamiast wywołań dla każdego elementu.

Witaj poniższy fragment kodu używa hello interfejs API partii .NET tooefficiently zapytania hello partii usługi statystyki hello zestawu pul. W tym scenariuszu użytkownik partii hello ma pule zarówno testowego i produkcyjnego. Hello testu puli identyfikatorów nazwy są poprzedzone ciągiem "test", a nazwy są poprzedzone ciągiem "produkcyjną" hello produkcji puli identyfikatorów. We fragmencie hello *myBatchClient* jest prawidłowo zainicjowany wystąpieniem hello [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) klasy.

```csharp
// First we need an ODATADetailLevel instance on which tooset hello filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want toopull only hello "test" pools, so we limit hello number of items returned
// by using a FilterClause and specifying that hello pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// toofurther limit hello data that crosses hello wire, configure hello SelectClause to
// limit hello properties that are returned on each CloudPool object tooonly
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify hello ExpandClause so that hello .NET API pulls hello statistics for the
// CloudPools in a single underlying REST API call. Note that we use hello pool's
// REST API element name "stats" here as opposed too"Statistics" as it appears in
// hello .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing hello amount of data that is returned
// by specifying hello detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> Wystąpienie [ODATADetailLevel] [ odata] skonfigurowanego wybierz i rozwiń klauzule mogą również zostać przekazana tooappropriate metody Get, takich jak [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx) , toolimit hello ilość danych, która jest zwracana.
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a>Mapowania partii interfejsu API REST too.NET
Nazwy właściwości w filtrze, wybierz i rozwiń ciągów *musi* ich odpowiedniki interfejsu API REST, zarówno w nazwie i w przypadku uwzględnienia. w poniższych tabelach Hello zawierają mapowania między hello .NET i odpowiedników interfejsu API REST.

### <a name="mappings-for-filter-strings"></a>Mapowania dla filtru ciągów
* **Metody listy .NET**: każdej z metod interfejsu API platformy .NET hello w tej kolumnie akceptuje [ODATADetailLevel] [ odata] obiektu jako parametr.
* **Żądania listy REST**: każdy interfejsu API REST strony połączonego tooin ta kolumna zawiera tabelę, która określa właściwości hello i operacji, które są dozwolone w *filtru* ciągów. Użyjesz tych nazw właściwości i operacji utworzenia [ODATADetailLevel.FilterClause] [ odata_filter] ciąg.

| Metody listy .NET | Żądania listy REST |
| --- | --- |
| [CertificateOperations.ListCertificates][net_list_certs] |[Wyświetl certyfikaty hello konta][rest_list_certs] |
| [CloudTask.ListNodeFiles][net_list_task_files] |[Lista hello pliki skojarzone z zadaniem][rest_list_task_files] |
| [JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status] |[Stan listy hello hello zadanie przygotowanie i zadania zlecenia zadań dla zadania][rest_list_jobprep_status] |
| [JobOperations.ListJobs][net_list_jobs] |[Lista hello zadania konta][rest_list_jobs] |
| [JobOperations.ListNodeFiles][net_list_nodefiles] |[Lista plików hello w węźle][rest_list_nodefiles] |
| [JobOperations.ListTasks][net_list_tasks] |[Lista zadań hello skojarzone z zadaniem][rest_list_tasks] |
| [JobScheduleOperations.ListJobSchedules][net_list_job_schedules] |[Harmonogramy zadań hello listy konta][rest_list_job_schedules] |
| [JobScheduleOperations.ListJobs][net_list_schedule_jobs] |[Lista hello zadań skojarzonych z harmonogramu zadań][rest_list_schedule_jobs] |
| [PoolOperations.ListComputeNodes][net_list_compute_nodes] |[Lista hello obliczeniowe węzłów w puli][rest_list_compute_nodes] |
| [PoolOperations.ListPools][net_list_pools] |[Lista pul hello konta][rest_list_pools] |

### <a name="mappings-for-select-strings"></a>Mapowania dla wybierz ciągów
* **Typy .NET partii**: typy interfejsu API partii .NET.
* **Interfejs API REST jednostek**: każdej strony w tej kolumnie zawiera co najmniej jednej tabeli, które listę nazw właściwości interfejsu API REST hello hello typu. Te nazwy właściwości są używane podczas utworzymy *wybierz* ciągów. Utworzenia użyje tych samych nazw właściwości [ODATADetailLevel.SelectClause] [ odata_select] ciąg.

| Typy .NET partii | Jednostki interfejsu API REST |
| --- | --- |
| [Certyfikat][net_cert] |[Uzyskiwanie informacji o certyfikacie][rest_get_cert] |
| [CloudJob][net_job] |[Pobierz informacje o zadaniu][rest_get_job] |
| [CloudJobSchedule][net_schedule] |[Pobierz informacje o harmonogram zadań][rest_get_schedule] |
| [ComputeNode][net_node] |[Pobierz informacje o węźle][rest_get_node] |
| [CloudPool][net_pool] |[Pobierz informacje o puli][rest_get_pool] |
| [CloudTask][net_task] |[Pobierz informacje o zadaniu][rest_get_task] |

## <a name="example-construct-a-filter-string"></a>Przykład: skonstruować ciąg filtru
Podczas konstruowania ciąg filtru dla [ODATADetailLevel.FilterClause][odata_filter], zapoznaj się z powyższej tabeli hello w obszarze "Mapowania dla filtru ciągów" toofind hello interfejsu API REST stronę dokumentacji odpowiadający Operacja listy toohello, że chcesz tooperform. W pierwszej tabeli multirow hello na tej stronie znajdziesz hello filtrowanie właściwości i ich operatory obsługiwane. Jeśli chcesz tooretrieve wszystkie zadania, którego kod zakończenia: różną od zera, na przykład to wiersz na [listy zadań hello skojarzonych z zadaniem] [ rest_list_tasks] Określa ciąg odpowiednie właściwości hello i dozwolone operatory:

| Właściwość | Operacje dozwolone | Typ |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

W związku z tym będzie hello ciąg filtru wyświetlania list wszystkie zadania z kodem zakończenia różną od zera:

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a>Przykład: skonstruować wybierz ciąg
tooconstruct [ODATADetailLevel.SelectClause][odata_select], zapoznaj się z powyższej tabeli hello w obszarze "Mapowania dla ciągów select" i przejdź toohello strony interfejsu API REST, która odpowiada toohello typ jednostki, które Lista. W pierwszej tabeli multirow hello na tej stronie można znaleźć właściwości selectable hello i ich operatory obsługiwane. Jeśli chcesz tylko identyfikator hello tooretrieve i wiersz polecenia dla każdego zadania na liście, na przykład można znaleźć te wiersze w tabeli dotyczy hello w [uzyskać informacje o zadaniu][rest_get_task]:

| Właściwość | Typ | Uwagi |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

następnie będzie wybierz ciąg Hello tylko identyfikator hello i wiersza polecenia do każdego zadania wymienione w tym:

`id, commandLine`

## <a name="code-samples"></a>Przykłady kodu
### <a name="efficient-list-queries-code-sample"></a>Przykładowy kod zapytania wydajne listy
Zapoznaj się z hello [EfficientListQueries] [ efficient_query_sample] przykładowy projekt w sposób wydajny toosee GitHub zapytań listy może wpłynąć na wydajność w aplikacji. Tę aplikację konsolową C#, tworzy i dodaje dużej liczby zadań tooa zadania. Następnie, ułatwia wielu wywołań toohello [JobOperations.ListTasks] [ net_list_tasks] — metoda i przekazuje [ODATADetailLevel] [ odata] obiektów, które są skonfigurowane przy użyciu różnych właściwości wartości toovary hello ilość danych toobe zwrócony. Generuje dane wyjściowe podobne toohello poniżej:

```
Adding 5000 tasks toojob jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER tooquery tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER toocontinue...
```

Jak pokazano na czas hello, można znacznie obniżyć czas odpowiedzi na zapytania, ograniczając hello właściwości i hello liczba elementów, które są zwracane. Możesz znaleźć tego i innych przykładowych projektach w hello [azure partii próbek] [ github_samples] repozytorium w witrynie GitHub.

### <a name="batchmetrics-library-and-code-sample"></a>BatchMetrics biblioteki i kod przykładowy
Ponadto toohello EfficientListQueries przykładowym kodzie powyżej można znaleźć hello [BatchMetrics] [ batch_metrics] projektu w hello [azure partii próbek] [ github_samples] Repozytorium GitHub. Witaj BatchMetrics przykładowy projekt pokazano, jak tooefficiently monitorować postęp zadania partii zadań Azure za pomocą hello interfejsu API partii.

Hello [BatchMetrics] [ batch_metrics] próbki obejmuje projektu biblioteki klas .NET, które można zastosować do własnych projektów i prostą wiersza polecenia programu tooexercise i Wykaż hello stosowania hello Biblioteka.

aplikacja przykładowa Hello w projekcie hello prezentuje hello następujące operacje:

1. Wybranie określonych atrybutów w kolejności toodownload tylko właściwości hello należy
2. Filtrowanie na czas przejścia stanu w kolejności toodownload zmienia tylko od czasu ostatniej kwerendy hello

Na przykład następujące metody hello pojawia się w hello BatchMetrics biblioteki. Zwraca ODATADetailLevel, która określa, że tylko hello `id` i `state` właściwości mają być uzyskiwane dla hello jednostek, które będą pytani. On również określa, że tylko obiektów, których stan zmienił się od hello określony `DateTime` parametr ma zostać zwrócony.

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a>Następne kroki
### <a name="parallel-node-tasks"></a>Zadania równoległych węzła
[Maksymalizowanie użycia zasobów obliczeniowych partii zadań Azure z węzła równoczesnych zadań](batch-parallel-node-tasks.md) jest inny artykuł powiązane tooBatch wydajność aplikacji. Niektóre rodzaje obciążeń mogą korzystać z wykonywanych zadań równoległych na większych — ale mniej — węzły obliczeniowe. Zapoznaj się z hello [przykładowy scenariusz](batch-parallel-node-tasks.md#example-scenario) w artykule hello, aby uzyskać szczegółowe informacje o takiej sytuacji.

### <a name="batch-forum"></a>Forum usługi partia zadań
Witaj [Forum usługi partia zadań Azure] [ forum] w witrynie MSDN jest doskonałym umieścić toodiscuss partii i zadać pytania dotyczące usługi hello. HEAD na za pośrednictwem przydatne Posty "trwałe" i opublikuj swoje pytania powstałych podczas tworzenia własnych rozwiązań partii.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job