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
# <a name="polymorphism-in-hello-reliable-actors-framework"></a><span data-ttu-id="71ebe-103">Polimorfizm w ramach Reliable Actors hello</span><span class="sxs-lookup"><span data-stu-id="71ebe-103">Polymorphism in hello Reliable Actors framework</span></span>
<span data-ttu-id="71ebe-104">Witaj Reliable Actors, który framework pozwala toobuild złośliwych użytkowników używających wiele hello tych samych metod, które należy użyć w projekcie zorientowane obiektowo.</span><span class="sxs-lookup"><span data-stu-id="71ebe-104">hello Reliable Actors framework allows you toobuild actors using many of hello same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="71ebe-105">Jeden z tych metod jest polimorfizm, co umożliwia typów i interfejsy tooinherit z więcej uogólniony elementów nadrzędnych.</span><span class="sxs-lookup"><span data-stu-id="71ebe-105">One of those techniques is polymorphism, which allows types and interfaces tooinherit from more generalized parents.</span></span> <span data-ttu-id="71ebe-106">Dziedziczenie w ramach Reliable Actors hello zazwyczaj następuje hello .NET modelu z kilku dodatkowe ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="71ebe-106">Inheritance in hello Reliable Actors framework generally follows hello .NET model with a few additional constraints.</span></span> <span data-ttu-id="71ebe-107">W przypadku języka Java/Linux wynika z hello Java modelu.</span><span class="sxs-lookup"><span data-stu-id="71ebe-107">In case of Java/Linux, it follows hello Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="71ebe-108">Interfejsy</span><span class="sxs-lookup"><span data-stu-id="71ebe-108">Interfaces</span></span>
<span data-ttu-id="71ebe-109">Witaj Reliable Actors framework wymaga toodefine toobe co najmniej jeden interfejs implementowany przez danego typu aktora.</span><span class="sxs-lookup"><span data-stu-id="71ebe-109">hello Reliable Actors framework requires you toodefine at least one interface toobe implemented by your actor type.</span></span> <span data-ttu-id="71ebe-110">Ten interfejs jest używane toogenerate klasy serwera proxy, które mogą być używane przez klientów toocommunicate z sieci złośliwych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="71ebe-110">This interface is used toogenerate a proxy class that can be used by clients toocommunicate with your actors.</span></span> <span data-ttu-id="71ebe-111">Interfejsy może dziedziczyć po elemencie inne interfejsy, jak długo każdy interfejs, który jest implementowany przez typ aktora i wszystkich jego obiektów nadrzędnych ostatecznie pochodzić od IActor(C#) lub Actor(Java).</span><span class="sxs-lookup"><span data-stu-id="71ebe-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="71ebe-112">IActor(C#) i Actor(Java) są odpowiednio hello zdefiniowane platformy interfejsach podstawowych dla uczestników hello platformy .NET i Java.</span><span class="sxs-lookup"><span data-stu-id="71ebe-112">IActor(C#) and Actor(Java) are hello platform-defined base interfaces for actors in hello frameworks .NET and Java respectively.</span></span> <span data-ttu-id="71ebe-113">W związku z tym przykład klasycznego polimorfizm Witaj za pomocą kształtów może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="71ebe-113">Thus, hello classic polymorphism example using shapes might look something like this:</span></span>

![Interfejs hierarchii osób kształtu][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="71ebe-115">Typy</span><span class="sxs-lookup"><span data-stu-id="71ebe-115">Types</span></span>
<span data-ttu-id="71ebe-116">Można również utworzyć hierarchię aktora typów, które pochodzą z hello aktora klasy podstawowej są dostarczane przez platformę hello.</span><span class="sxs-lookup"><span data-stu-id="71ebe-116">You can also create a hierarchy of actor types, which are derived from hello base Actor class that is provided by hello platform.</span></span> <span data-ttu-id="71ebe-117">W przypadku hello kształtów, może mieć podstawy `Shape`(C#) lub `ShapeImpl`typu (Java):</span><span class="sxs-lookup"><span data-stu-id="71ebe-117">In hello case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="71ebe-118">Subtypes z `Shape`(C#) lub `ShapeImpl`(Java) można zastąpić metody hello podstawowej.</span><span class="sxs-lookup"><span data-stu-id="71ebe-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from hello base.</span></span>

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

<span data-ttu-id="71ebe-119">Uwaga hello `ActorService` atrybut typu aktora hello.</span><span class="sxs-lookup"><span data-stu-id="71ebe-119">Note hello `ActorService` attribute on hello actor type.</span></span> <span data-ttu-id="71ebe-120">Ten atrybut informuje hello niezawodnego aktora framework, automatycznie należy utworzyć usługi hostingu uczestników tego typu.</span><span class="sxs-lookup"><span data-stu-id="71ebe-120">This attribute tells hello Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="71ebe-121">W niektórych przypadkach może być wymagane toocreate wyłącznie przeznaczony do udostępniania funkcji podtypy typu podstawowego i nigdy nie będą używane tooinstantiate konkretnych osób.</span><span class="sxs-lookup"><span data-stu-id="71ebe-121">In some cases, you may wish toocreate a base type that is solely intended for sharing functionality with subtypes and will never be used tooinstantiate concrete actors.</span></span> <span data-ttu-id="71ebe-122">W takich przypadkach należy użyć hello `abstract` tooindicate — słowo kluczowe, które nigdy nie zostanie utworzona na podstawie tego typu aktora.</span><span class="sxs-lookup"><span data-stu-id="71ebe-122">In those cases, you should use hello `abstract` keyword tooindicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71ebe-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71ebe-123">Next steps</span></span>
* <span data-ttu-id="71ebe-124">Zobacz [jak hello Reliable Actors framework korzysta z platformy sieć szkieletowa usług hello](service-fabric-reliable-actors-platform.md) tooprovide niezawodności i skalowalności oraz w spójnym stanie.</span><span class="sxs-lookup"><span data-stu-id="71ebe-124">See [how hello Reliable Actors framework leverages hello Service Fabric platform](service-fabric-reliable-actors-platform.md) tooprovide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="71ebe-125">Dowiedz się więcej o hello [cyklu życia aktora](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="71ebe-125">Learn about hello [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
