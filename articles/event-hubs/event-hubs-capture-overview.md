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
# <a name="azure-event-hubs-capture"></a>Usługi Azure Event Hubs przechwytywania

Azure przechwytywania centra zdarzeń umożliwia przesyłanie strumieniowe danych w usłudze Event Hubs tooan hello dostarczyć tooautomatically [magazynu obiektów Blob Azure](https://azure.microsoft.com/services/storage/blobs/) lub [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) elastyczność dodane konto wybranych z hello określania przedział czasu lub rozmiarze. Konfigurowanie przechwytywania jest szybkie, nie ma żadnych toorun koszty administracyjne go i automatycznie skaluje się z usługą Event Hubs [jednostek przepływności](event-hubs-features.md#capacity). Przechwyć centra zdarzeń jest hello Najprostszym sposobem tooload strumieniowego przesyłania danych na platformie Azure i pozwala toofocus przetwarzania danych, a nie do przechwytywania danych.

Przechwytywanie centra zdarzeń umożliwia tooprocess w czasie rzeczywistym oraz na podstawie partii potoki na hello samego strumienia. Oznacza to, że można tworzyć rozwiązania, które zwiększa potrzebami wraz z upływem czasu. Czy kompilujesz systemów opartych na procesorze partii z oka kierunku przyszłego przetwarzania w czasie rzeczywistym lub ma tooadd wydajne ścieżki zimnych tooan istniejącego rozwiązania w czasie rzeczywistym, przechwytywania centra zdarzeń ułatwia pracę z strumienia danych.

## <a name="how-event-hubs-capture-works"></a>Jak działa przechwytywania centra zdarzeń

Usługa Event Hubs to czas przechowywania bufor trwałego na ruch przychodzący telemetrii, podobne tooa dziennika rozproszonej. Witaj tooscaling kluczy w usłudze Event Hubs jest hello [partycjonowanego modelu odbiorców](event-hubs-features.md#partitions). Każda partycja jest niezależna segmentu danych i jest używane niezależnie. Wraz z upływem czasu te dane wieku off na podstawie okresu przechowywania można skonfigurować hello. W związku z tym Centrum zdarzeń danego nigdy nie pobiera "zapełniony."

Przechwyć centra zdarzeń umożliwia toospecify możesz własnego konta magazynu obiektów Blob platformy Azure i kontener lub konta usługi Azure Data Lake Store, które są używane toostore hello przechwycone dane. Konta te mogą znajdować się w hello tego samego regionu jako Centrum zdarzeń lub w innym regionie, dodawanie elastyczność toohello hello funkcji przechwytywania centrów zdarzeń.

Przechwycone dane są zapisywane [Apache Avro] [ Apache Avro] format: compact, szybkie i binarnego formatu, który zawiera struktury danych sformatowanego z wbudowanego schematu. Ten format jest powszechnie używany w ekosystemie Hadoop hello, Stream Analytics i fabryki danych Azure. Więcej informacji na temat pracy z Avro jest dostępna w dalszej części tego artykułu.

### <a name="capture-windowing"></a>Przechwyć okien

Przechwyć centra zdarzeń umożliwia tooset się przechwytywanie toocontrol okna. To okno jest minimalny rozmiar i Konfiguracja czasu za pomocą "pierwszy wins zasad," oznacza, że który hello pierwszy powoduje wyzwalacza napotkano operacji przechwytywania. Jeśli masz 15 minutowych, 100 MB okna Przechwytywanie i wysłać 1 MB na sekundę, hello rozmiar okna wyzwalaczy przed hello przedział czasu. Każdej partycji przechwytuje niezależnie i zapisuje ukończone blokowego obiektu blob w czasie hello przechwytywania, o nazwie odpowiadającej hello czasu, w których hello napotkano interwał przechwytywania. Konwencja nazewnictwa magazynu Hello jest następujący:

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a>Skalowanie toothroughput jednostki

Ruch centra zdarzeń jest kontrolowany przez [jednostek przepływności](event-hubs-features.md#capacity). Pojedyncza jednostka przepływności umożliwia 1 MB na sekundę lub 1000 zdarzeń na sekundę przychodzące i dwa razy ilość wyjście. Standardowa usługa Event Hubs można skonfigurować za pomocą 1-20 jednostek przepływności i możesz kupić więcej zwiększyć limit przydziału [żądania obsługi][support request]. Użycie poza jednostek przepływności zakupionych jest ograniczony. Przechwyć centra zdarzeń kopiuje dane bezpośrednio z hello wewnętrzny magazyn usługi Event Hubs, pomijanie przydziały wyjście jednostki przepływności i zapisywanie wyjście z innych czytniki przetwarzania, takich jak analiza strumienia lub Spark.

Po skonfigurowaniu przechwytywania centra zdarzeń jest uruchamiane automatycznie po wysłaniu pierwszego wydarzenia i będzie kontynuował działanie. toomake ułatwić dla Twojej przetwarzaniu podrzędnym tooknow które działa proces hello centra zdarzeń zapisuje pustych plików, gdy nie ma żadnych danych. Ten proces zapewnia przewidywalną okresach i znaczników, który może dostarczyć procesorów partii.

## <a name="setting-up-event-hubs-capture"></a>Konfigurowanie przechwytywania centra zdarzeń

Można skonfigurować przechwytywania hello zdarzenia koncentratora czas utworzenia przy użyciu hello [portalu Azure](https://portal.azure.com), lub za pomocą szablonów usługi Azure Resource Manager. Aby uzyskać więcej informacji zobacz następujące artykuły hello:

- [Włącz przy użyciu portalu Azure hello przechwytywania centra zdarzeń](event-hubs-capture-enable-through-portal.md)
- [Tworzenie przestrzeni nazw usługi Event Hubs z Centrum zdarzeń i Włączanie rejestracji przy użyciu szablonu usługi Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a>Eksplorowanie hello przechwycone pliki i Praca z Avro

Przechwyć centra zdarzeń tworzy pliki format Avro określoną na powitania skonfigurowane przedział czasu. Pliki te można wyświetlać takie jak dowolnego narzędzia [Eksploratora usługi Storage Azure][Azure Storage Explorer]. Możesz pobrać hello lokalnie pliki toowork na nich.

pliki Hello utworzonej przez funkcję przechwytywania centra zdarzeń mają następujące schemacie Avro hello:

![][3]

Pliki Avro tooexplore łatwy sposób polega na użyciu hello [narzędzia Avro] [ Avro Tools] jar z Apache. Po pobraniu tego jar, można wyświetlić hello schemat określonego pliku Avro, uruchamiając następujące polecenie hello:

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

To polecenie zwraca

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

Można również używać narzędzia Avro tooconvert hello pliku w formacie tooJSON i wykonywać inne przetwarzania.

tooperform bardziej zaawansowane przetwarzania, Pobierz i zainstaluj Avro dla wybór platformy. W chwili hello pisania tego dokumentu, są dostępne dla C, C++, C implementacje\#, Java, NodeJS, Perl, PHP, Python i Ruby.

Apache Avro ma pełne wprowadzenie przewodniki dotyczące [Java] [ Java] i [Python][Python]. Można również znaleźć hello [wprowadzenie do przechwytywania centra zdarzeń](event-hubs-capture-python.md) artykułu.

## <a name="how-event-hubs-capture-is-charged"></a>Jak jest rozliczana przechwytywania centra zdarzeń

Przechwyć centra zdarzeń taryfowych podobnie jednostki toothroughput: jako dodatkowy co godzinę. Opłata Hello jest wprost proporcjonalny toohello liczbę jednostek przepływności zakupionych dla przestrzeni nazw hello. Jednostki przepływności są zwiększyć i zmniejszyć, przechwytywania centra zdarzeń liczników zwiększyć i zmniejszyć tooprovide dopasowywania wydajności. liczniki Hello wystąpić w połączeniu. Aby uzyskać szczegółowe informacje o cenach, zobacz [cennik usługi Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/). 

## <a name="next-steps"></a>Następne kroki

Przechwyć centra zdarzeń to hello Najprostszym sposobem tooget danych na platformie Azure. Za pomocą usługi Azure Data Lake, fabryki danych Azure i usłudze Azure HDInsight, można wykonać przetwarzania wsadowego i innych analytics przy użyciu znanych narzędzi i platform wybrane, w dowolnej skali należy.

Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Rozpoczynanie pracy wysyłanie i odbieranie zdarzeń](event-hubs-dotnet-framework-getstarted-send.md)
* Kompletna [przykładowa aplikacja korzystająca z usługi Event Hubs][sample application that uses Event Hubs]
* [Przegląd usługi Event Hubs][Event Hubs overview]

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
