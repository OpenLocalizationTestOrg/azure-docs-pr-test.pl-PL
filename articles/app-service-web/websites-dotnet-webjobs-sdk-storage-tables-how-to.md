---
title: "Jak używać usługi Azure Table Storage z zestawem SDK usługi WebJobs"
description: "Dowiedz się, jak używać magazynu tabel Azure przy użyciu zestawu SDK zadań Webjob. Tworzenie tabel, Dodaj jednostki do tabel i istniejące tabele do odczytu."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 13cfc788c14d714df7022ce003d34691cf73d121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a>Jak używać usługi Azure Table Storage z zestawem SDK usługi WebJobs
## <a name="overview"></a>Omówienie
Ten przewodnik zawiera C# przykładów kodu przedstawiają sposób odczytu i zapisu przy użyciu tabel magazynu Azure [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md) wersja 1.x.

Przewodnik zakłada wiesz, [Tworzenie projektu zadania WebJob w programie Visual Studio z połączeniem ciągi prowadzące do konta magazynu](websites-dotnet-webjobs-sdk-get-started.md) lub [wielu kont magazynu](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Niektóre Pokaż wstawki kodu `Table` atrybutu używanego w funkcje, które są [wywołuje ręcznie](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), oznacza to, nie za pomocą jednego z atrybutów wyzwalacza. 

## <a id="ingress"></a>Jak dodać jednostek do tabeli
Aby dodać jednostek do tabeli, należy użyć `Table` atrybutem `ICollector<T>` lub `IAsyncCollector<T>` parametru gdzie `T` Określa schemat jednostek, które chcesz dodać. Konstruktor atrybutu ma parametr typu string, który określa nazwę tabeli. 

Poniższy przykładowy kod dodaje `Person` jednostek do tabeli o nazwie *wejściowych*.

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() { 
                        PartitionKey = "Test", 
                        RowKey = i.ToString(), 
                        Name = "Name" }
                    );
            }
        }

Zwykle typ używających `ICollector` pochodną `TableEntity` lub implementuje `ITableEntity`, ale nie ma. Jedną z następujących `Person` klasy pracy kodem przedstawionym w poprzednim `Ingress` metody.

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

Jeśli chcesz pracować bezpośrednio za pomocą interfejsu API magazynu Azure, można dodać `CloudStorageAccount` parametru w podpisie metody.

## <a id="monitor"></a>Monitorowanie w czasie rzeczywistym
Ponieważ danych wejściowych funkcji często przetwarzania dużych ilości danych, zestaw SDK zadań Webjob pulpitu nawigacyjnego zawiera dane monitorowania w czasie rzeczywistym. **Dziennika wywołania** sekcji informuje, czy funkcja jest nadal uruchomiony.

![Transfer danych przychodzących systemem — funkcja](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

**Szczegóły wywołania** raporty strony postępu funkcji (liczba jednostek zapisywane) jest uruchomiona, i daje możliwość jego przerwanie. 

![Transfer danych przychodzących systemem — funkcja](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

Po zakończeniu działania funkcji **szczegóły wywołania** liczbę wierszy, zapisany raporty strony.

![Transfer danych przychodzących Zakończono — funkcja](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <a id="multiple"></a>Jak można odczytać wiele jednostek z tabeli
Aby odczytać tabeli, należy użyć `Table` atrybutem `IQueryable<T>` parametru wpisuje `T` pochodną `TableEntity` lub implementuje `ITableEntity`.

Poniższy przykładowy kod odczytuje i rejestruje wszystkie wiersze z `Ingress` tabeli:

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}", 
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <a id="readone"></a>Jak można odczytać pojedyncza jednostka z tabeli
Brak `Table` konstruktora atrybutu z dwóch dodatkowych parametrów, które pozwalają określić klucz partycji i klucz wiersza, jeśli chcesz powiązać jednostki pojedynczej tabeli.

Poniższy przykładowy kod odczytuje wiersz tabeli `Person` jednostki na podstawie partycji klucza i wiersz klucza wartości otrzymane w wiadomości w kolejce:  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


`Person` Klasy w tym przykładzie nie musi implementować `ITableEntity`.

## <a id="storageapi"></a>Sposób użycia interfejsu API programu .NET magazynu bezpośrednio do pracy z tabeli
Można również użyć `Table` atrybutem `CloudTable` obiektu dla większą elastyczność podczas pracy z tabelą.

Poniższy kod przykładowy używa `CloudTable` obiekt do dodania do pojedynczej jednostki *wejściowych* tabeli. 

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

Aby uzyskać więcej informacji o sposobie używania `CloudTable` obiektów, zobacz [jak używać magazynu tabel w .NET](../cosmos-db/table-storage-how-to-use-dotnet.md). 

## <a id="queues"></a>Tematy pokrewne objętych artykule kolejek
Informacje o sposobie obsługi przetwarzania tabeli wyzwalane przez komunikatu w kolejce, lub zestaw SDK zadań Webjob scenariusze nie są typowe dla przetwarzania tabeli, zobacz [jak używać magazynu kolejek Azure przy użyciu zestawu SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Tematy w tym artykule są następujące:

* Funkcje asynchroniczne
* Wiele wystąpień
* Łagodne zamykanie
* Użyj zestawu SDK zadań Webjob atrybutów w treści funkcji
* Ustaw parametry połączenia SDK w kodzie
* Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie
* Wyzwalanie funkcji ręcznie
* Zapisywanie dzienników

## <a id="nextsteps"></a> Następne kroki
W tym przewodniku udostępnił przykłady kodu, które przedstawiają sposób obsługi typowe scenariusze dotyczące pracy z tabel Azure. Aby uzyskać więcej informacji o sposobie używania zadań Webjob Azure i zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).

