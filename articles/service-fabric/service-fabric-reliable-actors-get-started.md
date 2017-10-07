---
title: "aaaCreate Twojego pierwszego na podstawie aktora Azure mikrousługi w języku C# | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki tworzenia, debugowania i wdrażania prostego usługi aktora na podstawie przy użyciu usługi sieci szkieletowej Reliable Actors hello."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>Wprowadzenie do korzystania z Reliable Actors
> [!div class="op_single_selector"]
> * [C# w systemie Windows](service-fabric-reliable-actors-get-started.md)
> * [Java w systemie Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

W tym artykule opisano podstawy hello Azure Service Fabric Reliable Actors oraz przeprowadzi Cię przez proces tworzenia, debugowania i wdrażanie prostej aplikacji niezawodnego aktora w programie Visual Studio.

## <a name="installation-and-setup"></a>Instalacja i Konfiguracja
Przed rozpoczęciem upewnij się, że masz środowisko projektowania sieci szkieletowej usług hello na tym komputerze.
Jeśli potrzebujesz tooset go, zobaczyć szczegółowe instrukcje dotyczące [jak tooset się środowisko projektowe hello](service-fabric-get-started.md).

## <a name="basic-concepts"></a>Podstawowe pojęcia
wprowadzenie Reliable Actors, możesz tylko tooget należy toounderstand kilka podstawowych pojęć:

* **Usługa aktora**. Reliable Actors są popakowane w niezawodnej usługi, które można wdrożyć w infrastrukturze sieci szkieletowej usług hello. Wystąpienia aktora zostaną aktywowane w wystąpieniu usługi o nazwie.
* **Rejestracja aktora**. Jako z usługami Reliable Services, usługi niezawodnego aktora musi toobe zarejestrowane ze środowiskiem uruchomieniowym usługi sieć szkieletowa hello. Ponadto typ aktora hello musi toobe zarejestrowany hello aktora w czasie wykonywania.
* **Interfejs aktora**. Interfejs aktora Hello jest używany toodefine jednoznacznie interfejs publiczny aktora. W terminologii modelu niezawodnego aktora hello hello aktora interfejs definiuje hello typów komunikatów, które hello aktora można zrozumieć i przetworzyć. Interfejs aktora Hello jest używany przez innych uczestników i aplikacje klienckie zbyt "Wyślij" (asynchronicznie) aktora toohello wiadomości. Reliable Actors można zaimplementować wiele interfejsów.
* **Klasa ActorProxy**. Hello ActorProxy klasy jest używany przez klienta tooinvoke aplikacji hello metod udostępnianych za pośrednictwem interfejsu aktora hello. Witaj klasy ActorProxy zawiera dwie ważne funkcje:
  
  * Rozpoznawanie nazw: jest w stanie toolocate hello aktora w klastrze hello (Znajdź hello węzeł klastra hello, w którym jest hostowany).
  * Obsługa błąd: można ponowić próbę wywołania metody i ponownie rozwiązania lokalizacji aktora powitania po, na przykład błąd, który wymaga toobe aktora hello przeniesiony tooanother węzła w klastrze hello.

następujące reguły, które odnoszą się interfejsów tooactor Hello są warto zauważyć:

* Metody interfejsu aktora nie może być przeciążony.
* Interfejs aktora metody nie może mieć wychodzących, ref lub parametrów opcjonalnych.
* Interfejsy ogólne nie są obsługiwane.

## <a name="create-a-new-project-in-visual-studio"></a>Utwórz nowy projekt w programie Visual Studio
Uruchom program Visual Studio 2015 lub Visual Studio 2017 jako administrator, a następnie utwórz nowy projekt aplikacji sieci szkieletowej usług:

![Narzędzia usługi sieć szkieletowa usług dla programu Visual Studio — nowy projekt][1]

Okno dialogowe dalej hello można wybrać typ hello projektu, które mają toocreate.

![Szablony projektu sieci szkieletowej usług][5]

Dla projektu HelloWorld hello Użyjmy hello usługi Reliable Actors sieci szkieletowej usług.

Po utworzeniu rozwiązania hello powinny być widoczne następujące struktury hello:

![Struktury projektu sieci szkieletowej usług][2]

## <a name="reliable-actors-basic-building-blocks"></a>Niezawodne złośliwych użytkowników podstawowych bloków konstrukcyjnych
Typowe rozwiązania Reliable Actors składa się z trzech projektów:

* **Projekt aplikacji Hello (MyActorApplication)**. Jest to projekt hello wszystkich usług hello razem wdrożenia pakietów. Zawiera on hello *ApplicationManifest.xml* i skrypty programu PowerShell do zarządzania aplikacji hello.
* **Projekt interfejsu Hello (MyActor.Interfaces)**. Jest to projekt hello, który zawiera definicję interfejsu hello hello aktora. W projekcie MyActor.Interfaces hello można zdefiniować hello interfejsów, które będą używane przez uczestników hello hello rozwiązania. Interfejsów aktora można zdefiniować w każdym projekcie z żadną nazwą, jednak hello interfejs definiuje hello aktora kontraktu, który jest współużytkowany przez implementację aktora hello i klientów hello wywoływania aktora hello, dlatego zazwyczaj ułatwia wykrywanie toodefine w zestawie, do którego jest oddzielić od hello aktora implementacji i może być współużytkowane przez wiele innych projektów.

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* **projekt usługi aktora Hello (MyActor)**. To jest hello projektu używany toodefine hello usługi sieć szkieletowa jest będzie toohost hello aktora. Zawiera ona wdrożenia hello hello aktora. Implementacja aktora jest klasa, która pochodzi z typu podstawowego hello `Actor` i implementuje hello interfejsów, które są zdefiniowane w projekcie MyActor.Interfaces hello. Klasa aktora musi także implementować konstruktora akceptującego `ActorService` wystąpienia i `ActorId` i przekazuje je toohello podstawowej `Actor` klasy. Dzięki temu iniekcji zależności konstruktora zależności platformy.

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

Usługa aktora Hello musi być zarejestrowany w środowisku uruchomieniowym usługi sieć szkieletowa hello typ usługi. W celu dla hello toorun usługi aktora swoich wystąpień aktora, danego typu aktora również musi być zarejestrowany hello usługi aktora. Witaj `ActorRuntime` metoda rejestracji wykonuje tej pracy dla osób.

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

Jeśli masz tylko jedną definicję aktora w przypadku uruchomienia nowego projektu programu Visual Studio, rejestracja hello jest domyślnie włączone w hello kod, który generuje Visual Studio. Po zdefiniowaniu innych uczestników w usłudze hello należy tooadd hello aktora rejestracji przy użyciu:

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> Witaj środowisko uruchomieniowe usługi sieć szkieletowa podmiotów emituje niektóre [zdarzenia i liczniki wydajności związane z metody tooactor](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters). Są one przydatne w Diagnostyka i monitorowanie wydajności.
> 
> 

## <a name="debugging"></a>Debugowanie
Witaj usługi Service Fabric tools dla Visual Studio obsługuje debugowania na komputerze lokalnym. Możesz uruchomić sesję debugowania hello naciskać klawisz F5. Visual Studio kompiluje (w razie potrzeby) pakietów. Również wdraża aplikację hello na powitania lokalnego klastra usługi sieć szkieletowa usług i dołącza debuger hello.

Podczas procesu wdrażania hello, możesz wyświetlić postęp hello na powitania **dane wyjściowe** okna.

![Okno danych wyjściowych debugowania sieci szkieletowej usług][3]

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [wykorzystania platformy Service Fabric hello Reliable Actors](service-fabric-reliable-actors-platform.md).

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
