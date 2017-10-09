---
title: "aaaGetting uruchomiono z magazynu Azure i programu Visual Studio połączone usługi (zadania WebJob projekty)"
description: "Jak tooget pracy z magazynem tabel Azure w projekcie zadań Webjob Azure w programie Visual Studio, po łączenie tooa konto magazynu przy użyciu programu Visual Studio połączenia usługi"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 448dee3369207062ee85c6636c84bcb4e26a2085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a>Wprowadzenie do korzystania z usługi Azure magazynu (projekty zadanie WebJob platformy Azure)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Omówienie
Ten artykuł zawiera C# przykłady pokazujące Pokaż jak toouse hello zestawu SDK zadań Webjob Azure w wersji 1.x z hello usługi Magazyn tabel Azure. Przykłady kodu Hello Użyj hello [zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk.md) wersja 1.x.

Usługa Azure Table storage Hello umożliwia toostore dużych ilości danych strukturalnych. Usługa Hello jest magazynem danych NoSQL, który przyjmuje uwierzytelnione wywołania z wewnątrz, jak i poza hello chmury Azure. Tabele Azure idealnie nadają się do przechowywania strukturalnych danych nierelacyjnych.  Zobacz [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-tables.md#create-a-table) Aby uzyskać więcej informacji.

Niektóre fragmentów kodu hello widoczne hello **tabeli** atrybutu używanego w funkcje, które są nazywane ręcznie, oznacza to, nie za pomocą jednego z atrybutów wyzwalacza hello.

## <a name="how-tooadd-entities-tooa-table"></a>Jak tooadd jednostek tooa tabeli
tooadd jednostek tooa tabeli, użyj hello **tabeli** atrybutem **ICollector<T>**  lub **IAsyncCollector<T>**  parametru gdzie **T** Określa schemat hello jednostek hello ma tooadd. Konstruktor atrybutu Hello przyjmuje parametr ciąg określający nazwę hello hello tabeli.

Witaj Poniższy przykładowy kod dodaje **osoby** jednostek tooa tabeli o nazwie *wejściowych*.

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

Zwykle hello typu używających **ICollector** pochodną **TableEntity** lub implementuje **ITableEntity**, ale nie ma. Jedną z następujących hello **osoby** klasy Praca z kodem hello pokazano w poprzednim hello **transfer danych przychodzących** metody.

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

Jeśli chcesz toowork bezpośrednio z hello magazynu Azure, interfejsu API, można dodać **CloudStorageAccount** podpis metody toohello parametru.

## <a name="real-time-monitoring"></a>Monitorowanie w czasie rzeczywistym
Ponieważ danych wejściowych funkcji często przetwarzania dużych ilości danych, hello zestaw SDK zadań Webjob pulpitu nawigacyjnego zawiera dane monitorowania w czasie rzeczywistym. Witaj **dziennika wywołania** sekcji informuje, czy funkcja hello nadal działa.

![Transfer danych przychodzących systemem — funkcja](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

Hello **szczegóły wywołania** raporty strony hello funkcji postępu (liczba jednostek zapisywane) jest uruchomiona, i daje możliwość tooabort go.

![Transfer danych przychodzących systemem — funkcja](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

Gdy funkcja hello zakończeniu hello **szczegóły wywołania** hello liczbę wierszy, zapisany raporty strony.

![Transfer danych przychodzących Zakończono — funkcja](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a>Jak tooread wiele jednostek z tabeli
tooread tabelę, użyj hello **tabeli** atrybutem **IQueryable<T>**  parametru wpisuje **T** pochodną **TableEntity**lub implementuje **ITableEntity**.

Witaj Poniższy przykładowy kod odczytuje i rejestruje wszystkie wiersze z hello **wejściowych** tabeli:

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

### <a name="how-tooread-a-single-entity-from-a-table"></a>Jak tooread pojedyncza jednostka z tabeli
Brak **tabeli** konstruktora atrybutu z dwóch dodatkowych parametrów, które umożliwiają określenie hello klucz partycji i klucz wiersza, jeśli chcesz toobind tooa pojedynczej tabeli jednostki.

Witaj Poniższy przykładowy kod odczytuje wiersz tabeli **osoby** jednostki na podstawie partycji klucza i wiersz klucza wartości otrzymane w wiadomości w kolejce:  

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


Witaj **osoby** klasy w tym przykładzie nie ma tooimplement **ITableEntity**.

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a>Jak toouse hello interfejsu API magazynu .NET bezpośrednio toowork z tabeli
Można również użyć hello **tabeli** atrybutem **CloudTable** obiektu dla większą elastyczność podczas pracy z tabelą.

Witaj poniższy kod używa próbki **CloudTable** obiekt tooadd toohello pojedynczej jednostki *wejściowych* tabeli.

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

Aby uzyskać więcej informacji na temat toouse hello **CloudTable** obiektów, zobacz [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-tables.md).

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a>Tematy pokrewne objętych kolejek hello jak tooarticle
Uzyskać informacji na temat sposobu przetwarzania tabeli toohandle wyzwalane komunikatu w kolejce, lub dla zadań Webjob scenariusze zestawu SDK nie określonych tootable przetwarzania, zobacz [Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (zadania WebJob projekty) ](vs-storage-webjobs-getting-started-queues.md).

## <a name="next-steps"></a>Następne kroki
W tym artykule dostarczył kodu przykłady przedstawiające sposób toohandle typowe scenariusze dotyczące pracy z tabel Azure. Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasoby dokumentacji zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).

