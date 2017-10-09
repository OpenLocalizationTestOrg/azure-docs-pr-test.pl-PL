---
title: "aaaOverview życia na podstawie aktora Azure mikrousług | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="6a656-103">Cykl życia aktora, automatyczne wyrzucanie elementów bezużytecznych i ręcznego usuwania</span><span class="sxs-lookup"><span data-stu-id="6a656-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="6a656-104">Aktor jest uaktywniany hello po raz pierwszy tooany metody jest nawiązane połączenie.</span><span class="sxs-lookup"><span data-stu-id="6a656-104">An actor is activated hello first time a call is made tooany of its methods.</span></span> <span data-ttu-id="6a656-105">Aktor jest dezaktywowany (zebranych przez środowisko uruchomieniowe podmiotów hello pamięci), jeśli nie jest on używany przez można skonfigurować czas.</span><span class="sxs-lookup"><span data-stu-id="6a656-105">An actor is deactivated (garbage collected by hello Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="6a656-106">Aktor i stanu można również zostaną usunięte ręcznie w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="6a656-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="6a656-107">Aktywacja aktora</span><span class="sxs-lookup"><span data-stu-id="6a656-107">Actor activation</span></span>
<span data-ttu-id="6a656-108">Po uaktywnieniu aktora występuje hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6a656-108">When an actor is activated, hello following occurs:</span></span>

* <span data-ttu-id="6a656-109">Wywołanie jest dostępna dla aktora i jeszcze nie została active, nowe aktora zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="6a656-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="6a656-110">stanu aktora Hello jest ładowana, jeśli jest zachowanie stanu.</span><span class="sxs-lookup"><span data-stu-id="6a656-110">hello actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="6a656-111">Witaj `OnActivateAsync` (C#) lub `onActivateAsync` wywołanie metody (Java) (która może zostać zastąpiona w celu wykonania aktora hello).</span><span class="sxs-lookup"><span data-stu-id="6a656-111">hello `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span>
* <span data-ttu-id="6a656-112">Witaj aktora teraz jest traktowane jako aktywne.</span><span class="sxs-lookup"><span data-stu-id="6a656-112">hello actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="6a656-113">Dezaktywacja aktora</span><span class="sxs-lookup"><span data-stu-id="6a656-113">Actor deactivation</span></span>
<span data-ttu-id="6a656-114">Po dezaktywacji aktora hello rejestrowany:</span><span class="sxs-lookup"><span data-stu-id="6a656-114">When an actor is deactivated, hello following occurs:</span></span>

* <span data-ttu-id="6a656-115">Gdy aktora nie jest używany przez niektóre czas, zostanie ono usunięte z tabeli aktywnych uczestników hello.</span><span class="sxs-lookup"><span data-stu-id="6a656-115">When an actor is not used for some period of time, it is removed from hello Active Actors table.</span></span>
* <span data-ttu-id="6a656-116">Witaj `OnDeactivateAsync` (C#) lub `onDeactivateAsync` wywołanie metody (Java) (która może zostać zastąpiona w celu wykonania aktora hello).</span><span class="sxs-lookup"><span data-stu-id="6a656-116">hello `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span> <span data-ttu-id="6a656-117">Czyści wszystkie czasomierze hello na powitania aktora.</span><span class="sxs-lookup"><span data-stu-id="6a656-117">This clears all hello timers for hello actor.</span></span> <span data-ttu-id="6a656-118">Aktora operacji, takich jak stan, jaki zmiany nie powinna być wywoływana z tej metody.</span><span class="sxs-lookup"><span data-stu-id="6a656-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="6a656-119">Witaj środowisko uruchomieniowe sieci szkieletowej podmiotów emituje niektóre [zdarzenia związane z tooactor Aktywacja i dezaktywacja](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="6a656-119">hello Fabric Actors runtime emits some [events related tooactor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="6a656-120">Są one przydatne w Diagnostyka i monitorowanie wydajności.</span><span class="sxs-lookup"><span data-stu-id="6a656-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="6a656-121">Aktora wyrzucanie elementów bezużytecznych</span><span class="sxs-lookup"><span data-stu-id="6a656-121">Actor garbage collection</span></span>
<span data-ttu-id="6a656-122">Po dezaktywacji aktora obiektu aktora toohello odwołania są wydawane i może być bezużytecznych zwykle hello środowisko uruchomieniowe języka wspólnego (CLR) lub moduł zbierający elementy bezużyteczne programu java (JVM). maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6a656-122">When an actor is deactivated, references toohello actor object are released and it can be garbage collected normally by hello common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="6a656-123">Wyrzucanie elementów bezużytecznych tylko czyści hello obiektu aktora. robi **nie** usunąć stan przechowywane w Menedżerze stanu aktora hello.</span><span class="sxs-lookup"><span data-stu-id="6a656-123">Garbage collection only cleans up hello actor object; it does **not** remove state stored in hello actor's State Manager.</span></span> <span data-ttu-id="6a656-124">uaktywnieniu aktora hello czas następnego Hello, tworzony jest nowy obiekt aktora i jej przywróceniu.</span><span class="sxs-lookup"><span data-stu-id="6a656-124">hello next time hello actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="6a656-125">Co to jest traktowana jako "jest używane" hello w celu dezaktywacji i wyrzucanie elementów bezużytecznych?</span><span class="sxs-lookup"><span data-stu-id="6a656-125">What counts as “being used” for hello purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="6a656-126">Odbieranie wywołania</span><span class="sxs-lookup"><span data-stu-id="6a656-126">Receiving a call</span></span>
* <span data-ttu-id="6a656-127">`IRemindable.ReceiveReminderAsync`Metoda wywoływana (ma zastosowanie tylko wtedy, gdy aktora hello używa przypomnienia)</span><span class="sxs-lookup"><span data-stu-id="6a656-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if hello actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="6a656-128">Jeśli aktora hello używa czasomierze i jej wywołanie zwrotne czasomierza jest wywoływana, nie **nie** liczby jako "jest używane".</span><span class="sxs-lookup"><span data-stu-id="6a656-128">if hello actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="6a656-129">Przed możemy przejść do szczegółów hello dezaktywację, jest ważne toodefine hello następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="6a656-129">Before we go into hello details of deactivation, it is important toodefine hello following terms:</span></span>

* <span data-ttu-id="6a656-130">*Interwał skanowania*.</span><span class="sxs-lookup"><span data-stu-id="6a656-130">*Scan interval*.</span></span> <span data-ttu-id="6a656-131">Jest to interwał powitania, w których hello podmiotów środowiska uruchomieniowego skanuje jego tabeli aktywnych uczestników osób, które można dezaktywować i w ramach odzyskiwania pamięci.</span><span class="sxs-lookup"><span data-stu-id="6a656-131">This is hello interval at which hello Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="6a656-132">Witaj wartość domyślna to to 1 minuta.</span><span class="sxs-lookup"><span data-stu-id="6a656-132">hello default value for this is 1 minute.</span></span>
* <span data-ttu-id="6a656-133">*Limit czasu bezczynności*.</span><span class="sxs-lookup"><span data-stu-id="6a656-133">*Idle timeout*.</span></span> <span data-ttu-id="6a656-134">Jest to hello ilość czasu, że aktora wymaga tooremain nieużywane (bezczynny), zanim można dezaktywować i w ramach odzyskiwania pamięci.</span><span class="sxs-lookup"><span data-stu-id="6a656-134">This is hello amount of time that an actor needs tooremain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="6a656-135">Witaj wartość domyślna to wynosi 60 min.</span><span class="sxs-lookup"><span data-stu-id="6a656-135">hello default value for this is 60 minutes.</span></span>

<span data-ttu-id="6a656-136">Zazwyczaj nie trzeba toochange tych wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="6a656-136">Typically, you do not need toochange these defaults.</span></span> <span data-ttu-id="6a656-137">Jednak w razie potrzeby kolejnymi interwałami można zmienić za pomocą `ActorServiceSettings` podczas rejestrowania programu [usługi aktora](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="6a656-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

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
<span data-ttu-id="6a656-138">Dla każdego aktywnego aktora środowiska uruchomieniowego aktora hello przechowuje informacje o hello ilość czasu, który był bezczynny (tj. nie jest używany).</span><span class="sxs-lookup"><span data-stu-id="6a656-138">For each active actor, hello actor runtime keeps track of hello amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="6a656-139">środowisko uruchomieniowe aktora Hello sprawdza wszystkich podmiotów hello co `ScanIntervalInSeconds` toosee Jeśli pamięci może być zbierane i pobiera ją, jeśli był bezczynny `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="6a656-139">hello actor runtime checks each of hello actors every `ScanIntervalInSeconds` toosee if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="6a656-140">W dowolnym momencie aktora jest używany, jego czas bezczynności jest too0 resetowania.</span><span class="sxs-lookup"><span data-stu-id="6a656-140">Anytime an actor is used, its idle time is reset too0.</span></span> <span data-ttu-id="6a656-141">Po tym aktora hello może być bezużytecznych tylko wtedy, gdy ponownie pozostanie bezczynny `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="6a656-141">After this, hello actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="6a656-142">Odwołaj się, że aktora jest uznawany za toohave zostały użyte, jeśli wykonywane jest metody interfejsu aktora lub wywołania zwrotnego monitu aktora.</span><span class="sxs-lookup"><span data-stu-id="6a656-142">Recall that an actor is considered toohave been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="6a656-143">Aktor jest **nie** uznawane za toohave zostały użyte, jeśli jej wywołanie zwrotne czasomierza jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="6a656-143">An actor is **not** considered toohave been used if its timer callback is executed.</span></span>

<span data-ttu-id="6a656-144">Witaj Poniższy diagram przedstawia hello cyklem życia tooillustrate pojedynczego aktora te pojęcia.</span><span class="sxs-lookup"><span data-stu-id="6a656-144">hello following diagram shows hello lifecycle of a single actor tooillustrate these concepts.</span></span>

![Przykład czas bezczynności][1]

<span data-ttu-id="6a656-146">przykład Witaj zawiera wpływ hello wywołania metody aktora, przypomnienia i czasomierze hello okres istnienia tego aktora.</span><span class="sxs-lookup"><span data-stu-id="6a656-146">hello example shows hello impact of actor method calls, reminders, and timers on hello lifetime of this actor.</span></span> <span data-ttu-id="6a656-147">następujące kwestie dotyczące przykład Witaj Hello są warto zauważyć:</span><span class="sxs-lookup"><span data-stu-id="6a656-147">hello following points about hello example are worth mentioning:</span></span>

* <span data-ttu-id="6a656-148">ScanInterval IdleTimeout są ustawione i too5 i 10 odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="6a656-148">ScanInterval and IdleTimeout are set too5 and 10 respectively.</span></span> <span data-ttu-id="6a656-149">(Jednostek niezależnie od tego, ponieważ naszym celem jest tylko koncepcji hello tooillustrate.)</span><span class="sxs-lookup"><span data-stu-id="6a656-149">(Units do not matter here, since our purpose is only tooillustrate hello concept.)</span></span>
* <span data-ttu-id="6a656-150">skanowanie Hello osób toobe bezużytecznych odbywa się na T = 0, 5, 10, 15, 20, 25, zgodnie z definicją interwał skanowania powitania 5.</span><span class="sxs-lookup"><span data-stu-id="6a656-150">hello scan for actors toobe garbage collected happens at T=0,5,10,15,20,25, as defined by hello scan interval of 5.</span></span>
* <span data-ttu-id="6a656-151">Okresowe czasomierza wyzwala T = 4, 8, 12, 16, 20, 24, i wykonuje jej wywołanie zwrotne.</span><span class="sxs-lookup"><span data-stu-id="6a656-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="6a656-152">Nie ma ona wpływu hello bezczynności hello aktora.</span><span class="sxs-lookup"><span data-stu-id="6a656-152">It does not impact hello idle time of hello actor.</span></span>
* <span data-ttu-id="6a656-153">Wywołanie metody aktora w T = 7 resetuje hello too0 czas bezczynności i wybrano opcję opóźnienia hello wyrzucanie elementów bezużytecznych z hello aktora.</span><span class="sxs-lookup"><span data-stu-id="6a656-153">An actor method call at T=7 resets hello idle time too0 and delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="6a656-154">Wykonuje wywołanie zwrotne monitu aktora w T = 14 i dalsze opóźnienia hello wyrzucanie elementów bezużytecznych hello aktora.</span><span class="sxs-lookup"><span data-stu-id="6a656-154">An actor reminder callback executes at T=14 and further delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="6a656-155">Podczas skanowania kolekcji garbage hello na T = 25 czas bezczynności aktora hello finally przekracza limit czasu bezczynności hello 10, a aktora hello jest bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="6a656-155">During hello garbage collection scan at T=25, hello actor's idle time finally exceeds hello idle timeout of 10, and hello actor is garbage collected.</span></span>

<span data-ttu-id="6a656-156">Aktor nigdy nie będą bezużytecznych podczas wykonywania jednej z metod, niezależnie od tego, ile czas podczas wykonywania tej metody.</span><span class="sxs-lookup"><span data-stu-id="6a656-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="6a656-157">Jak wspomniano wcześniej, hello wykonywanie metod interfejsu aktora i wywołania zwrotne monitu zapobiega wyrzucanie elementów bezużytecznych resetując too0 czas bezczynności hello aktora.</span><span class="sxs-lookup"><span data-stu-id="6a656-157">As mentioned earlier, hello execution of actor interface methods and reminder callbacks prevents garbage collection by resetting hello actor's idle time too0.</span></span> <span data-ttu-id="6a656-158">wykonywanie Hello wywołania zwrotne czasomierza nie powoduje resetowania hello too0 czasu bezczynności.</span><span class="sxs-lookup"><span data-stu-id="6a656-158">hello execution of timer callbacks does not reset hello idle time too0.</span></span> <span data-ttu-id="6a656-159">Jednak hello wyrzucanie elementów bezużytecznych z aktorem hello została odroczona, dopóki nie zakończy się wywołanie zwrotne czasomierza hello wykonywania.</span><span class="sxs-lookup"><span data-stu-id="6a656-159">However, hello garbage collection of hello actor is deferred until hello timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="6a656-160">Usuwanie złośliwych użytkowników i ich stan</span><span class="sxs-lookup"><span data-stu-id="6a656-160">Deleting actors and their state</span></span>
<span data-ttu-id="6a656-161">Wyrzucanie elementów bezużytecznych dezaktywowane podmiotów tylko czyści hello aktora obiektu, ale nie powoduje usunięcia danych przechowywanych w Menedżerze stanu aktora.</span><span class="sxs-lookup"><span data-stu-id="6a656-161">Garbage collection of deactivated actors only cleans up hello actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="6a656-162">Aktor jest ponowna aktywacja, jego dane się ponownie tooit dostępne za pośrednictwem hello Menedżer stanów.</span><span class="sxs-lookup"><span data-stu-id="6a656-162">When an actor is re-activated, its data is again made available tooit through hello State Manager.</span></span> <span data-ttu-id="6a656-163">W przypadku gdy podmiotów przechowywania danych w Menedżerze stanu i są dezaktywowane, ale nigdy aktywowany ponownie może być konieczne tooclean zapasowej danych.</span><span class="sxs-lookup"><span data-stu-id="6a656-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary tooclean up their data.</span></span>

<span data-ttu-id="6a656-164">Witaj [usługi aktora](service-fabric-reliable-actors-platform.md) udostępnia funkcję usuwania złośliwych użytkowników z zdalnego procesu wywołującego:</span><span class="sxs-lookup"><span data-stu-id="6a656-164">hello [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

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

<span data-ttu-id="6a656-165">Usuwanie aktora ma następujące skutki w zależności od tego, czy jest obecnie aktywna aktora hello hello:</span><span class="sxs-lookup"><span data-stu-id="6a656-165">Deleting an actor has hello following effects depending on whether or not hello actor is currently active:</span></span>

* <span data-ttu-id="6a656-166">**Aktywne aktora**</span><span class="sxs-lookup"><span data-stu-id="6a656-166">**Active Actor**</span></span>
  * <span data-ttu-id="6a656-167">Aktora zostanie usunięty z listy active złośliwych użytkowników, a jest nieaktywne.</span><span class="sxs-lookup"><span data-stu-id="6a656-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="6a656-168">Jego stan jest trwale usunięte.</span><span class="sxs-lookup"><span data-stu-id="6a656-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="6a656-169">**Nieaktywne aktora**</span><span class="sxs-lookup"><span data-stu-id="6a656-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="6a656-170">Jego stan jest trwale usunięte.</span><span class="sxs-lookup"><span data-stu-id="6a656-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="6a656-171">Należy pamiętać, że nie można wywołać aktora usunąć na samym sobie z jednego z jego metody aktora, ponieważ aktora hello nie można usunąć podczas wykonywania w kontekście wywołań aktora, w których hello środowiska uruchomieniowego uzyskał blokady wokół hello aktora wywołania tooenforce jednowątkowe dostępu.</span><span class="sxs-lookup"><span data-stu-id="6a656-171">Note that an actor cannot call delete on itself from one of its actor methods because hello actor cannot be deleted while executing within an actor call context, in which hello runtime has obtained a lock around hello actor call tooenforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a656-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6a656-172">Next steps</span></span>
* [<span data-ttu-id="6a656-173">Czasomierze aktora i przypomnieniami</span><span class="sxs-lookup"><span data-stu-id="6a656-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="6a656-174">Zdarzenia aktora</span><span class="sxs-lookup"><span data-stu-id="6a656-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="6a656-175">Wielobieżność aktora</span><span class="sxs-lookup"><span data-stu-id="6a656-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="6a656-176">Aktora Diagnostyka i monitorowanie wydajności</span><span class="sxs-lookup"><span data-stu-id="6a656-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="6a656-177">Dokumentację referencyjną aktora interfejsu API</span><span class="sxs-lookup"><span data-stu-id="6a656-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="6a656-178">C# przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="6a656-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="6a656-179">Java przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="6a656-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
