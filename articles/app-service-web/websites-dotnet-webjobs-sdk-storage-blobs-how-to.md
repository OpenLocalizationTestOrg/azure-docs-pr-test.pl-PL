---
title: "Jak korzystać z Magazynu obiektów blob platformy Azure przy użyciu zestawu SDK WebJobs"
description: "Dowiedz się, jak używać magazynu obiektów blob platformy Azure przy użyciu zestawu SDK zadań Webjob. Wyzwalanie proces po wyświetleniu nowego obiektu blob w kontenerze i obsługiwać \"skażone obiekty BLOB\"."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: e0a792ccdf8097d5cde254d6d4690a64838378ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a>Jak korzystać z Magazynu obiektów blob platformy Azure przy użyciu zestawu SDK WebJobs
## <a name="overview"></a>Omówienie
Ten przewodnik zawiera C# przykłady kodu, których pokazano, jak do wyzwalania procesu podczas tworzenia lub aktualizowania obiektów blob platformy Azure. Kod przykłady użycia [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md) wersja 1.x.

Aby uzyskać przykłady kodu, które pokazują, jak utworzyć obiekty BLOB, zobacz [jak używać magazynu kolejek Azure przy użyciu zestawu SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Przewodnik zakłada wiesz, [Tworzenie projektu zadania WebJob w programie Visual Studio z połączeniem ciągi prowadzące do konta magazynu](websites-dotnet-webjobs-sdk-get-started.md) lub [wielu kont magazynu](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

## <a id="trigger"></a>Sposób włączania funkcji podczas tworzenia lub aktualizowania obiektu blob
W tej sekcji przedstawiono sposób użycia `BlobTrigger` atrybutu. 

> [!NOTE]
> Zestaw SDK zadań Webjob skanuje pliki dziennika, aby wyszukiwać nowych lub zmienionych obiektów blob. Ten proces nie jest w czasie rzeczywistym; funkcja może nie pobrać są uruchamiane kilka minut lub dłużej po utworzeniu obiektu blob. Ponadto [magazynu dzienniki są tworzone na "starań"](https://msdn.microsoft.com/library/azure/hh343262.aspx) ciągły, lub nie ma żadnej gwarancji, że wszystkie zdarzenia zostaną przechwycone. W niektórych warunkach może pominąć dzienników. Jeśli szybkość i niezawodność ograniczenia wyzwalacze obiektu blob nie są dozwolone dla aplikacji, zalecaną metodą jest utworzenie komunikatu w kolejce podczas tworzenia obiektu blob i użyj [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) zamiast atrybutu`BlobTrigger` atrybutu w funkcji, która przetwarza obiektu blob.
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a>Jeden symbol zastępczy dla obiektu blob nazwy z rozszerzeniem
Poniższy przykładowy kod kopiuje tekst obiektów blob, które są widoczne w *wejściowych* kontener, aby *dane wyjściowe* kontenera:

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Konstruktor atrybutu ma parametr typu string, który określa nazwę kontenera i nazwę obiektu blob. W tym przykładzie o nazwie obiektu blob *Blob1.txt* jest tworzony w *wejściowych* kontenera, funkcja ta umożliwia tworzenie obiektu blob o nazwie *Blob1.txt* w *dane wyjściowe* kontenera. 

Wzorzec nazwy można określić za pomocą nazwy obiektu blob — symbol zastępczy, jak pokazano w poniższym przykładzie kodu:

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Ten kod kopiuje tylko obiekty BLOB o nazwach rozpoczynających się od "oryginalnego-". Na przykład *Blob1.txt oryginalne* w *wejściowych* kontenera jest kopiowany do *Blob1.txt kopiowania* w *dane wyjściowe* kontenera.

Jeśli musisz określić wzorzec nazw dla nazwy obiektów blob, które mają nawiasy klamrowe w nazwie dwukrotnie nawiasów klamrowych. Na przykład, jeśli chcesz znaleźć obiekty BLOB w *obrazów* kontenera, w którym mają nazwy w następujący sposób:

        {20140101}-soundfile.mp3

Użyj tego deseniu:

        images/{{20140101}}-{name}

W tym przykładzie *nazwa* wartość symbolu zastępczego będzie *soundfile.mp3*. 

### <a name="separate-blob-name-and-extension-placeholders"></a>Symbole zastępcze nazwę i rozszerzenie oddzielnych obiektów blob
Poniższy przykładowy kod powoduje zmianę rozszerzenia pliku jako kopiowania obiektów blob, które są widoczne w *wejściowych* kontener, aby *dane wyjściowe* kontenera. Kod rejestruje rozszerzenie *wejściowych* obiektu blob i Ustawia rozszerzenie *dane wyjściowe* obiektu blob do *.txt*.

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <a id="types"></a>Typy, które można powiązać obiekty BLOB
Można użyć `BlobTrigger` atrybutu w następujących typów:

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* Inne typy deserializacji przez [ICloudBlobStreamBinder](#icbsb) 

Jeśli chcesz pracować bezpośrednio z kontem magazynu platformy Azure, możesz także dodać `CloudStorageAccount` parametru w podpisie metody.

Aby uzyskać przykłady, zobacz [obiektu blob powiązanie kod w repozytorium zestaw sdk zadań webjob azure w witrynie GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).

## <a id="string"></a>Pobieranie zawartości obiektu blob tekstu przez powiązanie do ciągu
Jeśli oczekiwano tekstu w obiektach blob, `BlobTrigger` można zastosować do `string` parametru. Poniższy przykładowy kod wiąże obiektu blob tekstu do `string` parametru o nazwie `logMessage`. Funkcja używa parametru do zapisania zawartości obiektu blob do pulpitu nawigacyjnego, zestaw SDK zadań Webjob. 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a id="icbsb"></a>Pobieranie serializacji zawartość obiektu blob przy użyciu ICloudBlobStreamBinder
Poniższy przykład kodu wykorzystuje klasy, która implementuje `ICloudBlobStreamBinder` umożliwiające `BlobTrigger` atrybutu będzie tworzone powiązanie obiektu blob do `WebImage` typu.

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK", 
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

`WebImage` Powiązanie kod znajduje się w `WebImageBinder` klasą pochodzącą z `ICloudBlobStreamBinder`.

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input, 
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="getting-the-blob-path-for-the-triggering-blob"></a>Pobieranie ścieżki obiektu blob wyzwalająca obiektu blob
Aby uzyskać nazwę kontenera i nazwa obiektu blob obiektu blob, który ma wywołał funkcję, dołącz `blobTrigger` parametr w sygnaturze funkcji typu string.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <a id="poison"></a>Sposób obsługi skażone obiektów blob
Gdy `BlobTrigger` funkcja kończy się niepowodzeniem, zestaw SDK wymaga go ponownie, w przypadku, gdy błąd został spowodowany przez błąd przejściowy. Jeśli niepowodzenie jest spowodowane zawartość obiektu blob, funkcja zakończy się niepowodzeniem, za każdym razem, gdy próbuje przetworzyć obiektu blob. Domyślnie zestaw SDK wywołuje funkcję maksymalnie 5 razy dla danego obiektu blob. Jeśli piątym spróbuj kończy się niepowodzeniem, zestaw SDK dodaje komunikat do kolejki o nazwie *webjob blobtrigger-poison*.

Konfiguruje się maksymalnej liczby ponownych prób. Taki sam [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) ustawienie służy do obsługi skażone obiektów blob i kolejki skażone komunikat — Obsługa. 

Komunikat z kolejki skażone obiektów blob jest obiekt JSON, który zawiera następujące właściwości:

* FunctionId (w formacie *{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*, na przykład: WebJob1.Functions.CopyBlob)
* BlobType ("BlockBlob" lub "PageBlob")
* Właściwość ContainerName
* Element BlobName
* Element ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")

W poniższym przykładzie kodu `CopyBlob` funkcja ma kod powodujący niepowodzenie za każdym razem, gdy jest ona wywoływana. Po zestaw SDK wymaga on maksymalnej liczby ponownych prób, wiadomość jest tworzony w kolejce skażone obiektów blob, a ten komunikat jest przetwarzany przez `LogPoisonBlob` funkcji. 

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

Zestaw SDK automatycznie deserializuje komunikat JSON. Oto `PoisonBlobMessage` klasy: 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a id="polling"></a>Algorytm sondowania obiektów blob
Zestaw SDK zadań Webjob skanuje wszystkie kontenery określony przez `BlobTrigger` atrybuty podczas uruchamiania aplikacji. Na koncie magazynu dużych ten tryb skanowania może zająć trochę czasu, dlatego może być trochę czasu, zanim znajdują się nowe obiekty BLOB i `BlobTrigger` funkcje są wykonywane.

Aby wykryć nowe lub zmienione obiekty BLOB po uruchomieniu aplikacji, zestaw SDK okresowo odczytuje z dzienników magazynu obiektów blob. Dzienniki obiektów blob są buforowane oraz tylko fizycznie zapisane co 10 minut lub tak, więc mogą występować znaczne opóźnienie po obiektu blob jest tworzony lub aktualizowany przed odpowiadającego `BlobTrigger` wykonuje funkcji. 

Występuje wyjątek dla obiektów blob, które utworzono za pomocą `Blob` atrybutu. Gdy zestaw SDK zadań Webjob tworzy nowy obiekt blob, przekazaniem nowego obiektu blob natychmiast żadnych zgodnych `BlobTrigger` funkcji. W związku z tym jeśli łańcuch blob wejściach i wyjściach, zestaw SDK może je przetwarzać wydajnie. Ale jeśli chcesz małych opóźnieniach uruchomiona z obiektu blob funkcji przetwarzania dla obiektów blob, które są tworzone lub zaktualizowany w inny sposób, firma Microsoft zaleca używanie `QueueTrigger` zamiast `BlobTrigger`.

### <a id="receipts"></a>Potwierdzenia obiektów blob
Zestaw SDK zadań Webjob, sprawdza nie `BlobTrigger` funkcja jest wywoływana więcej niż raz dla tego samego obiektu blob nowe lub zaktualizowane. Dzieje się tak dzięki utrzymywaniu *obiektu blob potwierdzenia* w celu ustalenia, czy wersja danego obiektu blob został przetworzony.

Potwierdzenia obiektów blob są przechowywane w kontenerze o nazwie *azure webjobs hostów* w określona przez ciąg połączenia AzureWebJobsStorage konto magazynu Azure. Potwierdzenie obiektu blob zawiera następujące informacje:

* Funkcja, która została wywołana dla obiektu blob ("*{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*", na przykład:"WebJob1.Functions.CopyBlob")
* Nazwa kontenera
* Typ obiektów blob ("BlockBlob" lub "PageBlob")
* Nazwa obiektu blob
* Element ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")

Jeśli chcesz wymusić ponowne przetworzenie obiektu blob, należy ręcznie usunąć potwierdzenia obiektu blob dla tego obiektu blob z *azure webjobs hostów* kontenera.

## <a id="queues"></a>Tematy pokrewne objętych artykułem kolejek
Informacje dotyczące obsługi przetwarzania obiektu blob wyzwalane przez komunikatu w kolejce, lub zestaw SDK zadań Webjob do obiektu blob nie są typowe scenariusze przetwarzania, zobacz [jak używać magazynu kolejek Azure przy użyciu zestawu SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Tematy pokrewne omówione w tym artykule są następujące:

* Funkcje asynchroniczne
* Wiele wystąpień
* Łagodne zamykanie
* Użyj zestawu SDK zadań Webjob atrybutów w treści funkcji
* Ustaw parametry połączenia SDK w kodzie.
* Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie
* Skonfiguruj `MaxDequeueCount` obsługi skażone obiektu blob.
* Wyzwalanie funkcji ręcznie
* Zapisywanie dzienników

## <a id="nextsteps"></a> Następne kroki
W tym przewodniku udostępnił przykłady kodu, które przedstawiają sposób obsługi typowe scenariusze dotyczące pracy z obiektami blob Azure. Aby uzyskać więcej informacji o sposobie używania zadań Webjob Azure i zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).

