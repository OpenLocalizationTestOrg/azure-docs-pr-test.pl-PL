---
title: "aaaEvents w podstawie aktora Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Wprowadzenie tooevents dla elementów Reliable Actors sieci szkieletowej usług."
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
ms.openlocfilehash: a51e41c35441a5fea508138968b36a35f0ba6699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="actor-events"></a><span data-ttu-id="5249b-103">Zdarzenia aktora</span><span class="sxs-lookup"><span data-stu-id="5249b-103">Actor events</span></span>
<span data-ttu-id="5249b-104">Zdarzenia aktora udostępniają sposób toosend optymalnych powiadomienia z hello aktora toohello klientów.</span><span class="sxs-lookup"><span data-stu-id="5249b-104">Actor events provide a way toosend best-effort notifications from hello actor toohello clients.</span></span> <span data-ttu-id="5249b-105">Aktora zdarzeń są przeznaczone dla komunikacji aktora do klienta i nie powinna być używana do komunikacji aktora aktora.</span><span class="sxs-lookup"><span data-stu-id="5249b-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="5249b-106">Hello poniższy kod Pokaż wstawki jak toouse aktora zdarzenia w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5249b-106">hello following code snippets show how toouse actor events in your application.</span></span>

<span data-ttu-id="5249b-107">Zdefiniuj interfejs, który opisuje zdarzenia hello opublikowanych przez hello aktora.</span><span class="sxs-lookup"><span data-stu-id="5249b-107">Define an interface that describes hello events published by hello actor.</span></span> <span data-ttu-id="5249b-108">Ten interfejs musi pochodzić z hello `IActorEvents` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="5249b-108">This interface must be derived from hello `IActorEvents` interface.</span></span> <span data-ttu-id="5249b-109">Witaj argumenty metod hello muszą być [serializacji kontraktu danych](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="5249b-109">hello arguments of hello methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="5249b-110">metody Hello musi zwracać typ void, jako zdarzenie powiadomienia są jednym ze sposobów i optymalnego.</span><span class="sxs-lookup"><span data-stu-id="5249b-110">hello methods must return void, as event notifications are one way and best effort.</span></span>

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
<span data-ttu-id="5249b-111">Deklarowanie zdarzeń hello opublikowanych przez aktora hello hello aktora interfejsu.</span><span class="sxs-lookup"><span data-stu-id="5249b-111">Declare hello events published by hello actor in hello actor interface.</span></span>

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
<span data-ttu-id="5249b-112">Na powitania po stronie klienta należy zaimplementować hello obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="5249b-112">On hello client side, implement hello event handler.</span></span>

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

<span data-ttu-id="5249b-113">Na powitania klienta tworzenie aktora toohello serwera proxy, który publikuje hello zdarzeń i subskrypcję tooits zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="5249b-113">On hello client, create a proxy toohello actor that publishes hello event and subscribe tooits events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="5249b-114">W przypadku hello przechodzenia w tryb failover aktora hello może zakończyć się niepowodzeniem przez inny proces tooa lub węzeł.</span><span class="sxs-lookup"><span data-stu-id="5249b-114">In hello event of failovers, hello actor may fail over tooa different process or node.</span></span> <span data-ttu-id="5249b-115">Serwer proxy aktora Hello zarządza hello aktywne subskrypcje i automatycznie ponownie je subskrybuje.</span><span class="sxs-lookup"><span data-stu-id="5249b-115">hello actor proxy manages hello active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="5249b-116">Można kontrolować interwał ponownej subskrypcji powitania za pośrednictwem hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5249b-116">You can control hello re-subscription interval through hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="5249b-117">toounsubscribe, użyj hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5249b-117">toounsubscribe, use hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="5249b-118">Na powitania aktora po prostu publikowanie zdarzeń powitania po ich wprowadzeniu.</span><span class="sxs-lookup"><span data-stu-id="5249b-118">On hello actor, simply publish hello events as they happen.</span></span> <span data-ttu-id="5249b-119">W przypadku subskrybentów toohello zdarzenia środowiska uruchomieniowego podmiotów hello wyśle je hello powiadomień.</span><span class="sxs-lookup"><span data-stu-id="5249b-119">If there are subscribers toohello event, hello Actors runtime will send them hello notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="5249b-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5249b-120">Next steps</span></span>
* [<span data-ttu-id="5249b-121">Wielobieżność aktora</span><span class="sxs-lookup"><span data-stu-id="5249b-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="5249b-122">Aktora Diagnostyka i monitorowanie wydajności</span><span class="sxs-lookup"><span data-stu-id="5249b-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="5249b-123">Dokumentację referencyjną aktora interfejsu API</span><span class="sxs-lookup"><span data-stu-id="5249b-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="5249b-124">C# przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="5249b-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="5249b-125">C# .NET Core przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="5249b-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="5249b-126">Java przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="5249b-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
