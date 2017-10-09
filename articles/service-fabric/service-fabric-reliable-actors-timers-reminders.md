---
title: "aaaReliable podmiotów czasomierze i przypomnieniami | Dokumentacja firmy Microsoft"
description: "Wprowadzenie tootimers i przypomnienia dla elementów Reliable Actors sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 00c48716-569e-4a64-bd6c-25234c85ff4f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c5116ec1923014e131130b9f4e86dd1e133bbf7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="ce691-103">Czasomierze aktora i przypomnieniami</span><span class="sxs-lookup"><span data-stu-id="ce691-103">Actor timers and reminders</span></span>
<span data-ttu-id="ce691-104">Złośliwych użytkowników można zaplanować okresowe pracy od samych siebie rejestrując czasomierze lub przypomnienia.</span><span class="sxs-lookup"><span data-stu-id="ce691-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="ce691-105">W tym artykule przedstawiono sposób toouse czasomierze i przypomnienia wraz z wyjaśnieniem hello różnice między nimi.</span><span class="sxs-lookup"><span data-stu-id="ce691-105">This article shows how toouse timers and reminders and explains hello differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="ce691-106">Czasomierze aktora</span><span class="sxs-lookup"><span data-stu-id="ce691-106">Actor timers</span></span>
<span data-ttu-id="ce691-107">Czasomierze aktora zapewniają prosty otokę .NET lub Java tooensure czasomierza że metody wywołania zwrotnego hello przestrzegać gwarantuje współbieżności opartej na włączanie hello hello podmiotów zawiera środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="ce691-107">Actor timers provide a simple wrapper around a .NET or Java timer tooensure that hello callback methods respect hello turn-based concurrency guarantees that hello Actors runtime provides.</span></span>

<span data-ttu-id="ce691-108">Złośliwych użytkowników można używać hello `RegisterTimer`(C#) lub `registerTimer`(Java) i `UnregisterTimer`(C#) lub `unregisterTimer`metody (Java) na ich podstawie klasy tooregister i ich czasomierze wyrejestrować.</span><span class="sxs-lookup"><span data-stu-id="ce691-108">Actors can use hello `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class tooregister and unregister their timers.</span></span> <span data-ttu-id="ce691-109">Witaj w poniższym przykładzie pokazano sposób użycia hello czasomierza interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="ce691-109">hello example below shows hello use of timer APIs.</span></span> <span data-ttu-id="ce691-110">Hello interfejsy API są bardzo podobne czasomierza .NET toohello lub Java czasomierza.</span><span class="sxs-lookup"><span data-stu-id="ce691-110">hello APIs are very similar toohello .NET timer or Java timer.</span></span> <span data-ttu-id="ce691-111">W tym przykładzie, gdy czasomierza hello jest wymagany, hello złośliwych użytkowników w czasie wykonywania będzie wywoływać hello `MoveObject`(C#) lub `moveObject`— metoda (Java).</span><span class="sxs-lookup"><span data-stu-id="ce691-111">In this example, when hello timer is due, hello Actors runtime will call hello `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="ce691-112">Metoda Hello jest gwarantowana toorespect hello Włącz współbieżności oparta na wątkach.</span><span class="sxs-lookup"><span data-stu-id="ce691-112">hello method is guaranteed toorespect hello turn-based concurrency.</span></span> <span data-ttu-id="ce691-113">Oznacza to, że nie ma innych metod aktora lub wywołania zwrotne czasomierza/monitu będzie w toku zakończenia wykonywania tego wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="ce691-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

```csharp
class VisualObjectActor : Actor, IVisualObject
{
    private IActorTimer _updateTimer;

    public VisualObjectActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    protected override Task OnActivateAsync()
    {
        ...

        _updateTimer = RegisterTimer(
            MoveObject,                     // Callback method
            null,                           // Parameter toopass toohello callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time toodelay before hello callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of hello callback method

        return base.OnActivateAsync();
    }

    protected override Task OnDeactivateAsync()
    {
        if (_updateTimer != null)
        {
            UnregisterTimer(_updateTimer);
        }

        return base.OnDeactivateAsync();
    }

    private Task MoveObject(object state)
    {
        ...
        return Task.FromResult(true);
    }
}
```
```Java
public class VisualObjectActorImpl extends FabricActor implements VisualObjectActor
{
    private ActorTimer updateTimer;

    public VisualObjectActorImpl(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    @Override
    protected CompletableFuture onActivateAsync()
    {
        ...

        return this.stateManager()
                .getOrAddStateAsync(
                        stateName,
                        VisualObject.createRandom(
                                this.getId().toString(),
                                new Random(this.getId().toString().hashCode())))
                .thenApply((r) -> {
                    this.registerTimer(
                            (o) -> this.moveObject(o),                        // Callback method
                            "moveObject",
                            null,                                             // Parameter toopass toohello callback method
                            Duration.ofMillis(10),                            // Amount of time toodelay before hello callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of hello callback method
                    return null;
                });
    }

    @Override
    protected CompletableFuture onDeactivateAsync()
    {
        if (updateTimer != null)
        {
            unregisterTimer(updateTimer);
        }

        return super.onDeactivateAsync();
    }

    private CompletableFuture moveObject(Object state)
    {
        ...
        return this.stateManager().getStateAsync(this.stateName).thenCompose(v -> {
            VisualObject v1 = (VisualObject)v;
            v1.move();
            return (CompletableFuture<?>)this.stateManager().setStateAsync(stateName, v1).
                    thenApply(r -> {
                      ...
                      return null;});
        });
    }
}
```

<span data-ttu-id="ce691-114">Hello następnego okresu czasomierza hello rozpoczyna się po wywołania zwrotnego hello zakończeniem wykonywania.</span><span class="sxs-lookup"><span data-stu-id="ce691-114">hello next period of hello timer starts after hello callback completes execution.</span></span> <span data-ttu-id="ce691-115">Oznacza to, że czasomierza hello jest zatrzymana podczas wywołania zwrotnego hello jest wykonywany i została uruchomiona po zakończeniu wywołania zwrotnego hello.</span><span class="sxs-lookup"><span data-stu-id="ce691-115">This implies that hello timer is stopped while hello callback is executing and is started when hello callback finishes.</span></span>

<span data-ttu-id="ce691-116">środowisko uruchomieniowe podmiotów Hello zapisuje zmiany wprowadzone Menedżer stanu aktora toohello, po zakończeniu hello wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="ce691-116">hello Actors runtime saves changes made toohello actor's State Manager when hello callback finishes.</span></span> <span data-ttu-id="ce691-117">Jeśli wystąpi błąd podczas zapisywania stanu hello, ten obiekt aktora spowoduje wyłączenie i nowe wystąpienie zostanie aktywowany.</span><span class="sxs-lookup"><span data-stu-id="ce691-117">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="ce691-118">Zatrzymuje wszystkie czasomierze aktora hello jest dezaktywowana w ramach operacji wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="ce691-118">All timers are stopped when hello actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="ce691-119">Nie wywołania zwrotne czasomierza są wywoływane po tym.</span><span class="sxs-lookup"><span data-stu-id="ce691-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="ce691-120">Ponadto hello złośliwych użytkowników w czasie wykonywania nie zachowuje żadnych informacji o hello czasomierzy, które były uruchomione przed dezaktywacji.</span><span class="sxs-lookup"><span data-stu-id="ce691-120">Also, hello Actors runtime does not retain any information about hello timers that were running before deactivation.</span></span> <span data-ttu-id="ce691-121">Jest zapasowej tooregister aktora toohello żadnych czasomierzy, które wymaga uaktwnieniu w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="ce691-121">It is up toohello actor tooregister any timers that it needs when it is reactivated in hello future.</span></span> <span data-ttu-id="ce691-122">Aby uzyskać więcej informacji, zobacz sekcję hello na [aktora wyrzucanie elementów bezużytecznych](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="ce691-122">For more information, see hello section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="ce691-123">Przypomnienia aktora</span><span class="sxs-lookup"><span data-stu-id="ce691-123">Actor reminders</span></span>
<span data-ttu-id="ce691-124">Przypomnienia są tootrigger mechanizmu trwałe wywołań zwrotnych na aktora w określonych godzinach.</span><span class="sxs-lookup"><span data-stu-id="ce691-124">Reminders are a mechanism tootrigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="ce691-125">Ich funkcje są podobne tootimers.</span><span class="sxs-lookup"><span data-stu-id="ce691-125">Their functionality is similar tootimers.</span></span> <span data-ttu-id="ce691-126">Jednak w przeciwieństwie do czasomierze, przypomnienia są wyzwalane we wszystkich okolicznościach, aż do ich wyrejestrowuje jawnie aktora hello lub aktora hello jest jawnie usunięte.</span><span class="sxs-lookup"><span data-stu-id="ce691-126">But unlike timers, reminders are triggered under all circumstances until hello actor explicitly unregisters them or hello actor is explicitly deleted.</span></span> <span data-ttu-id="ce691-127">W szczególności przypomnienia są wyzwalane przez aktora deactivations i tryb failover, ponieważ hello złośliwych użytkowników w czasie wykonywania będzie nadal występował, informacje o przypomnienia hello aktora.</span><span class="sxs-lookup"><span data-stu-id="ce691-127">Specifically, reminders are triggered across actor deactivations and failovers because hello Actors runtime persists information about hello actor's reminders.</span></span>

<span data-ttu-id="ce691-128">tooregister przypomnienie aktora wywołuje hello `RegisterReminderAsync` metoda w klasie podstawowej hello, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="ce691-128">tooregister a reminder, an actor calls hello `RegisterReminderAsync` method provided on hello base class, as shown in hello following example:</span></span>

```csharp
protected override async Task OnActivateAsync()
{
    string reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    IActorReminder reminderRegistration = await this.RegisterReminderAsync(
        reminderName,
        BitConverter.GetBytes(amountInDollars),
        TimeSpan.FromDays(3),
        TimeSpan.FromDays(1));
}
```

```Java
@Override
protected CompletableFuture onActivateAsync()
{
    String reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    ActorReminder reminderRegistration = this.registerReminderAsync(
            reminderName,
            state,
            dueTime,    //hello amount of time toodelay before firing hello reminder
            period);    //hello time interval between firing of reminders
}
```

<span data-ttu-id="ce691-129">W tym przykładzie `"Pay cell phone bill"` jest nazwą monitu hello.</span><span class="sxs-lookup"><span data-stu-id="ce691-129">In this example, `"Pay cell phone bill"` is hello reminder name.</span></span> <span data-ttu-id="ce691-130">Jest to ciąg hello używa aktora toouniquely zidentyfikować przypomnienia.</span><span class="sxs-lookup"><span data-stu-id="ce691-130">This is a string that hello actor uses toouniquely identify a reminder.</span></span> <span data-ttu-id="ce691-131">`BitConverter.GetBytes(amountInDollars)`(C#) jest kontekstem hello, który jest skojarzony z hello monitu.</span><span class="sxs-lookup"><span data-stu-id="ce691-131">`BitConverter.GetBytes(amountInDollars)`(C#) is hello context that is associated with hello reminder.</span></span> <span data-ttu-id="ce691-132">Zostanie przekazana aktora wstecz toohello jako argument toohello monitu wywołania zwrotnego, tj. `IRemindable.ReceiveReminderAsync`(C#) lub `Remindable.receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="ce691-132">It will be passed back toohello actor as an argument toohello reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="ce691-133">Aktorów używających przypomnienia muszą implementować hello `IRemindable` interfejsu, jak pokazano w poniższym przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="ce691-133">Actors that use reminders must implement hello `IRemindable` interface, as shown in hello example below.</span></span>

```csharp
public class ToDoListActor : Actor, IToDoListActor, IRemindable
{
    public ToDoListActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task ReceiveReminderAsync(string reminderName, byte[] context, TimeSpan dueTime, TimeSpan period)
    {
        if (reminderName.Equals("Pay cell phone bill"))
        {
            int amountToPay = BitConverter.ToInt32(context, 0);
            System.Console.WriteLine("Please pay your cell phone bill of ${0}!", amountToPay);
        }
        return Task.FromResult(true);
    }
}
```
```Java
public class ToDoListActorImpl extends FabricActor implements ToDoListActor, Remindable
{
    public ToDoListActor(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture receiveReminderAsync(String reminderName, byte[] context, Duration dueTime, Duration period)
    {
        if (reminderName.equals("Pay cell phone bill"))
        {
            int amountToPay = ByteBuffer.wrap(context).getInt();
            System.out.println("Please pay your cell phone bill of " + amountToPay);
        }
        return CompletableFuture.completedFuture(true);
    }

```

<span data-ttu-id="ce691-134">Po wyzwoleniu przypomnienie hello Reliable Actors w czasie wykonywania zostaną wywołane hello `ReceiveReminderAsync`(C#) lub `receiveReminderAsync`— metoda (Java) na powitania aktora.</span><span class="sxs-lookup"><span data-stu-id="ce691-134">When a reminder is triggered, hello Reliable Actors runtime will invoke hello  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on hello Actor.</span></span> <span data-ttu-id="ce691-135">Aktora można zarejestrować wiele przypomnienia i hello `ReceiveReminderAsync`(C#) lub `receiveReminderAsync`(Java) metoda jest wywoływana po żadnego z tych przypomnienia zostanie wywołany.</span><span class="sxs-lookup"><span data-stu-id="ce691-135">An actor can register multiple reminders, and hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="ce691-136">aktora Hello można używać nazwy monitu hello jest przekazywany w toohello `ReceiveReminderAsync`(C#) lub `receiveReminderAsync`się, które zostało wyzwolone monitu toofigure — metoda (Java).</span><span class="sxs-lookup"><span data-stu-id="ce691-136">hello actor can use hello reminder name that is passed in toohello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method toofigure out which reminder was triggered.</span></span>

<span data-ttu-id="ce691-137">Hello środowiska uruchomieniowego podmiotów zapisuje stanu aktora hello, gdy hello `ReceiveReminderAsync`(C#) lub `receiveReminderAsync`zakończeniu wywołania (Java).</span><span class="sxs-lookup"><span data-stu-id="ce691-137">hello Actors runtime saves hello actor's state when hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="ce691-138">Jeśli wystąpi błąd podczas zapisywania stanu hello, ten obiekt aktora spowoduje wyłączenie i nowe wystąpienie zostanie aktywowany.</span><span class="sxs-lookup"><span data-stu-id="ce691-138">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="ce691-139">toounregister przypomnienie aktora wywołuje hello `UnregisterReminderAsync`(C#) lub `unregisterReminderAsync`— metoda (Java), jak pokazano w poniższych przykładach hello.</span><span class="sxs-lookup"><span data-stu-id="ce691-139">toounregister a reminder, an actor calls hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in hello examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="ce691-140">Jak pokazano powyżej, hello `UnregisterReminderAsync`(C#) lub `unregisterReminderAsync`— metoda (Java) akceptuje `IActorReminder`(C#) lub `ActorReminder`interfejsu (Java).</span><span class="sxs-lookup"><span data-stu-id="ce691-140">As shown above, hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="ce691-141">Witaj obsługuje klasy podstawowej aktora `GetReminder`(C#) lub `getReminder`— metoda (Java), które mogą być używane tooretrieve hello `IActorReminder`(C#) lub `ActorReminder`interfejsu (Java) przez przekazywanie hello przypomnienia o nazwie.</span><span class="sxs-lookup"><span data-stu-id="ce691-141">hello actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used tooretrieve hello `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in hello reminder name.</span></span> <span data-ttu-id="ce691-142">Jest to wygodny, ponieważ aktora hello nie jest konieczne toopersist hello `IActorReminder`(C#) lub `ActorReminder`interfejsu (Java), który został zwrócony z hello `RegisterReminder`(C#) lub `registerReminder`wywołanie metody (Java).</span><span class="sxs-lookup"><span data-stu-id="ce691-142">This is convenient because hello actor does not need toopersist hello `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from hello `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce691-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ce691-143">Next Steps</span></span>
<span data-ttu-id="ce691-144">Więcej informacji na temat zdarzeń niezawodnego aktora i ponowne wejście:</span><span class="sxs-lookup"><span data-stu-id="ce691-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="ce691-145">Zdarzenia aktora</span><span class="sxs-lookup"><span data-stu-id="ce691-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="ce691-146">Wielobieżność aktora</span><span class="sxs-lookup"><span data-stu-id="ce691-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
