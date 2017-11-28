---
title: "Niezawodne czasomierze złośliwych użytkowników i przypomnieniami | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do czasomierze i przypomnienia dla elementów Reliable Actors sieci szkieletowej usług."
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
ms.openlocfilehash: 06b026ce06e0f16a77ac238de0af2263f272933c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="585e8-103">Czasomierze aktora i przypomnieniami</span><span class="sxs-lookup"><span data-stu-id="585e8-103">Actor timers and reminders</span></span>
<span data-ttu-id="585e8-104">Złośliwych użytkowników można zaplanować okresowe pracy od samych siebie rejestrując czasomierze lub przypomnienia.</span><span class="sxs-lookup"><span data-stu-id="585e8-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="585e8-105">W tym artykule przedstawiono sposób użycia czasomierze i przypomnieniami i wyjaśniono różnice między nimi.</span><span class="sxs-lookup"><span data-stu-id="585e8-105">This article shows how to use timers and reminders and explains the differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="585e8-106">Czasomierze aktora</span><span class="sxs-lookup"><span data-stu-id="585e8-106">Actor timers</span></span>
<span data-ttu-id="585e8-107">Czasomierze aktora zapewniają prosty otokę .NET lub Java czasomierza aby upewnić się, że metody wywołania zwrotnego przestrzegać współbieżności opartej na włączanie gwarantuje, że runtime podmiotów zawiera.</span><span class="sxs-lookup"><span data-stu-id="585e8-107">Actor timers provide a simple wrapper around a .NET or Java timer to ensure that the callback methods respect the turn-based concurrency guarantees that the Actors runtime provides.</span></span>

<span data-ttu-id="585e8-108">Można użyć złośliwych użytkowników `RegisterTimer`(C#) lub `registerTimer`(Java) i `UnregisterTimer`(C#) lub `unregisterTimer`metod klasy podstawowej umożliwia rejestrowanie i wyrejestrowywanie ich czasomierze (Java).</span><span class="sxs-lookup"><span data-stu-id="585e8-108">Actors can use the `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class to register and unregister their timers.</span></span> <span data-ttu-id="585e8-109">W poniższym przykładzie pokazano sposób użycia czasomierza interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="585e8-109">The example below shows the use of timer APIs.</span></span> <span data-ttu-id="585e8-110">Interfejsy API są bardzo podobne do czasomierz .NET lub Java czasomierza.</span><span class="sxs-lookup"><span data-stu-id="585e8-110">The APIs are very similar to the .NET timer or Java timer.</span></span> <span data-ttu-id="585e8-111">W tym przykładzie, gdy zegar jest wymagany, środowiska uruchomieniowego podmiotów wywoła `MoveObject`(C#) lub `moveObject`— metoda (Java).</span><span class="sxs-lookup"><span data-stu-id="585e8-111">In this example, when the timer is due, the Actors runtime will call the `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="585e8-112">Metoda jest gwarantowana przestrzegać współbieżności opartej na ruch.</span><span class="sxs-lookup"><span data-stu-id="585e8-112">The method is guaranteed to respect the turn-based concurrency.</span></span> <span data-ttu-id="585e8-113">Oznacza to, że nie ma innych metod aktora lub wywołania zwrotne czasomierza/monitu będzie w toku zakończenia wykonywania tego wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="585e8-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

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
            null,                           // Parameter to pass to the callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time to delay before the callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of the callback method

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
                            null,                                             // Parameter to pass to the callback method
                            Duration.ofMillis(10),                            // Amount of time to delay before the callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of the callback method
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

<span data-ttu-id="585e8-114">Następnym okresie czasomierza rozpoczyna się wykonanie zakończone wywołanie zwrotne.</span><span class="sxs-lookup"><span data-stu-id="585e8-114">The next period of the timer starts after the callback completes execution.</span></span> <span data-ttu-id="585e8-115">Oznacza to, że zegar jest zatrzymywany podczas wywołania zwrotnego jest wykonywany i została uruchomiona po zakończeniu wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="585e8-115">This implies that the timer is stopped while the callback is executing and is started when the callback finishes.</span></span>

<span data-ttu-id="585e8-116">Środowisko uruchomieniowe podmiotów zapisuje zmiany wprowadzone Menedżer stanu aktora po zakończeniu wywołania zwrotnego.</span><span class="sxs-lookup"><span data-stu-id="585e8-116">The Actors runtime saves changes made to the actor's State Manager when the callback finishes.</span></span> <span data-ttu-id="585e8-117">Jeśli wystąpi błąd podczas zapisywania stanu, ten obiekt aktora spowoduje wyłączenie i nowe wystąpienie zostanie aktywowany.</span><span class="sxs-lookup"><span data-stu-id="585e8-117">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="585e8-118">Zatrzymuje wszystkie czasomierze aktora jest dezaktywowana w ramach operacji wyrzucania elementów bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="585e8-118">All timers are stopped when the actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="585e8-119">Nie wywołania zwrotne czasomierza są wywoływane po tym.</span><span class="sxs-lookup"><span data-stu-id="585e8-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="585e8-120">Ponadto środowiska uruchomieniowego złośliwych użytkowników nie zachowuje żadnych informacji o czasomierzy, które były uruchomione przed dezaktywacji.</span><span class="sxs-lookup"><span data-stu-id="585e8-120">Also, the Actors runtime does not retain any information about the timers that were running before deactivation.</span></span> <span data-ttu-id="585e8-121">Jest aktora, aby zarejestrować wszelkie czasomierzy, które wymaga uaktwnieniu go w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="585e8-121">It is up to the actor to register any timers that it needs when it is reactivated in the future.</span></span> <span data-ttu-id="585e8-122">Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [aktora wyrzucanie elementów bezużytecznych](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="585e8-122">For more information, see the section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="585e8-123">Przypomnienia aktora</span><span class="sxs-lookup"><span data-stu-id="585e8-123">Actor reminders</span></span>
<span data-ttu-id="585e8-124">Przypomnienia są mechanizm umożliwiający wyzwalanie trwałe wywołań zwrotnych na aktora w określonych godzinach.</span><span class="sxs-lookup"><span data-stu-id="585e8-124">Reminders are a mechanism to trigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="585e8-125">Czasomierze odpowiada ich funkcje.</span><span class="sxs-lookup"><span data-stu-id="585e8-125">Their functionality is similar to timers.</span></span> <span data-ttu-id="585e8-126">Jednak w przeciwieństwie do czasomierze, przypomnienia są wyzwalane we wszystkich okolicznościach, dopóki aktora jawnie wyrejestrowuje je lub aktora jest jawnie usunięte.</span><span class="sxs-lookup"><span data-stu-id="585e8-126">But unlike timers, reminders are triggered under all circumstances until the actor explicitly unregisters them or the actor is explicitly deleted.</span></span> <span data-ttu-id="585e8-127">W szczególności przypomnienia są wyzwalane przez aktora deactivations i tryb failover, ponieważ środowisko uruchomieniowe złośliwych użytkowników będzie się powtarzał informacji na temat przypomnienia aktora.</span><span class="sxs-lookup"><span data-stu-id="585e8-127">Specifically, reminders are triggered across actor deactivations and failovers because the Actors runtime persists information about the actor's reminders.</span></span>

<span data-ttu-id="585e8-128">Aby zarejestrować przypomnienie, wywołuje aktora `RegisterReminderAsync` metoda w klasie podstawowej, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="585e8-128">To register a reminder, an actor calls the `RegisterReminderAsync` method provided on the base class, as shown in the following example:</span></span>

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
            dueTime,    //The amount of time to delay before firing the reminder
            period);    //The time interval between firing of reminders
}
```

<span data-ttu-id="585e8-129">W tym przykładzie `"Pay cell phone bill"` jest nazwą monitu.</span><span class="sxs-lookup"><span data-stu-id="585e8-129">In this example, `"Pay cell phone bill"` is the reminder name.</span></span> <span data-ttu-id="585e8-130">Jest to ciąg, który aktora używany do jednoznacznego identyfikowania przypomnienia.</span><span class="sxs-lookup"><span data-stu-id="585e8-130">This is a string that the actor uses to uniquely identify a reminder.</span></span> <span data-ttu-id="585e8-131">`BitConverter.GetBytes(amountInDollars)`(C#) jest kontekstem, który jest skojarzony z monitu.</span><span class="sxs-lookup"><span data-stu-id="585e8-131">`BitConverter.GetBytes(amountInDollars)`(C#) is the context that is associated with the reminder.</span></span> <span data-ttu-id="585e8-132">Go zostaną przekazane do aktora jako argument do wywołania zwrotnego monitu, tj. `IRemindable.ReceiveReminderAsync`(C#) lub `Remindable.receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="585e8-132">It will be passed back to the actor as an argument to the reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="585e8-133">Aktorów używających przypomnienia muszą implementować `IRemindable` interfejsu, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="585e8-133">Actors that use reminders must implement the `IRemindable` interface, as shown in the example below.</span></span>

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

<span data-ttu-id="585e8-134">Po wyzwoleniu przypomnienie wywoła środowisko uruchomieniowe Reliable Actors `ReceiveReminderAsync`(C#) lub `receiveReminderAsync`(Java) metoda aktora.</span><span class="sxs-lookup"><span data-stu-id="585e8-134">When a reminder is triggered, the Reliable Actors runtime will invoke the  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on the Actor.</span></span> <span data-ttu-id="585e8-135">Aktora można zarejestrować wiele przypomnienia i `ReceiveReminderAsync`(C#) lub `receiveReminderAsync`(Java) metoda jest wywoływana po żadnego z tych przypomnienia wyzwoleniu.</span><span class="sxs-lookup"><span data-stu-id="585e8-135">An actor can register multiple reminders, and the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="585e8-136">Aktor można użyć nazwy monitu, który jest przekazywany do `ReceiveReminderAsync`(C#) lub `receiveReminderAsync`— metoda (Java), aby dowiedzieć się, które monitu zostało wyzwolone.</span><span class="sxs-lookup"><span data-stu-id="585e8-136">The actor can use the reminder name that is passed in to the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method to figure out which reminder was triggered.</span></span>

<span data-ttu-id="585e8-137">Podmiotów środowiska uruchomieniowego zapisuje aktora stan, kiedy `ReceiveReminderAsync`(C#) lub `receiveReminderAsync`zakończeniu wywołania (Java).</span><span class="sxs-lookup"><span data-stu-id="585e8-137">The Actors runtime saves the actor's state when the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="585e8-138">Jeśli wystąpi błąd podczas zapisywania stanu, ten obiekt aktora spowoduje wyłączenie i nowe wystąpienie zostanie aktywowany.</span><span class="sxs-lookup"><span data-stu-id="585e8-138">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="585e8-139">Wyrejestrować przypomnienie, wywołuje aktora `UnregisterReminderAsync`(C#) lub `unregisterReminderAsync`— metoda (Java), jak pokazano w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="585e8-139">To unregister a reminder, an actor calls the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in the examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="585e8-140">Jak pokazano powyżej, `UnregisterReminderAsync`(C#) lub `unregisterReminderAsync`— metoda (Java) akceptuje `IActorReminder`(C#) lub `ActorReminder`interfejsu (Java).</span><span class="sxs-lookup"><span data-stu-id="585e8-140">As shown above, the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="585e8-141">Obsługuje klasy podstawowej aktora `GetReminder`(C#) lub `getReminder`— metoda (Java), który może służyć do pobierania `IActorReminder`(C#) lub `ActorReminder`interfejsu (Java), przekazując w nazwie monitu.</span><span class="sxs-lookup"><span data-stu-id="585e8-141">The actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used to retrieve the `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in the reminder name.</span></span> <span data-ttu-id="585e8-142">Jest to wygodna, ponieważ aktora nie potrzeba utrwalenia `IActorReminder`(C#) lub `ActorReminder`interfejsu (Java), który został zwrócony z `RegisterReminder`(C#) lub `registerReminder`wywołanie metody (Java).</span><span class="sxs-lookup"><span data-stu-id="585e8-142">This is convenient because the actor does not need to persist the `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from the `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="585e8-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="585e8-143">Next Steps</span></span>
<span data-ttu-id="585e8-144">Więcej informacji na temat zdarzeń niezawodnego aktora i ponowne wejście:</span><span class="sxs-lookup"><span data-stu-id="585e8-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="585e8-145">Zdarzenia aktora</span><span class="sxs-lookup"><span data-stu-id="585e8-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="585e8-146">Wielobieżność aktora</span><span class="sxs-lookup"><span data-stu-id="585e8-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
