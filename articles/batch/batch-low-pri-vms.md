---
title: "aaaRun partii zadań Azure obciążenie ekonomicznego niskiego priorytetu maszyny wirtualne (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprovision niskiego priorytetu maszyny wirtualne tooreduce hello koszt obciążeń partii zadań Azure."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a>Niskiego priorytetu maszyn wirtualnych za pomocą partii (wersja zapoznawcza)

Partia zadań Azure oferuje małej priorty maszynach wirtualnych (VM) tooreduce hello koszt obciążeń partii. Maszyny wirtualne o niskim priorytecie umożliwiają nowe typy obciążeń partii, zapewniając dużo mocy obliczeniowej, który jest również ekonomiczny.

Maszyny wirtualne niskiego priorytetu korzystać z nadwyżki zdolności produkcyjnych na platformie Azure. Po określeniu niskiego priorytetu maszyny wirtualne w Twojej puli partii zadań Azure automatycznie można użyć tego nadwyżka, jeśli jest dostępna.

Hello rozwiązanie dla przy użyciu maszyn wirtualnych o niskim priorytecie jest, że tych maszyn wirtualnych może być wywłaszczony gdy nie zdolności nadwyżki nie jest dostępny w systemie Azure. Z tego powodu niskiego priorytetu maszyny wirtualne są najbardziej odpowiednie dla pewnych typów obciążeń. Użyj maszyn wirtualnych niskiego priorytetu partii i przetwarzania asynchronicznego obciążeń, których czas ukończenia zadania hello jest elastyczny i pracy hello jest rozmieszczona na wiele maszyn wirtualnych.

Maszyny wirtualne o niskim priorytecie są znacznie tańszy niż dedykowanych maszyn wirtualnych. Aby uzyskać szczegółowe informacje o cenach, zobacz [cennik partii](https://azure.microsoft.com/pricing/details/batch/).

Dodatkowe omówienie niskiego priorytetu maszyn wirtualnych, można znaleźć w sekcji anons blogu hello: [partii obliczeniowych w ułamku cen hello](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).

> [!IMPORTANT]
> Maszyny wirtualne o niskim priorytecie są obecnie w wersji zapoznawczej i są dostępne tylko dla obciążeń działających w partii. 
>
>

## <a name="use-cases-for-low-priority-vms"></a>Przypadki użycia dla maszyn wirtualnych o niskim priorytecie

Biorąc pod uwagę charakterystykę hello niskiego priorytetu maszyn wirtualnych, jakie obciążenia może i nie można ich używać? Ogólnie rzecz biorąc obciążeń przetwarzania wsadowego są świetnie sprawdza się, ponieważ zadania są podzielone na wiele zadań równoległych lub ma wiele zadań, które skalowana w poziomie i rozproszone na wielu maszyn wirtualnych.

-   Użycie toomaximize nadwyżki zdolności produkcyjnych Azure, odpowiednich zadań można skalować w poziomie.

-   Czasami maszyny wirtualne mogą być niedostępne lub będzie być wywłaszczony, co spowoduje zmniejszenie wydajności dla zadań i może spowodować przerwanie tootask i powtórki. Zadania w związku z tym muszą być elastyczne w czasie hello, które podejmują toorun.

-   Zadania z zadaniami dłużej może to mieć wpływ na więcej przerwania. Jeśli długotrwałych zadań implementować postępu toosave punkty kontrolne, ponieważ są one wykonywane, następnie wpływ przerwania byłby znacznie mniej. Zadania związane z krótszy czas wykonywania zwykle toowork najlepiej z maszynami wirtualnymi niskiego priorytetu wpływ hello przerwania jest znacznie mniej.

-   Długotrwałych zadań MPI, które korzystają z wieloma maszynami wirtualnymi nie są dobrze nadają się toouse maszyn wirtualnych niskiego priorytetu jako jedna maszyna wirtualna, które są zastępowane będzie prawdopodobnie realizacji toohello całą pracę o toobe, uruchom ponownie.

Przykłady przetwarzania wsadowego Użyj przypadków toouse dobrze nadają się niskiego priorytetu maszyny wirtualne są:

-   **Projektowanie i testowanie**: W szczególności, jeśli są opracowywane na dużą skalę rozwiązania znaczne oszczędności może istnieć. Wszystkie typy testowania można korzystać, ale testów obciążenia na dużą skalę i testowania regresji są doskonałe używa.

-   **Uzupełniające pojemności na żądanie**: niskiego priorytetu maszyn wirtualnych może służyć do uzupełnienia regular dedykowanych maszyn wirtualnych — Jeśli jest dostępny, zadania można skalować i z tego powodu ukończyć przyspieszają obniżenia kosztów; nie jest dostępny, hello linii bazowej dedykowanych maszyn wirtualnych są dostępne.

-   **Czas wykonania zadania elastyczne**: Jeśli elastyczność w zadaniach czasu hello mieć toocomplete, a następnie potencjalnych porzucania pojemności może następować; jednak z hello dodawania zadań maszyn wirtualnych niskiego priorytetu będzie często działają szybciej i obniżenia kosztów.

Pule partii można toouse skonfigurowany czas wykonania zadania maszyn wirtualnych niskiego priorytetu na kilka sposobów, w zależności od elastyczność hello:

-   Maszyny wirtualne niskiego priorytetu może służyć wyłącznie w puli i partii zostanie odzyskana po prostu żadnych preempted pojemności, jeśli jest dostępna. Jest to hello najtańszej sposób tooexecute zadania, ponieważ są używane tylko niskiego priorytetu maszyn wirtualnych.

-   Maszyny wirtualne niskiego priorytetu może służyć w połączeniu z linii bazowej stałym dedykowanych maszyn wirtualnych. Witaj stała liczba dedykowanych maszyn wirtualnych zapewnia, że istnieje zawsze niektórych tookeep pojemności postęp zadania.

-   Może istnieć dynamiczne mieszanego dedykowanej i niskiego priorytetu maszyn wirtualnych, dzięki czemu tańsze VMs niskiego priorytetu wyłącznie są używane, jeśli jest dostępny, ale hello cenach pełnej dedykowanych maszyn wirtualnych są skalowane w górę na żądanie, tookeep minimalna ilość zadania hello tookeep dostępna pojemność postęp.

## <a name="batch-support-for-low-priority-vms"></a>Obsługa partii dla maszyn wirtualnych o niskim priorytecie

Partia zadań Azure oferuje kilka możliwości była tooconsume łatwe, które korzystają z maszyn wirtualnych o niskim priorytecie:

-   Pule partii może zawierać zarówno dedykowanych maszyn wirtualnych, jak i niskiego priorytetu maszyn wirtualnych. Liczba Hello każdego typu maszyny Wirtualnej można określić podczas tworzenia puli lub zmienić w dowolnym momencie dla istniejącej puli, przy użyciu operacji zmiany rozmiaru jawne hello lub automatyczne skalowanie. Przesyłanie zadań i zadań może pozostać bez zmian i nie trzeba zajmować się hello typach maszyn wirtualnych w puli hello. Możliwe jest również możliwe toohave puli całkowicie Użyj niskiego priorytetu maszyny wirtualne toorun zadania jako tanio, jak to możliwe, ale pokrętła zapasowej dedykowanych maszyn wirtualnych Jeśli pojemność hello spadnie poniżej minimalnej, aby zachować zadania uruchomione.

-   Pule partii automatycznie wyszukiwać toohello docelowej liczby maszyn wirtualnych o niskim priorytecie. Jeśli maszyny wirtualne są zastępowane, partii podejmie hello tooreplace utraty pojemności i zwracany toohello docelowej.

-   W przypadku hello zadania zostanie przerwane partii wykryje i automatycznie requeue toobe zadania, uruchom ponownie.

-   Maszyny wirtualne niskiego priorytetu ma limit przydziału rdzeni, która różni się od dedykowanych maszyn wirtualnych. 
    Hello cudzysłowu dla maszyn wirtualnych niskiego priorytetu jest wyższy niż dedykowanych maszyn wirtualnych, ponieważ koszt niskiego priorytetu maszyn wirtualnych. Zobacz [partii usługi przydziały i limity](batch-quota-limit.md#resource-quotas) Aby uzyskać więcej informacji.    

> [!NOTE]
> Niskiego priorytetu maszyny wirtualne nie są obsługiwane dla konta usługi partia zadań, w którym tryb alokacji puli hello ustawiono zbyt[subskrypcji użytkownika](batch-account-create-portal.md#user-subscription-mode).
>
>

## <a name="create-and-update-pools"></a>Tworzenie i aktualizowanie pul

Pula usługi partia zadań może zawierać dedykowanych i niskiego priorytetu maszyny wirtualne (również określonego tooas węzły obliczeniowe). Można ustawić hello docelowej liczby węzłów obliczeniowych dedykowanych i niskiego priorytetu maszyn wirtualnych. Hello docelowej liczby węzłów Określa numer hello maszyn wirtualnych ma toohave hello puli.

Na przykład toocreate puli przy użyciu usługi w chmurze Azure maszyn wirtualnych z elementem docelowym 5 dedykowanych maszyn wirtualnych i 20 niskiego priorytetu maszyn wirtualnych:

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

maszyny wirtualne i 20 niskiego priorytetu maszyny wirtualne w wersji dedykowanej toocreate puli przy użyciu maszyn wirtualnych platformy Azure (w tym przypadku maszyn wirtualnych systemu Linux) z docelowym 5:

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

Możesz też uzyskać hello bieżąca liczba węzłów dedykowanych i niskiego priorytetu maszyn wirtualnych:

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

Węzły puli mają tooindicate właściwości, jeśli węzeł hello jest dedykowanej lub niskiego priorytetu maszyny Wirtualnej:

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

Co najmniej jeden węzeł w puli są zastępowane, operację listy węzłów w puli nadal będzie zwracać tych węzłów hello bieżąca liczba węzłów niskiego priorytetu pozostaną niezmienione, ale te węzły będą mieć ich stan wartość toothe **przeniesione**stanu. Wsadowe podejmie zastępczy toofind maszyn wirtualnych, a w przypadku powodzenia hello węzłów będzie przejście przez **tworzenie** , a następnie **uruchamianie** stanów, zanim staną się dostępne do wykonania zadania, podobnie jak nowe węzły.

## <a name="scale-a-pool-containing-low-priority-vms"></a>Skalowanie pulę zawierającą maszyn wirtualnych o niskim priorytecie

Podobnie jak w przypadku pul wyłącznie składające się z dedykowanych maszyn wirtualnych, jest maszyn wirtualnych możliwe tooscale puli zawierającej niskim priorytecie przez wywołanie metody zmiany rozmiaru hello lub przy użyciu automatycznego skalowania.

Witaj operacji zmiany rozmiaru puli przyjmuje opcjonalny drugi parametr, który aktualizuje wartość **targetLowPriorityNodes**:

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

Formuła automatycznego skalowania puli Hello obsługuje niskiego priorytetu maszyn wirtualnych w następujący sposób:

-   Można pobrać lub ustawić hello wartość zmiennej hello zdefiniowane przez usługi **$TargetLowPriorityNodes**.

-   Można pobrać wartości hello hello zmiennej zdefiniowanej przez usługę **$CurrentLowPriorityNodes**.

-   Można pobrać wartości hello hello zmiennej zdefiniowanej przez usługę **$PreemptedNodeCount**. 
    Ta zmienna zwraca hello liczby węzłów w hello wywłaszczone stanu i umożliwia skalowanie w górę lub w dół hello Liczba dedykowanych węzłów, w zależności od hello liczba węzłów wywłaszczone, które są niedostępne.

## <a name="jobs-and-tasks"></a>Zadań i zadań

Zadań i zadań wymaga bardzo małego obsługi węzłów niskiego priorytetu; obsługiwane jest tylko Hello jest następujący:

-   Witaj JobManagerTask właściwości zadania ma nową właściwość **AllowLowPriorityNode**. 
    Jeśli ta właściwość ma wartość true, można zaplanować zadanie Menedżer zadania hello w węźle dedykowanej lub niskim priorytecie. Jeśli ta właściwość ma wartość false, hello zadania Menedżera zadań będzie zaplanowane tooa tylko dedykowane węzła.

-   [Zmiennej środowiskowej](batch-compute-node-environment-variables.md) jest tooa dostępne zadania aplikacji, dzięki czemu można określić, czy jest uruchomiona w węźle niskiego priorytetu lub dedykowanych. Zmienna środowiskowa Hello jest AZ_BATCH_NODE_IS_DEDICATED.

## <a name="handling-preemption"></a>Obsługa wywłaszczania

Maszyny wirtualne od czasu do czasu może być wywłaszczony; w takim przypadku partii hello następujące:

-   Witaj wywłaszczone maszyny wirtualne mają ich stan zaktualizowane**przeniesione**.
-   Jeśli zadania zostały uruchomione na hello przeniesiona węzła maszyn wirtualnych, te zadania są umieszczony w kolejce i uruchom ponownie.
-   Hello wirtualna skutecznie zostanie usunięty, początkowe tooany dane przechowywane lokalnie na powitania utratę maszyny Wirtualnej.
-   Pula Hello podejmuje stale tooreach hello docelowej liczby węzłów niskiego priorytetu dostępne. Po znalezieniu pojemności zastępczy Zachowaj ich identyfikatory węzłów, ale są ponownie inicjowane, pośrednictwa **tworzenie** i **uruchamianie** stwierdza, zanim staną się dostępne do planowania zadań.
-   Wywłaszczanie liczniki są dostępne jako metrykę w hello portalu Azure.

## <a name="metrics"></a>Metryki

Nowe metryki są dostępne w hello [portalu Azure](https://portal.azure.com) dla węzłów o niskim priorytecie. Te metryki są:

- Liczba węzłów o niskim priorytecie
- Liczby rdzeni o niskim priorytecie 
- Wywłaszczone liczba węzłów

metryki tooview w hello portalu Azure:

1. Przejdź tooyour konta usługi partia zadań w portalu hello i wyświetlić hello ustawień konta usługi partia zadań.
2. Wybierz **metryki** z hello **monitorowanie** sekcji.
3. Wybierz metryki hello chcesz z hello **dostępne metryki** listy.

![Metryki dla węzłów o niskim priorytecie](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a>Następne kroki

* Witaj odczytu [Przegląd funkcji partii dla deweloperów](batch-api-basics.md), ważne informacje dla każdego przygotowywanie toouse partii. Witaj artykuł zawiera bardziej szczegółowe informacje o partii usługi zasobów, takich jak pule, węzłów, zadań i zadań i hello wiele funkcji interfejsu API, które można używać podczas tworzenia aplikacji partii.
* Dowiedz się więcej o hello [narzędzia i interfejsy API partii](batch-apis-tools.md) dostępne do tworzenia rozwiązań partii.
