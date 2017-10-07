---
title: "zasoby usługi Azure Storage aaaList z hello biblioteki klienta usługi Storage dla języka C++ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello toouse listę interfejsów API w biblioteki klienta usługi Microsoft Azure Storage dla języka C++ tooenumerate kontenerów, obiektów blob, kolejek, tabel i jednostek."
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: d20a86688938704c24339aa9a1145786783fea5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a>Lista zasobów magazynu Azure w języku C++
Operacje listy są scenariusze programowania toomany klucza z usługą Azure Storage. W tym artykule opisano, jak toomost wydajnie wyliczanie obiektów w usłudze Azure Storage za pomocą hello listę interfejsów API dostarczonych w hello biblioteki klienta usługi Microsoft Azure Storage dla języka C++.

> [!NOTE]
> Ten przewodnik jest przeznaczony dla hello biblioteki klienta magazynu Azure dla języka C++ w wersji 2.x, który jest dostępny za pośrednictwem [NuGet](http://www.nuget.org/packages/wastorage) lub [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

Hello biblioteki klienta magazynu zapewnia różne metody toolist lub obiekty zapytania w usłudze Azure Storage. W tym artykule opisano hello następujące scenariusze:

* Kontenery listy konta
* Listy BLOB w kontenerze lub katalogu wirtualnego obiektów blob
* Lista kolejek w ramach konta
* Listy tabel na koncie
* Jednostki zapytania w tabeli

Każda z tych metod jest wyświetlany za pomocą innego przeciążenia dla różnych scenariuszy.

## <a name="asynchronous-versus-synchronous"></a>Asynchroniczne i synchroniczne
Ponieważ hello biblioteki klienta usługi Storage dla języka C++ jest oparty na powitania [biblioteki C++ REST](https://github.com/Microsoft/cpprestsdk), obsługujemy z założenia operacji asynchronicznych za pomocą [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html). Na przykład:

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

Operacje synchroniczne zawijać hello odpowiednich operacji asynchronicznych:

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

Jeśli pracujesz z wielu wątków aplikacji lub usługi, zalecane jest użycie asynchronicznego hello interfejsów API bezpośrednio, zamiast tworzyć wątku synchronizacji hello toocall interfejsów API, które znacząco wpływa na wydajność.

## <a name="segmented-listing"></a>Lista wybranych
skalę Hello magazynu w chmurze wymaga listy segmentu. Na przykład można mieć w milion BLOB w kontenerze obiektów blob platformy Azure lub za pośrednictwem miliarda podmiotów w tabeli platformy Azure. Nie są teoretycznego cyfr, ale odbiorcy rzeczywistych przypadków użycia.

Dlatego jest niepraktyczne toolist wszystkie obiekty w pojedynczą odpowiedź. Zamiast tego można wyświetlić listę obiektów za pomocą stronicowania. Każdy hello listę interfejsów API ma *segmentowanych* przeciążenia.

Witaj odpowiedzi dla operacji segmentowanych listę obejmuje:

* <i>_segment</i>, zawierającą hello zestaw wyników zwrócony dla toohello jednego wywołania interfejsu API wyświetlania.
* *continuation_token*, który jest przekazywany toohello następne wywołanie w kolejności tooget hello następnej strony wyników. Jeśli nie ma żadnych więcej tooreturn wyników, token kontynuacji hello ma wartość null.

Na przykład toolist Typowe wywołania wszystkie obiekty BLOB w kontenerze może wyglądać jak hello następującego fragmentu kodu. Kod Hello jest dostępny w naszym [przykłady](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):

```cpp
// List blobs in hello blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

Należy pamiętać, że hello liczbę wyników zwracanych na stronie można kontrolować przez parametr hello *max_results* w hello przeciążenia każdego interfejsu API, na przykład:

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

Jeśli nie określisz hello *max_results* parametru, domyślne hello maksymalną wartość zapasową too5000 wyników jest zwracany w jednej strony.

Należy również zauważyć, że zapytanie magazynu tabel Azure może zwracać żadnych rekordów lub mniej rekordów niż wartość hello hello *max_results* parametr, który jest określony, nawet jeśli token kontynuacji hello nie jest pusty. Powodem może być się, że nie można ukończyć tej kwerendy hello w ciągu pięciu sekund. Tak długo, jak token kontynuacji hello nie jest pusta, powinno być kontynuowane hello zapytania i kodu nie należy zakładać hello rozmiar segmentu wyników.

Witaj zalecane kodowania wzorca dla większości scenariuszy składa się z wyświetlania, zapewniające jawne postęp wyświetlania lub zapytań i jak usługa hello odpowiada tooeach żądania. Szczególnie w przypadku aplikacji C++ lub usług niższego poziomu kontroli hello Wyświetlanie postępu mogą pomóc sterowania pamięcią i wydajnością.

## <a name="greedy-listing"></a>Zachłanne listy
Wcześniejszych wersji hello biblioteki klienta usługi Storage dla języka C++ (Preview wersji 0.5.0 i starszych) uwzględnione niepodzielony listę interfejsów API dla tabel i kolejek, tak jak hello poniższy przykład:

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

Te metody zostały zaimplementowane jako otoki segmentowanych interfejsów API. Dla każdej odpowiedzi listę segmentu kod hello dołączany hello wyniki tooa wektora i zwrócone wszystkie wyniki Po przeskanowaniu były pełne kontenery hello.

Takie podejście może działać hello konta magazynu lub tabela zawiera niewielką liczbę obiektów. Jednak wraz ze wzrostem hello liczba obiektów hello pamięci wymaganej można zwiększyć bez ograniczeń, ponieważ wszystkie wyniki pozostaje w pamięci. Jedną operację wyświetlania listy może zająć bardzo dużo czasu, podczas których hello obiekt wywołujący nie zawierała informacji dotyczących o postępie.

Te intensywnie listę interfejsów API w hello zestawu SDK nie istnieje w języku C#, Java, lub hello środowiska JavaScript Node.js. tooavoid hello potencjalne problemy związane z używaniem tych intensywnie interfejsów API, firma Microsoft usunęła je w wersji 0.6.0 podglądu.

Jeśli kod jest wywołanie te intensywnie interfejsów API:

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

Następnie należy zmodyfikować kod toouse hello segmentem listę interfejsów API:

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

Określając hello *max_results* parametru hello segmentu, można równoważyć między hello liczby żądań i zagadnienia dotyczące wydajności toomeet użycia pamięci dla aplikacji.

Ponadto, jeśli jest przy użyciu wybranych listy interfejsów API, ale hello dane przechowywane w kolekcji lokalnej w stylu "zachłannego", również stanowczo zaleca się czy Refaktoryzuj toohandle Twojego kodu, przechowywanie danych w kolekcji lokalnej dokładnie na dużą skalę.

## <a name="lazy-listing"></a>Lista opóźnieniem
Chociaż intensywnie listę wywoływane potencjalne problemy, jest wygodne Jeśli nie ma zbyt wiele obiektów w kontenerze hello.

Jeśli używasz również języka C# lub Oracle Java SDK, należy zapoznać się z hello Wyliczalny model programowania, który oferuje opóźnieniem styl — wyświetlanie, gdzie hello z niektórych przesunięciem jest tylko pobierane dane w razie potrzeby. W języku C++ szablonu na podstawie iteratora hello także podejście podobne.

Typowy interfejsu API, listę opóźnieniem przy użyciu **list_blobs** na przykład wygląda podobnie do następującej:

```cpp
list_blob_item_iterator list_blobs() const;
```

Fragment kodu typowe, który korzysta ze wzorca opóźnieniem listę hello może wyglądać następująco:

```cpp
// List blobs in hello blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

Należy pamiętać, że lista opóźnieniem jest dostępna tylko w trybie synchronicznym.

W porównaniu z listą intensywnie opóźnieniem listę pobiera dane tylko wtedy, gdy jest to konieczne. W obszarze obejmuje hello go pobiera dane z usługi Azure Storage tylko wtedy, gdy iteratora dalej hello przenosi do następnego segmentu. W związku z tym pamięć jest określana za pomocą ograniczonego rozmiar, a operacja hello jest szybkie.

Lista opóźnieniem interfejsy API są objęte hello biblioteki klienta usługi Storage dla języka C++ w wersji 2.2.0.

## <a name="conclusion"></a>Podsumowanie
W tym artykule omówiono różne przeciążenia do wyświetlania listy interfejsów API dla różnych obiektów w hello biblioteki klienta usługi Storage dla języka C++. toosummarize:

* Interfejsy API Async zdecydowanie zalecane jest używanie w wielu scenariuszach wątków.
* Lista segmentu jest zalecane dla większości scenariuszy.
* Opóźnieniem listy znajduje się w bibliotece hello jako otoka wygodny w scenariusze synchroniczne z.
* Zachłanne lista nie jest zalecane i została usunięta z biblioteki hello.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o bibliotece klienta i usługi Azure Storage dla języka C++ zobacz następujące zasoby hello.

* [Jak toouse magazynu obiektów Blob w języku C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Jak toouse magazynu tabel w języku C++](storage-c-plus-plus-how-to-use-tables.md)
* [Jak toouse magazynu kolejek w języku C++](storage-c-plus-plus-how-to-use-queues.md)
* [Biblioteki klienta usługi Azure Storage dokumentacji interfejsu API języka C++.](http://azure.github.io/azure-storage-cpp/)
* [Blog zespołu odpowiedzialnego za usługę Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)
* [Dokumentacja usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/)

