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
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="02e1f-103">Uwagi dotyczące usługi sieci szkieletowej Reliable Actors typu serializacji</span><span class="sxs-lookup"><span data-stu-id="02e1f-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="02e1f-104">Argumenty metod wszystkie typy wyników zadań zwracane przez każda metoda w interfejsie aktora, a obiekty przechowywane w Menedżerze stanu aktora musi być [serializacji kontraktu danych](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="02e1f-104">The arguments of all methods, result types of the tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="02e1f-105">Dotyczy to również argumenty metody zdefiniowane w [interfejsów zdarzeń aktora](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="02e1f-105">This also applies to the arguments of the methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="02e1f-106">(Metod interfejsu zdarzenia aktora zawsze zwracać typ void.)</span><span class="sxs-lookup"><span data-stu-id="02e1f-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="02e1f-107">Niestandardowe typy danych</span><span class="sxs-lookup"><span data-stu-id="02e1f-107">Custom data types</span></span>
<span data-ttu-id="02e1f-108">W tym przykładzie interfejsu aktora definiuje metodę, która zwraca niestandardowego typu danych o nazwie `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="02e1f-108">In this example, the following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

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

<span data-ttu-id="02e1f-109">Interfejs jest implementowany przez aktora, który używa Menedżera stanu do przechowywania `VoicemailBox` obiektu:</span><span class="sxs-lookup"><span data-stu-id="02e1f-109">The interface is implemented by an actor that uses the state manager to store a `VoicemailBox` object:</span></span>

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

<span data-ttu-id="02e1f-110">W tym przykładzie `VoicemailBox` serializowany jest obiekt po:</span><span class="sxs-lookup"><span data-stu-id="02e1f-110">In this example, the `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="02e1f-111">Obiekt przesyłane między wystąpieniem aktora i obiekt wywołujący.</span><span class="sxs-lookup"><span data-stu-id="02e1f-111">The object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="02e1f-112">Obiekt zostanie zapisany menedżera stanu, gdzie jest utrwalony na dysku i replikowany do innych węzłów.</span><span class="sxs-lookup"><span data-stu-id="02e1f-112">The object is saved in the state manager where it is persisted to disk and replicated to other nodes.</span></span>

<span data-ttu-id="02e1f-113">Platforma niezawodnego aktora korzysta z serializacji DataContract.</span><span class="sxs-lookup"><span data-stu-id="02e1f-113">The Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="02e1f-114">W związku z tym obiektów danych niestandardowych i ich elementy Członkowskie musi być adnotowany przy **DataContract** i **DataMember** atrybuty odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="02e1f-114">Therefore, the custom data objects and their members must be annotated with the **DataContract** and **DataMember** attributes, respectively.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="02e1f-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02e1f-115">Next steps</span></span>
* [<span data-ttu-id="02e1f-116">Aktora cykl życia i odzyskiwanie pamięci</span><span class="sxs-lookup"><span data-stu-id="02e1f-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="02e1f-117">Czasomierze aktora i przypomnieniami</span><span class="sxs-lookup"><span data-stu-id="02e1f-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="02e1f-118">Zdarzenia aktora</span><span class="sxs-lookup"><span data-stu-id="02e1f-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="02e1f-119">Wielobieżność aktora</span><span class="sxs-lookup"><span data-stu-id="02e1f-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="02e1f-120">Polimorfizm aktora i wzorce projektowe zorientowane obiektowo</span><span class="sxs-lookup"><span data-stu-id="02e1f-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="02e1f-121">Aktora Diagnostyka i monitorowanie wydajności</span><span class="sxs-lookup"><span data-stu-id="02e1f-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
