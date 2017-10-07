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
# <a name="actor-events"></a>Zdarzenia aktora
Zdarzenia aktora udostępniają sposób toosend optymalnych powiadomienia z hello aktora toohello klientów. Aktora zdarzeń są przeznaczone dla komunikacji aktora do klienta i nie powinna być używana do komunikacji aktora aktora.

Hello poniższy kod Pokaż wstawki jak toouse aktora zdarzenia w aplikacji.

Zdefiniuj interfejs, który opisuje zdarzenia hello opublikowanych przez hello aktora. Ten interfejs musi pochodzić z hello `IActorEvents` interfejsu. Witaj argumenty metod hello muszą być [serializacji kontraktu danych](service-fabric-reliable-actors-notes-on-actor-type-serialization.md). metody Hello musi zwracać typ void, jako zdarzenie powiadomienia są jednym ze sposobów i optymalnego.

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
Deklarowanie zdarzeń hello opublikowanych przez aktora hello hello aktora interfejsu.

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
Na powitania po stronie klienta należy zaimplementować hello obsługi zdarzeń.

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

Na powitania klienta tworzenie aktora toohello serwera proxy, który publikuje hello zdarzeń i subskrypcję tooits zdarzenia.

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

W przypadku hello przechodzenia w tryb failover aktora hello może zakończyć się niepowodzeniem przez inny proces tooa lub węzeł. Serwer proxy aktora Hello zarządza hello aktywne subskrypcje i automatycznie ponownie je subskrybuje. Można kontrolować interwał ponownej subskrypcji powitania za pośrednictwem hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` interfejsu API. toounsubscribe, użyj hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` interfejsu API.

Na powitania aktora po prostu publikowanie zdarzeń powitania po ich wprowadzeniu. W przypadku subskrybentów toohello zdarzenia środowiska uruchomieniowego podmiotów hello wyśle je hello powiadomień.

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a>Następne kroki
* [Wielobieżność aktora](service-fabric-reliable-actors-reentrancy.md)
* [Aktora Diagnostyka i monitorowanie wydajności](service-fabric-reliable-actors-diagnostics.md)
* [Dokumentację referencyjną aktora interfejsu API](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [C# przykładowy kod](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [C# .NET Core przykładowy kod](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [Java przykładowy kod](http://github.com/Azure-Samples/service-fabric-java-getting-started)
