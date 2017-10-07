---
title: "toouse aaaHow magazynu obiektów blob platformy Azure z hello zestaw SDK zadań Webjob"
description: "Dowiedz się, jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob. Wyzwalanie proces po wyświetleniu nowego obiektu blob w kontenerze i obsługiwać \"skażone obiekty BLOB\"."
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
ms.openlocfilehash: b34ea8cffee7c0475641886150dee521130a3132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a>Jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob
## <a name="overview"></a>Omówienie
Ten przewodnik zawiera C# jak przykłady kodu przedstawiające tootrigger procesu podczas tworzenia lub aktualizowania obiektów blob platformy Azure. Przykłady kodu Hello użyj [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md) wersja 1.x.

Aby uzyskać przykłady kodu, które pokazują, jak obiekty BLOB toocreate, zobacz [jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Witaj przewodnika przyjęto założenia, wiadomo, [jak toocreate projektu zadania WebJob w programie Visual Studio z połączeniem ciągi konto magazynu punktu tooyour](websites-dotnet-webjobs-sdk-get-started.md) lub zbyt[wielu kont magazynu](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

## <a id="trigger"></a>Jak tootrigger funkcja, gdy obiekt blob jest tworzony lub aktualizowany
W tej sekcji przedstawiono sposób toouse hello `BlobTrigger` atrybutu. 

> [!NOTE]
> zestaw SDK zadań Webjob skanowania dziennika Hello pliki toowatch dla nowych lub zmienionych obiektów blob. Ten proces nie jest w czasie rzeczywistym; funkcja może nie pobrać są uruchamiane kilka minut lub dłużej po utworzeniu obiektu blob hello. Ponadto [magazynu dzienniki są tworzone na "starań"](https://msdn.microsoft.com/library/azure/hh343262.aspx) ciągły, lub nie ma żadnej gwarancji, że wszystkie zdarzenia zostaną przechwycone. W niektórych warunkach może pominąć dzienników. Jeśli ograniczenia szybkości i niezawodności hello wyzwalaczy obiektu blob nie są dozwolone dla aplikacji, hello zalecana metoda jest toocreate komunikatu w kolejce, podczas tworzenia obiektu blob hello i użyj hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) atrybutu zamiast Witaj `BlobTrigger` atrybutu w funkcji hello, który przetwarza hello obiektu blob.
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a>Jeden symbol zastępczy dla obiektu blob nazwy z rozszerzeniem
Witaj Poniższy przykładowy kod kopiuje tekst obiektów blob, które pojawiają się w hello *wejściowych* toohello kontenera *dane wyjściowe* kontenera:

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Hello Konstruktor atrybutu ma parametr ciąg, który określa nazwę kontenera hello i hello nazwę obiektu blob. W tym przykładzie o nazwie obiektu blob *Blob1.txt* jest tworzony w hello *wejściowych* kontenera, funkcja hello tworzy obiektu blob o nazwie *Blob1.txt* w hello *danych wyjściowych*  kontenera. 

Wzorzec nazwy można określić za pomocą hello blob nazwa symbolu zastępczego, jak pokazano w powitania po przykładowy kod:

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Ten kod kopiuje tylko obiekty BLOB o nazwach rozpoczynających się od "oryginalnego-". Na przykład *Blob1.txt oryginalne* w hello *wejściowych* kontenera jest kopiowana za*Blob1.txt kopiowania* w hello *dane wyjściowe* kontenera.

Jeśli potrzebujesz toospecify wzorzec nazw dla nazwy obiektów blob, które mają nawiasy klamrowe w nazwie hello dwukrotnie hello nawiasów klamrowych. Na przykład, jeśli chcesz, aby obiekty BLOB toofind na powitania *obrazów* kontenera, w którym mają nazwy w następujący sposób:

        {20140101}-soundfile.mp3

Użyj tego deseniu:

        images/{{20140101}}-{name}

Przykład Witaj Witaj *nazwa* wartość symbolu zastępczego będzie *soundfile.mp3*. 

### <a name="separate-blob-name-and-extension-placeholders"></a>Symbole zastępcze nazwę i rozszerzenie oddzielnych obiektów blob
Witaj następujące zmiany przykładowy kod hello rozszerzenie pliku jako kopiuje obiektów blob, które są wyświetlane w hello *wejściowych* toohello kontenera *dane wyjściowe* kontenera. Kod Hello rejestruje rozszerzenie hello hello *wejściowych* obiektu blob i Ustawia rozszerzenie hello hello *dane wyjściowe* obiektów blob za*.txt*.

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

## <a id="types"></a>Czy można powiązać tooblobs typów
Można użyć hello `BlobTrigger` atrybutu na powitania następujące typy:

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

Jeśli chcesz toowork bezpośrednio z hello kontem magazynu platformy Azure, możesz także dodać `CloudStorageAccount` podpis metody toohello parametru.

Przykłady można znaleźć hello [obiektu blob powiązanie kod w repozytorium zestaw sdk zadań webjob azure hello w witrynie GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).

## <a id="string"></a>Pobieranie zawartości obiektu blob tekstu przez powiązanie toostring
Jeśli oczekiwano tekstu w obiektach blob, `BlobTrigger` może być zastosowane tooa `string` parametru. Witaj Poniższy przykładowy kod wiąże tooa obiektu blob tekst `string` parametru o nazwie `logMessage`. Funkcja Hello korzysta zawartości hello toowrite parametru tego toohello obiektu blob hello zestaw SDK zadań Webjob pulpitu nawigacyjnego. 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a id="icbsb"></a>Pobieranie serializacji zawartość obiektu blob przy użyciu ICloudBlobStreamBinder
Witaj Poniższy przykładowy kod używa klasy, która implementuje `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` toobind toohello obiektu blob atrybutu `WebImage` typu.

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

Witaj `WebImage` powiązanie kod znajduje się w `WebImageBinder` klasą pochodzącą z `ICloudBlobStreamBinder`.

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

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a>Trwa pobieranie ścieżka obiektu blob hello hello wyzwalania obiektów blob
Nazwa kontenera hello tooget i nazwa obiektu blob hello obiektu blob, który wyzwolił funkcja hello obejmują `blobTrigger` parametr w sygnaturze funkcji hello typu string.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <a id="poison"></a>Jak obiekty BLOB toohandle poison
Gdy `BlobTrigger` funkcja kończy się niepowodzeniem, hello zestawu SDK wywołania go ponownie, w przypadku hello błąd został spowodowany przez błąd przejściowy. Jeśli hello jest przyczyną niepowodzenia hello zawartości obiektu hello blob, funkcja hello zakończy się niepowodzeniem, zawsze próbuje tooprocess hello blob. Domyślnie program hello SDK wywołuje funkcję się too5 razy dla danego obiektu blob. W przypadku niepowodzenia spróbuj piątym powitania hello SDK dodaje tooa kolejki komunikatów o nazwie *webjob blobtrigger-poison*.

konfiguruje się Hello maksymalnej liczby ponownych prób. Witaj sam [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) ustawienie służy do obsługi skażone obiektów blob i kolejki skażone komunikat — Obsługa. 

komunikat z kolejki Hello skażone obiektów blob jest obiekt JSON, który zawiera hello następujące właściwości:

* FunctionId (w formacie hello *{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*, na przykład: WebJob1.Functions.CopyBlob)
* BlobType ("BlockBlob" lub "PageBlob")
* Właściwość ContainerName
* Element BlobName
* Element ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")

W następujących hello kodu próbki hello `CopyBlob` funkcja ma kod powodujący toofail za każdym razem, gdy jest ona wywoływana. Po hello zestaw SDK wymaga on hello maksymalnej liczby ponownych prób, wiadomość jest tworzona na powitania skażone blob kolejki, a ten komunikat jest przetwarzany przez hello `LogPoisonBlob` funkcji. 

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

Witaj SDK automatycznie deserializuje wiadomości powitania JSON. Oto hello `PoisonBlobMessage` klasy: 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a id="polling"></a>Algorytm sondowania obiektów blob
Witaj zestaw SDK zadań Webjob skanuje wszystkie kontenery określony przez `BlobTrigger` atrybuty podczas uruchamiania aplikacji. Na koncie magazynu dużych ten tryb skanowania może zająć trochę czasu, dlatego może być trochę czasu, zanim znajdują się nowe obiekty BLOB i `BlobTrigger` funkcje są wykonywane.

rejestruje powitalne SDK okresowo odczytuje z magazynu obiektów blob hello toodetect nowych lub zmienionych obiektów blob w po uruchomieniu aplikacji. Witaj dzienniki obiektów blob są buforowane i tylko fizycznie zapisane co 10 minut lub tak, więc mogą występować znaczne opóźnienia po obiektu blob jest tworzony lub aktualizowany przed odpowiadającego hello `BlobTrigger` wykonuje funkcji. 

Brak wyjątek dla obiektów blob, które są tworzone przy użyciu hello `Blob` atrybutu. Gdy hello zestaw SDK zadań Webjob tworzy nowy obiekt blob, natychmiast przekazaniem nowego obiektu blob hello dopasowania tooany `BlobTrigger` funkcji. W związku z tym jeśli łańcuch blob wejściach i wyjściach, hello SDK może je przetwarzać wydajnie. Ale jeśli chcesz małych opóźnieniach uruchomiona z obiektu blob funkcji przetwarzania dla obiektów blob, które są tworzone lub zaktualizowany w inny sposób, firma Microsoft zaleca używanie `QueueTrigger` zamiast `BlobTrigger`.

### <a id="receipts"></a>Potwierdzenia obiektów blob
zestaw SDK zadań Webjob Hello, sprawdza nie `BlobTrigger` funkcja jest wywoływana więcej niż raz dla hello sam nowe lub zaktualizowane obiektu blob. Dzieje się tak dzięki utrzymywaniu *obiektu blob potwierdzenia* w kolejności toodetermine wersji danego obiektu blob został przetworzony.

Potwierdzenia obiektów blob są przechowywane w kontenerze o nazwie *azure webjobs hostów* na koncie magazynu Azure hello określona przez ciąg połączenia AzureWebJobsStorage hello. Potwierdzenie obiektu blob ma hello następujących informacji:

* Funkcja, która została wywołana dla obiektu blob hello Hello ("*{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*", na przykład:"WebJob1.Functions.CopyBlob")
* Nazwa kontenera Hello
* Typ obiektu blob Hello ("BlockBlob" lub "PageBlob")
* Nazwa obiektu blob Hello
* Witaj ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")

Jeśli chcesz tooforce ponowne przetworzenie obiektu blob, można ręcznie usunąć hello potwierdzenia obiektu blob dla tego obiektu blob z hello *azure webjobs hostów* kontenera.

## <a id="queues"></a>Tematy pokrewne objętych hello kolejek artykułu
Informacje dotyczące sposobu przetwarzania obiektu blob toohandle wyzwalane komunikatu w kolejce, lub dla zadań Webjob scenariusze zestawu SDK nie określonych tooblob przetwarzania, zobacz [jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Tematy pokrewne omówione w tym artykule Uwzględnij hello następujące elementy:

* Funkcje asynchroniczne
* Wiele wystąpień
* Łagodne zamykanie
* Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji
* Ustawianie parametrów połączenia SDK hello w kodzie.
* Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie
* Skonfiguruj `MaxDequeueCount` obsługi skażone obiektu blob.
* Wyzwalanie funkcji ręcznie
* Zapisywanie dzienników

## <a id="nextsteps"></a> Następne kroki
W tym przewodniku udostępnił przykłady kodu przedstawiające jak obiekty BLOB toohandle typowe scenariusze dotyczące pracy z platformą Azure. Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).

