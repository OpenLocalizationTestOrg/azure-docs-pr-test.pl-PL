---
title: "aaaCreate pierwszej aplikacji platformy Service Fabric w języku C# | Dokumentacja firmy Microsoft"
description: "Wprowadzenie toocreating aplikację usługi sieć szkieletowa usług Microsoft Azure z usług bezstanowych i stanowych."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Wprowadzenie do usług Reliable Services
> [!div class="op_single_selector"]
> * [C# w systemie Windows](service-fabric-reliable-services-quick-start.md)
> * [Java w systemie Linux](service-fabric-reliable-services-quick-start-java.md)
> 
> 

Aplikację usługi Azure Service Fabric zawiera jeden lub więcej usług, które uruchomić kod. W tym przewodniku przedstawiono sposób toocreate zarówno bezstanowe i stanowe aplikacji sieci szkieletowej usług za pomocą [niezawodne usługi](service-fabric-reliable-services-introduction.md).  Ten film Microsoft Virtual Academy również przedstawiono toocreate bezstanowej niezawodnej usługi:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965">  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a>Podstawowe pojęcia
tooget pracy z usługami Reliable Services, musisz tylko należy toounderstand kilka podstawowych pojęć:

* **Typ usługi**: jest to implementacji usługi. Jest on zdefiniowany przez klasę hello pisania, rozszerzający `StatelessService` i innego kodu lub zależności używany, oraz nazwę i numer wersji.
* **Nazwane wystąpienie usługi**: toorun usługi tworzenia nazwanego wystąpienia danego typu usługi znacznie tak, jak utworzyć wystąpienia obiektu typu klasy. Wystąpienie usługi ma nazwę w postaci hello identyfikatora URI przy użyciu hello "fabric: /" schemat, takich jak "sieci szkieletowej: / MyApp/Moja_usługa".
* **Host usługi**: hello nazwane wystąpienia usługi, utworzyć toorun potrzeby wewnątrz procesu hosta. host usługi Hello jest właśnie procesu, których można uruchomić wystąpienia usługi.
* **Usługa rejestracji**: rejestracji, połączono wszystko. Witaj typ usługi musi być zarejestrowana z hello sieci szkieletowej usług środowiska uruchomieniowego w usłudze hosta tooallow sieci szkieletowej usług toocreate wystąpień toorun.  

## <a name="create-a-stateless-service"></a>Tworzenie usługi bezstanowej
Usługi bezstanowej jest typem usługi, która jest obecnie normy hello w aplikacji w chmurze. Uznano bezstanowych, ponieważ sama usługa hello nie zawiera danych, które wymagałyby toobe przechowywane niezawodnie lub zyskuje dużą dostępność. Jeśli wystąpienie usługi bezstanowej zostanie wyłączony, wszystkie jego stanu wewnętrznego zostaną utracone. W tym typie usługi, musi mieć tooan utrwalonego zewnętrznym sklepie, takie jak tabele Azure lub bazą danych SQL, stan dla niego toobe wprowadzone wysokiej dostępności i niezawodne.

Uruchom program Visual Studio 2015 lub Visual Studio 2017 jako administrator, a następnie utwórz nowy projekt aplikacji sieci szkieletowej usług o nazwie *HelloWorld*:

![Użyj hello nowy projekt okna dialogowego pole toocreate nowej aplikacji sieci szkieletowej usług](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

Następnie utwórz projekt usługi bezstanowej o nazwie *HelloWorldStateless*:

![W hello drugie okno dialogowe Tworzenie projektu usługi bezstanowej](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

Rozwiązanie zawiera teraz dwa projekty:

* *HelloWorld*. Jest to hello *aplikacji* projekt, który zawiera Twoje *usług*. Zawiera ona także manifest aplikacji hello opisujący aplikacji hello, a także wiele skryptów programu PowerShell, które ułatwiają toodeploy aplikacji.
* *HelloWorldStateless*. Jest to projekt usługi hello. Zawiera ona wdrożenia usługi bezstanowej hello.

## <a name="implement-hello-service"></a>Wdrożenie usługi hello
Otwórz hello **HelloWorldStateless.cs** plik w projekcie usługi hello. W sieci szkieletowej usług usługi można uruchomić wszelka logika biznesowa. Interfejs API usługi Hello zawiera dwa punkty wejścia kodu:

* Metoda punktu wejścia otwarty, nazywany *RunAsync*, w którym można rozpocząć wykonywania dowolnych zadań, w tym obciążeń obliczeniowych długotrwałe.

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* Punkt wejścia komunikacji, gdzie można podłączyć stosu komunikacji wyboru, takich jak ASP.NET Core. Jest to, gdzie można uruchomić odbieranie żądań od użytkowników i innych usług.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

W tym samouczku, firma Microsoft będzie skupić się na powitania `RunAsync()` metoda punktu wejścia. Jest to, gdzie natychmiast można rozpocząć uruchamianie kodu.
szablon projektu Hello zawiera przykładowe zastosowanie z `RunAsync()` który zwiększa liczbę stopniowe.

> [!NOTE]
> Aby uzyskać szczegóły, jak toowork z komunikacją na stosie, zobacz [usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN](service-fabric-reliable-services-communication-webapi.md)
> 
> 

### <a name="runasync"></a>RunAsync
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

Platforma Hello wywołuje tę metodę, gdy wystąpienie usługi jest tooexecute umieścić i gotowe. Dla usługi bezstanowej po prostu oznacza to, gdy wystąpienie usługi hello jest otwarty. Token anulowania podano toocoordinate, gdy wystąpienie usługi musi toobe zamknięte. W sieci szkieletowej usług ten cykl otwarcie i zamknięcie wystąpienia usługi może wystąpić wiele razy w ciągu okresu istnienia hello hello usługi jako całość. Może się to zdarzyć z różnych powodów, w tym:

* Hello system przenosi swoich wystąpień usługi dla równoważenia zasobów.
* Błędy występują w kodzie.
* Uaktualnianie aplikacji Hello lub systemu.
* używany sprzęt Hello ulegnie awarii.

Aranżacja zarządza tookeep systemu hello usługi wysokiej dostępności i nieprawidłowo zrównoważone.

`RunAsync()`nie zablokować synchronicznie. Implementacji RunAsync powinna zwracać zadanie lub oczekiwania na wszystkie operacje długotrwałe lub blokowania tooallow hello środowiska uruchomieniowego toocontinue. Zanotuj w hello `while(true)` pętli w poprzednim przykładzie hello, umożliwiające zwracanie zadań `await Task.Delay()` jest używany. Jeśli obciążenie może zablokować synchronicznie, należy zaplanować nowe zadanie z `Task.Run()` w Twojej `RunAsync` implementacji.

Anulowanie obciążenie jest współpracy wysiłku, zorkiestrowana przez hello podany token anulowania. Witaj system będzie oczekiwał tooend Twojego zadania (przez pomyślne zakończenie anulowania lub fault) przed przesyłane w. Jest ważne toohonor hello anulowania tokenu, Zakończ wszelkie pracy i zamknięcie `RunAsync()` tak szybko jak to możliwe, gdy hello system żądań anulowania.

W tym przykładzie usługi bezstanowej liczba hello są przechowywane w zmiennej lokalnej. Ale ponieważ jest to usługi bezstanowej, hello wartość przechowywana istnieje tylko dla bieżącego cyklu życia hello jego wystąpienia usługi. Gdy usługa hello przenosi lub ponownego uruchomienia, wartość hello zostaną utracone.

## <a name="create-a-stateful-service"></a>Tworzenie usługi stanowej
Sieć szkieletowa usług wprowadzono nowy rodzaj usługi, który jest obiektem stanowym. Usługa stanowa można zachować stanu niezawodnie w hello sama usługa wspólnie z kodem hello, który jest używany przez. Stan dokonuje wysokiej dostępności usługi sieć szkieletowa bez hello potrzeby toopersist stanu tooan zewnętrznym sklepie.

tooconvert wartość licznika z bezstanowej toohighly dostępne i trwałe, nawet wtedy, gdy usługa hello przenosi lub uruchomieniu należy usługi stanowej.

W hello sam *HelloWorld* aplikacji, można dodać nową usługę przez kliknięcie prawym przyciskiem myszy hello usług odwołań w projekt aplikacji hello i wybierając **Nowa usługa sieci szkieletowej usług -> Dodaj**.

![Dodaj tooyour usługi sieć szkieletowa usług aplikacji](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

Wybierz **usługi Stateful** i nadaj mu nazwę *HelloWorldStateful*. Kliknij przycisk **OK**.

![Użyj hello nowy projekt okna dialogowego pole toocreate nowej usługi stanowej sieci szkieletowej usług](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

Aplikacja powinna mieć teraz dwie usługi: hello usługi bezstanowej *HelloWorldStateless* i usługi stanowej hello *HelloWorldStateful*.

Usługa stanowa ma hello tego samego punkty wejścia jako usługę bezstanową. Witaj podstawowa różnica polega na dostępność hello *dostawcy stanu* który niezawodne przechowywanie stanu. Usługi sieć szkieletowa jest dostarczany z implementacja dostawcy stanu o nazwie [niezawodnej kolekcje](service-fabric-reliable-services-reliable-collections.md), co umożliwia tworzenie struktury replikowanych danych za pośrednictwem hello niezawodnej Menedżer stanu. Domyślnie usługa stanowa niezawodnej używa tego dostawcy stanu.

Otwórz **HelloWorldStateful.cs** w *HelloWorldStateful*, który zawiera powitania po metodzie RunAsync:

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a>RunAsync
`RunAsync()`działa podobnie, w usługach stanowe i bezstanowe. Jednak w usługi stanowej, platforma hello wykonuje dodatkowych działań w Twoim imieniu przed rozpoczęciem wykonywania `RunAsync()`. Te działania mogą obejmować zapewnienie, że hello niezawodnej Menedżer stanu i niezawodne kolekcje są gotowe toouse.

### <a name="reliable-collections-and-hello-reliable-state-manager"></a>Niezawodne kolekcje i hello niezawodnej Menedżer stanu
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) jest implementacją słownika służy tooreliably stanu magazynu w usłudze hello. Z sieci szkieletowej usług i niezawodne kolekcji można przechowywać danych bezpośrednio w usłudze bez potrzeby hello zewnętrznych magazynu trwałego. Niezawodne kolekcje danych wysokiej dostępności. Sieć szkieletowa usług rozwiązanie to tworzenie i zarządzanie wieloma *replik* usługi dla Ciebie. Udostępnia również interfejs API, który abstracts złożoności hello zadań zarządzania tych replik i ich przejścia stanu.

Kolekcje niezawodnej może przechowywać żadnych typ architektury .NET, łącznie z niestandardowych typów, za pomocą paru ostrzeżenia:

* Usługa sieci szkieletowej udostępnia swój stan wysokiej przez *replikowanie* stanu między węzły i niezawodne kolekcje przechowywania dysku toolocal danych dla każdej repliki. To oznacza, że wszystkie zasoby, które są przechowywane w niezawodnej kolekcje muszą zostać *serializacji*. Domyślnie używają niezawodnej kolekcje [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) serializacji, dlatego jest ważne toomake się, że Twoje typy są [obsługiwane przez serializator kontraktu danych hello](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) używając domyślnego hello Serializator.
* Obiekty są replikowane wysokiej dostępności po zatwierdzeniu transakcji na niezawodne kolekcji. Obiekty przechowywane w niezawodnej kolekcje są przechowywane w lokalnej pamięci w usłudze. Oznacza to, że obiekt toohello lokalnego odwołania.
  
   Należy pamiętać, że nie zmodyfikować lokalnych wystąpień tych obiektów, bez wykonywania operacji update na powitania niezawodnej kolekcji w transakcji. Jest to spowodowane zmiany toolocal wystąpienia obiektów, nie będą automatycznie replikowane. Należy ponownie wstawić hello obiekt do słownika hello lub użyj jednej z hello *aktualizacji* metod na powitania słownika.

Witaj niezawodnej Menedżer stanu zarządza niezawodnej kolekcji. Po prostu poproś hello niezawodnej Menedżer stanu niezawodnej kolekcji o nazwie w dowolnym momencie i w dowolnym miejscu w usłudze. Hello niezawodnej Menedżer stanu zapewnia ponownie uzyskać odwołanie. Nie zaleca się zapisanie odwołania tooreliable kolekcji wystąpień w zmiennych Członkowskich klas lub właściwości. Specjalne należy zachować ostrożność tooensure ustawionej odwołanie hello wystąpienia tooan przez cały czas w cyklu życia usług hello. Witaj niezawodnej Menedżer stanu obsługuje tę pracę za Ciebie i jest zoptymalizowany do powtarzania wizytach.

### <a name="transactional-and-asynchronous-operations"></a>Operacje transakcyjne i asynchroniczne
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

Kolekcje niezawodnej mają wiele hello te same operacje który ich `System.Collections.Generic` i `System.Collections.Concurrent` odpowiednikami z wyjątkiem LINQ. Operacje na niezawodne kolekcje są asynchroniczne. Jest to spowodowane operacji zapisu z kolekcjami niezawodnej wykonać tooreplicate operacji We/Wy i utrwalić toodisk danych.

Są niezawodne operacje kolekcji *transakcyjnych*, dzięki czemu można zachować stanu spójne w wielu kolekcjach niezawodnej i operacji. Może na przykład usuwania z kolejki elementu roboczego z kolejką niezawodne, wykonaj operację i zapisz wynik hello w słowniku niezawodne, wszystkie w ramach pojedynczej transakcji. Jest ona traktowana jako operacją niepodzielną i gwarantuje, że hello całego operacja zostanie wykonana pomyślnie lub całej operacji hello cofnie. Jeśli błąd wystąpi po dequeue hello elementu, ale przed zapisaniem wynik hello, hello cała transakcja zostanie wycofana i hello element pozostaje w kolejce hello do przetwarzania.

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello
Teraz zostanie zwrócona toohello *HelloWorld* aplikacji. Teraz możesz skompilować i wdrażanie usług. Po naciśnięciu **F5**, aplikacja będzie klastra lokalnego tooyour wbudowanych i wdrożone.

Po hello usług rozpoczęcie działania, można wyświetlać zdarzenia funkcji Śledzenie zdarzeń systemu Windows () hello generowane w **zdarzeń diagnostycznych** okna. Należy zauważyć, że zdarzenia hello wyświetlane zarówno usługi bezstanowej hello, jak i usługi stanowej hello w aplikacji hello. W przypadku wstrzymania hello strumienia, klikając hello **wstrzymać** przycisku. Następnie można sprawdzić szczegóły wiadomość hello rozwijając tej wiadomości.

> [!NOTE]
> Przed uruchomieniem aplikacji hello upewnij się, że masz lokalne działania projektowe klastra z systemem. Zapoznaj się z hello [Wprowadzenie — przewodnik](service-fabric-get-started.md) informacji na temat konfigurowania środowiska lokalnego.
> 
> 

![Wyświetl zdarzenia diagnostycznego w programie Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a>Następne kroki
[Debugowanie aplikacji sieci szkieletowej usług w programie Visual Studio](service-fabric-debugging-your-application.md)

[Wprowadzenie: usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN](service-fabric-reliable-services-communication-webapi.md)

[Dowiedz się więcej o niezawodnej kolekcje](service-fabric-reliable-services-reliable-collections.md)

[Wdrażanie aplikacji](service-fabric-deploy-remove-applications.md)

[Uaktualnianie aplikacji](service-fabric-application-upgrade.md)

[Dokumentacja dla deweloperów dla niezawodne usługi](https://msdn.microsoft.com/library/azure/dn706529.aspx)

