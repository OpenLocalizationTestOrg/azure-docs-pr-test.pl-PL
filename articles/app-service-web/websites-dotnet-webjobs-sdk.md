---
title: "Co to jest zestaw SDK usługi Azure WebJobs"
description: "Wprowadzenie do zestawu SDK zadań Webjob Azure. Opis zestawu SDK, typowe scenariusze jest przydatne w przypadku i przykłady kodu."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 8eb05b7cbfb4505f2e94c5b8e6d367ec63a2f033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-the-azure-webjobs-sdk"></a>Co to jest zestaw SDK usługi Azure WebJobs
## <a id="overview"></a>Omówienie
W tym artykule opisano, co to jest zestaw SDK zadań Webjob, recenzje niektórych typowych scenariuszy jest przydatne w przypadku i zawiera omówienie sposobu ich używania w kodzie.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[Zadania Webjob](websites-webjobs-resources.md) to funkcja usługi Azure App Service umożliwia uruchamianie programu lub skryptu w tym samym kontekście jako aplikacji sieci web, aplikacji mobilnej lub aplikacji interfejsu API. Celem [zestaw SDK zadań Webjob](websites-webjobs-resources.md) jest uprościć kod zapisu typowych zadań, które mogą wykonywać zadanie WebJob, takich jak przetwarzania obrazu, przetwarzanie kolejki, agregacja danych RSS, plików obsługi i wysyłania wiadomości e-mail. Zestaw SDK zadań Webjob ma wbudowane funkcje do pracy z usługą Azure Storage i usługi Service Bus, planowanie zadań i obsługa błędów i wielu innych typowych scenariuszy. Ponadto zostało zaprojektowane do być rozszerzalne. [To zestaw SDK zadań Webjob typu open source](https://github.com/Azure/azure-webjobs-sdk/)i ma [repozytorium typu open source dla rozszerzeń](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Zestaw SDK zadań Webjob obejmuje następujące składniki:

* **Pakiety NuGet**. Pakiety NuGet, które można dodać do projektu aplikacji Konsolowej programu Visual Studio Podaj platforma, która używa Twój kod przez dekoracji metody z atrybutami zestaw SDK zadań Webjob.
* **Pulpit nawigacyjny**. Część zestawu SDK zadań Webjob znajduje się w usłudze Azure App Service i udostępnia rozbudowane monitorowanie i informacji diagnostycznych dla programów, które korzystają z pakietu NuGet. Nie trzeba napisać kod, aby korzystać z tych funkcji monitorowania i diagnostyki.

## <a id="scenarios"></a>Scenariusze
Poniżej przedstawiono niektóre typowe scenariusze, które można łatwiej obsługiwać przy użyciu zestawu SDK zadań Webjob Azure:

* Obraz przetwarzania lub innych zadań użycie Procesora CPU. Typową funkcją witryn sieci Web jest przekazywanie obrazów lub plików wideo. Często ma być manipulować zawartością po przekazaniu, ale nie chcesz użytkownik Zaczekaj, aż można to zrobić.
* Przetwarzanie kolejki. Typowa dla frontonu sieci web do komunikowania się z usługą wewnętrznej bazy danych ma używać kolejek. Jeśli witryna sieci Web musi pracować, wypycha wiadomości do kolejki. Usługi zaplecza ściąga wiadomości z kolejki i wykonuje pracę. Możesz użyć kolejki przetwarzania obrazów: na przykład po użytkownik przekazuje liczba plików, umieść nazwy plików w kolejki komunikatów w celu pobrania przez wewnętrznej bazy danych do przetwarzania. Lub można zwiększyć elastyczność lokacji za pomocą kolejek. Na przykład zamiast zapisywania bezpośrednio do bazy danych SQL, napisz do kolejki, poinformuj użytkownika, którego wszystko będzie gotowe, i umożliwić wewnętrznej bazy danych usługi dojścia dużymi opóźnieniami relacyjna baza danych działa. Na przykład kolejki przetwarzania z procesem obrazu zobacz [WebJobs SDK Wprowadzenie — samouczek](websites-dotnet-webjobs-sdk-get-started.md).
* Agregacja danych RSS. Jeśli witryna jest przechowywana lista źródeł danych RSS, można ściągnąć we wszystkich artykułów ze źródeł danych w tle.
* Plik konserwacji, takich jak agregowanie lub czyszczenie plików dziennika.  Konieczne może być tworzona przez kilka witryn lub dla oddzielnego okresów, które mają zostać połączone w celu uruchomienia zadania analizy na ich pliki dziennika. Możesz też zaplanować zadanie co tydzień, aby wyczyścić stare pliki dziennika.
* Transfer danych przychodzących w tabelach platformy Azure. Może być przechowywane pliki i obiekty BLOB i chcesz je przeanalizować i przechowuje dane w tabelach. Funkcja wejściowych można zapisywania wiele wierszy (miliony w niektórych przypadkach) i zestaw SDK zadań Webjob pozwala łatwo zaimplementować tę funkcję. Zestaw SDK zawiera również monitorowanie w czasie rzeczywistym wskaźniki postępu, takie jak liczba wierszy w tabeli.
* Inne długotrwałych zadań, które mają być uruchamiane w wątku w tle, takie jak [wysyłania wiadomości e-mail](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure). 
* Zadania, które mają być uruchamiane zgodnie z harmonogramem, takich jak wykonywanie operacji tworzenia kopii zapasowych każdej nocy.

W wielu z tych scenariuszy można skalować aplikacji sieci web, do uruchamiania na wielu maszyn wirtualnych, które będą działać jednocześnie wiele zadań Webjob. W niektórych przypadkach może to spowodować tych samych danych przetwarzana wiele razy, ale nie jest problem podczas korzystania z wbudowanych kolejek, obiektów blob i wyzwalaczy usługi Service Bus zestawu SDK zadań Webjob. Zestaw SDK gwarantuje, że funkcje będą przetwarzane tylko raz dla każdego komunikatu lub obiektu blob.

Zestaw SDK zadań Webjob ułatwia także do obsługi błędu typowe scenariusze obsługi. Alerty można skonfigurować do wysyłania powiadomień, gdy operacja zakończy się niepowodzeniem i przekroczeń limitu czasu oczekiwania można ustawić tak, aby funkcja została anulowana automatycznie, jeśli nie zakończy się przed upływem określonego limitu czasu.

## <a id="code"></a>Przykłady kodu
Kod obsługi typowych zadań, które współpracują z usługą Azure Storage jest proste. W aplikacji konsoli `Main` metody tworzenia `JobHost` obiekt, który koordynuje wywołań do metod pisania. Zestaw SDK zadań Webjob framework wie, kiedy do wywołania metody, i jakie wartości parametrów do użycia na podstawie zestawu SDK zadań Webjob atrybutów używanego w nich. Zestaw SDK udostępnia *wyzwalaczy* które określają, jakie warunki spowodować, że funkcja wywoływana, i *integratorów* określające, jak uzyskać informacji do i z parametrów metody.

Na przykład [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) atrybutu powoduje, że funkcja wywoływana, gdy wiadomość zostanie odebrana w kolejce, a jeśli wiadomość jest w formacie JSON dla tablicy bajtów lub typ niestandardowy, wiadomości automatycznie zdeserializowany. [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) atrybutu wyzwala proces zawsze, gdy nowy obiekt blob jest tworzony na koncie magazynu Azure.

Oto prosty program, który sonduje kolejkę i utworzenie obiektu blob dla każdego Odebrano komunikat z kolejki:

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

`JobHost` Obiektu to kontener dla zestawu funkcji tła. `JobHost` Obiekt monitoruje funkcje Obserwujący zdarzeń wyzwalających i wykonuje funkcje po wystąpieniu zdarzenia wyzwalacza. Należy wywołać `JobHost` metodę, aby wskazać, czy Proces kontenera do uruchomienia na bieżącym wątku lub wątku w tle. W tym przykładzie `RunAndBlock` metody uruchamia proces stale w bieżącym wątku.

Ponieważ `ProcessQueueMessage` metoda w tym przykładzie ma `QueueTrigger` atrybutu wyzwalacza dla tej funkcji jest odebranie nowej kolejki wiadomości. `JobHost` Obiekt oczekuje na nowe komunikaty w kolejce na określonej kolejki ("webjobsqueue" w tym przykładzie) i kiedy zostanie odnaleziony, wywołuje `ProcessQueueMessage`. 

`QueueTrigger` Atrybut wiązania `inputText` wartość komunikat z kolejki. I `Blob` atrybut wiązania `TextWriter` obiektu do obiektu blob o nazwie "element blobname" w kontenerze o nazwie "containername".  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

Funkcja następnie korzysta z tych parametrów można zapisać wartości komunikatu w kolejce do obiektu blob:

        writer.WriteLine(inputText);

Wyzwalacz i integratora funkcje zestawu SDK zadań Webjob znacznego uproszczenia trzeba napisać kod. Niskiego poziomu kod wymagany do przetwarzania kolejek, obiektów blob lub plików lub zainicjować zaplanowanych zadań odbywa się automatycznie przez platformę, zestaw SDK zadań Webjob. Na przykład platformę tworzy kolejek, dla których nie istnieje jeszcze, otwiera kolejkę, odczyty kolejki komunikatów, usuwa kolejka komunikatów podczas przetwarzania ukończenia, tworzy kontenerów obiektów blob, które nie istnieją, ale zapisuje obiekty BLOB i tak dalej.

Poniższy przykładowy kod przedstawia różne Wyzwalacze w jednym zadań WebJob: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, i `ErrorTrigger`. 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

        public static void ErrorMonitor(
        [ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
        [SendGrid(
            To = "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors to the Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <a id="schedule"></a>Planowanie
`TimerTrigger` Atrybut pozwala na uruchamianie zgodnie z harmonogramem funkcji wyzwalacza. Można zaplanować zadanie WebJob jako całość przy użyciu platformy Azure lub harmonogram pojedynczych funkcji zadanie WebJob przy użyciu zestawu SDK zadań Webjob `TimerTrigger`. Oto przykładowy kod.

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

Aby uzyskać więcej przykładowy kod, zobacz [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) w repozytorium azure-zadań webjob sdk rozszerzeń w witrynie GitHub.com.

## <a name="extensibility"></a>Rozszerzalność
Nie masz ograniczone do wbudowanej funkcji — zestaw SDK zadań Webjob umożliwia pisanie niestandardowych wyzwalaczy i integratorów.  Na przykład można napisać wyzwalacze zdarzeń pamięci podręcznej i okresowo harmonogramów. [Repozytorium typu open source](https://github.com/Azure/azure-webjobs-sdk-extensions) zawiera [szczegółowy przewodnik na zestaw SDK zadań Webjob rozszerzalności](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) i przykładowy kod i ułatwiają rozpoczęcie pracy zapisywania swoje własne wyzwalacze i integratorów.

## <a id="workerrole"></a>Przy użyciu zestawu SDK zadań Webjob poza zadań Webjob
Program, który korzysta z zestawu SDK zadań Webjob to standardowa aplikacja konsoli i mogą uruchamiane w dowolnym miejscu — nie ma do uruchamiania jako zadanie WebJob. Program można przetestować lokalnie na komputerze deweloperskim, a w środowisku produkcyjnym można uruchomić w roli procesu roboczego usługi w chmurze lub usługa systemu Windows, jeśli wolisz jeden z tych środowisk. 

Jednak pulpit nawigacyjny jest dostępny tylko jako rozszerzenie dla aplikacji sieci web w usłudze Azure App Service. Jeśli chcesz uruchomić poza zadanie WebJob i nadal korzystać z pulpitu nawigacyjnego, można skonfigurować aplikacji sieci web, aby użyć tego samego konta magazynu odnoszący się do ciągu połączenia pulpitu nawigacyjnego zestawu SDK zadań Webjob i aplikacji sieci web pulpitu nawigacyjnego zadań Webjob następnie będą wyświetlane dane o wykonanie funkcji z programu, który jest uruchomiona w innym miejscu. Przejść do pulpitu nawigacyjnego za pomocą adresu URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions. Aby uzyskać więcej informacji, zobacz [pobierania pulpitu nawigacyjnego dla wdrożenia lokalnego przy użyciu zestawu SDK zadań Webjob](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ale należy pamiętać, że wpis w blogu zawiera stara nazwa ciągu połączenia. 

## <a id="nostorage"></a>Funkcje pulpitu nawigacyjnego
Zestaw SDK zadań Webjob ma wiele zalet, nawet jeśli nie jest używany zestaw SDK zadań Webjob Wyzwalacze lub integratorów:

* Można wywołać funkcji z poziomu pulpitu nawigacyjnego.
* Można powtarzania funkcji z poziomu pulpitu nawigacyjnego.
* Dzienniki można wyświetlać na pulpicie nawigacyjnym, połączony do określonego zadania WebJob (Dzienniki aplikacji napisane przy użyciu Console.Out, Console.Error, śledzenia, itp.) lub połączony wywołania określonej funkcji, które powstały (Dzienniki napisane przy użyciu `TextWriter` obiekt przekazujący jako parametru funkcji zestawu SDK). 

Aby uzyskać więcej informacji, zobacz [jak ręcznie wywołanie funkcji](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) i [jak zapisywanie dzienników](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs) 

## <a id="nextsteps"></a>Następne kroki
Aby uzyskać więcej informacji na temat zestawu SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).

Informacje o najnowszych ulepszeń do zestawu SDK zadań Webjob, zobacz [wersji](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).

