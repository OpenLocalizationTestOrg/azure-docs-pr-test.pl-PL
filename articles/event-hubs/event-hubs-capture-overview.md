---
title: "aaaOverview Przechwytywanie zawartości centra zdarzeń platformy Azure | Dokumentacja firmy Microsoft"
description: "Przechwytywania danych telemetrycznych z przechwytywania centra zdarzeń"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="fc6d1-103">Usługi Azure Event Hubs przechwytywania</span><span class="sxs-lookup"><span data-stu-id="fc6d1-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="fc6d1-104">Azure przechwytywania centra zdarzeń umożliwia przesyłanie strumieniowe danych w usłudze Event Hubs tooan hello dostarczyć tooautomatically [magazynu obiektów Blob Azure](https://azure.microsoft.com/services/storage/blobs/) lub [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) elastyczność dodane konto wybranych z hello określania przedział czasu lub rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-104">Azure Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooan [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with hello added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="fc6d1-105">Konfigurowanie przechwytywania jest szybkie, nie ma żadnych toorun koszty administracyjne go i automatycznie skaluje się z usługą Event Hubs [jednostek przepływności](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="fc6d1-105">Setting up Capture is fast, there are no administrative costs toorun it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="fc6d1-106">Przechwyć centra zdarzeń jest hello Najprostszym sposobem tooload strumieniowego przesyłania danych na platformie Azure i pozwala toofocus przetwarzania danych, a nie do przechwytywania danych.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-106">Event Hubs Capture is hello easiest way tooload streaming data into Azure, and enables you toofocus on data processing rather than on data capture.</span></span>

<span data-ttu-id="fc6d1-107">Przechwytywanie centra zdarzeń umożliwia tooprocess w czasie rzeczywistym oraz na podstawie partii potoki na hello samego strumienia.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-107">Event Hubs Capture enables you tooprocess real-time and batch-based pipelines on hello same stream.</span></span> <span data-ttu-id="fc6d1-108">Oznacza to, że można tworzyć rozwiązania, które zwiększa potrzebami wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="fc6d1-109">Czy kompilujesz systemów opartych na procesorze partii z oka kierunku przyszłego przetwarzania w czasie rzeczywistym lub ma tooadd wydajne ścieżki zimnych tooan istniejącego rozwiązania w czasie rzeczywistym, przechwytywania centra zdarzeń ułatwia pracę z strumienia danych.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want tooadd an efficient cold path tooan existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="fc6d1-110">Jak działa przechwytywania centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="fc6d1-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="fc6d1-111">Usługa Event Hubs to czas przechowywania bufor trwałego na ruch przychodzący telemetrii, podobne tooa dziennika rozproszonej.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar tooa distributed log.</span></span> <span data-ttu-id="fc6d1-112">Witaj tooscaling kluczy w usłudze Event Hubs jest hello [partycjonowanego modelu odbiorców](event-hubs-features.md#partitions).</span><span class="sxs-lookup"><span data-stu-id="fc6d1-112">hello key tooscaling in Event Hubs is hello [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="fc6d1-113">Każda partycja jest niezależna segmentu danych i jest używane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="fc6d1-114">Wraz z upływem czasu te dane wieku off na podstawie okresu przechowywania można skonfigurować hello.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-114">Over time this data ages off, based on hello configurable retention period.</span></span> <span data-ttu-id="fc6d1-115">W związku z tym Centrum zdarzeń danego nigdy nie pobiera "zapełniony."</span><span class="sxs-lookup"><span data-stu-id="fc6d1-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="fc6d1-116">Przechwyć centra zdarzeń umożliwia toospecify możesz własnego konta magazynu obiektów Blob platformy Azure i kontener lub konta usługi Azure Data Lake Store, które są używane toostore hello przechwycone dane.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-116">Event Hubs Capture enables you toospecify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used toostore hello captured data.</span></span> <span data-ttu-id="fc6d1-117">Konta te mogą znajdować się w hello tego samego regionu jako Centrum zdarzeń lub w innym regionie, dodawanie elastyczność toohello hello funkcji przechwytywania centrów zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-117">These accounts can be in hello same region as your event hub or in another region, adding toohello flexibility of hello Event Hubs Capture feature.</span></span>

<span data-ttu-id="fc6d1-118">Przechwycone dane są zapisywane [Apache Avro] [ Apache Avro] format: compact, szybkie i binarnego formatu, który zawiera struktury danych sformatowanego z wbudowanego schematu.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="fc6d1-119">Ten format jest powszechnie używany w ekosystemie Hadoop hello, Stream Analytics i fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-119">This format is widely used in hello Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="fc6d1-120">Więcej informacji na temat pracy z Avro jest dostępna w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="fc6d1-121">Przechwyć okien</span><span class="sxs-lookup"><span data-stu-id="fc6d1-121">Capture windowing</span></span>

<span data-ttu-id="fc6d1-122">Przechwyć centra zdarzeń umożliwia tooset się przechwytywanie toocontrol okna.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-122">Event Hubs Capture enables you tooset up a window toocontrol capturing.</span></span> <span data-ttu-id="fc6d1-123">To okno jest minimalny rozmiar i Konfiguracja czasu za pomocą "pierwszy wins zasad," oznacza, że który hello pierwszy powoduje wyzwalacza napotkano operacji przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-123">This window is a minimum size and time configuration with a "first wins policy," meaning that hello first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="fc6d1-124">Jeśli masz 15 minutowych, 100 MB okna Przechwytywanie i wysłać 1 MB na sekundę, hello rozmiar okna wyzwalaczy przed hello przedział czasu.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, hello size window triggers before hello time window.</span></span> <span data-ttu-id="fc6d1-125">Każdej partycji przechwytuje niezależnie i zapisuje ukończone blokowego obiektu blob w czasie hello przechwytywania, o nazwie odpowiadającej hello czasu, w których hello napotkano interwał przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-125">Each partition captures independently and writes a completed block blob at hello time of capture, named for hello time at which hello capture interval was encountered.</span></span> <span data-ttu-id="fc6d1-126">Konwencja nazewnictwa magazynu Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="fc6d1-126">hello storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a><span data-ttu-id="fc6d1-127">Skalowanie toothroughput jednostki</span><span class="sxs-lookup"><span data-stu-id="fc6d1-127">Scaling toothroughput units</span></span>

<span data-ttu-id="fc6d1-128">Ruch centra zdarzeń jest kontrolowany przez [jednostek przepływności](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="fc6d1-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="fc6d1-129">Pojedyncza jednostka przepływności umożliwia 1 MB na sekundę lub 1000 zdarzeń na sekundę przychodzące i dwa razy ilość wyjście.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="fc6d1-130">Standardowa usługa Event Hubs można skonfigurować za pomocą 1-20 jednostek przepływności i możesz kupić więcej zwiększyć limit przydziału [żądania obsługi][support request].</span><span class="sxs-lookup"><span data-stu-id="fc6d1-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="fc6d1-131">Użycie poza jednostek przepływności zakupionych jest ograniczony.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="fc6d1-132">Przechwyć centra zdarzeń kopiuje dane bezpośrednio z hello wewnętrzny magazyn usługi Event Hubs, pomijanie przydziały wyjście jednostki przepływności i zapisywanie wyjście z innych czytniki przetwarzania, takich jak analiza strumienia lub Spark.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-132">Event Hubs Capture copies data directly from hello internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="fc6d1-133">Po skonfigurowaniu przechwytywania centra zdarzeń jest uruchamiane automatycznie po wysłaniu pierwszego wydarzenia i będzie kontynuował działanie.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="fc6d1-134">toomake ułatwić dla Twojej przetwarzaniu podrzędnym tooknow które działa proces hello centra zdarzeń zapisuje pustych plików, gdy nie ma żadnych danych.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-134">toomake it easier for your downstream processing tooknow that hello process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="fc6d1-135">Ten proces zapewnia przewidywalną okresach i znaczników, który może dostarczyć procesorów partii.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="fc6d1-136">Konfigurowanie przechwytywania centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="fc6d1-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="fc6d1-137">Można skonfigurować przechwytywania hello zdarzenia koncentratora czas utworzenia przy użyciu hello [portalu Azure](https://portal.azure.com), lub za pomocą szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-137">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="fc6d1-138">Aby uzyskać więcej informacji zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="fc6d1-138">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="fc6d1-139">Włącz przy użyciu portalu Azure hello przechwytywania centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="fc6d1-139">Enable Event Hubs Capture using hello Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="fc6d1-140">Tworzenie przestrzeni nazw usługi Event Hubs z Centrum zdarzeń i Włączanie rejestracji przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fc6d1-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a><span data-ttu-id="fc6d1-141">Eksplorowanie hello przechwycone pliki i Praca z Avro</span><span class="sxs-lookup"><span data-stu-id="fc6d1-141">Exploring hello captured files and working with Avro</span></span>

<span data-ttu-id="fc6d1-142">Przechwyć centra zdarzeń tworzy pliki format Avro określoną na powitania skonfigurowane przedział czasu.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-142">Event Hubs Capture creates files in Avro format, as specified on hello configured time window.</span></span> <span data-ttu-id="fc6d1-143">Pliki te można wyświetlać takie jak dowolnego narzędzia [Eksploratora usługi Storage Azure][Azure Storage Explorer].</span><span class="sxs-lookup"><span data-stu-id="fc6d1-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="fc6d1-144">Możesz pobrać hello lokalnie pliki toowork na nich.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-144">You can download hello files locally toowork on them.</span></span>

<span data-ttu-id="fc6d1-145">pliki Hello utworzonej przez funkcję przechwytywania centra zdarzeń mają następujące schemacie Avro hello:</span><span class="sxs-lookup"><span data-stu-id="fc6d1-145">hello files produced by Event Hubs Capture have hello following Avro schema:</span></span>

![][3]

<span data-ttu-id="fc6d1-146">Pliki Avro tooexplore łatwy sposób polega na użyciu hello [narzędzia Avro] [ Avro Tools] jar z Apache.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-146">An easy way tooexplore Avro files is by using hello [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="fc6d1-147">Po pobraniu tego jar, można wyświetlić hello schemat określonego pliku Avro, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="fc6d1-147">After downloading this jar, you can see hello schema of a specific Avro file by running hello following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="fc6d1-148">To polecenie zwraca</span><span class="sxs-lookup"><span data-stu-id="fc6d1-148">This command returns</span></span>

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

<span data-ttu-id="fc6d1-149">Można również używać narzędzia Avro tooconvert hello pliku w formacie tooJSON i wykonywać inne przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-149">You can also use Avro Tools tooconvert hello file tooJSON format and perform other processing.</span></span>

<span data-ttu-id="fc6d1-150">tooperform bardziej zaawansowane przetwarzania, Pobierz i zainstaluj Avro dla wybór platformy.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-150">tooperform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="fc6d1-151">W chwili hello pisania tego dokumentu, są dostępne dla C, C++, C implementacje\#, Java, NodeJS, Perl, PHP, Python i Ruby.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-151">At hello time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="fc6d1-152">Apache Avro ma pełne wprowadzenie przewodniki dotyczące [Java] [ Java] i [Python][Python].</span><span class="sxs-lookup"><span data-stu-id="fc6d1-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="fc6d1-153">Można również znaleźć hello [wprowadzenie do przechwytywania centra zdarzeń](event-hubs-capture-python.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-153">You can also read hello [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="fc6d1-154">Jak jest rozliczana przechwytywania centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="fc6d1-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="fc6d1-155">Przechwyć centra zdarzeń taryfowych podobnie jednostki toothroughput: jako dodatkowy co godzinę.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-155">Event Hubs Capture is metered similarly toothroughput units: as an hourly charge.</span></span> <span data-ttu-id="fc6d1-156">Opłata Hello jest wprost proporcjonalny toohello liczbę jednostek przepływności zakupionych dla przestrzeni nazw hello.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-156">hello charge is directly proportional toohello number of throughput units purchased for hello namespace.</span></span> <span data-ttu-id="fc6d1-157">Jednostki przepływności są zwiększyć i zmniejszyć, przechwytywania centra zdarzeń liczników zwiększyć i zmniejszyć tooprovide dopasowywania wydajności.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease tooprovide matching performance.</span></span> <span data-ttu-id="fc6d1-158">liczniki Hello wystąpić w połączeniu.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-158">hello meters occur in tandem.</span></span> <span data-ttu-id="fc6d1-159">Aby uzyskać szczegółowe informacje o cenach, zobacz [cennik usługi Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="fc6d1-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fc6d1-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fc6d1-160">Next steps</span></span>

<span data-ttu-id="fc6d1-161">Przechwyć centra zdarzeń to hello Najprostszym sposobem tooget danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-161">Event Hubs Capture is hello easiest way tooget data into Azure.</span></span> <span data-ttu-id="fc6d1-162">Za pomocą usługi Azure Data Lake, fabryki danych Azure i usłudze Azure HDInsight, można wykonać przetwarzania wsadowego i innych analytics przy użyciu znanych narzędzi i platform wybrane, w dowolnej skali należy.</span><span class="sxs-lookup"><span data-stu-id="fc6d1-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="fc6d1-163">Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="fc6d1-163">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="fc6d1-164">Rozpoczynanie pracy wysyłanie i odbieranie zdarzeń</span><span class="sxs-lookup"><span data-stu-id="fc6d1-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="fc6d1-165">Kompletna [przykładowa aplikacja korzystająca z usługi Event Hubs][sample application that uses Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="fc6d1-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="fc6d1-166">[Przegląd usługi Event Hubs][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="fc6d1-166">[Event Hubs overview][Event Hubs overview]</span></span>

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
