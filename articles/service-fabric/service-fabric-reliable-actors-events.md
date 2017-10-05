---
title: "Zdarzenia w podstawie aktora Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do zdarzeń dla elementów Reliable Actors sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: aa01b0f7-8f88-403a-bfe1-5aba00312c24
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: d936670c548ff709fc2e935d3f28d94e4bde8a04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="actor-events"></a><span data-ttu-id="156b8-103">Zdarzenia aktora</span><span class="sxs-lookup"><span data-stu-id="156b8-103">Actor events</span></span>
<span data-ttu-id="156b8-104">Zdarzenia aktora umożliwiają wysyłanie powiadomień optymalnych z aktora do klientów.</span><span class="sxs-lookup"><span data-stu-id="156b8-104">Actor events provide a way to send best-effort notifications from the actor to the clients.</span></span> <span data-ttu-id="156b8-105">Aktora zdarzeń są przeznaczone dla komunikacji aktora do klienta i nie powinna być używana do komunikacji aktora aktora.</span><span class="sxs-lookup"><span data-stu-id="156b8-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="156b8-106">Poniższe fragmenty kodu przedstawiają sposób korzystanie ze zdarzeń aktora w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="156b8-106">The following code snippets show how to use actor events in your application.</span></span>

<span data-ttu-id="156b8-107">Zdefiniuj interfejs, który opisuje zdarzenia opublikowanych przez aktora.</span><span class="sxs-lookup"><span data-stu-id="156b8-107">Define an interface that describes the events published by the actor.</span></span> <span data-ttu-id="156b8-108">Ten interfejs musi pochodzić od `IActorEvents` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="156b8-108">This interface must be derived from the `IActorEvents` interface.</span></span> <span data-ttu-id="156b8-109">Argumenty metod muszą być [serializacji kontraktu danych](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="156b8-109">The arguments of the methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="156b8-110">Metody musi zwracać typ void, jako zdarzenie powiadomienia są jednym ze sposobów i optymalnego.</span><span class="sxs-lookup"><span data-stu-id="156b8-110">The methods must return void, as event notifications are one way and best effort.</span></span>

```csharp
public interface IGameEvents : IActorEvents
{
    void GameScoreUpdated(Guid gameId, string currentScore);
}
```
```Java
public interface GameEvents implements ActorEvents
{
    void gameScoreUpdated(UUID gameId, String currentScore);
}
```
<span data-ttu-id="156b8-111">Deklarowanie zdarzeń, opublikowanych przez aktora w interfejsie aktora.</span><span class="sxs-lookup"><span data-stu-id="156b8-111">Declare the events published by the actor in the actor interface.</span></span>

```csharp
public interface IGameActor : IActor, IActorEventPublisher<IGameEvents>
{
    Task UpdateGameStatus(GameStatus status);

    Task<string> GetGameScore();
}
```
```Java
public interface GameActor extends Actor, ActorEventPublisherE<GameEvents>
{
    CompletableFuture<?> updateGameStatus(GameStatus status);

    CompletableFuture<String> getGameScore();
}
```
<span data-ttu-id="156b8-112">Po stronie klienta implementacji programu obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="156b8-112">On the client side, implement the event handler.</span></span>

```csharp
class GameEventsHandler : IGameEvents
{
    public void GameScoreUpdated(Guid gameId, string currentScore)
    {
        Console.WriteLine(@"Updates: Game: {0}, Score: {1}", gameId, currentScore);
    }
}
```

```Java
class GameEventsHandler implements GameEvents {
    public void gameScoreUpdated(UUID gameId, String currentScore)
    {
        System.out.println("Updates: Game: "+gameId+" ,Score: "+currentScore);
    }
}
```

<span data-ttu-id="156b8-113">Na komputerze klienckim utworzyć proxy aktora, która publikuje zdarzenia i subskrybowanie jego zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="156b8-113">On the client, create a proxy to the actor that publishes the event and subscribe to its events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="156b8-114">W przypadku przełączenia do trybu failover aktora może przełączyć się inny proces lub węzeł.</span><span class="sxs-lookup"><span data-stu-id="156b8-114">In the event of failovers, the actor may fail over to a different process or node.</span></span> <span data-ttu-id="156b8-115">Serwer proxy aktora zarządza aktywne subskrypcje i automatycznie ponownie subskrybuje je.</span><span class="sxs-lookup"><span data-stu-id="156b8-115">The actor proxy manages the active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="156b8-116">Można kontrolować interwał ponownej subskrypcji za pośrednictwem `ActorProxyEventExtensions.SubscribeAsync<TEvent>` interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="156b8-116">You can control the re-subscription interval through the `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="156b8-117">Aby anulować subskrypcję, należy użyć `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="156b8-117">To unsubscribe, use the `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="156b8-118">Na aktora po prostu opublikować zdarzenia wystąpią.</span><span class="sxs-lookup"><span data-stu-id="156b8-118">On the actor, simply publish the events as they happen.</span></span> <span data-ttu-id="156b8-119">W przypadku subskrybentów w zdarzeniu środowiska wykonawczego podmiotów wyśle je powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="156b8-119">If there are subscribers to the event, the Actors runtime will send them the notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="156b8-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="156b8-120">Next steps</span></span>
* [<span data-ttu-id="156b8-121">Wielobieżność aktora</span><span class="sxs-lookup"><span data-stu-id="156b8-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="156b8-122">Aktora Diagnostyka i monitorowanie wydajności</span><span class="sxs-lookup"><span data-stu-id="156b8-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="156b8-123">Dokumentację referencyjną aktora interfejsu API</span><span class="sxs-lookup"><span data-stu-id="156b8-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="156b8-124">C# przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="156b8-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="156b8-125">C# .NET Core przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="156b8-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="156b8-126">Java przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="156b8-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
