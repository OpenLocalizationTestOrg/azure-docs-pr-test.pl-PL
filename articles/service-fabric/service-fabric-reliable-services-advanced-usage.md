---
title: "Użycie aaaAdvanced niezawodne usługi | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zaawansowanych funkcji usługi sieć szkieletowa usług niezawodnej dodano elastyczność w usługach."
services: Service-Fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: masnider
ms.assetid: f2942871-863d-47c3-b14a-7cdad9a742c7
ms.service: Service-Fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: e6d6310a4deae9edcfcd76551e1337f0e39e9e5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-usage-of-hello-reliable-services-programming-model"></a>Zaawansowane użycia hello model programowania usług niezawodnej
Sieć szkieletowa usług Azure ułatwia pisanie usług oraz zarządzania nimi niezawodnej bezstanowe i stanowe. Ten przewodnik zawiera informacje o zaawansowanych użycia toogain niezawodne usługi więcej kontrolę i elastyczność za pośrednictwem usługi. Wcześniejsze tooreading tego przewodnika, zapoznaj się z [model programowania usług niezawodnej hello](service-fabric-reliable-services-introduction.md).

Zarówno stanowe i bezstanowe usługi mają dwa punkty wejścia głównej dla kodu użytkownika:

* `RunAsync(C#) / runAsync(Java)`jest punktem wejścia ogólnego przeznaczenia dla kodu usługi.
* `CreateServiceReplicaListeners(C#)`i `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` jest otwierania odbiorników komunikacji do obsługi żądań klientów.

W przypadku większości usług te punkty wejścia dwóch są wystarczające. W rzadkich przypadkach większą kontrolę nad cyklem życia usługi jest wymagane, zdarzenia cyklu życia dodatkowe są dostępne.

## <a name="stateless-service-instance-lifecycle"></a>Cykl życia wystąpienia usługi bezstanowej
Cykl życia usługi bezstanowej jest bardzo prosty. Usługi bezstanowej tylko można otworzyć, zamknięta lub zostało przerwane. `RunAsync`usługi bezstanowej jest wykonywane, gdy wystąpienie usługi jest otwarta i anulowany, gdy wystąpienie usługi jest zamknięty lub zostało przerwane.

Mimo że `RunAsync` powinny być wystarczające w niemal wszystkich przypadkach hello otwarte, zamknij i przerwania zdarzeń usługi bezstanowej są także dostępne:

* `Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java`OnOpenAsync jest wywoływana, gdy wystąpienie usługi bezstanowej hello jest o toobe używane. W tym momencie można uruchomić zadania inicjowania usługi rozszerzonej.
* `Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java`OnCloseAsync jest wywoływane, gdy wystąpienie usługi bezstanowej hello będzie toobe bezpiecznie zamykanie systemu. Może to wystąpić, gdy kod usługi hello jest uaktualniany, wystąpienie usługi hello jest przenoszony powodu tooload równoważenia lub wykrycia błędu przejściowego. OnCloseAsync może być używane toosafely Zamknij wszystkie zasoby, Zatrzymaj przetwarzanie w tle, Zakończ zapisywanie stanu zewnętrznych lub zamknięcia w istniejących połączeń.
* `void OnAbort() - C# / void onAbort() - Java`OnAbort jest wywoływane, gdy wystąpienie usługi bezstanowej hello trwa wymuszone zamykanie. Zazwyczaj jest to nazywane po wykryciu trwałego błędu w węźle hello lub sieci szkieletowej usług nie można niezawodnie zarządzania cyklem życia wystąpienie usługi hello powodu niepowodzenia toointernal.

## <a name="stateful-service-replica-lifecycle"></a>Cykl życia repliki usługi stanowej

> [!NOTE]
> Niezawodne usługi stanowej nie są obsługiwane w języku Java jeszcze.
>
>

Cykl życia repliki usługi stanowej jest znacznie bardziej skomplikowane niż wystąpienie usługi bezstanowej. Ponadto tooopen, zamknij i abort zdarzenia, repliki usługi stanowej podlega zmianom roli przez jego okres istnienia. Po zmianie roli repliki usługi stanowej hello `OnChangeRoleAsync` zdarzenie zostanie wyzwolone:

* `Task OnChangeRoleAsync(ReplicaRole, CancellationToken)`OnChangeRoleAsync jest wywoływane, gdy replika usługi stanowej hello jest zmiana roli, na przykład tooprimary lub pomocniczej. Replik podstawowych podano stanu zapisu (dozwolone są toocreate i zapisu tooReliable kolekcji). Replik pomocniczych podano stanu (tylko można odczytać z istniejących zbiorach niezawodnej). Większość pracy w usługi stanowej odbywa się hello repliki podstawowej. Replik pomocniczych można wykonać walidacji tylko do odczytu, generowanie raportów, wyszukiwania danych lub innych zadań tylko do odczytu.

W usługi stanowej tylko replika podstawowa hello ma dostęp do zapisu toostate i dlatego zazwyczaj gdy usługa hello wykonuje całą pracę. Witaj `RunAsync` metoda w usługi stanowej jest wykonywana tylko wtedy, gdy replika usługi stanowej hello jest kluczem podstawowym. Witaj `RunAsync` metody jest anulowany, gdy zmiany roli repliki podstawowej od podstawowego, a także podczas hello Zamknij i abort zdarzenia.

Przy użyciu hello `OnChangeRoleAsync` zdarzeń umożliwia tooperform pracy w zależności od roli repliki oraz jak zmiana toorole odpowiedzi.

Usługa stanowa oferuje także funkcje hello czterech tego samego zdarzenia cyklu życia jako usługę bezstanową hello tej samej semantyki i przypadki użycia:

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a>Następne kroki
Dla bardziej zaawansowanych tematów powiązanych tooService sieci szkieletowej Zobacz hello następujące artykuły:

* [Konfigurowanie stanowe niezawodne usługi](service-fabric-reliable-services-configuration.md)
* [Wprowadzenie kondycji sieci szkieletowej usług](service-fabric-health-introduction.md)
* [Korzystanie z raportów kondycji systemu do rozwiązywania problemów](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Konfigurowanie usług za pomocą hello zasobu klastra sieci szkieletowej programu Service Manager](service-fabric-cluster-resource-manager-configure-services.md)
