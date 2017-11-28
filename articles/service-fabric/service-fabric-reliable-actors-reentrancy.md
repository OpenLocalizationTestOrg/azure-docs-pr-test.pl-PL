---
title: "Ponownego rozpoczęcia w podstawie aktora Azure mikrousług | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do ponownego rozpoczęcia dla elementów Reliable Actors sieci szkieletowej usług"
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
ms.openlocfilehash: 00fcccb379bf1ba3875fbaba57a05b00fa228622
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="813f4-103">Niezawodne wielobieżność złośliwych użytkowników</span><span class="sxs-lookup"><span data-stu-id="813f4-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="813f4-104">Środowisko uruchomieniowe Reliable Actors, domyślnie umożliwia wywołanie logiczną na podstawie kontekstu wielobieżność.</span><span class="sxs-lookup"><span data-stu-id="813f4-104">The Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="813f4-105">Dzięki temu podmiotów być współużytkowane, jeśli są w tym samym łańcuchu kontekstu wywołania.</span><span class="sxs-lookup"><span data-stu-id="813f4-105">This allows for actors to be reentrant if they are in the same call context chain.</span></span> <span data-ttu-id="813f4-106">Na przykład aktora A wysyła komunikat do aktora B, który wysyła wiadomość do aktora. Podczas przetwarzania komunikatu C aktora wywołuje aktora A, wiadomość jest współużytkowane, więc może być.</span><span class="sxs-lookup"><span data-stu-id="813f4-106">For example, Actor A sends a message to Actor B, who sends a message to Actor C. As part of the message processing, if Actor C calls Actor A, the message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="813f4-107">Komunikaty, które są częścią kontekstu wywołania różnych zostaną zablokowane na aktora A zakończenie przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="813f4-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="813f4-108">Dostępne są dwie opcje do ponownego rozpoczęcia aktora zdefiniowane w `ActorReentrancyMode` wyliczenia:</span><span class="sxs-lookup"><span data-stu-id="813f4-108">There are two options available for actor reentrancy defined in the `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="813f4-109">`LogicalCallContext`(domyślnie)</span><span class="sxs-lookup"><span data-stu-id="813f4-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="813f4-110">`Disallowed`— Wyłącza ponowne wejście</span><span class="sxs-lookup"><span data-stu-id="813f4-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="813f4-111">Wielobieżność można skonfigurować w `ActorService`tego ustawienia podczas rejestracji.</span><span class="sxs-lookup"><span data-stu-id="813f4-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="813f4-112">Ustawienie ma zastosowanie do wszystkich wystąpień aktora utworzone w usłudze aktora.</span><span class="sxs-lookup"><span data-stu-id="813f4-112">The setting applies to all actor instances created in the actor service.</span></span>

<span data-ttu-id="813f4-113">W poniższym przykładzie przedstawiono usługi aktora, która ustawia tryb wielobieżność `ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="813f4-113">The following example shows an actor service that sets the reentrancy mode to `ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="813f4-114">W tym przypadku aktora wysyła komunikat współużytkowane do innego aktora, wyjątek typu `FabricException` zostanie wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="813f4-114">In this case, if an actor sends a reentrant message to another actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="813f4-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="813f4-115">Next steps</span></span>
* <span data-ttu-id="813f4-116">Dowiedz się więcej na temat ponownego rozpoczęcia w [dokumentacji interfejsu API aktora](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="813f4-116">Learn more about reentrancy in the [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
