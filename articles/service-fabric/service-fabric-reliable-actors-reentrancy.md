---
title: "aaaReentrancy w podstawie aktora Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Tooreentrancy wprowadzenie do usługi sieci szkieletowej Reliable Actors"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: be23464a-0eea-4eca-ae5a-2e1b650d365e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 61c69bcf0f100e075d19ba155954c05789b71761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="2d2f2-103">Niezawodne wielobieżność złośliwych użytkowników</span><span class="sxs-lookup"><span data-stu-id="2d2f2-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="2d2f2-104">środowisko uruchomieniowe Reliable Actors Hello, domyślnie umożliwia ponowne wejście wywołania logiczną na podstawie kontekstu.</span><span class="sxs-lookup"><span data-stu-id="2d2f2-104">hello Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="2d2f2-105">Dzięki temu wielobieżna toobe złośliwych użytkowników, jeśli są one hello sam wywołać kontekstu łańcucha.</span><span class="sxs-lookup"><span data-stu-id="2d2f2-105">This allows for actors toobe reentrant if they are in hello same call context chain.</span></span> <span data-ttu-id="2d2f2-106">Na przykład aktora A wysyła tooActor komunikat B, który wysyła wiadomości tooActor C. W ramach przetwarzania wiadomość hello C aktora wywołuje aktora A, wiadomość hello jest współużytkowane, więc będą dozwolone.</span><span class="sxs-lookup"><span data-stu-id="2d2f2-106">For example, Actor A sends a message tooActor B, who sends a message tooActor C. As part of hello message processing, if Actor C calls Actor A, hello message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="2d2f2-107">Komunikaty, które są częścią kontekstu wywołania różnych zostaną zablokowane na aktora A zakończenie przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="2d2f2-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="2d2f2-108">Dostępne są dwie opcje do ponownego rozpoczęcia aktora zdefiniowane w hello `ActorReentrancyMode` wyliczenia:</span><span class="sxs-lookup"><span data-stu-id="2d2f2-108">There are two options available for actor reentrancy defined in hello `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="2d2f2-109">`LogicalCallContext`(domyślnie)</span><span class="sxs-lookup"><span data-stu-id="2d2f2-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="2d2f2-110">`Disallowed`— Wyłącza ponowne wejście</span><span class="sxs-lookup"><span data-stu-id="2d2f2-110">`Disallowed` - disables reentrancy</span></span>

```csharp
public enum ActorReentrancyMode
{
    LogicalCallContext = 1,
    Disallowed = 2
}
```
```Java
public enum ActorReentrancyMode
{
    LogicalCallContext(1),
    Disallowed(2)
}
```
<span data-ttu-id="2d2f2-111">Wielobieżność można skonfigurować w `ActorService`tego ustawienia podczas rejestracji.</span><span class="sxs-lookup"><span data-stu-id="2d2f2-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="2d2f2-112">Ustawienie Hello dotyczy tooall aktora wystąpienia utworzone w hello usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="2d2f2-112">hello setting applies tooall actor instances created in hello actor service.</span></span>

<span data-ttu-id="2d2f2-113">Witaj poniższy przykład przedstawia usługa aktora, która ustawia tryb wielobieżność hello zbyt`ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="2d2f2-113">hello following example shows an actor service that sets hello reentrancy mode too`ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="2d2f2-114">W tym przypadku aktora wysyła komunikat współużytkowane aktora tooanother, wyjątek typu `FabricException` zostanie wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="2d2f2-114">In this case, if an actor sends a reentrant message tooanother actor, an exception of type `FabricException` will be thrown.</span></span>

```csharp
static class Program
{
    static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<Actor1>(
                (context, actorType) => new ActorService(
                    context,
                    actorType, () => new Actor1(),
                    settings: new ActorServiceSettings()
                    {
                        ActorConcurrencySettings = new ActorConcurrencySettings()
                        {
                            ReentrancyMode = ActorReentrancyMode.Disallowed
                        }
                    }))
                .GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}
```
```Java
static class Program
{
    static void Main()
    {
        try
        {
            ActorConcurrencySettings actorConcurrencySettings = new ActorConcurrencySettings();
            actorConcurrencySettings.setReentrancyMode(ActorReentrancyMode.Disallowed);

            ActorServiceSettings actorServiceSettings = new ActorServiceSettings();
            actorServiceSettings.setActorConcurrencySettings(actorConcurrencySettings);

            ActorRuntime.registerActorAsync(
                Actor1.getClass(),
                (context, actorType) -> new FabricActorService(
                    context,
                    actorType, () -> new Actor1(),
                    null,
                    stateProvider,
                    actorServiceSettings, timeout);

            Thread.sleep(Long.MAX_VALUE);
        }
        catch (Exception e)
        {
            throw e;
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="2d2f2-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2d2f2-115">Next steps</span></span>
* <span data-ttu-id="2d2f2-116">Dowiedz się więcej na temat ponownego rozpoczęcia w hello [dokumentacji interfejsu API aktora](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="2d2f2-116">Learn more about reentrancy in hello [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
