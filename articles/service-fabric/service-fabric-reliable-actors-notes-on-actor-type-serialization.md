---
title: "Niezawodne dodatkowej podmiotów aktora typu serializacji | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono podstawowe wymagania dotyczące Definiowanie klas możliwych do serializacji, które mogą służyć do definiowania stanów Reliable Actors sieci szkieletowej usług i interfejsów"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 6e50e4dc-969a-4a1c-b36c-b292d964c7e3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4b48b893e5a3bf5620f00a336576efe1ad63def8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a>Uwagi dotyczące usługi sieci szkieletowej Reliable Actors typu serializacji
Argumenty metod wszystkie typy wyników zadań zwracane przez każda metoda w interfejsie aktora, a obiekty przechowywane w Menedżerze stanu aktora musi być [serializacji kontraktu danych](https://msdn.microsoft.com/library/ms731923.aspx). Dotyczy to również argumenty metody zdefiniowane w [interfejsów zdarzeń aktora](service-fabric-reliable-actors-events.md). (Metod interfejsu zdarzenia aktora zawsze zwracać typ void.)

## <a name="custom-data-types"></a>Niestandardowe typy danych
W tym przykładzie interfejsu aktora definiuje metodę, która zwraca niestandardowego typu danych o nazwie `VoicemailBox`:

```csharp
public interface IVoiceMailBoxActor : IActor
{
    Task<VoicemailBox> GetMailBoxAsync();
}
```

```Java
public interface VoiceMailBoxActor extends Actor
{
    CompletableFuture<VoicemailBox> getMailBoxAsync();
}
```

Interfejs jest implementowany przez aktora, który używa Menedżera stanu do przechowywania `VoicemailBox` obiektu:

```csharp
[StatePersistence(StatePersistence.Persisted)]
public class VoiceMailBoxActor : Actor, IVoicemailBoxActor
{
    public VoiceMailBoxActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<VoicemailBox> GetMailboxAsync()
    {
        return this.StateManager.GetStateAsync<VoicemailBox>("Mailbox");
    }
}

```

```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class VoiceMailBoxActorImpl extends FabricActor implements VoicemailBoxActor
{
    public VoiceMailBoxActorImpl(ActorService actorService, ActorId actorId)
    {
         super(actorService, actorId);
    }

    public CompletableFuture<VoicemailBox> getMailBoxAsync()
    {
         return this.stateManager().getStateAsync("Mailbox");
    }
}

```

W tym przykładzie `VoicemailBox` serializowany jest obiekt po:

* Obiekt przesyłane między wystąpieniem aktora i obiekt wywołujący.
* Obiekt zostanie zapisany menedżera stanu, gdzie jest utrwalony na dysku i replikowany do innych węzłów.

Platforma niezawodnego aktora korzysta z serializacji DataContract. W związku z tym obiektów danych niestandardowych i ich elementy Członkowskie musi być adnotowany przy **DataContract** i **DataMember** atrybuty odpowiednio.

```csharp
[DataContract]
public class Voicemail
{
    [DataMember]
    public Guid Id { get; set; }

    [DataMember]
    public string Message { get; set; }

    [DataMember]
    public DateTime ReceivedAt { get; set; }
}
```
```Java
public class Voicemail implements Serializable
{
    private static final long serialVersionUID = 42L;

    private UUID id;                    //getUUID() and setUUID()

    private String message;             //getMessage() and setMessage()

    private GregorianCalendar receivedAt; //getReceivedAt() and setReceivedAt()
}
```


```csharp
[DataContract]
public class VoicemailBox
{
    public VoicemailBox()
    {
        this.MessageList = new List<Voicemail>();
    }

    [DataMember]
    public List<Voicemail> MessageList { get; set; }

    [DataMember]
    public string Greeting { get; set; }
}
```
```Java
public class VoicemailBox implements Serializable
{
    static final long serialVersionUID = 42L;
    
    public VoicemailBox()
    {
        this.messageList = new ArrayList<Voicemail>();
    }

    private List<Voicemail> messageList;   //getMessageList() and setMessageList()

    private String greeting;               //getGreeting() and setGreeting()
}
```


## <a name="next-steps"></a>Następne kroki
* [Aktora cykl życia i odzyskiwanie pamięci](service-fabric-reliable-actors-lifecycle.md)
* [Czasomierze aktora i przypomnieniami](service-fabric-reliable-actors-timers-reminders.md)
* [Zdarzenia aktora](service-fabric-reliable-actors-events.md)
* [Wielobieżność aktora](service-fabric-reliable-actors-reentrancy.md)
* [Polimorfizm aktora i wzorce projektowe zorientowane obiektowo](service-fabric-reliable-actors-polymorphism.md)
* [Aktora Diagnostyka i monitorowanie wydajności](service-fabric-reliable-actors-diagnostics.md)
