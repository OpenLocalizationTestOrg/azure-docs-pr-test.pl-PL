---
title: "aaaAzure partii jest uruchamiany na dużą skalę równoległych rozwiązania informatyczne w chmurze hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o korzystaniu z usługi partia zadań Azure hello równolegle na dużą skalę i obciążeń HPC"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 93e37d44-7585-495e-8491-312ed584ab79
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: acc52e46330c465f81951441d9067371098cf63a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-intrinsically-parallel-workloads-with-batch"></a>Uruchamianie wewnętrznie równoległych obciążeń przy użyciu usługi Batch

Partia zadań Azure to usługa platformy dla wydajne działanie aplikacji na dużą skalę równoległych i wysokiej wydajności obliczeniowej (HPC) w chmurze hello. Partia zadań Azure planuje toorun pracy obliczeniowych w zarządzanej kolekcji maszyn wirtualnych, a można automatycznie skali obliczeniowe zasobów toomeet hello potrzeb zadań.

Z partii zadań Azure można łatwo zdefiniować tooexecute zasobów obliczeniowych Azure aplikacji równolegle i na dużą skalę. Nie istnieje toomanually nie konieczności tworzenia, konfigurowania i zarządzania klastra HPC, poszczególnych maszyn wirtualnych, sieci wirtualnych lub złożonych zadań i zadań planowania infrastruktury. Te podzadania zostaną zautomatyzowane lub uproszczone przez usługę Azure Batch.

## <a name="use-cases-for-batch"></a>Przypadki użycia usługi Batch
Usługa Batch jest zarządzaną usługą platformy Azure, której używa się do *przetwarzania wsadowego* lub *obliczania wsadowego* — uruchamiania dużej liczby podobnych podzadań w celu uzyskania pożądanych efektów. Obliczanie wsadowe jest najczęściej używane przez organizacje, które regularnie przetwarzają, przekształcają i analizują duże ilości danych.

Z usługą Batch działają dobrze aplikacje i obciążenia wewnętrznie równoległe (zwane również „zaskakująco równoległymi”). Obciążenia wewnętrznie równoległe to takie, które można łatwo podzielić na wiele podzadań, które wykonują prace na wielu komputerach równocześnie.

![Podzadania równoległe][1]<br/>

Przykładowe obciążenia, które zwykle są przetwarzane przy użyciu tej metody:

* Modelowanie ryzyka finansowego
* Analiza danych dotycząca klimatu i hydrologii
* Renderowanie, analiza i przetwarzanie obrazu
* Kodowanie i transkodowanie multimediów
* Analiza sekwencji genetycznych
* Analiza naprężeń konstrukcji
* Testowanie oprogramowania

Partii można również wykonywać równoległe obliczenia z krokiem Zmniejsz na końcu hello i wykonanie bardziej złożonych HPC obciążeń takich jak [komunikat interfejsu (Passing Interface)](batch-mpi.md) aplikacji.

Aby porównać usługę Batch oraz inne opcje rozwiązań HPC na platformie Azure, zobacz artykuł [Rozwiązania usługi Batch i HPC](batch-hpc-solutions.md)

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="scenario-scale-out-a-parallel-workload"></a>Scenariusz: skalowanie obciążenia równoległego
Typowe rozwiązania obejmującego hello toointeract API partii z hello usługa partia zadań obejmuje skalowania leżą równoległych pracy — przykład renderowanie Witaj obrazów sceny 3W — w puli węzłów obliczeniowych. Ta pula węzły obliczeniowe może być "farmie renderowania" który udostępnia dziesiątki, setek lub tysięcy nawet rdzenia tooyour renderowania zadania, na przykład.

Hello poniższym diagramie przedstawiono typowe przepływu pracy partii, przy użyciu aplikacji klienta lub przy użyciu toorun partii równoległe obciążenie usługi hostowanej.

![Przepływ pracy rozwiązania usługi Batch][2]

W tym scenariuszu typowych aplikacji lub usługi przetwarza obliczeniową obciążenia w partii zadań Azure, wykonując następujące kroki hello:

1. Przekaż hello **pliki wejściowe** i hello **aplikacji** który przetworzy tych plików tooyour konta magazynu Azure. pliki wejściowe Hello można żadnych danych, która będzie przetwarzać aplikacji, takich jak dane finansowe modelowania lub przekodowane toobe plików wideo. pliki aplikacji Hello może być dowolna aplikacja, która jest używana do przetwarzania danych hello, takich jak renderowania 3W aplikacji lub transcoder nośnika.
2. Utwórz plik wsadowy **puli** węzłów obliczeniowych w ramach konta usługi partia zadań — te węzły są hello maszyn wirtualnych, które będą wykonywane zadania. Należy określić właściwości, takie jak hello [rozmiaru węzła](../cloud-services/cloud-services-sizes-specs.md), ich systemu operacyjnego i hello lokalizację w usłudze Azure Storage tooinstall aplikacji hello nowi węzłów hello hello puli (aplikacja hello, który został przekazany w kroku #1). Można również skonfigurować pulę hello zbyt[automatycznie skalować](batch-automatic-scaling.md) pracą toohello odpowiedzi, który generuje zadań. Automatyczne skalowanie dynamicznie dostosowuje hello liczba węzłów obliczeniowych w puli hello.
3. Utwórz plik wsadowy **zadania** toorun hello obciążenie puli hello węzłów obliczeniowych. Podczas tworzenia zadania skojarz je z pulą usługi Batch.
4. Dodaj **zadania** toohello zadania. Podczas dodawania zadań tooa zadania hello usługa partia zadań umożliwia zaplanowanie na powitania zadań do wykonania na powitania węzłów obliczeniowych w puli hello. Każde zadanie używa aplikacji hello, aby przekazać pliki wejściowe hello tooprocess.
   
   * 4a. Przed wykonaniem zadania, może pobierać dane hello (hello pliki wejściowe), które jest węzeł obliczeniowy toohello tooprocess, który jest przypisany do. Jeśli aplikacja hello nie została jeszcze zainstalowana w węźle hello (zobacz krok #2), można go pobrać tutaj zamiast tego. Po zakończeniu pobierania hello hello zadania wykonywania w ich przypisanej węzłach.
5. Uruchom zadania hello, można zbadać w partii toomonitor hello postęp hello zadania i jego zadań podrzędnych. Klient aplikacji lub usługi komunikuje się z hello usługa partia zadań za pośrednictwem protokołu HTTPS. Upewnij się, ponieważ na monitorowanie tysiące zadań uruchomionych na tysiącach węzłów obliczeniowych, zbyt[wydajnie zapytania usługi partia zadań hello](batch-efficient-list-queries.md).
6. Jak ukończyć powitalnych zadania, przekazywać ich wynik tooAzure danych magazynu. Można również pobrać pliki bezpośrednio z systemu plików hello w węźle obliczeń.
7. Gdy monitorowanie wykryje, czy zadań hello w zadania zostały wykonane, klienta aplikacji lub usługi można pobrać hello danych wyjściowych dla dalszego przetwarzania lub ewaluacji.

Należy pamiętać, jest to po prostu jednokierunkowej toouse partii, a w tym scenariuszu opisano tylko kilka funkcji dostępnych. Na przykład możesz wykonać [wielu zadań jednocześnie](batch-parallel-node-tasks.md) na każdym węźle obliczeń, a następnie można użyć [zadania działań przygotowania i kończenia zadań](batch-job-prep-release.md) tooprepare hello węzłów dla zadań, a następnie wyczyścić później.

## <a name="next-steps"></a>Następne kroki
Teraz, gdy masz ogólne omówienie hello usługa partia zadań jest bardziej toolearn toodig czas używania go tooprocess równoległych obciążeń obliczeniowych.

* Witaj odczytu [Przegląd funkcji partii dla deweloperów](batch-api-basics.md), ważne informacje dla każdego przygotowywanie toouse partii. Witaj artykuł zawiera bardziej szczegółowe informacje o partii usługi zasobów, takich jak pule, węzłów, zadań i zadań i hello wiele funkcji interfejsu API, które można używać podczas tworzenia aplikacji partii.
* Dowiedz się więcej o hello [narzędzia i interfejsy API partii](batch-apis-tools.md) dostępne do tworzenia rozwiązań partii.
* [Rozpoczynanie pracy z hello biblioteki partii zadań Azure dla platformy .NET](batch-dotnet-get-started.md) toolearn jak toouse C# i hello proste obciążenia za pomocą wspólnego przepływu pracy partii tooexecute biblioteki partiami platformy .NET. W tym artykule powinien być jednym z Twojego pierwszego zatrzymuje podczas nauki jak toouse hello usługa partia zadań. Istnieje również [wersji języka Python](batch-python-tutorial.md) hello samouczka.
* Pobierz hello [przykłady w serwisie GitHub kodu] [ github_samples] toosee jak zarówno C# i Python umożliwia łączenie z obciążeń próbki tooschedule i procesu wsadowego.
* Zapoznaj się z hello [ścieżka szkoleniowa dotycząca partii] [ learning_path] tooget pomysł tooyou hello zasoby dostępne w trakcie informacje toowork z partii.


[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/

[1]: ./media/batch-technical-overview/tech_overview_01.png
[2]: ./media/batch-technical-overview/tech_overview_02.png
