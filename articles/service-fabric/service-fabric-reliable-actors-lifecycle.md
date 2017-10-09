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
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a>Cykl życia aktora, automatyczne wyrzucanie elementów bezużytecznych i ręcznego usuwania
Aktor jest uaktywniany hello po raz pierwszy tooany metody jest nawiązane połączenie. Aktor jest dezaktywowany (zebranych przez środowisko uruchomieniowe podmiotów hello pamięci), jeśli nie jest on używany przez można skonfigurować czas. Aktor i stanu można również zostaną usunięte ręcznie w dowolnym momencie.

## <a name="actor-activation"></a>Aktywacja aktora
Po uaktywnieniu aktora występuje hello następujące czynności:

* Wywołanie jest dostępna dla aktora i jeszcze nie została active, nowe aktora zostanie utworzona.
* stanu aktora Hello jest ładowana, jeśli jest zachowanie stanu.
* Witaj `OnActivateAsync` (C#) lub `onActivateAsync` wywołanie metody (Java) (która może zostać zastąpiona w celu wykonania aktora hello).
* Witaj aktora teraz jest traktowane jako aktywne.

## <a name="actor-deactivation"></a>Dezaktywacja aktora
Po dezaktywacji aktora hello rejestrowany:

* Gdy aktora nie jest używany przez niektóre czas, zostanie ono usunięte z tabeli aktywnych uczestników hello.
* Witaj `OnDeactivateAsync` (C#) lub `onDeactivateAsync` wywołanie metody (Java) (która może zostać zastąpiona w celu wykonania aktora hello). Czyści wszystkie czasomierze hello na powitania aktora. Aktora operacji, takich jak stan, jaki zmiany nie powinna być wywoływana z tej metody.

> [!TIP]
> Witaj środowisko uruchomieniowe sieci szkieletowej podmiotów emituje niektóre [zdarzenia związane z tooactor Aktywacja i dezaktywacja](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters). Są one przydatne w Diagnostyka i monitorowanie wydajności.
>
>

### <a name="actor-garbage-collection"></a>Aktora wyrzucanie elementów bezużytecznych
Po dezaktywacji aktora obiektu aktora toohello odwołania są wydawane i może być bezużytecznych zwykle hello środowisko uruchomieniowe języka wspólnego (CLR) lub moduł zbierający elementy bezużyteczne programu java (JVM). maszyny wirtualnej. Wyrzucanie elementów bezużytecznych tylko czyści hello obiektu aktora. robi **nie** usunąć stan przechowywane w Menedżerze stanu aktora hello. uaktywnieniu aktora hello czas następnego Hello, tworzony jest nowy obiekt aktora i jej przywróceniu.

Co to jest traktowana jako "jest używane" hello w celu dezaktywacji i wyrzucanie elementów bezużytecznych?

* Odbieranie wywołania
* `IRemindable.ReceiveReminderAsync`Metoda wywoływana (ma zastosowanie tylko wtedy, gdy aktora hello używa przypomnienia)

> [!NOTE]
> Jeśli aktora hello używa czasomierze i jej wywołanie zwrotne czasomierza jest wywoływana, nie **nie** liczby jako "jest używane".
>
>

Przed możemy przejść do szczegółów hello dezaktywację, jest ważne toodefine hello następujące warunki:

* *Interwał skanowania*. Jest to interwał powitania, w których hello podmiotów środowiska uruchomieniowego skanuje jego tabeli aktywnych uczestników osób, które można dezaktywować i w ramach odzyskiwania pamięci. Witaj wartość domyślna to to 1 minuta.
* *Limit czasu bezczynności*. Jest to hello ilość czasu, że aktora wymaga tooremain nieużywane (bezczynny), zanim można dezaktywować i w ramach odzyskiwania pamięci. Witaj wartość domyślna to wynosi 60 min.

Zazwyczaj nie trzeba toochange tych wartości domyślnych. Jednak w razie potrzeby kolejnymi interwałami można zmienić za pomocą `ActorServiceSettings` podczas rejestrowania programu [usługi aktora](service-fabric-reliable-actors-platform.md):

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
Dla każdego aktywnego aktora środowiska uruchomieniowego aktora hello przechowuje informacje o hello ilość czasu, który był bezczynny (tj. nie jest używany). środowisko uruchomieniowe aktora Hello sprawdza wszystkich podmiotów hello co `ScanIntervalInSeconds` toosee Jeśli pamięci może być zbierane i pobiera ją, jeśli był bezczynny `IdleTimeoutInSeconds`.

W dowolnym momencie aktora jest używany, jego czas bezczynności jest too0 resetowania. Po tym aktora hello może być bezużytecznych tylko wtedy, gdy ponownie pozostanie bezczynny `IdleTimeoutInSeconds`. Odwołaj się, że aktora jest uznawany za toohave zostały użyte, jeśli wykonywane jest metody interfejsu aktora lub wywołania zwrotnego monitu aktora. Aktor jest **nie** uznawane za toohave zostały użyte, jeśli jej wywołanie zwrotne czasomierza jest wykonywana.

Witaj Poniższy diagram przedstawia hello cyklem życia tooillustrate pojedynczego aktora te pojęcia.

![Przykład czas bezczynności][1]

przykład Witaj zawiera wpływ hello wywołania metody aktora, przypomnienia i czasomierze hello okres istnienia tego aktora. następujące kwestie dotyczące przykład Witaj Hello są warto zauważyć:

* ScanInterval IdleTimeout są ustawione i too5 i 10 odpowiednio. (Jednostek niezależnie od tego, ponieważ naszym celem jest tylko koncepcji hello tooillustrate.)
* skanowanie Hello osób toobe bezużytecznych odbywa się na T = 0, 5, 10, 15, 20, 25, zgodnie z definicją interwał skanowania powitania 5.
* Okresowe czasomierza wyzwala T = 4, 8, 12, 16, 20, 24, i wykonuje jej wywołanie zwrotne. Nie ma ona wpływu hello bezczynności hello aktora.
* Wywołanie metody aktora w T = 7 resetuje hello too0 czas bezczynności i wybrano opcję opóźnienia hello wyrzucanie elementów bezużytecznych z hello aktora.
* Wykonuje wywołanie zwrotne monitu aktora w T = 14 i dalsze opóźnienia hello wyrzucanie elementów bezużytecznych hello aktora.
* Podczas skanowania kolekcji garbage hello na T = 25 czas bezczynności aktora hello finally przekracza limit czasu bezczynności hello 10, a aktora hello jest bezużytecznych.

Aktor nigdy nie będą bezużytecznych podczas wykonywania jednej z metod, niezależnie od tego, ile czas podczas wykonywania tej metody. Jak wspomniano wcześniej, hello wykonywanie metod interfejsu aktora i wywołania zwrotne monitu zapobiega wyrzucanie elementów bezużytecznych resetując too0 czas bezczynności hello aktora. wykonywanie Hello wywołania zwrotne czasomierza nie powoduje resetowania hello too0 czasu bezczynności. Jednak hello wyrzucanie elementów bezużytecznych z aktorem hello została odroczona, dopóki nie zakończy się wywołanie zwrotne czasomierza hello wykonywania.

## <a name="deleting-actors-and-their-state"></a>Usuwanie złośliwych użytkowników i ich stan
Wyrzucanie elementów bezużytecznych dezaktywowane podmiotów tylko czyści hello aktora obiektu, ale nie powoduje usunięcia danych przechowywanych w Menedżerze stanu aktora. Aktor jest ponowna aktywacja, jego dane się ponownie tooit dostępne za pośrednictwem hello Menedżer stanów. W przypadku gdy podmiotów przechowywania danych w Menedżerze stanu i są dezaktywowane, ale nigdy aktywowany ponownie może być konieczne tooclean zapasowej danych.

Witaj [usługi aktora](service-fabric-reliable-actors-platform.md) udostępnia funkcję usuwania złośliwych użytkowników z zdalnego procesu wywołującego:

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

Usuwanie aktora ma następujące skutki w zależności od tego, czy jest obecnie aktywna aktora hello hello:

* **Aktywne aktora**
  * Aktora zostanie usunięty z listy active złośliwych użytkowników, a jest nieaktywne.
  * Jego stan jest trwale usunięte.
* **Nieaktywne aktora**
  * Jego stan jest trwale usunięte.

Należy pamiętać, że nie można wywołać aktora usunąć na samym sobie z jednego z jego metody aktora, ponieważ aktora hello nie można usunąć podczas wykonywania w kontekście wywołań aktora, w których hello środowiska uruchomieniowego uzyskał blokady wokół hello aktora wywołania tooenforce jednowątkowe dostępu.

## <a name="next-steps"></a>Następne kroki
* [Czasomierze aktora i przypomnieniami](service-fabric-reliable-actors-timers-reminders.md)
* [Zdarzenia aktora](service-fabric-reliable-actors-events.md)
* [Wielobieżność aktora](service-fabric-reliable-actors-reentrancy.md)
* [Aktora Diagnostyka i monitorowanie wydajności](service-fabric-reliable-actors-diagnostics.md)
* [Dokumentację referencyjną aktora interfejsu API](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [C# przykładowy kod](https://github.com/Azure/servicefabric-samples)
* [Java przykładowy kod](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
