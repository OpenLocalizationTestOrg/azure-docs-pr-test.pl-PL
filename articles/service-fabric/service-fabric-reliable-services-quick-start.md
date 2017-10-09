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
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="b10ba-103">Wprowadzenie do usług Reliable Services</span><span class="sxs-lookup"><span data-stu-id="b10ba-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b10ba-104">C# w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="b10ba-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="b10ba-105">Java w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="b10ba-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="b10ba-106">Aplikację usługi Azure Service Fabric zawiera jeden lub więcej usług, które uruchomić kod.</span><span class="sxs-lookup"><span data-stu-id="b10ba-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="b10ba-107">W tym przewodniku przedstawiono sposób toocreate zarówno bezstanowe i stanowe aplikacji sieci szkieletowej usług za pomocą [niezawodne usługi](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b10ba-107">This guide shows you how toocreate both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="b10ba-108">Ten film Microsoft Virtual Academy również przedstawiono toocreate bezstanowej niezawodnej usługi:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="b10ba-108">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="b10ba-109">Podstawowe pojęcia</span><span class="sxs-lookup"><span data-stu-id="b10ba-109">Basic concepts</span></span>
<span data-ttu-id="b10ba-110">tooget pracy z usługami Reliable Services, musisz tylko należy toounderstand kilka podstawowych pojęć:</span><span class="sxs-lookup"><span data-stu-id="b10ba-110">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="b10ba-111">**Typ usługi**: jest to implementacji usługi.</span><span class="sxs-lookup"><span data-stu-id="b10ba-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="b10ba-112">Jest on zdefiniowany przez klasę hello pisania, rozszerzający `StatelessService` i innego kodu lub zależności używany, oraz nazwę i numer wersji.</span><span class="sxs-lookup"><span data-stu-id="b10ba-112">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="b10ba-113">**Nazwane wystąpienie usługi**: toorun usługi tworzenia nazwanego wystąpienia danego typu usługi znacznie tak, jak utworzyć wystąpienia obiektu typu klasy.</span><span class="sxs-lookup"><span data-stu-id="b10ba-113">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="b10ba-114">Wystąpienie usługi ma nazwę w postaci hello identyfikatora URI przy użyciu hello "fabric: /" schemat, takich jak "sieci szkieletowej: / MyApp/Moja_usługa".</span><span class="sxs-lookup"><span data-stu-id="b10ba-114">A service instance has a name in hello form of a URI using hello "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="b10ba-115">**Host usługi**: hello nazwane wystąpienia usługi, utworzyć toorun potrzeby wewnątrz procesu hosta.</span><span class="sxs-lookup"><span data-stu-id="b10ba-115">**Service host**: hello named service instances you create need toorun inside a host process.</span></span> <span data-ttu-id="b10ba-116">host usługi Hello jest właśnie procesu, których można uruchomić wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="b10ba-116">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="b10ba-117">**Usługa rejestracji**: rejestracji, połączono wszystko.</span><span class="sxs-lookup"><span data-stu-id="b10ba-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="b10ba-118">Witaj typ usługi musi być zarejestrowana z hello sieci szkieletowej usług środowiska uruchomieniowego w usłudze hosta tooallow sieci szkieletowej usług toocreate wystąpień toorun.</span><span class="sxs-lookup"><span data-stu-id="b10ba-118">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="b10ba-119">Tworzenie usługi bezstanowej</span><span class="sxs-lookup"><span data-stu-id="b10ba-119">Create a stateless service</span></span>
<span data-ttu-id="b10ba-120">Usługi bezstanowej jest typem usługi, która jest obecnie normy hello w aplikacji w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b10ba-120">A stateless service is a type of service that is currently hello norm in cloud applications.</span></span> <span data-ttu-id="b10ba-121">Uznano bezstanowych, ponieważ sama usługa hello nie zawiera danych, które wymagałyby toobe przechowywane niezawodnie lub zyskuje dużą dostępność.</span><span class="sxs-lookup"><span data-stu-id="b10ba-121">It is considered stateless because hello service itself does not contain data that needs toobe stored reliably or made highly available.</span></span> <span data-ttu-id="b10ba-122">Jeśli wystąpienie usługi bezstanowej zostanie wyłączony, wszystkie jego stanu wewnętrznego zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="b10ba-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="b10ba-123">W tym typie usługi, musi mieć tooan utrwalonego zewnętrznym sklepie, takie jak tabele Azure lub bazą danych SQL, stan dla niego toobe wprowadzone wysokiej dostępności i niezawodne.</span><span class="sxs-lookup"><span data-stu-id="b10ba-123">In this type of service, state must be persisted tooan external store, such as Azure Tables or a SQL database, for it toobe made highly available and reliable.</span></span>

<span data-ttu-id="b10ba-124">Uruchom program Visual Studio 2015 lub Visual Studio 2017 jako administrator, a następnie utwórz nowy projekt aplikacji sieci szkieletowej usług o nazwie *HelloWorld*:</span><span class="sxs-lookup"><span data-stu-id="b10ba-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Użyj hello nowy projekt okna dialogowego pole toocreate nowej aplikacji sieci szkieletowej usług](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="b10ba-126">Następnie utwórz projekt usługi bezstanowej o nazwie *HelloWorldStateless*:</span><span class="sxs-lookup"><span data-stu-id="b10ba-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![W hello drugie okno dialogowe Tworzenie projektu usługi bezstanowej](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="b10ba-128">Rozwiązanie zawiera teraz dwa projekty:</span><span class="sxs-lookup"><span data-stu-id="b10ba-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="b10ba-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="b10ba-129">*HelloWorld*.</span></span> <span data-ttu-id="b10ba-130">Jest to hello *aplikacji* projekt, który zawiera Twoje *usług*.</span><span class="sxs-lookup"><span data-stu-id="b10ba-130">This is hello *application* project that contains your *services*.</span></span> <span data-ttu-id="b10ba-131">Zawiera ona także manifest aplikacji hello opisujący aplikacji hello, a także wiele skryptów programu PowerShell, które ułatwiają toodeploy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b10ba-131">It also contains hello application manifest that describes hello application, as well as a number of PowerShell scripts that help you toodeploy your application.</span></span>
* <span data-ttu-id="b10ba-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="b10ba-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="b10ba-133">Jest to projekt usługi hello.</span><span class="sxs-lookup"><span data-stu-id="b10ba-133">This is hello service project.</span></span> <span data-ttu-id="b10ba-134">Zawiera ona wdrożenia usługi bezstanowej hello.</span><span class="sxs-lookup"><span data-stu-id="b10ba-134">It contains hello stateless service implementation.</span></span>

## <a name="implement-hello-service"></a><span data-ttu-id="b10ba-135">Wdrożenie usługi hello</span><span class="sxs-lookup"><span data-stu-id="b10ba-135">Implement hello service</span></span>
<span data-ttu-id="b10ba-136">Otwórz hello **HelloWorldStateless.cs** plik w projekcie usługi hello.</span><span class="sxs-lookup"><span data-stu-id="b10ba-136">Open hello **HelloWorldStateless.cs** file in hello service project.</span></span> <span data-ttu-id="b10ba-137">W sieci szkieletowej usług usługi można uruchomić wszelka logika biznesowa.</span><span class="sxs-lookup"><span data-stu-id="b10ba-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="b10ba-138">Interfejs API usługi Hello zawiera dwa punkty wejścia kodu:</span><span class="sxs-lookup"><span data-stu-id="b10ba-138">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="b10ba-139">Metoda punktu wejścia otwarty, nazywany *RunAsync*, w którym można rozpocząć wykonywania dowolnych zadań, w tym obciążeń obliczeniowych długotrwałe.</span><span class="sxs-lookup"><span data-stu-id="b10ba-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="b10ba-140">Punkt wejścia komunikacji, gdzie można podłączyć stosu komunikacji wyboru, takich jak ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="b10ba-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="b10ba-141">Jest to, gdzie można uruchomić odbieranie żądań od użytkowników i innych usług.</span><span class="sxs-lookup"><span data-stu-id="b10ba-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="b10ba-142">W tym samouczku, firma Microsoft będzie skupić się na powitania `RunAsync()` metoda punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="b10ba-142">In this tutorial, we will focus on hello `RunAsync()` entry point method.</span></span> <span data-ttu-id="b10ba-143">Jest to, gdzie natychmiast można rozpocząć uruchamianie kodu.</span><span class="sxs-lookup"><span data-stu-id="b10ba-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="b10ba-144">szablon projektu Hello zawiera przykładowe zastosowanie z `RunAsync()` który zwiększa liczbę stopniowe.</span><span class="sxs-lookup"><span data-stu-id="b10ba-144">hello project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="b10ba-145">Aby uzyskać szczegóły, jak toowork z komunikacją na stosie, zobacz [usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="b10ba-145">For details about how toowork with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="b10ba-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="b10ba-146">RunAsync</span></span>
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

<span data-ttu-id="b10ba-147">Platforma Hello wywołuje tę metodę, gdy wystąpienie usługi jest tooexecute umieścić i gotowe.</span><span class="sxs-lookup"><span data-stu-id="b10ba-147">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="b10ba-148">Dla usługi bezstanowej po prostu oznacza to, gdy wystąpienie usługi hello jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="b10ba-148">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="b10ba-149">Token anulowania podano toocoordinate, gdy wystąpienie usługi musi toobe zamknięte.</span><span class="sxs-lookup"><span data-stu-id="b10ba-149">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="b10ba-150">W sieci szkieletowej usług ten cykl otwarcie i zamknięcie wystąpienia usługi może wystąpić wiele razy w ciągu okresu istnienia hello hello usługi jako całość.</span><span class="sxs-lookup"><span data-stu-id="b10ba-150">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="b10ba-151">Może się to zdarzyć z różnych powodów, w tym:</span><span class="sxs-lookup"><span data-stu-id="b10ba-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="b10ba-152">Hello system przenosi swoich wystąpień usługi dla równoważenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="b10ba-152">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="b10ba-153">Błędy występują w kodzie.</span><span class="sxs-lookup"><span data-stu-id="b10ba-153">Faults occur in your code.</span></span>
* <span data-ttu-id="b10ba-154">Uaktualnianie aplikacji Hello lub systemu.</span><span class="sxs-lookup"><span data-stu-id="b10ba-154">hello application or system is upgraded.</span></span>
* <span data-ttu-id="b10ba-155">używany sprzęt Hello ulegnie awarii.</span><span class="sxs-lookup"><span data-stu-id="b10ba-155">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="b10ba-156">Aranżacja zarządza tookeep systemu hello usługi wysokiej dostępności i nieprawidłowo zrównoważone.</span><span class="sxs-lookup"><span data-stu-id="b10ba-156">This orchestration is managed by hello system tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="b10ba-157">`RunAsync()`nie zablokować synchronicznie.</span><span class="sxs-lookup"><span data-stu-id="b10ba-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="b10ba-158">Implementacji RunAsync powinna zwracać zadanie lub oczekiwania na wszystkie operacje długotrwałe lub blokowania tooallow hello środowiska uruchomieniowego toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b10ba-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="b10ba-159">Zanotuj w hello `while(true)` pętli w poprzednim przykładzie hello, umożliwiające zwracanie zadań `await Task.Delay()` jest używany.</span><span class="sxs-lookup"><span data-stu-id="b10ba-159">Note in hello `while(true)` loop in hello previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="b10ba-160">Jeśli obciążenie może zablokować synchronicznie, należy zaplanować nowe zadanie z `Task.Run()` w Twojej `RunAsync` implementacji.</span><span class="sxs-lookup"><span data-stu-id="b10ba-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="b10ba-161">Anulowanie obciążenie jest współpracy wysiłku, zorkiestrowana przez hello podany token anulowania.</span><span class="sxs-lookup"><span data-stu-id="b10ba-161">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="b10ba-162">Witaj system będzie oczekiwał tooend Twojego zadania (przez pomyślne zakończenie anulowania lub fault) przed przesyłane w.</span><span class="sxs-lookup"><span data-stu-id="b10ba-162">hello system will wait for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="b10ba-163">Jest ważne toohonor hello anulowania tokenu, Zakończ wszelkie pracy i zamknięcie `RunAsync()` tak szybko jak to możliwe, gdy hello system żądań anulowania.</span><span class="sxs-lookup"><span data-stu-id="b10ba-163">It is important toohonor hello cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when hello system requests cancellation.</span></span>

<span data-ttu-id="b10ba-164">W tym przykładzie usługi bezstanowej liczba hello są przechowywane w zmiennej lokalnej.</span><span class="sxs-lookup"><span data-stu-id="b10ba-164">In this stateless service example, hello count is stored in a local variable.</span></span> <span data-ttu-id="b10ba-165">Ale ponieważ jest to usługi bezstanowej, hello wartość przechowywana istnieje tylko dla bieżącego cyklu życia hello jego wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="b10ba-165">But because this is a stateless service, hello value that's stored exists only for hello current lifecycle of its service instance.</span></span> <span data-ttu-id="b10ba-166">Gdy usługa hello przenosi lub ponownego uruchomienia, wartość hello zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="b10ba-166">When hello service moves or restarts, hello value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="b10ba-167">Tworzenie usługi stanowej</span><span class="sxs-lookup"><span data-stu-id="b10ba-167">Create a stateful service</span></span>
<span data-ttu-id="b10ba-168">Sieć szkieletowa usług wprowadzono nowy rodzaj usługi, który jest obiektem stanowym.</span><span class="sxs-lookup"><span data-stu-id="b10ba-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="b10ba-169">Usługa stanowa można zachować stanu niezawodnie w hello sama usługa wspólnie z kodem hello, który jest używany przez.</span><span class="sxs-lookup"><span data-stu-id="b10ba-169">A stateful service can maintain state reliably within hello service itself, co-located with hello code that's using it.</span></span> <span data-ttu-id="b10ba-170">Stan dokonuje wysokiej dostępności usługi sieć szkieletowa bez hello potrzeby toopersist stanu tooan zewnętrznym sklepie.</span><span class="sxs-lookup"><span data-stu-id="b10ba-170">State is made highly available by Service Fabric without hello need toopersist state tooan external store.</span></span>

<span data-ttu-id="b10ba-171">tooconvert wartość licznika z bezstanowej toohighly dostępne i trwałe, nawet wtedy, gdy usługa hello przenosi lub uruchomieniu należy usługi stanowej.</span><span class="sxs-lookup"><span data-stu-id="b10ba-171">tooconvert a counter value from stateless toohighly available and persistent, even when hello service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="b10ba-172">W hello sam *HelloWorld* aplikacji, można dodać nową usługę przez kliknięcie prawym przyciskiem myszy hello usług odwołań w projekt aplikacji hello i wybierając **Nowa usługa sieci szkieletowej usług -> Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="b10ba-172">In hello same *HelloWorld* application, you can add a new service by right-clicking on hello Services references in hello application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Dodaj tooyour usługi sieć szkieletowa usług aplikacji](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="b10ba-174">Wybierz **usługi Stateful** i nadaj mu nazwę *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="b10ba-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="b10ba-175">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b10ba-175">Click **OK**.</span></span>

![Użyj hello nowy projekt okna dialogowego pole toocreate nowej usługi stanowej sieci szkieletowej usług](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="b10ba-177">Aplikacja powinna mieć teraz dwie usługi: hello usługi bezstanowej *HelloWorldStateless* i usługi stanowej hello *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="b10ba-177">Your application should now have two services: hello stateless service *HelloWorldStateless* and hello stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="b10ba-178">Usługa stanowa ma hello tego samego punkty wejścia jako usługę bezstanową.</span><span class="sxs-lookup"><span data-stu-id="b10ba-178">A stateful service has hello same entry points as a stateless service.</span></span> <span data-ttu-id="b10ba-179">Witaj podstawowa różnica polega na dostępność hello *dostawcy stanu* który niezawodne przechowywanie stanu.</span><span class="sxs-lookup"><span data-stu-id="b10ba-179">hello main difference is hello availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="b10ba-180">Usługi sieć szkieletowa jest dostarczany z implementacja dostawcy stanu o nazwie [niezawodnej kolekcje](service-fabric-reliable-services-reliable-collections.md), co umożliwia tworzenie struktury replikowanych danych za pośrednictwem hello niezawodnej Menedżer stanu.</span><span class="sxs-lookup"><span data-stu-id="b10ba-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through hello Reliable State Manager.</span></span> <span data-ttu-id="b10ba-181">Domyślnie usługa stanowa niezawodnej używa tego dostawcy stanu.</span><span class="sxs-lookup"><span data-stu-id="b10ba-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="b10ba-182">Otwórz **HelloWorldStateful.cs** w *HelloWorldStateful*, który zawiera powitania po metodzie RunAsync:</span><span class="sxs-lookup"><span data-stu-id="b10ba-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains hello following RunAsync method:</span></span>

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

### <a name="runasync"></a><span data-ttu-id="b10ba-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="b10ba-183">RunAsync</span></span>
<span data-ttu-id="b10ba-184">`RunAsync()`działa podobnie, w usługach stanowe i bezstanowe.</span><span class="sxs-lookup"><span data-stu-id="b10ba-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="b10ba-185">Jednak w usługi stanowej, platforma hello wykonuje dodatkowych działań w Twoim imieniu przed rozpoczęciem wykonywania `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="b10ba-185">However, in a stateful service, hello platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="b10ba-186">Te działania mogą obejmować zapewnienie, że hello niezawodnej Menedżer stanu i niezawodne kolekcje są gotowe toouse.</span><span class="sxs-lookup"><span data-stu-id="b10ba-186">This work can include ensuring that hello Reliable State Manager and Reliable Collections are ready toouse.</span></span>

### <a name="reliable-collections-and-hello-reliable-state-manager"></a><span data-ttu-id="b10ba-187">Niezawodne kolekcje i hello niezawodnej Menedżer stanu</span><span class="sxs-lookup"><span data-stu-id="b10ba-187">Reliable Collections and hello Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="b10ba-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) jest implementacją słownika służy tooreliably stanu magazynu w usłudze hello.</span><span class="sxs-lookup"><span data-stu-id="b10ba-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use tooreliably store state in hello service.</span></span> <span data-ttu-id="b10ba-189">Z sieci szkieletowej usług i niezawodne kolekcji można przechowywać danych bezpośrednio w usłudze bez potrzeby hello zewnętrznych magazynu trwałego.</span><span class="sxs-lookup"><span data-stu-id="b10ba-189">With Service Fabric and Reliable Collections, you can store data directly in your service without hello need for an external persistent store.</span></span> <span data-ttu-id="b10ba-190">Niezawodne kolekcje danych wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="b10ba-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="b10ba-191">Sieć szkieletowa usług rozwiązanie to tworzenie i zarządzanie wieloma *replik* usługi dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="b10ba-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="b10ba-192">Udostępnia również interfejs API, który abstracts złożoności hello zadań zarządzania tych replik i ich przejścia stanu.</span><span class="sxs-lookup"><span data-stu-id="b10ba-192">It also provides an API that abstracts away hello complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="b10ba-193">Kolekcje niezawodnej może przechowywać żadnych typ architektury .NET, łącznie z niestandardowych typów, za pomocą paru ostrzeżenia:</span><span class="sxs-lookup"><span data-stu-id="b10ba-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="b10ba-194">Usługa sieci szkieletowej udostępnia swój stan wysokiej przez *replikowanie* stanu między węzły i niezawodne kolekcje przechowywania dysku toolocal danych dla każdej repliki.</span><span class="sxs-lookup"><span data-stu-id="b10ba-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data toolocal disk on each replica.</span></span> <span data-ttu-id="b10ba-195">To oznacza, że wszystkie zasoby, które są przechowywane w niezawodnej kolekcje muszą zostać *serializacji*.</span><span class="sxs-lookup"><span data-stu-id="b10ba-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="b10ba-196">Domyślnie używają niezawodnej kolekcje [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) serializacji, dlatego jest ważne toomake się, że Twoje typy są [obsługiwane przez serializator kontraktu danych hello](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) używając domyślnego hello Serializator.</span><span class="sxs-lookup"><span data-stu-id="b10ba-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important toomake sure that your types are [supported by hello Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use hello default serializer.</span></span>
* <span data-ttu-id="b10ba-197">Obiekty są replikowane wysokiej dostępności po zatwierdzeniu transakcji na niezawodne kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b10ba-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="b10ba-198">Obiekty przechowywane w niezawodnej kolekcje są przechowywane w lokalnej pamięci w usłudze.</span><span class="sxs-lookup"><span data-stu-id="b10ba-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="b10ba-199">Oznacza to, że obiekt toohello lokalnego odwołania.</span><span class="sxs-lookup"><span data-stu-id="b10ba-199">This means that you have a local reference toohello object.</span></span>
  
   <span data-ttu-id="b10ba-200">Należy pamiętać, że nie zmodyfikować lokalnych wystąpień tych obiektów, bez wykonywania operacji update na powitania niezawodnej kolekcji w transakcji.</span><span class="sxs-lookup"><span data-stu-id="b10ba-200">It is important that you do not mutate local instances of those objects without performing an update operation on hello reliable collection in a transaction.</span></span> <span data-ttu-id="b10ba-201">Jest to spowodowane zmiany toolocal wystąpienia obiektów, nie będą automatycznie replikowane.</span><span class="sxs-lookup"><span data-stu-id="b10ba-201">This is because changes toolocal instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="b10ba-202">Należy ponownie wstawić hello obiekt do słownika hello lub użyj jednej z hello *aktualizacji* metod na powitania słownika.</span><span class="sxs-lookup"><span data-stu-id="b10ba-202">You must re-insert hello object back into hello dictionary or use one of hello *update* methods on hello dictionary.</span></span>

<span data-ttu-id="b10ba-203">Witaj niezawodnej Menedżer stanu zarządza niezawodnej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b10ba-203">hello Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="b10ba-204">Po prostu poproś hello niezawodnej Menedżer stanu niezawodnej kolekcji o nazwie w dowolnym momencie i w dowolnym miejscu w usłudze.</span><span class="sxs-lookup"><span data-stu-id="b10ba-204">You can simply ask hello Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="b10ba-205">Hello niezawodnej Menedżer stanu zapewnia ponownie uzyskać odwołanie.</span><span class="sxs-lookup"><span data-stu-id="b10ba-205">hello Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="b10ba-206">Nie zaleca się zapisanie odwołania tooreliable kolekcji wystąpień w zmiennych Członkowskich klas lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="b10ba-206">We don't recommended that you save references tooreliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="b10ba-207">Specjalne należy zachować ostrożność tooensure ustawionej odwołanie hello wystąpienia tooan przez cały czas w cyklu życia usług hello.</span><span class="sxs-lookup"><span data-stu-id="b10ba-207">Special care must be taken tooensure that hello reference is set tooan instance at all times in hello service lifecycle.</span></span> <span data-ttu-id="b10ba-208">Witaj niezawodnej Menedżer stanu obsługuje tę pracę za Ciebie i jest zoptymalizowany do powtarzania wizytach.</span><span class="sxs-lookup"><span data-stu-id="b10ba-208">hello Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="b10ba-209">Operacje transakcyjne i asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="b10ba-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="b10ba-210">Kolekcje niezawodnej mają wiele hello te same operacje który ich `System.Collections.Generic` i `System.Collections.Concurrent` odpowiednikami z wyjątkiem LINQ.</span><span class="sxs-lookup"><span data-stu-id="b10ba-210">Reliable Collections have many of hello same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="b10ba-211">Operacje na niezawodne kolekcje są asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="b10ba-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="b10ba-212">Jest to spowodowane operacji zapisu z kolekcjami niezawodnej wykonać tooreplicate operacji We/Wy i utrwalić toodisk danych.</span><span class="sxs-lookup"><span data-stu-id="b10ba-212">This is because write operations with Reliable Collections perform I/O operations tooreplicate and persist data toodisk.</span></span>

<span data-ttu-id="b10ba-213">Są niezawodne operacje kolekcji *transakcyjnych*, dzięki czemu można zachować stanu spójne w wielu kolekcjach niezawodnej i operacji.</span><span class="sxs-lookup"><span data-stu-id="b10ba-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="b10ba-214">Może na przykład usuwania z kolejki elementu roboczego z kolejką niezawodne, wykonaj operację i zapisz wynik hello w słowniku niezawodne, wszystkie w ramach pojedynczej transakcji.</span><span class="sxs-lookup"><span data-stu-id="b10ba-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save hello result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="b10ba-215">Jest ona traktowana jako operacją niepodzielną i gwarantuje, że hello całego operacja zostanie wykonana pomyślnie lub całej operacji hello cofnie.</span><span class="sxs-lookup"><span data-stu-id="b10ba-215">This is treated as an atomic operation, and it guarantees that either hello entire operation will succeed or hello entire operation will roll back.</span></span> <span data-ttu-id="b10ba-216">Jeśli błąd wystąpi po dequeue hello elementu, ale przed zapisaniem wynik hello, hello cała transakcja zostanie wycofana i hello element pozostaje w kolejce hello do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="b10ba-216">If an error occurs after you dequeue hello item but before you save hello result, hello entire transaction is rolled back and hello item remains in hello queue for processing.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="b10ba-217">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="b10ba-217">Run hello application</span></span>
<span data-ttu-id="b10ba-218">Teraz zostanie zwrócona toohello *HelloWorld* aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b10ba-218">We now return toohello *HelloWorld* application.</span></span> <span data-ttu-id="b10ba-219">Teraz możesz skompilować i wdrażanie usług.</span><span class="sxs-lookup"><span data-stu-id="b10ba-219">You can now build and deploy your services.</span></span> <span data-ttu-id="b10ba-220">Po naciśnięciu **F5**, aplikacja będzie klastra lokalnego tooyour wbudowanych i wdrożone.</span><span class="sxs-lookup"><span data-stu-id="b10ba-220">When you press **F5**, your application will be built and deployed tooyour local cluster.</span></span>

<span data-ttu-id="b10ba-221">Po hello usług rozpoczęcie działania, można wyświetlać zdarzenia funkcji Śledzenie zdarzeń systemu Windows () hello generowane w **zdarzeń diagnostycznych** okna.</span><span class="sxs-lookup"><span data-stu-id="b10ba-221">After hello services start running, you can view hello generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="b10ba-222">Należy zauważyć, że zdarzenia hello wyświetlane zarówno usługi bezstanowej hello, jak i usługi stanowej hello w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b10ba-222">Note that hello events displayed are from both hello stateless service and hello stateful service in hello application.</span></span> <span data-ttu-id="b10ba-223">W przypadku wstrzymania hello strumienia, klikając hello **wstrzymać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b10ba-223">You can pause hello stream by clicking hello **Pause** button.</span></span> <span data-ttu-id="b10ba-224">Następnie można sprawdzić szczegóły wiadomość hello rozwijając tej wiadomości.</span><span class="sxs-lookup"><span data-stu-id="b10ba-224">You can then examine hello details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="b10ba-225">Przed uruchomieniem aplikacji hello upewnij się, że masz lokalne działania projektowe klastra z systemem.</span><span class="sxs-lookup"><span data-stu-id="b10ba-225">Before you run hello application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="b10ba-226">Zapoznaj się z hello [Wprowadzenie — przewodnik](service-fabric-get-started.md) informacji na temat konfigurowania środowiska lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b10ba-226">Check out hello [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Wyświetl zdarzenia diagnostycznego w programie Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="b10ba-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b10ba-228">Next steps</span></span>
[<span data-ttu-id="b10ba-229">Debugowanie aplikacji sieci szkieletowej usług w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b10ba-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="b10ba-230">Wprowadzenie: usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN</span><span class="sxs-lookup"><span data-stu-id="b10ba-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="b10ba-231">Dowiedz się więcej o niezawodnej kolekcje</span><span class="sxs-lookup"><span data-stu-id="b10ba-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="b10ba-232">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b10ba-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="b10ba-233">Uaktualnianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b10ba-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="b10ba-234">Dokumentacja dla deweloperów dla niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="b10ba-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

