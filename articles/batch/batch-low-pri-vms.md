---
title: "Uruchom partii zadań Azure obciążeń na ekonomicznego niskiego priorytetu maszyny wirtualne (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie obsługi administracyjnej maszyn wirtualnych niskiego priorytetu będzie zmniejszenie kosztów obciążeń partii zadań Azure."
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
ms.openlocfilehash: 9bf0ac322020d8a8453011c3207c1930175db6d3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a>Niskiego priorytetu maszyn wirtualnych za pomocą partii (wersja zapoznawcza)

Partia zadań Azure oferuje małej priorty maszyn wirtualnych (VM) będzie zmniejszenie kosztów obciążeń partii. Maszyny wirtualne o niskim priorytecie umożliwiają nowe typy obciążeń partii, zapewniając dużo mocy obliczeniowej, który jest również ekonomiczny.

Maszyny wirtualne niskiego priorytetu korzystać z nadwyżki zdolności produkcyjnych na platformie Azure. Po określeniu niskiego priorytetu maszyny wirtualne w Twojej puli partii zadań Azure automatycznie można użyć tego nadwyżka, jeśli jest dostępna.

Rozwiązanie dla przy użyciu maszyn wirtualnych o niskim priorytecie jest, że tych maszyn wirtualnych może być wywłaszczony gdy nie zdolności nadwyżki nie jest dostępny w systemie Azure. Z tego powodu niskiego priorytetu maszyny wirtualne są najbardziej odpowiednie dla pewnych typów obciążeń. Użyj maszyn wirtualnych niskiego priorytetu partii i przetwarzania asynchronicznego obciążeń, których czas ukończenia zadania są elastyczne i praca będzie rozmieszczona na wiele maszyn wirtualnych.

Maszyny wirtualne o niskim priorytecie są znacznie tańszy niż dedykowanych maszyn wirtualnych. Aby uzyskać szczegółowe informacje o cenach, zobacz [cennik partii](https://azure.microsoft.com/pricing/details/batch/).

Dodatkowe omówienie niskiego priorytetu maszyn wirtualnych, można znaleźć w sekcji powiadomienia post blogu: [partii obliczeniowych w ułamku ceny](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).

> [!IMPORTANT]
> Maszyny wirtualne o niskim priorytecie są obecnie w wersji zapoznawczej i są dostępne tylko dla obciążeń działających w partii. 
>
>

## <a name="use-cases-for-low-priority-vms"></a>Przypadki użycia dla maszyn wirtualnych o niskim priorytecie

Podane właściwości niskiego priorytetu maszyny wirtualne, jakie obciążenia może i nie można ich używać? Ogólnie rzecz biorąc obciążeń przetwarzania wsadowego są świetnie sprawdza się, ponieważ zadania są podzielone na wiele zadań równoległych lub ma wiele zadań, które skalowana w poziomie i rozproszone na wielu maszyn wirtualnych.

-   Aby zapewnić maksymalne użycie nadwyżki pojemności na platformie Azure, odpowiedniego zadania można skalować w poziomie.

-   Czasami maszyny wirtualne mogą być niedostępne lub będzie być wywłaszczony, co spowoduje zmniejszenie wydajności dla zadań i może prowadzić do przerwania zadań i powtórki. W związku z tym należy elastycznych w czasie, które można wykonać, aby uruchomić zadania.

-   Zadania z zadaniami dłużej może to mieć wpływ na więcej przerwania. Jeśli długotrwałych zadań implementować tworzenie punktów kontrolnych do zapisania postępu, ponieważ są one wykonywane, następnie wpływ przerwania byłby znacznie mniej. Zadania związane z krótszy czas wykonywania zazwyczaj najlepiej z maszynami wirtualnymi niskiego priorytetu wpływ przerwania jest znacznie mniej.

-   Długotrwałych zadań MPI, które korzystają z wieloma maszynami wirtualnymi nie są dobrze nadają się do użycia niskiego priorytetu maszyny wirtualne zgodnie z jedną wywłaszczone maszyny Wirtualnej prawdopodobnie spowoduje całą pracę o ponowne uruchomienie.

Przykładowe przypadki użycia przetwarzania wsadowego dobrze nadaje się do użycia niskiego priorytetu maszyny wirtualne to:

-   **Projektowanie i testowanie**: W szczególności, jeśli są opracowywane na dużą skalę rozwiązania znaczne oszczędności może istnieć. Wszystkie typy testowania można korzystać, ale testów obciążenia na dużą skalę i testowania regresji są doskonałe używa.

-   **Uzupełniające pojemności na żądanie**: niskiego priorytetu maszyn wirtualnych może służyć do uzupełnienia regular dedykowanych maszyn wirtualnych — Jeśli jest dostępny, zadania można skalować i z tego powodu ukończyć przyspieszają obniżenia kosztów; nie jest dostępny, używana jest linia bazowa dedykowanych maszyn wirtualnych są dostępne.

-   **Czas wykonania zadania elastyczne**: w przypadku elastyczność w zadaniach czasu trzeba wykonać, a następnie potencjalnych porzucania pojemności może następować; z uwzględnieniem niskiego priorytetu maszyny wirtualne zadania będą często wykonywane szybsze i tańsze.

Pule partii może być skonfigurowana do używania niskiego priorytetu maszyny wirtualne na kilka sposobów, w zależności od elastyczność w czasie wykonywania zadania:

-   Maszyny wirtualne niskiego priorytetu może służyć wyłącznie w puli i partii zostanie odzyskana po prostu żadnych preempted pojemności, jeśli jest dostępna. Jest to sposób najtańszej można uruchomić zadania, które są używane tylko niskiego priorytetu maszyny wirtualne.

-   Maszyny wirtualne niskiego priorytetu może służyć w połączeniu z linii bazowej stałym dedykowanych maszyn wirtualnych. Stała liczba dedykowanych maszyn wirtualnych zapewnia, że jest zawsze niektórych wydajności, aby zachować postęp zadania.

-   Może istnieć dynamiczne mieszanego dedykowanej i niskiego priorytetu maszyn wirtualnych, tak, aby tańsze niskiego priorytetu maszyny wirtualnej wyłącznie są używane, jeśli jest dostępny, ale dedykowanych maszyn wirtualnych cenach full są skalowane w górę na żądanie, aby zachować minimalną ilość zdolności do prowadzenia postęp zadania.

## <a name="batch-support-for-low-priority-vms"></a>Obsługa partii dla maszyn wirtualnych o niskim priorytecie

Partia zadań Azure oferuje kilka możliwości, które ułatwiają korzystanie i korzystają z maszyn wirtualnych o niskim priorytecie:

-   Pule partii może zawierać zarówno dedykowanych maszyn wirtualnych, jak i niskiego priorytetu maszyn wirtualnych. Podczas tworzenia puli lub zmienić w dowolnym momencie dla istniejącej puli, przy użyciu operacji zmiany rozmiaru jawne lub automatyczne skalowanie można określić liczbę każdego typu maszyny wirtualnej. Przesyłanie zadań i zadań może pozostać bez zmian i nie trzeba zajmować się typy maszyn wirtualnych w puli. Istnieje również możliwość dostępna pula całkowicie używają maszyn wirtualnych niskiego priorytetu uruchomienie zadania jako tanio, jak to możliwe, ale pokrętła zapasowej dedykowanych maszyn wirtualnych, jeśli pojemność spadnie poniżej minimalnej, aby zachować zadania uruchomione.

-   Pule partii automatycznie przejść do docelowej liczby maszyn wirtualnych o niskim priorytecie. Jeśli maszyny wirtualne są zastępowane, partii będzie podejmować próby Zastąp utracone pojemności i zwracany do obiektu docelowego.

-   W przypadku zadania zostanie przerwane wykryje partii i automatycznie requeue zadań, aby ponownie uruchomić.

-   Maszyny wirtualne niskiego priorytetu ma limit przydziału rdzeni, która różni się od dedykowanych maszyn wirtualnych. 
    Oferta dla maszyn wirtualnych niskiego priorytetu jest wyższy niż dedykowanych maszyn wirtualnych, ponieważ koszt niskiego priorytetu maszyny wirtualne. Zobacz [partii usługi przydziały i limity](batch-quota-limit.md#resource-quotas) Aby uzyskać więcej informacji.    

> [!NOTE]
> Niskiego priorytetu maszyny wirtualne nie są obsługiwane dla konta usługi partia zadań, w których ustawiono tryb alokacji puli [subskrypcji użytkownika](batch-account-create-portal.md#user-subscription-mode).
>
>

## <a name="create-and-update-pools"></a>Tworzenie i aktualizowanie pul

Pula usługi partia zadań może zawierać dedykowanych i niskiego priorytetu maszyny wirtualne (zwaną także jako węzły obliczeniowe). Można ustawić docelowy liczba węzłów obliczeniowych dla dedykowanych i niskiego priorytetu maszyn wirtualnych. Docelowy liczba węzłów określa liczbę maszyn wirtualnych mają w puli.

Na przykład aby utworzyć pulę przy użyciu usługi w chmurze Azure maszyn wirtualnych z elementem docelowym 5 dedykowanych maszyn wirtualnych i 20 niskiego priorytetu maszyn wirtualnych:

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

Aby utworzyć pulę przy użyciu maszyn wirtualnych platformy Azure (w tym przypadku maszyn wirtualnych systemu Linux) z docelowym 5 dedykowanych maszyn wirtualnych i 20 niskiego priorytetu maszyn wirtualnych:

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

Bieżąca liczba węzłów można uzyskać dedykowane i niskiego priorytetu maszyn wirtualnych:

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

Węzły puli mają właściwości, aby wskazać, czy węzeł jest dedykowanej lub niskiego priorytetu maszyny Wirtualnej:

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

Co najmniej jeden węzeł w puli są zastępowane, operację listy węzłów w puli nadal będzie zwracać tych węzłów, bieżąca liczba węzłów niskiego priorytetu pozostaną niezmienione, ale te węzły będą mieć stanu ustawioną **przeniesione** Stan. Partii spróbuje znaleźć zastąpienia maszyn wirtualnych, a w razie powodzenia węzłów będzie przejście przez **tworzenie** , a następnie **uruchamianie** stanów, zanim staną się dostępne do wykonania zadania, podobnie jak nowe węzły.

## <a name="scale-a-pool-containing-low-priority-vms"></a>Skalowanie pulę zawierającą maszyn wirtualnych o niskim priorytecie

Podobnie jak w przypadku pul wyłącznie składające się z dedykowanych maszyn wirtualnych, jest możliwość skalowania zawierających maszyny wirtualne o niskim priorytecie przez wywołanie metody zmiany rozmiaru lub przy użyciu automatycznego skalowania puli.

Drugi parametr opcjonalny, który aktualizuje wartość przyjmuje operacji zmiany rozmiaru puli **targetLowPriorityNodes**:

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

Formuła automatycznego skalowania puli obsługuje niskiego priorytetu maszyn wirtualnych w następujący sposób:

-   Można pobrać lub ustawić wartość zmiennej zdefiniowanej przez usługę **$TargetLowPriorityNodes**.

-   Można uzyskać wartości zmiennej zdefiniowanej przez usługę **$CurrentLowPriorityNodes**.

-   Można uzyskać wartości zmiennej zdefiniowanej przez usługę **$PreemptedNodeCount**. 
    Ta zmienna zwraca liczbę węzłów w stanie preempted i umożliwia skalowanie w górę lub w dół Liczba dedykowanych węzłów, w zależności od liczby węzłów wywłaszczone, które są niedostępne.

## <a name="jobs-and-tasks"></a>Zadań i zadań

Zadań i zadań wymaga bardzo małego obsługi węzłów niskiego priorytetu; obsługiwane jest tylko wygląda następująco:

-   Właściwość JobManagerTask zadania ma nową właściwość **AllowLowPriorityNode**. 
    Jeśli ta właściwość ma wartość true, można zaplanować zadanie Menedżer zadania w węźle dedykowanej lub niskim priorytecie. Jeśli ta właściwość ma wartość false, do dedykowanych węzła tylko zostanie zaplanowane zadanie Menedżer zadania.

-   [Zmiennej środowiskowej](batch-compute-node-environment-variables.md) jest dostępna w aplikacji zadań, dzięki czemu można określić, czy jest uruchomiona w węźle niskiego priorytetu lub dedykowanych. Zmienna środowiskowa jest AZ_BATCH_NODE_IS_DEDICATED.

## <a name="handling-preemption"></a>Obsługa wywłaszczania

Maszyny wirtualne od czasu do czasu może być wywłaszczony; w takim przypadku partii wykonuje następujące czynności:

-   Preempted maszyny wirtualne mają ich stan aktualizacji do **przeniesione**.
-   Jeśli zadania zostały uruchomione na maszynach wirtualnych węzła wywłaszczone, te zadania są umieszczony w kolejce i uruchom ponownie.
-   Maszyna wirtualna skutecznie zostanie usunięty, co może prowadzić do wszystkich danych przechowywanych lokalnie na utratę maszyny Wirtualnej.
-   Pula stale próbuje nawiązać połączenie docelowej liczba dostępnych węzłów niskiego priorytetu. Po znalezieniu pojemności zastępczy Zachowaj ich identyfikatory węzłów, ale są ponownie inicjowane, pośrednictwa **tworzenie** i **uruchamianie** stwierdza, zanim staną się dostępne do planowania zadań.
-   Wywłaszczanie liczniki są dostępne jako metrykę w portalu Azure.

## <a name="metrics"></a>Metryki

Dostępne są nowe metryki [portalu Azure](https://portal.azure.com) dla węzłów o niskim priorytecie. Te metryki są:

- Liczba węzłów o niskim priorytecie
- Liczby rdzeni o niskim priorytecie 
- Wywłaszczone liczba węzłów

Aby wyświetlić metryki w portalu Azure:

1. Przejdź do konta partii zadań w portalu i wyświetlenia ustawień konta usługi partia zadań.
2. Wybierz **metryki** z **monitorowanie** sekcji.
3. Wybrać metryki chcesz z **dostępne metryki** listy.

![Metryki dla węzłów o niskim priorytecie](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a>Następne kroki

* Przeczytaj artykuł [Batch feature overview for developers](batch-api-basics.md) (Omówienie funkcji usługi Batch dla deweloperów) zawierający informacje kluczowe dla wszystkich osób przygotowujących się do korzystania z usługi Batch. Ten artykuł zawiera bardziej szczegółowe informacje o zasobach usługi Batch, takich jak pule, węzły i zadania oraz wielu funkcjach API, których można używać podczas kompilowania aplikacji usługi Batch.
* Dowiedz się więcej o [interfejsach API i narzędziach usługi Batch](batch-apis-tools.md) umożliwiających tworzenie rozwiązań usługi Batch.
