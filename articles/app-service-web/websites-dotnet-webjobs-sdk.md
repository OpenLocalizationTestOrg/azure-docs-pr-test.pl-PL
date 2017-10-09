---
title: aaaWhat jest hello Azure WebJobs SDK
description: "Toohello wprowadzenie Azure WebJobs SDK. Opisano, jakie hello jest zestaw SDK, typowe scenariusze, które jest przydatne w przypadku oraz przykłady kodu."
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
ms.openlocfilehash: efac7a75c3b68a6a6601fb298f2ccac9bd71709d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-webjobs-sdk"></a>Co to jest hello Azure WebJobs SDK
## <a id="overview"></a>Omówienie
W tym artykule opisano, co hello zestaw SDK zadań Webjob jest, recenzje niektórych typowych scenariuszy jest przydatne w przypadku i zawiera omówienie sposobu ich używania w kodzie.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[Zadania Webjob](websites-webjobs-resources.md) to funkcja usługi Azure App Service pozwala toorun programu lub skryptu w hello tego samego kontekstu jako aplikacji sieci web, aplikacji mobilnej lub aplikacji interfejsu API. Witaj celem hello [zestaw SDK zadań Webjob](websites-webjobs-resources.md) jest kod hello toosimplify zapisu typowych zadań, które mogą wykonywać zadanie WebJob, takich jak przetwarzania obrazu, przetwarzanie kolejki, agregacja danych RSS, plików obsługi i wysyłania wiadomości e-mail. zestaw SDK zadań Webjob Hello ma wbudowane funkcje do pracy z usługą Azure Storage i usługi Service Bus, planowanie zadań i obsługa błędów i wielu innych typowych scenariuszy. Ponadto zaprojektowano toobe rozszerzonego. Witaj [to zestaw SDK zadań Webjob typu open source](https://github.com/Azure/azure-webjobs-sdk/)i ma [repozytorium typu open source dla rozszerzeń](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

zestaw SDK zadań Webjob Hello obejmuje hello następujące składniki:

* **Pakiety NuGet**. Pakiety NuGet, czy dodać projekt aplikacji konsoli w usłudze Visual Studio tooa Podaj platforma, która używa Twój kod przez dekoracji metody z atrybutami zestaw SDK zadań Webjob.
* **Pulpit nawigacyjny**. Część hello zestaw SDK zadań Webjob znajduje się w usłudze Azure App Service i udostępnia rozbudowane monitorowanie i informacji diagnostycznych dla programów, które używają hello pakietów NuGet. Nie masz toouse kodu toowrite te funkcje monitorowania i diagnostyki.

## <a id="scenarios"></a>Scenariusze
Poniżej przedstawiono niektóre typowe scenariusze, które można łatwiej obsługiwać z hello Azure WebJobs SDK:

* Obraz przetwarzania lub innych zadań użycie Procesora CPU. Typową funkcją witryn sieci Web jest hello możliwości tooupload obrazów lub plików wideo. Często ma toomanipulate hello zawartości po przekazaniu, ale nie mają toomake hello użytkownika oczekiwania, podczas gdy można to zrobić.
* Przetwarzanie kolejki. Typowa dla toocommunicate frontonu sieci web, przy użyciu usługi wewnętrznej bazy danych jest toouse kolejek. Gdy hello witryny sieci Web musi pracować tooget, wypycha wiadomości do kolejki. Usługi zaplecza ściąga wiadomości z kolejki hello i hello pracy. Możesz użyć kolejki przetwarzania obrazów: na przykład po hello użytkownik prześle liczba plików, umieść hello nazwy plików w toobe komunikat kolejki, pobrana przez hello wewnętrznej bazy danych do przetwarzania. Można także użyć czasu odpowiedzi witryny tooimprove kolejek. Na przykład zamiast zapisywania bezpośrednio tooa bazy danych SQL, zapis tooa kolejki, poinformuj użytkownika hello wszystko gotowe i umożliwić hello wewnętrznej bazy danych usługi dojścia dużymi opóźnieniami relacyjna baza danych działa. Na przykład kolejki przetwarzania z procesem obrazu Zobacz hello [WebJobs SDK Wprowadzenie — samouczek](websites-dotnet-webjobs-sdk-get-started.md).
* Agregacja danych RSS. Jeśli witryna jest przechowywana lista źródeł danych RSS, można ściągnąć we wszystkich artykułów hello ze źródeł danych hello w tle.
* Plik konserwacji, takich jak agregowanie lub czyszczenie plików dziennika.  Może być tworzona przez kilka witryn lub dla oddzielnego pliki dziennika okresów, które mają być toocombine w kolejności toorun zadania analizy na nich. Można też tooschedule zadań toorun co tydzień tooclean starych plików dziennika.
* Transfer danych przychodzących w tabelach platformy Azure. Mogą być przechowywane pliki i obiekty BLOB i chcesz tooparse je i hello dane są przechowywane w tabelach. Funkcja wejściowych Hello można zapisywania wiele wierszy (miliony w niektórych przypadkach) i hello zestaw SDK zadań Webjob ułatwia możliwe tooimplement ta funkcja łatwe. Witaj zestaw SDK zawiera również monitorowanie w czasie rzeczywistym wskaźniki postępu, takich jak hello liczba wierszy w tabeli hello.
* Inne długotrwałych zadań, które mają toorun w wątku w tle, takie jak [wysyłania wiadomości e-mail](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure). 
* Wszystkie zadania, które mają toorun zgodnie z harmonogramem, takich jak wykonywanie operacji tworzenia kopii zapasowych każdej nocy.

W wielu z tych scenariuszy można tooscale toorun aplikacji sieci web, na wiele maszyn wirtualnych, które będą działać jednocześnie wiele zadań Webjob. W niektórych scenariuszach, może to spowodować hello sam danych przetwarzana wiele razy, ale nie stanowi to problemu podczas korzystania z wbudowanych kolejki hello, obiektów blob i wyzwalaczy usługi Service Bus hello zestaw SDK zadań Webjob. Hello SDK gwarantuje, że funkcje będą przetwarzane tylko raz dla każdego komunikatu lub obiektu blob.

Witaj zestaw SDK zadań Webjob ułatwia też łatwo toohandle typowe scenariusze obsługi błędów. Można skonfigurować alerty toosend powiadomienia po funkcji nie powiedzie się i przekroczeń limitu czasu oczekiwania można ustawić tak, aby funkcja została anulowana automatycznie, jeśli nie zakończy się przed upływem określonego limitu czasu.

## <a id="code"></a>Przykłady kodu
Kod Hello obsługi typowych zadań, które współpracują z usługą Azure Storage jest proste. W aplikacji konsoli `Main` metody tworzenia `JobHost` toomethods pisania wywołuje obiekt, który koordynuje hello. Hello framework zestaw SDK zadań Webjob wie, gdy toocall metody i jakie parametru wartości toouse oparte na powitania zestaw SDK zadań Webjob atrybutów, można użyć w nich. Witaj zestaw SDK zawiera *wyzwalaczy* które określają, jakie warunki spowodować hello toobe funkcja wywoływana, i *integratorów* określające, jak tooget informacji do i z parametrów metody.

Na przykład Witaj [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) atrybut powoduje toobe funkcja wywoływana, gdy wiadomość zostanie odebrana w kolejce, a jeśli hello wiadomość jest w formacie JSON dla tablicy bajtów lub typ niestandardowy, wiadomość hello automatycznie zdeserializowany. Witaj [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) atrybutu wyzwala proces zawsze, gdy nowy obiekt blob jest tworzony na koncie magazynu Azure.

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

Witaj `JobHost` obiektu to kontener dla zestawu funkcji tła. Witaj `JobHost` hello monitorów obiektu funkcje, obserwuje zdarzenia, które mogą powodować je i wykonuje funkcje powitania po wystąpieniu zdarzenia wyzwalacza. Należy wywołać `JobHost` tooindicate metody czy toorun procesu kontenera hello na hello bieżącego wątku lub wątku w tle. Przykład Witaj Witaj `RunAndBlock` metody uruchamia proces hello stale na powitania bieżącego wątku.

Ponieważ hello `ProcessQueueMessage` metoda w tym przykładzie ma `QueueTrigger` atrybutu hello wyzwalacza dla tej funkcji jest odbioru hello nowego komunikatu w kolejce. Witaj `JobHost` obiekt oczekuje na nowe komunikaty w kolejce na powitania określonej kolejki ("webjobsqueue" w tym przykładzie) i kiedy zostanie odnaleziony, wywołuje `ProcessQueueMessage`. 

Witaj `QueueTrigger` atrybutu wiąże hello `inputText` wartość parametru toohello hello kolejki wiadomości. I hello `Blob` atrybut wiązania `TextWriter` obiektu blob tooa o nazwie "element blobname" w kontenerze o nazwie "containername".  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

Funkcja Hello używa następnie te parametry toowrite hello wartość hello kolejki wiadomości toohello blob:

        writer.WriteLine(inputText);

Funkcje wyzwalacza i integratora Hello hello zestaw SDK zadań Webjob znacznego uproszczenia kodu hello masz toowrite. Witaj niskiego poziomu kod wymagany tooprocess kolejek, obiektów blob, lub plików lub tooinitiate zaplanowane zadania, odbywa się automatycznie przez hello framework zestaw SDK zadań Webjob. Na przykład hello framework tworzy kolejki, które jeszcze nie istnieje, zostanie otwarta hello kolejki, odczyty kolejki komunikatów, usuwa kolejka komunikatów podczas przetwarzania ukończenia, tworzy kontenerów obiektów blob, które nie istnieją, ale zapisuje tooblobs i tak dalej.

Witaj Poniższy przykładowy kod przedstawia różne Wyzwalacze w jednym zadania WebJob: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, i `ErrorTrigger`. 

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
            too= "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors toohello Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <a id="schedule"></a>Planowanie
Witaj `TimerTrigger` atrybutu zapewnia hello możliwości tootrigger funkcje toorun zgodnie z harmonogramem. Można zaplanować zadanie WebJob, jak zestaw SDK zadań Webjob hello całego za pomocą funkcji poszczególnych Azure lub harmonogram zadania WebJob, używając `TimerTrigger`. Oto przykładowy kod.

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

Aby uzyskać więcej przykładowy kod, zobacz [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) w repozytorium azure-zadań webjob sdk rozszerzenia hello w witrynie GitHub.com.

## <a name="extensibility"></a>Rozszerzalność
W przypadku innymi toobuilt w funkcji--hello zestaw SDK zadań Webjob pozwala toowrite wyzwalaczy niestandardowych i integratorów.  Na przykład można napisać wyzwalacze zdarzeń pamięci podręcznej i okresowo harmonogramów. [Repozytorium typu open source](https://github.com/Azure/azure-webjobs-sdk-extensions) zawiera [szczegółowy przewodnik na zestaw SDK zadań Webjob rozszerzalności](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) i przykładowy kod toohelp rozpoczęcie zapisywania swoje własne wyzwalacze i integratorów.

## <a id="workerrole"></a>Przy użyciu hello zestaw SDK zadań Webjob poza zadań Webjob
Program, który używa hello hello zestaw SDK zadań Webjob to standardowa aplikacja konsoli i można uruchomić w dowolnym miejscu — nie ma toorun jako zadanie WebJob. Hello program można przetestować lokalnie na komputerze deweloperskim i w środowisku produkcyjnym, można uruchamiać go w roli procesu roboczego usługi w chmurze lub usługa Windows Jeśli wolisz jeden z tych środowisk. 

Jednak hello pulpit nawigacyjny jest dostępny tylko jako rozszerzenie dla aplikacji sieci web w usłudze Azure App Service. Jeśli mają toorun poza zadanie WebJob i nadal używać hello pulpitu nawigacyjnego, można skonfigurować sieci web toouse aplikacji hello tego samego konta magazynu, że parametry połączenia pulpitu nawigacyjnego zestawu SDK zadań Webjob odwołuje się do i pulpitu nawigacyjnego zadań Webjob, aplikacja sieci web, następnie spowodują wyświetlenie danych dotyczących funkcji wykonanie programu, który jest uruchomiona w innym miejscu. Toohello pulpitu nawigacyjnego można uzyskać za pomocą hello adresu URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions. Aby uzyskać więcej informacji, zobacz [pobierania pulpitu nawigacyjnego lokalnego środowiska deweloperskiego przy użyciu zestawu SDK zadań Webjob hello](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ale należy pamiętać, że wpis w blogu hello zawiera stara nazwa ciągu połączenia. 

## <a id="nostorage"></a>Funkcje pulpitu nawigacyjnego
zestaw SDK zadań Webjob Hello ma wiele zalet, nawet wtedy, gdy nie jest używany zestaw SDK zadań Webjob Wyzwalacze lub integratorów:

* Można wywołać funkcji z hello pulpitu nawigacyjnego.
* Można powtarzania funkcji z hello pulpitu nawigacyjnego.
* Dzienniki można wyświetlać w hello pulpitu nawigacyjnego, połączone toohello określonego zadania WebJob (Dzienniki aplikacji napisane przy użyciu Console.Out, Console.Error, śledzenia, itp.) lub połączone toohello wywołania określonej funkcji, które powstały (Dzienniki napisane przy użyciu `TextWriter` obiekt tego zestawu SDK przekazuje funkcja toohello jako parametr powitalne). 

Aby uzyskać więcej informacji, zobacz [jak toomanually wywołanie funkcji](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) i [sposób rejestrowania toowrite](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs) 

## <a id="nextsteps"></a>Następne kroki
Aby uzyskać więcej informacji na temat hello zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).

Informacje o hello najnowsze ulepszenia toohello zestaw SDK zadań Webjob, zobacz hello [wersji](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).

