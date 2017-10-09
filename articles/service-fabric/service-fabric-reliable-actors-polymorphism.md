---
title: aaaPolymorphism w ramach Reliable Actors hello | Dokumentacja firmy Microsoft
description: "Tworzenie hierarchii interfejsów .NET i typów w hello Reliable Actors framework tooreuse funkcjonalność i definicje interfejsu API."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: vturecek
ms.assetid: ef0eeff6-32b7-410d-ac69-87cba8b8fd46
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ed9ec442595bd9a5e48c9af1f6aac003439b81f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="polymorphism-in-hello-reliable-actors-framework"></a>Polimorfizm w ramach Reliable Actors hello
Witaj Reliable Actors, który framework pozwala toobuild złośliwych użytkowników używających wiele hello tych samych metod, które należy użyć w projekcie zorientowane obiektowo. Jeden z tych metod jest polimorfizm, co umożliwia typów i interfejsy tooinherit z więcej uogólniony elementów nadrzędnych. Dziedziczenie w ramach Reliable Actors hello zazwyczaj następuje hello .NET modelu z kilku dodatkowe ograniczenia. W przypadku języka Java/Linux wynika z hello Java modelu.

## <a name="interfaces"></a>Interfejsy
Witaj Reliable Actors framework wymaga toodefine toobe co najmniej jeden interfejs implementowany przez danego typu aktora. Ten interfejs jest używane toogenerate klasy serwera proxy, które mogą być używane przez klientów toocommunicate z sieci złośliwych użytkowników. Interfejsy może dziedziczyć po elemencie inne interfejsy, jak długo każdy interfejs, który jest implementowany przez typ aktora i wszystkich jego obiektów nadrzędnych ostatecznie pochodzić od IActor(C#) lub Actor(Java). IActor(C#) i Actor(Java) są odpowiednio hello zdefiniowane platformy interfejsach podstawowych dla uczestników hello platformy .NET i Java. W związku z tym przykład klasycznego polimorfizm Witaj za pomocą kształtów może wyglądać następująco:

![Interfejs hierarchii osób kształtu][shapes-interface-hierarchy]

## <a name="types"></a>Typy
Można również utworzyć hierarchię aktora typów, które pochodzą z hello aktora klasy podstawowej są dostarczane przez platformę hello. W przypadku hello kształtów, może mieć podstawy `Shape`(C#) lub `ShapeImpl`typu (Java):

```csharp
public abstract class Shape : Actor, IShape
{
    public abstract Task<int> GetVerticeCount();

    public abstract Task<double> GetAreaAsync();
}
```
```Java
public abstract class ShapeImpl extends FabricActor implements Shape
{
    public abstract CompletableFuture<int> getVerticeCount();

    public abstract CompletableFuture<double> getAreaAsync();
}
```

Subtypes z `Shape`(C#) lub `ShapeImpl`(Java) można zastąpić metody hello podstawowej.

```csharp
[ActorService(Name = "Circle")]
[StatePersistence(StatePersistence.Persisted)]
public class Circle : Shape, ICircle
{
    public override Task<int> GetVerticeCount()
    {
        return Task.FromResult(0);
    }

    public override async Task<double> GetAreaAsync()
    {
        CircleState state = await this.StateManager.GetStateAsync<CircleState>("circle");

        return Math.PI *
            state.Radius *
            state.Radius;
    }
}
```
```Java
@ActorServiceAttribute(name = "Circle")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class Circle extends ShapeImpl implements Circle
{
    @Override
    public CompletableFuture<Integer> getVerticeCount()
    {
        return CompletableFuture.completedFuture(0);
    }

    @Override
    public CompletableFuture<Double> getAreaAsync()
    {
        return (this.stateManager().getStateAsync<CircleState>("circle").thenApply(state->{
          return Math.PI * state.radius * state.radius;
        }));
    }
}
```

Uwaga hello `ActorService` atrybut typu aktora hello. Ten atrybut informuje hello niezawodnego aktora framework, automatycznie należy utworzyć usługi hostingu uczestników tego typu. W niektórych przypadkach może być wymagane toocreate wyłącznie przeznaczony do udostępniania funkcji podtypy typu podstawowego i nigdy nie będą używane tooinstantiate konkretnych osób. W takich przypadkach należy użyć hello `abstract` tooindicate — słowo kluczowe, które nigdy nie zostanie utworzona na podstawie tego typu aktora.

## <a name="next-steps"></a>Następne kroki
* Zobacz [jak hello Reliable Actors framework korzysta z platformy sieć szkieletowa usług hello](service-fabric-reliable-actors-platform.md) tooprovide niezawodności i skalowalności oraz w spójnym stanie.
* Dowiedz się więcej o hello [cyklu życia aktora](service-fabric-reliable-actors-lifecycle.md).

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
