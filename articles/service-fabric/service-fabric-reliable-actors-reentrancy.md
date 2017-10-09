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
# <a name="reliable-actors-reentrancy"></a>Niezawodne wielobieżność złośliwych użytkowników
środowisko uruchomieniowe Reliable Actors Hello, domyślnie umożliwia ponowne wejście wywołania logiczną na podstawie kontekstu. Dzięki temu wielobieżna toobe złośliwych użytkowników, jeśli są one hello sam wywołać kontekstu łańcucha. Na przykład aktora A wysyła tooActor komunikat B, który wysyła wiadomości tooActor C. W ramach przetwarzania wiadomość hello C aktora wywołuje aktora A, wiadomość hello jest współużytkowane, więc będą dozwolone. Komunikaty, które są częścią kontekstu wywołania różnych zostaną zablokowane na aktora A zakończenie przetwarzania.

Dostępne są dwie opcje do ponownego rozpoczęcia aktora zdefiniowane w hello `ActorReentrancyMode` wyliczenia:

* `LogicalCallContext`(domyślnie)
* `Disallowed`— Wyłącza ponowne wejście

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
Wielobieżność można skonfigurować w `ActorService`tego ustawienia podczas rejestracji. Ustawienie Hello dotyczy tooall aktora wystąpienia utworzone w hello usługi aktora.

Witaj poniższy przykład przedstawia usługa aktora, która ustawia tryb wielobieżność hello zbyt`ActorReentrancyMode.Disallowed`. W tym przypadku aktora wysyła komunikat współużytkowane aktora tooanother, wyjątek typu `FabricException` zostanie wygenerowany.

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


## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej na temat ponownego rozpoczęcia w hello [dokumentacji interfejsu API aktora](https://msdn.microsoft.com/library/azure/dn971626.aspx)
