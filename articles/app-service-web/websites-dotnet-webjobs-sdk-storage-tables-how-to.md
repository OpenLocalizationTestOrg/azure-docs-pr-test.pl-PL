---
title: "toouse aaaHow magazynu tabel platformy Azure z hello zestaw SDK zadań Webjob"
description: "Dowiedz się, jak toouse Azure tabeli magazynu z hello zestaw SDK zadań Webjob. Tworzenie tabel, Dodaj tootables jednostek, a istniejące tabele do odczytu."
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
ms.openlocfilehash: 8e28c69df4a934646add9e50c6de28e76dca1636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a>Jak toouse Azure tabeli magazynu z hello zestaw SDK zadań Webjob
## <a name="overview"></a>Omówienie
Ten przewodnik zawiera przykłady kodu w języku C# przedstawiające sposób zapisu magazynu Azure i tooread tabel za pomocą [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md) wersja 1.x.

Witaj przewodnika przyjęto założenia, wiadomo, [jak toocreate projektu zadania WebJob w programie Visual Studio z połączeniem ciągi konto magazynu punktu tooyour](websites-dotnet-webjobs-sdk-get-started.md) lub zbyt[wielu kont magazynu](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Niektóre fragmentów kodu hello widoczne hello `Table` atrybutu używanego w funkcje, które są [wywołuje ręcznie](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), oznacza to, nie za pomocą jednego z atrybutów wyzwalacza hello. 

## <a id="ingress"></a>Jak tooadd jednostek tooa tabeli
tooadd jednostek tooa tabeli, użyj hello `Table` atrybutem `ICollector<T>` lub `IAsyncCollector<T>` parametru gdzie `T` Określa schemat hello jednostek hello ma tooadd. Konstruktor atrybutu Hello przyjmuje parametr ciąg określający nazwę hello hello tabeli. 

Witaj Poniższy przykładowy kod dodaje `Person` jednostek tooa tabeli o nazwie *wejściowych*.

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

Zwykle hello typu używających `ICollector` pochodną `TableEntity` lub implementuje `ITableEntity`, ale nie ma. Jedną z następujących hello `Person` klasy Praca z kodem hello pokazano w poprzednim hello `Ingress` metody.

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

Jeśli chcesz toowork bezpośrednio z hello magazynu Azure, interfejsu API, można dodać `CloudStorageAccount` podpis metody toohello parametru.

## <a id="monitor"></a>Monitorowanie w czasie rzeczywistym
Ponieważ danych wejściowych funkcji często przetwarzania dużych ilości danych, hello zestaw SDK zadań Webjob pulpitu nawigacyjnego zawiera dane monitorowania w czasie rzeczywistym. Witaj **dziennika wywołania** sekcji informuje, czy funkcja hello nadal działa.

![Transfer danych przychodzących systemem — funkcja](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

Hello **szczegóły wywołania** raporty strony hello funkcji postępu (liczba jednostek zapisywane) jest uruchomiona, i daje możliwość tooabort go. 

![Transfer danych przychodzących systemem — funkcja](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

Gdy funkcja hello zakończeniu hello **szczegóły wywołania** hello liczbę wierszy, zapisany raporty strony.

![Transfer danych przychodzących Zakończono — funkcja](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <a id="multiple"></a>Jak tooread wiele jednostek z tabeli
tooread tabelę, użyj hello `Table` atrybutem `IQueryable<T>` parametru wpisuje `T` pochodną `TableEntity` lub implementuje `ITableEntity`.

Witaj Poniższy przykładowy kod odczytuje i rejestruje wszystkie wiersze z hello `Ingress` tabeli:

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

### <a id="readone"></a>Jak tooread pojedyncza jednostka z tabeli
Brak `Table` konstruktora atrybutu z dwóch dodatkowych parametrów, które umożliwiają określenie hello klucz partycji i klucz wiersza, jeśli chcesz toobind tooa pojedynczej tabeli jednostki.

Witaj Poniższy przykładowy kod odczytuje wiersz tabeli `Person` jednostki na podstawie partycji klucza i wiersz klucza wartości otrzymane w wiadomości w kolejce:  

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


Witaj `Person` klasy w tym przykładzie nie ma tooimplement `ITableEntity`.

## <a id="storageapi"></a>Jak toouse hello interfejsu API magazynu .NET bezpośrednio toowork z tabeli
Można również użyć hello `Table` atrybutem `CloudTable` obiektu dla większą elastyczność podczas pracy z tabelą.

Witaj poniższy kod używa próbki `CloudTable` obiekt tooadd toohello pojedynczej jednostki *wejściowych* tabeli. 

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

Aby uzyskać więcej informacji na temat toouse hello `CloudTable` obiektów, zobacz [jak toouse magazynu tabel w .NET](../cosmos-db/table-storage-how-to-use-dotnet.md). 

## <a id="queues"></a>Tematy pokrewne objętych kolejek hello jak tooarticle
Uzyskać informacji na temat sposobu przetwarzania tabeli toohandle wyzwalane komunikatu w kolejce, lub dla zadań Webjob scenariusze zestawu SDK nie określonych tootable przetwarzania, zobacz [jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Tematy w tym artykule Uwzględnij hello następujące elementy:

* Funkcje asynchroniczne
* Wiele wystąpień
* Łagodne zamykanie
* Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji
* Ustawianie parametrów połączenia SDK hello w kodzie
* Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie
* Wyzwalanie funkcji ręcznie
* Zapisywanie dzienników

## <a id="nextsteps"></a> Następne kroki
W tym przewodniku dostarczył kodu przykłady przedstawiające sposób toohandle typowe scenariusze dotyczące pracy z tabel Azure. Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).

