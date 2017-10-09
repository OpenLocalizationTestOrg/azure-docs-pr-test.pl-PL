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
# <a name="actor-timers-and-reminders"></a>Czasomierze aktora i przypomnieniami
Złośliwych użytkowników można zaplanować okresowe pracy od samych siebie rejestrując czasomierze lub przypomnienia. W tym artykule przedstawiono sposób toouse czasomierze i przypomnienia wraz z wyjaśnieniem hello różnice między nimi.

## <a name="actor-timers"></a>Czasomierze aktora
Czasomierze aktora zapewniają prosty otokę .NET lub Java tooensure czasomierza że metody wywołania zwrotnego hello przestrzegać gwarantuje współbieżności opartej na włączanie hello hello podmiotów zawiera środowiska wykonawczego.

Złośliwych użytkowników można używać hello `RegisterTimer`(C#) lub `registerTimer`(Java) i `UnregisterTimer`(C#) lub `unregisterTimer`metody (Java) na ich podstawie klasy tooregister i ich czasomierze wyrejestrować. Witaj w poniższym przykładzie pokazano sposób użycia hello czasomierza interfejsów API. Hello interfejsy API są bardzo podobne czasomierza .NET toohello lub Java czasomierza. W tym przykładzie, gdy czasomierza hello jest wymagany, hello złośliwych użytkowników w czasie wykonywania będzie wywoływać hello `MoveObject`(C#) lub `moveObject`— metoda (Java). Metoda Hello jest gwarantowana toorespect hello Włącz współbieżności oparta na wątkach. Oznacza to, że nie ma innych metod aktora lub wywołania zwrotne czasomierza/monitu będzie w toku zakończenia wykonywania tego wywołania zwrotnego.

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

Hello następnego okresu czasomierza hello rozpoczyna się po wywołania zwrotnego hello zakończeniem wykonywania. Oznacza to, że czasomierza hello jest zatrzymana podczas wywołania zwrotnego hello jest wykonywany i została uruchomiona po zakończeniu wywołania zwrotnego hello.

środowisko uruchomieniowe podmiotów Hello zapisuje zmiany wprowadzone Menedżer stanu aktora toohello, po zakończeniu hello wywołania zwrotnego. Jeśli wystąpi błąd podczas zapisywania stanu hello, ten obiekt aktora spowoduje wyłączenie i nowe wystąpienie zostanie aktywowany.

Zatrzymuje wszystkie czasomierze aktora hello jest dezaktywowana w ramach operacji wyrzucania elementów bezużytecznych. Nie wywołania zwrotne czasomierza są wywoływane po tym. Ponadto hello złośliwych użytkowników w czasie wykonywania nie zachowuje żadnych informacji o hello czasomierzy, które były uruchomione przed dezaktywacji. Jest zapasowej tooregister aktora toohello żadnych czasomierzy, które wymaga uaktwnieniu w przyszłości hello. Aby uzyskać więcej informacji, zobacz sekcję hello na [aktora wyrzucanie elementów bezużytecznych](service-fabric-reliable-actors-lifecycle.md).

## <a name="actor-reminders"></a>Przypomnienia aktora
Przypomnienia są tootrigger mechanizmu trwałe wywołań zwrotnych na aktora w określonych godzinach. Ich funkcje są podobne tootimers. Jednak w przeciwieństwie do czasomierze, przypomnienia są wyzwalane we wszystkich okolicznościach, aż do ich wyrejestrowuje jawnie aktora hello lub aktora hello jest jawnie usunięte. W szczególności przypomnienia są wyzwalane przez aktora deactivations i tryb failover, ponieważ hello złośliwych użytkowników w czasie wykonywania będzie nadal występował, informacje o przypomnienia hello aktora.

tooregister przypomnienie aktora wywołuje hello `RegisterReminderAsync` metoda w klasie podstawowej hello, jak pokazano w hello poniższy przykład:

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

W tym przykładzie `"Pay cell phone bill"` jest nazwą monitu hello. Jest to ciąg hello używa aktora toouniquely zidentyfikować przypomnienia. `BitConverter.GetBytes(amountInDollars)`(C#) jest kontekstem hello, który jest skojarzony z hello monitu. Zostanie przekazana aktora wstecz toohello jako argument toohello monitu wywołania zwrotnego, tj. `IRemindable.ReceiveReminderAsync`(C#) lub `Remindable.receiveReminderAsync`(Java).

Aktorów używających przypomnienia muszą implementować hello `IRemindable` interfejsu, jak pokazano w poniższym przykładzie hello.

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

Po wyzwoleniu przypomnienie hello Reliable Actors w czasie wykonywania zostaną wywołane hello `ReceiveReminderAsync`(C#) lub `receiveReminderAsync`— metoda (Java) na powitania aktora. Aktora można zarejestrować wiele przypomnienia i hello `ReceiveReminderAsync`(C#) lub `receiveReminderAsync`(Java) metoda jest wywoływana po żadnego z tych przypomnienia zostanie wywołany. aktora Hello można używać nazwy monitu hello jest przekazywany w toohello `ReceiveReminderAsync`(C#) lub `receiveReminderAsync`się, które zostało wyzwolone monitu toofigure — metoda (Java).

Hello środowiska uruchomieniowego podmiotów zapisuje stanu aktora hello, gdy hello `ReceiveReminderAsync`(C#) lub `receiveReminderAsync`zakończeniu wywołania (Java). Jeśli wystąpi błąd podczas zapisywania stanu hello, ten obiekt aktora spowoduje wyłączenie i nowe wystąpienie zostanie aktywowany.

toounregister przypomnienie aktora wywołuje hello `UnregisterReminderAsync`(C#) lub `unregisterReminderAsync`— metoda (Java), jak pokazano w poniższych przykładach hello.

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

Jak pokazano powyżej, hello `UnregisterReminderAsync`(C#) lub `unregisterReminderAsync`— metoda (Java) akceptuje `IActorReminder`(C#) lub `ActorReminder`interfejsu (Java). Witaj obsługuje klasy podstawowej aktora `GetReminder`(C#) lub `getReminder`— metoda (Java), które mogą być używane tooretrieve hello `IActorReminder`(C#) lub `ActorReminder`interfejsu (Java) przez przekazywanie hello przypomnienia o nazwie. Jest to wygodny, ponieważ aktora hello nie jest konieczne toopersist hello `IActorReminder`(C#) lub `ActorReminder`interfejsu (Java), który został zwrócony z hello `RegisterReminder`(C#) lub `registerReminder`wywołanie metody (Java).

## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat zdarzeń niezawodnego aktora i ponowne wejście:
* [Zdarzenia aktora](service-fabric-reliable-actors-events.md)
* [Wielobieżność aktora](service-fabric-reliable-actors-reentrancy.md)
