---
title: "aaaGet wprowadzenie do magazynu obiektów blob i Visual Studio podłączonych usług (projekty zadania WebJob) | Dokumentacja firmy Microsoft"
description: "Sposób uruchamiania przy użyciu magazynu obiektów Blob w projektu zadania WebJob po połączeniu tooan magazynu platformy Azure przy użyciu programu Visual Studio tooget połączone usługi."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: cb2cecacbb1a59f093d5453a91fae33e0f279d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a>Wprowadzenie do obiektów Blob platformy Azure magazynu i Visual Studio połączone usługi (zadania WebJob projekty)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Omówienie
Ten artykuł zawiera C# jak przykłady kodu przedstawiające tootrigger procesu podczas tworzenia lub aktualizowania obiektów blob platformy Azure. Przykłady kodu Hello Użyj hello [zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk.md) wersja 1.x. Po dodaniu projektu zadania WebJob tooa konto magazynu przy użyciu programu Visual Studio hello **dodać usług połączonych** okna dialogowego, hello odpowiedniego pakietu NuGet usługi Magazyn Azure jest zainstalowany, hello odpowiednie .NET odwołania są dodane toohello Projekt i parametry połączenia dla konta magazynu hello są aktualizowane w pliku App.config hello.

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a>Jak tootrigger funkcja, gdy obiekt blob jest tworzony lub aktualizowany
W tej sekcji przedstawiono sposób toouse hello **BlobTrigger** atrybutu.

 **Uwaga:** hello zestaw SDK zadań Webjob skanowania dziennika pliki toowatch dla nowych lub zmienionych obiektów blob. Ten proces jest z założenia powolne; funkcja może nie pobrać są uruchamiane kilka minut lub dłużej po utworzeniu obiektu blob hello.  Jeśli aplikacja wymaga obiekty BLOB tooprocess natychmiast, hello zalecana metoda to toocreate komunikatu w kolejce, podczas tworzenia obiektu blob hello i użyj hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) zamiast hello atrybutu **BlobTrigger** atrybutu w funkcji hello, który przetwarza hello obiektu blob.

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

## <a name="types-that-you-can-bind-tooblobs"></a>Czy można powiązać tooblobs typów
Można użyć hello **BlobTrigger** atrybutu na powitania następujące typy:

* **ciąg**
* **TextReader**
* **Strumień**
* **ICloudBlob**
* **CloudBlockBlob**
* **CloudPageBlob**
* Inne typy deserializacji przez [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)

Jeśli chcesz toowork bezpośrednio z hello kontem magazynu platformy Azure, możesz także dodać **CloudStorageAccount** podpis metody toohello parametru.

## <a name="getting-text-blob-content-by-binding-toostring"></a>Pobieranie zawartości obiektu blob tekstu przez powiązanie toostring
Jeśli oczekiwano tekstu w obiektach blob, **BlobTrigger** może być zastosowane tooa **ciąg** parametru. Witaj Poniższy przykładowy kod wiąże tooa obiektu blob tekst **ciąg** parametru o nazwie **logMessage**. Funkcja Hello korzysta zawartości hello toowrite parametru tego toohello obiektu blob hello zestaw SDK zadań Webjob pulpitu nawigacyjnego.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a>Pobieranie serializacji zawartość obiektu blob przy użyciu ICloudBlobStreamBinder
Witaj Poniższy przykładowy kod używa klasy, która implementuje **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** toobind toohello obiektu blob atrybutu **WebImage** typu.

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

Witaj **WebImage** powiązanie kod znajduje się w **WebImageBinder** klasą pochodzącą z **ICloudBlobStreamBinder**.

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

## <a name="how-toohandle-poison-blobs"></a>Jak obiekty BLOB toohandle poison
Gdy **BlobTrigger** funkcja kończy się niepowodzeniem, hello zestawu SDK wywołania go ponownie, w przypadku hello błąd został spowodowany przez błąd przejściowy. Jeśli hello jest przyczyną niepowodzenia hello zawartości obiektu hello blob, funkcja hello zakończy się niepowodzeniem, zawsze próbuje tooprocess hello blob. Domyślnie program hello SDK wywołuje funkcję się too5 razy dla danego obiektu blob. W przypadku niepowodzenia spróbuj piątym powitania hello SDK dodaje tooa kolejki komunikatów o nazwie *webjob blobtrigger-poison*.

konfiguruje się Hello maksymalnej liczby ponownych prób. Witaj sam [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) ustawienie służy do obsługi skażone obiektów blob i kolejki skażone komunikat — Obsługa.

komunikat z kolejki Hello skażone obiektów blob jest obiekt JSON, który zawiera hello następujące właściwości:

* FunctionId (w formacie hello *{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*, na przykład: WebJob1.Functions.CopyBlob)
* BlobType ("BlockBlob" lub "PageBlob")
* Właściwość ContainerName
* Element BlobName
* Element ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")

W następujących hello kodu próbki hello **CopyBlob** funkcja ma kod powodujący toofail za każdym razem, gdy jest ona wywoływana. Po hello zestaw SDK wymaga on hello maksymalnej liczby ponownych prób, wiadomość jest tworzona na powitania skażone blob kolejki, a ten komunikat jest przetwarzany przez hello **LogPoisonBlob** funkcji.

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

Witaj SDK automatycznie deserializuje wiadomości powitania JSON. Oto hello **PoisonBlobMessage** klasy:

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a>Algorytm sondowania obiektów blob
Witaj zestaw SDK zadań Webjob skanuje wszystkie kontenery określony przez **BlobTrigger** atrybuty podczas uruchamiania aplikacji. Na koncie magazynu dużych ten tryb skanowania może zająć trochę czasu, dlatego może być trochę czasu, zanim znajdują się nowe obiekty BLOB i **BlobTrigger** funkcje są wykonywane.

rejestruje powitalne SDK okresowo odczytuje z magazynu obiektów blob hello toodetect nowych lub zmienionych obiektów blob w po uruchomieniu aplikacji. Witaj dzienniki obiektów blob są buforowane i tylko fizycznie zapisane co 10 minut lub tak, więc mogą występować znaczne opóźnienia po obiektu blob jest tworzony lub aktualizowany przed hello odpowiadającego **BlobTrigger** wykonuje funkcji.

Brak wyjątek dla obiektów blob, które są tworzone przy użyciu hello **obiektu Blob** atrybutu. Gdy hello zestaw SDK zadań Webjob tworzy nowy obiekt blob, natychmiast przekazaniem nowego obiektu blob hello dopasowania tooany **BlobTrigger** funkcji. W związku z tym jeśli łańcuch blob wejściach i wyjściach, hello SDK może je przetwarzać wydajnie. Ale jeśli chcesz małych opóźnieniach uruchomiona z obiektu blob funkcji przetwarzania dla obiektów blob, które są tworzone lub zaktualizowany w inny sposób, firma Microsoft zaleca używanie **QueueTrigger** zamiast **BlobTrigger**.

### <a name="blob-receipts"></a>Potwierdzenia obiektów blob
zestaw SDK zadań Webjob Hello, sprawdza nie **BlobTrigger** funkcja jest wywoływana więcej niż raz dla hello sam nowe lub zaktualizowane obiektu blob. Dzieje się tak dzięki utrzymywaniu *obiektu blob potwierdzenia* w kolejności toodetermine wersji danego obiektu blob został przetworzony.

Potwierdzenia obiektów blob są przechowywane w kontenerze o nazwie *azure webjobs hostów* na koncie magazynu Azure hello określona przez ciąg połączenia AzureWebJobsStorage hello. Potwierdzenie obiektu blob ma hello następujących informacji:

* Funkcja, która została wywołana dla obiektu blob hello Hello ("*{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*", na przykład:"WebJob1.Functions.CopyBlob")
* Nazwa kontenera Hello
* Typ obiektu blob Hello ("BlockBlob" lub "PageBlob")
* Nazwa obiektu blob Hello
* Witaj ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")

Jeśli chcesz tooforce ponowne przetworzenie obiektu blob, można ręcznie usunąć hello potwierdzenia obiektu blob dla tego obiektu blob z hello *azure webjobs hostów* kontenera.

## <a name="related-topics-covered-by-hello-queues-article"></a>Tematy pokrewne objętych hello kolejek artykułu
Informacje dotyczące sposobu przetwarzania obiektu blob toohandle wyzwalane komunikatu w kolejce, lub dla zadań Webjob scenariusze zestawu SDK nie określonych tooblob przetwarzania, zobacz [jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).

Tematy pokrewne omówione w tym artykule Uwzględnij hello następujące elementy:

* Funkcje asynchroniczne
* Wiele wystąpień
* Łagodne zamykanie
* Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji
* Ustawianie parametrów połączenia SDK hello w kodzie.
* Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie
* Skonfiguruj **MaxDequeueCount** obsługi skażone obiektu blob.
* Wyzwalanie funkcji ręcznie
* Zapisywanie dzienników

## <a name="next-steps"></a>Następne kroki
W tym artykule udostępnił przykłady kodu przedstawiające jak obiekty BLOB toohandle typowe scenariusze dotyczące pracy z platformą Azure. Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasoby dokumentacji zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).

