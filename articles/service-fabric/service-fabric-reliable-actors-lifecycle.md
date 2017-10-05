---
title: "Przegląd cyklu życia na podstawie aktora Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Wyjaśniono niezawodnego aktora sieci szkieletowej usługi cyklu życia, wyrzucanie elementów bezużytecznych i ręcznego usuwania złośliwych użytkowników i ich stan"
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: 75b7b77a0bef2051599a4f61183109cfb2ffff3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="6ae1d-103">Cykl życia aktora, automatyczne wyrzucanie elementów bezużytecznych i ręcznego usuwania</span><span class="sxs-lookup"><span data-stu-id="6ae1d-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="6ae1d-104">Aktor jest uaktywniany przy pierwszym uruchomieniu połączenie jest nawiązywane w przypadku dowolnej metody.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-104">An actor is activated the first time a call is made to any of its methods.</span></span> <span data-ttu-id="6ae1d-105">Aktor jest dezaktywowany (odzyskiwanie zebranych przez środowisko uruchomieniowe złośliwych użytkowników), jeśli nie jest on używany przez można skonfigurować czas.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-105">An actor is deactivated (garbage collected by the Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="6ae1d-106">Aktor i stanu można również zostaną usunięte ręcznie w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="6ae1d-107">Aktywacja aktora</span><span class="sxs-lookup"><span data-stu-id="6ae1d-107">Actor activation</span></span>
<span data-ttu-id="6ae1d-108">Po uaktywnieniu aktora są następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="6ae1d-108">When an actor is activated, the following occurs:</span></span>

* <span data-ttu-id="6ae1d-109">Wywołanie jest dostępna dla aktora i jeszcze nie została active, nowe aktora zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="6ae1d-110">Stanu aktora jest ładowana, jeśli jest zachowanie stanu.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-110">The actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="6ae1d-111">`OnActivateAsync` (C#) lub `onActivateAsync` wywołanie metody (Java) (która może zostać zastąpiona w celu wykonania aktora).</span><span class="sxs-lookup"><span data-stu-id="6ae1d-111">The `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span>
* <span data-ttu-id="6ae1d-112">Aktor teraz jest traktowane jako aktywne.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-112">The actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="6ae1d-113">Dezaktywacja aktora</span><span class="sxs-lookup"><span data-stu-id="6ae1d-113">Actor deactivation</span></span>
<span data-ttu-id="6ae1d-114">Gdy aktora jest dezaktywowany, są następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="6ae1d-114">When an actor is deactivated, the following occurs:</span></span>

* <span data-ttu-id="6ae1d-115">Gdy aktora nie jest używany przez niektóre czas, zostanie ono usunięte z tabeli aktywnych złośliwych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-115">When an actor is not used for some period of time, it is removed from the Active Actors table.</span></span>
* <span data-ttu-id="6ae1d-116">`OnDeactivateAsync` (C#) lub `onDeactivateAsync` wywołanie metody (Java) (która może zostać zastąpiona w celu wykonania aktora).</span><span class="sxs-lookup"><span data-stu-id="6ae1d-116">The `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span> <span data-ttu-id="6ae1d-117">Czyści wszystkie czasomierze aktora.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-117">This clears all the timers for the actor.</span></span> <span data-ttu-id="6ae1d-118">Aktora operacji, takich jak stan, jaki zmiany nie powinna być wywoływana z tej metody.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="6ae1d-119">Środowisko uruchomieniowe sieci szkieletowej podmiotów emituje niektóre [zdarzenia związane z aktorem Aktywacja i dezaktywacja](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="6ae1d-119">The Fabric Actors runtime emits some [events related to actor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="6ae1d-120">Są one przydatne w Diagnostyka i monitorowanie wydajności.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="6ae1d-121">Aktora wyrzucanie elementów bezużytecznych</span><span class="sxs-lookup"><span data-stu-id="6ae1d-121">Actor garbage collection</span></span>
<span data-ttu-id="6ae1d-122">Gdy aktora jest dezaktywowana, odwołania do obiektu aktora są wydawane i może być bezużytecznych zwykle przez środowisko uruchomieniowe języka wspólnego (CLR) lub moduł zbierający elementy bezużyteczne programu java (JVM). maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-122">When an actor is deactivated, references to the actor object are released and it can be garbage collected normally by the common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="6ae1d-123">Wyrzucanie elementów bezużytecznych tylko czyści obiektu aktora. robi **nie** usunąć stan przechowywane w Menedżerze stanu aktora.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-123">Garbage collection only cleans up the actor object; it does **not** remove state stored in the actor's State Manager.</span></span> <span data-ttu-id="6ae1d-124">Przy następnym aktora jest aktywna, tworzony jest nowy obiekt aktora i jej przywróceniu.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-124">The next time the actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="6ae1d-125">Co to jest traktowana jako "jest używane" na potrzeby dezaktywacji i wyrzucanie elementów bezużytecznych?</span><span class="sxs-lookup"><span data-stu-id="6ae1d-125">What counts as “being used” for the purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="6ae1d-126">Odbieranie wywołania</span><span class="sxs-lookup"><span data-stu-id="6ae1d-126">Receiving a call</span></span>
* <span data-ttu-id="6ae1d-127">`IRemindable.ReceiveReminderAsync`Metoda wywoływana (ma zastosowanie tylko wtedy, gdy aktor używa przypomnienia)</span><span class="sxs-lookup"><span data-stu-id="6ae1d-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if the actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="6ae1d-128">Jeśli aktora używa czasomierze i jej wywołanie zwrotne czasomierza jest wywoływana, nie **nie** liczby jako "jest używane".</span><span class="sxs-lookup"><span data-stu-id="6ae1d-128">if the actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="6ae1d-129">Przed możemy przejść do szczegółów dezaktywację, należy zdefiniować następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="6ae1d-129">Before we go into the details of deactivation, it is important to define the following terms:</span></span>

* <span data-ttu-id="6ae1d-130">*Interwał skanowania*.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-130">*Scan interval*.</span></span> <span data-ttu-id="6ae1d-131">Jest to interwał, jaką środowiska uruchomieniowego podmiotów skanowania tabeli aktywnych uczestników osób, które można dezaktywować i w ramach odzyskiwania pamięci.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-131">This is the interval at which the Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="6ae1d-132">Wartość domyślna to to 1 minuta.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-132">The default value for this is 1 minute.</span></span>
* <span data-ttu-id="6ae1d-133">*Limit czasu bezczynności*.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-133">*Idle timeout*.</span></span> <span data-ttu-id="6ae1d-134">Jest to czas, który musi pozostać nieużywane aktora (bezczynny), zanim można dezaktywować i w ramach odzyskiwania pamięci.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-134">This is the amount of time that an actor needs to remain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="6ae1d-135">Wartość domyślna to wynosi 60 min.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-135">The default value for this is 60 minutes.</span></span>

<span data-ttu-id="6ae1d-136">Zazwyczaj nie trzeba zmieniać tych wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-136">Typically, you do not need to change these defaults.</span></span> <span data-ttu-id="6ae1d-137">Jednak w razie potrzeby kolejnymi interwałami można zmienić za pomocą `ActorServiceSettings` podczas rejestrowania programu [usługi aktora](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="6ae1d-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
    }
}
```

```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
    }
}
```
<span data-ttu-id="6ae1d-138">Dla każdego aktywnego aktora środowiska uruchomieniowego aktora przechowuje informacje o czas, który był bezczynny (tj. nie jest używany).</span><span class="sxs-lookup"><span data-stu-id="6ae1d-138">For each active actor, the actor runtime keeps track of the amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="6ae1d-139">Środowisko uruchomieniowe aktora sprawdza każdego podmiotów co `ScanIntervalInSeconds` aby zobaczyć, czy może być odzyskiwanie zbierane i pobiera ją, jeśli był bezczynny `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-139">The actor runtime checks each of the actors every `ScanIntervalInSeconds` to see if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="6ae1d-140">W dowolnym momencie aktora jest używany, jego czas bezczynności jest resetowany do 0.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-140">Anytime an actor is used, its idle time is reset to 0.</span></span> <span data-ttu-id="6ae1d-141">Następnie aktora może być bezużytecznych tylko wtedy, gdy ponownie pozostanie bezczynny `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-141">After this, the actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="6ae1d-142">Odwołaj, że zostały użyte, jeśli wykonywane jest metody interfejsu aktora lub wywołania zwrotnego monitu aktora jest uznawany za aktora.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-142">Recall that an actor is considered to have been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="6ae1d-143">Aktor jest **nie** uznaje użyte, jeśli jej wywołanie zwrotne czasomierza jest wykonywane.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-143">An actor is **not** considered to have been used if its timer callback is executed.</span></span>

<span data-ttu-id="6ae1d-144">Na poniższym diagramie przedstawiono cyklem życia pojedynczego aktora w celu zilustrowania koncepcji te.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-144">The following diagram shows the lifecycle of a single actor to illustrate these concepts.</span></span>

![Przykład czas bezczynności][1]

<span data-ttu-id="6ae1d-146">W przykładzie wpływ wywołania metody aktora, przypomnienia i czasomierze na okres istnienia tego aktora.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-146">The example shows the impact of actor method calls, reminders, and timers on the lifetime of this actor.</span></span> <span data-ttu-id="6ae1d-147">Są następujące kwestie dotyczące przykładzie warto zauważyć:</span><span class="sxs-lookup"><span data-stu-id="6ae1d-147">The following points about the example are worth mentioning:</span></span>

* <span data-ttu-id="6ae1d-148">ScanInterval i IdleTimeout są ustawiane odpowiednio 5 i 10.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-148">ScanInterval and IdleTimeout are set to 5 and 10 respectively.</span></span> <span data-ttu-id="6ae1d-149">(Jednostek niezależnie od tego, ponieważ naszym celem jest tylko w celu zilustrowania koncepcji.)</span><span class="sxs-lookup"><span data-stu-id="6ae1d-149">(Units do not matter here, since our purpose is only to illustrate the concept.)</span></span>
* <span data-ttu-id="6ae1d-150">Skanowanie pod kątem uczestników jako bezużytecznych odbywa się na T = 0, 5, 10, 15, 20, 25, zgodnie z definicją interwał skanowania 5.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-150">The scan for actors to be garbage collected happens at T=0,5,10,15,20,25, as defined by the scan interval of 5.</span></span>
* <span data-ttu-id="6ae1d-151">Okresowe czasomierza wyzwala T = 4, 8, 12, 16, 20, 24, i wykonuje jej wywołanie zwrotne.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="6ae1d-152">Nie wpływa na czas bezczynności aktora.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-152">It does not impact the idle time of the actor.</span></span>
* <span data-ttu-id="6ae1d-153">Wywołanie metody aktora w T = 7 resetuje czas bezczynności, po 0 i wybrano opcję opóźnienia wyrzucanie elementów bezużytecznych aktora.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-153">An actor method call at T=7 resets the idle time to 0 and delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="6ae1d-154">Wywołanie zwrotne monitu aktora jest wykonywana co T = 14 i dalsze opóźnienia wyrzucanie elementów bezużytecznych aktora.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-154">An actor reminder callback executes at T=14 and further delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="6ae1d-155">Podczas skanowania kolekcji pamięci na T = 25 czas bezczynności aktora finally przekracza limit czasu bezczynności 10 i aktora jest bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-155">During the garbage collection scan at T=25, the actor's idle time finally exceeds the idle timeout of 10, and the actor is garbage collected.</span></span>

<span data-ttu-id="6ae1d-156">Aktor nigdy nie będą bezużytecznych podczas wykonywania jednej z metod, niezależnie od tego, ile czas podczas wykonywania tej metody.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="6ae1d-157">Jak wspomniano wcześniej, wykonywanie metod interfejsu aktora i wywołania zwrotne monitu zapobiega wyrzucanie elementów bezużytecznych resetując czas bezczynności aktora na 0.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-157">As mentioned earlier, the execution of actor interface methods and reminder callbacks prevents garbage collection by resetting the actor's idle time to 0.</span></span> <span data-ttu-id="6ae1d-158">Wykonywanie wywołań zwrotnych czasomierza nie powoduje resetowania czas bezczynności na 0.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-158">The execution of timer callbacks does not reset the idle time to 0.</span></span> <span data-ttu-id="6ae1d-159">Wyrzucanie elementów bezużytecznych aktora jest jednak opóźnione aż do zakończenia wykonywania wywołanie zwrotne czasomierza.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-159">However, the garbage collection of the actor is deferred until the timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="6ae1d-160">Usuwanie złośliwych użytkowników i ich stan</span><span class="sxs-lookup"><span data-stu-id="6ae1d-160">Deleting actors and their state</span></span>
<span data-ttu-id="6ae1d-161">Wyrzucanie elementów bezużytecznych dezaktywowane podmiotów tylko czyści obiektu aktora, ale nie powoduje usunięcia danych przechowywanych w Menedżerze stanu aktora.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-161">Garbage collection of deactivated actors only cleans up the actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="6ae1d-162">Aktor jest ponowna aktywacja, jego dane ponownie się dostępne za pośrednictwem Menedżera stanu.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-162">When an actor is re-activated, its data is again made available to it through the State Manager.</span></span> <span data-ttu-id="6ae1d-163">W przypadku gdy podmiotów przechowywania danych w Menedżerze stanu i są dezaktywowane ale nigdy aktywowany ponownie może być konieczne wyczyścić swoje dane.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary to clean up their data.</span></span>

<span data-ttu-id="6ae1d-164">[Usługi aktora](service-fabric-reliable-actors-platform.md) udostępnia funkcję usuwania złośliwych użytkowników z zdalnego procesu wywołującego:</span><span class="sxs-lookup"><span data-stu-id="6ae1d-164">The [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="6ae1d-165">Usuwanie aktora ma następujące skutki w zależności od tego, czy aktora jest obecnie aktywna:</span><span class="sxs-lookup"><span data-stu-id="6ae1d-165">Deleting an actor has the following effects depending on whether or not the actor is currently active:</span></span>

* <span data-ttu-id="6ae1d-166">**Aktywne aktora**</span><span class="sxs-lookup"><span data-stu-id="6ae1d-166">**Active Actor**</span></span>
  * <span data-ttu-id="6ae1d-167">Aktora zostanie usunięty z listy active złośliwych użytkowników, a jest nieaktywne.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="6ae1d-168">Jego stan jest trwale usunięte.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="6ae1d-169">**Nieaktywne aktora**</span><span class="sxs-lookup"><span data-stu-id="6ae1d-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="6ae1d-170">Jego stan jest trwale usunięte.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="6ae1d-171">Należy pamiętać, że nie można wywołać aktora usunąć na samym sobie z jednego z jego metody aktora, ponieważ aktora nie można usunąć podczas wykonywania w kontekście wywołań aktora, w którym środowiska uruchomieniowego uzyskał blokady wokół wymuszenia dostępu jednowątkowe wywołanie aktora.</span><span class="sxs-lookup"><span data-stu-id="6ae1d-171">Note that an actor cannot call delete on itself from one of its actor methods because the actor cannot be deleted while executing within an actor call context, in which the runtime has obtained a lock around the actor call to enforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ae1d-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ae1d-172">Next steps</span></span>
* [<span data-ttu-id="6ae1d-173">Czasomierze aktora i przypomnieniami</span><span class="sxs-lookup"><span data-stu-id="6ae1d-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="6ae1d-174">Zdarzenia aktora</span><span class="sxs-lookup"><span data-stu-id="6ae1d-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="6ae1d-175">Wielobieżność aktora</span><span class="sxs-lookup"><span data-stu-id="6ae1d-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="6ae1d-176">Aktora Diagnostyka i monitorowanie wydajności</span><span class="sxs-lookup"><span data-stu-id="6ae1d-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="6ae1d-177">Dokumentację referencyjną aktora interfejsu API</span><span class="sxs-lookup"><span data-stu-id="6ae1d-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="6ae1d-178">C# przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="6ae1d-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="6ae1d-179">Java przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="6ae1d-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
