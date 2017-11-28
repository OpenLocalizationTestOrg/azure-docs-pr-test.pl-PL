---
title: "Tworzenie pierwszej aplikacji platformy Service Fabric w języku C# | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do tworzenia aplikacji usługi sieć szkieletowa usług Microsoft Azure z usług bezstanowych i stanowych."
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
ms.openlocfilehash: 813021d6239ae3cf79bb84b78f77e39c9e0783f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="e2eef-103">Wprowadzenie do usług Reliable Services</span><span class="sxs-lookup"><span data-stu-id="e2eef-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e2eef-104">C# w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="e2eef-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="e2eef-105">Java w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="e2eef-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="e2eef-106">Aplikację usługi Azure Service Fabric zawiera jeden lub więcej usług, które uruchomić kod.</span><span class="sxs-lookup"><span data-stu-id="e2eef-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="e2eef-107">W tym przewodniku przedstawiono sposób tworzenia aplikacji platformy Service Fabric zarówno bezstanowe i stanowe z [niezawodne usługi](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e2eef-107">This guide shows you how to create both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="e2eef-108">Microsoft Virtual Academy wideo przedstawiono również sposób tworzenia bezstanowej niezawodnej usługi:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="e2eef-108">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="e2eef-109">Podstawowe pojęcia</span><span class="sxs-lookup"><span data-stu-id="e2eef-109">Basic concepts</span></span>
<span data-ttu-id="e2eef-110">Aby rozpocząć pracę z usługami Reliable Services, tylko musisz poznać kilka podstawowych pojęć:</span><span class="sxs-lookup"><span data-stu-id="e2eef-110">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="e2eef-111">**Typ usługi**: jest to implementacji usługi.</span><span class="sxs-lookup"><span data-stu-id="e2eef-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="e2eef-112">Jest on zdefiniowany przez klasę pisania, rozszerzający `StatelessService` i innego kodu lub zależności używany, oraz nazwę i numer wersji.</span><span class="sxs-lookup"><span data-stu-id="e2eef-112">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="e2eef-113">**Nazwane wystąpienie usługi**: Aby uruchomić usługę, tworzenia nazwanego wystąpienia danego typu usługi znacznie tak, jak utworzyć wystąpienia obiektu typu klasy.</span><span class="sxs-lookup"><span data-stu-id="e2eef-113">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="e2eef-114">Wystąpienie usługi ma nazwę w postaci przy użyciu identyfikatora URI "fabric: /" schemat, takich jak "sieci szkieletowej: / MyApp/Moja_usługa".</span><span class="sxs-lookup"><span data-stu-id="e2eef-114">A service instance has a name in the form of a URI using the "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="e2eef-115">**Host usługi**: wystąpień usługi o nazwie, należy utworzyć niezbędne do uruchomienia wewnątrz procesu hosta.</span><span class="sxs-lookup"><span data-stu-id="e2eef-115">**Service host**: The named service instances you create need to run inside a host process.</span></span> <span data-ttu-id="e2eef-116">Host usługi jest właśnie procesu, których można uruchomić wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="e2eef-116">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="e2eef-117">**Usługa rejestracji**: rejestracji, połączono wszystko.</span><span class="sxs-lookup"><span data-stu-id="e2eef-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="e2eef-118">Typ usługi musi być zarejestrowana ze środowiskiem uruchomieniowym usługi sieć szkieletowa w umożliwia sieci szkieletowej usług do tworzenia wystąpień usługi hosta do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="e2eef-118">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="e2eef-119">Tworzenie usługi bezstanowej</span><span class="sxs-lookup"><span data-stu-id="e2eef-119">Create a stateless service</span></span>
<span data-ttu-id="e2eef-120">Usługi bezstanowej jest typem usługi, która jest obecnie normą w aplikacji w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e2eef-120">A stateless service is a type of service that is currently the norm in cloud applications.</span></span> <span data-ttu-id="e2eef-121">Uznano bezstanowych, ponieważ sama usługa nie zawiera danych, który musi być niezawodnie przechowywane lub zyskuje dużą dostępność.</span><span class="sxs-lookup"><span data-stu-id="e2eef-121">It is considered stateless because the service itself does not contain data that needs to be stored reliably or made highly available.</span></span> <span data-ttu-id="e2eef-122">Jeśli wystąpienie usługi bezstanowej zostanie wyłączony, wszystkie jego stanu wewnętrznego zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="e2eef-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="e2eef-123">W tym typie usługi stanu musi zostać utrwalony na zewnętrznym sklepie, takie jak tabele Azure lub bazy danych SQL, na jego się wysoką dostępność i niezawodne.</span><span class="sxs-lookup"><span data-stu-id="e2eef-123">In this type of service, state must be persisted to an external store, such as Azure Tables or a SQL database, for it to be made highly available and reliable.</span></span>

<span data-ttu-id="e2eef-124">Uruchom program Visual Studio 2015 lub Visual Studio 2017 jako administrator, a następnie utwórz nowy projekt aplikacji sieci szkieletowej usług o nazwie *HelloWorld*:</span><span class="sxs-lookup"><span data-stu-id="e2eef-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Użyj okna dialogowego Nowy projekt do tworzenia nowej aplikacji sieci szkieletowej usług](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="e2eef-126">Następnie utwórz projekt usługi bezstanowej o nazwie *HelloWorldStateless*:</span><span class="sxs-lookup"><span data-stu-id="e2eef-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![W oknie dialogowym drugi utworzyć projekt usługi bezstanowej](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="e2eef-128">Rozwiązanie zawiera teraz dwa projekty:</span><span class="sxs-lookup"><span data-stu-id="e2eef-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="e2eef-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="e2eef-129">*HelloWorld*.</span></span> <span data-ttu-id="e2eef-130">Jest to *aplikacji* projekt, który zawiera Twoje *usług*.</span><span class="sxs-lookup"><span data-stu-id="e2eef-130">This is the *application* project that contains your *services*.</span></span> <span data-ttu-id="e2eef-131">Zawiera ona także manifest aplikacji, który opisuje aplikacji, a także wiele skryptów programu PowerShell, które ułatwiają wdrażanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2eef-131">It also contains the application manifest that describes the application, as well as a number of PowerShell scripts that help you to deploy your application.</span></span>
* <span data-ttu-id="e2eef-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="e2eef-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="e2eef-133">Jest to projekt usługi.</span><span class="sxs-lookup"><span data-stu-id="e2eef-133">This is the service project.</span></span> <span data-ttu-id="e2eef-134">Zawiera ona wdrożenia usługi bezstanowej.</span><span class="sxs-lookup"><span data-stu-id="e2eef-134">It contains the stateless service implementation.</span></span>

## <a name="implement-the-service"></a><span data-ttu-id="e2eef-135">Wdrożenie usługi</span><span class="sxs-lookup"><span data-stu-id="e2eef-135">Implement the service</span></span>
<span data-ttu-id="e2eef-136">Otwórz **HelloWorldStateless.cs** plik w projekcie usługi.</span><span class="sxs-lookup"><span data-stu-id="e2eef-136">Open the **HelloWorldStateless.cs** file in the service project.</span></span> <span data-ttu-id="e2eef-137">W sieci szkieletowej usług usługi można uruchomić wszelka logika biznesowa.</span><span class="sxs-lookup"><span data-stu-id="e2eef-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="e2eef-138">Interfejs API usługi zawiera dwa punkty wejścia kodu:</span><span class="sxs-lookup"><span data-stu-id="e2eef-138">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="e2eef-139">Metoda punktu wejścia otwarty, nazywany *RunAsync*, w którym można rozpocząć wykonywania dowolnych zadań, w tym obciążeń obliczeniowych długotrwałe.</span><span class="sxs-lookup"><span data-stu-id="e2eef-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="e2eef-140">Punkt wejścia komunikacji, gdzie można podłączyć stosu komunikacji wyboru, takich jak ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="e2eef-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="e2eef-141">Jest to, gdzie można uruchomić odbieranie żądań od użytkowników i innych usług.</span><span class="sxs-lookup"><span data-stu-id="e2eef-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="e2eef-142">W tym samouczku, firma Microsoft będzie skupić się na `RunAsync()` metoda punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="e2eef-142">In this tutorial, we will focus on the `RunAsync()` entry point method.</span></span> <span data-ttu-id="e2eef-143">Jest to, gdzie natychmiast można rozpocząć uruchamianie kodu.</span><span class="sxs-lookup"><span data-stu-id="e2eef-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="e2eef-144">Szablon projektu zawiera implementację próbki `RunAsync()` który zwiększa liczbę stopniowe.</span><span class="sxs-lookup"><span data-stu-id="e2eef-144">The project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="e2eef-145">Aby uzyskać szczegółowe informacje dotyczące pracy z stosu komunikacji, zobacz [usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="e2eef-145">For details about how to work with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="e2eef-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="e2eef-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
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

<span data-ttu-id="e2eef-147">Platforma wywołuje tę metodę, gdy wystąpienie usługi jest umieszczony i gotowa do wykonania.</span><span class="sxs-lookup"><span data-stu-id="e2eef-147">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="e2eef-148">Dla usługi bezstanowej po prostu oznacza to, gdy wystąpienie usługi jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="e2eef-148">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="e2eef-149">Token anulowania został dostarczony do koordynowania, gdy wystąpienie usługi musi zostać zamknięty.</span><span class="sxs-lookup"><span data-stu-id="e2eef-149">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="e2eef-150">W sieci szkieletowej usług ten cykl otwarcie i zamknięcie wystąpienia usługi może wystąpić wiele razy w okresie istnienia usługi jako całość.</span><span class="sxs-lookup"><span data-stu-id="e2eef-150">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="e2eef-151">Może się to zdarzyć z różnych powodów, w tym:</span><span class="sxs-lookup"><span data-stu-id="e2eef-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="e2eef-152">System przeniesie swoich wystąpień usługi dla równoważenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="e2eef-152">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="e2eef-153">Błędy występują w kodzie.</span><span class="sxs-lookup"><span data-stu-id="e2eef-153">Faults occur in your code.</span></span>
* <span data-ttu-id="e2eef-154">Uaktualnianie aplikacji lub systemu.</span><span class="sxs-lookup"><span data-stu-id="e2eef-154">The application or system is upgraded.</span></span>
* <span data-ttu-id="e2eef-155">Sprzętu źródłowego ulegnie awarii.</span><span class="sxs-lookup"><span data-stu-id="e2eef-155">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="e2eef-156">Aranżacja jest zarządzany przez system do zachowania usługi wysokiej dostępności i nieprawidłowo zrównoważone.</span><span class="sxs-lookup"><span data-stu-id="e2eef-156">This orchestration is managed by the system to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="e2eef-157">`RunAsync()`nie zablokować synchronicznie.</span><span class="sxs-lookup"><span data-stu-id="e2eef-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="e2eef-158">Implementacji RunAsync powinna zwracać zadanie lub oczekiwania na żadnych operacji długotrwałe lub blokowania, aby umożliwić środowiska wykonawczego kontynuować.</span><span class="sxs-lookup"><span data-stu-id="e2eef-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations to allow the runtime to continue.</span></span> <span data-ttu-id="e2eef-159">Należy zwrócić uwagę w `while(true)` pętli w poprzednim przykładzie, umożliwiające zwracanie zadań `await Task.Delay()` jest używany.</span><span class="sxs-lookup"><span data-stu-id="e2eef-159">Note in the `while(true)` loop in the previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="e2eef-160">Jeśli obciążenie może zablokować synchronicznie, należy zaplanować nowe zadanie z `Task.Run()` w Twojej `RunAsync` implementacji.</span><span class="sxs-lookup"><span data-stu-id="e2eef-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="e2eef-161">Anulowanie obciążenie jest współpraca wysiłku, zorkiestrowana przez token anulowania podanego.</span><span class="sxs-lookup"><span data-stu-id="e2eef-161">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="e2eef-162">System będzie oczekiwał na zadania zakończenia (przez pomyślne zakończenie anulowania lub fault), zanim przesyłane w.</span><span class="sxs-lookup"><span data-stu-id="e2eef-162">The system will wait for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="e2eef-163">Ważne jest, aby uwzględnić token anulowania, Zakończ pracę i zamknąć `RunAsync()` tak szybko jak to możliwe, gdy system żąda anulowania.</span><span class="sxs-lookup"><span data-stu-id="e2eef-163">It is important to honor the cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when the system requests cancellation.</span></span>

<span data-ttu-id="e2eef-164">W tym przykładzie usługi bezstanowej licznika są przechowywane w zmiennej lokalnej.</span><span class="sxs-lookup"><span data-stu-id="e2eef-164">In this stateless service example, the count is stored in a local variable.</span></span> <span data-ttu-id="e2eef-165">Ale jest usługi bezstanowej, dlatego wartość przechowywana istnieje tylko dla bieżącego cyklu życia jego wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="e2eef-165">But because this is a stateless service, the value that's stored exists only for the current lifecycle of its service instance.</span></span> <span data-ttu-id="e2eef-166">Gdy usługa przenosi lub ponownego uruchomienia, wartość jest utracone.</span><span class="sxs-lookup"><span data-stu-id="e2eef-166">When the service moves or restarts, the value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="e2eef-167">Tworzenie usługi stanowej</span><span class="sxs-lookup"><span data-stu-id="e2eef-167">Create a stateful service</span></span>
<span data-ttu-id="e2eef-168">Sieć szkieletowa usług wprowadzono nowy rodzaj usługi, który jest obiektem stanowym.</span><span class="sxs-lookup"><span data-stu-id="e2eef-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="e2eef-169">Usługa stanowa można zachować stanie niezawodnie w ramach usługi, wspólnie z kodem, który go używa.</span><span class="sxs-lookup"><span data-stu-id="e2eef-169">A stateful service can maintain state reliably within the service itself, co-located with the code that's using it.</span></span> <span data-ttu-id="e2eef-170">Stan dokonuje wysokiej dostępności sieci szkieletowej usług bez konieczności utrwalić stanu do magazynu zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="e2eef-170">State is made highly available by Service Fabric without the need to persist state to an external store.</span></span>

<span data-ttu-id="e2eef-171">Aby przekonwertować wartość licznika z bezstanowej wysokiej dostępności i trwałe, nawet wtedy, gdy usługi są przenoszone lub ponownego uruchomienia, należy usługi stanowej.</span><span class="sxs-lookup"><span data-stu-id="e2eef-171">To convert a counter value from stateless to highly available and persistent, even when the service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="e2eef-172">W tym samym *HelloWorld* aplikacji, można dodać nową usługę prawym przyciskiem myszy w ramach usług odwołań w projekcie aplikacji i wybierając **Nowa usługa sieci szkieletowej usług -> Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="e2eef-172">In the same *HelloWorld* application, you can add a new service by right-clicking on the Services references in the application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Dodawanie usługi do aplikacji sieci szkieletowej usług](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="e2eef-174">Wybierz **usługi Stateful** i nadaj mu nazwę *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="e2eef-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="e2eef-175">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2eef-175">Click **OK**.</span></span>

![Użyj okna dialogowego Nowy projekt do utworzenia nowej usługi stanowej sieci szkieletowej usług](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="e2eef-177">Aplikacja powinna mieć teraz dwie usługi: usługi bezstanowej *HelloWorldStateless* i usługi stanowej *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="e2eef-177">Your application should now have two services: the stateless service *HelloWorldStateless* and the stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="e2eef-178">Usługa stanowa ma tego samego punkty wejścia jako usługę bezstanową.</span><span class="sxs-lookup"><span data-stu-id="e2eef-178">A stateful service has the same entry points as a stateless service.</span></span> <span data-ttu-id="e2eef-179">Główna różnica polega na dostępność *dostawcy stanu* który niezawodne przechowywanie stanu.</span><span class="sxs-lookup"><span data-stu-id="e2eef-179">The main difference is the availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="e2eef-180">Sieć szkieletowa usług jest dostarczany z implementacja dostawcy stanu o nazwie [niezawodnej kolekcje](service-fabric-reliable-services-reliable-collections.md), która umożliwia tworzenie replikowane struktury danych za pośrednictwem niezawodnych menedżera stanu.</span><span class="sxs-lookup"><span data-stu-id="e2eef-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through the Reliable State Manager.</span></span> <span data-ttu-id="e2eef-181">Domyślnie usługa stanowa niezawodnej używa tego dostawcy stanu.</span><span class="sxs-lookup"><span data-stu-id="e2eef-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="e2eef-182">Otwórz **HelloWorldStateful.cs** w *HelloWorldStateful*, który zawiera następujące metodzie RunAsync:</span><span class="sxs-lookup"><span data-stu-id="e2eef-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains the following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
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

            // If an exception is thrown before calling CommitAsync, the transaction aborts, all changes are
            // discarded, and nothing is saved to the secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="e2eef-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="e2eef-183">RunAsync</span></span>
<span data-ttu-id="e2eef-184">`RunAsync()`działa podobnie, w usługach stanowe i bezstanowe.</span><span class="sxs-lookup"><span data-stu-id="e2eef-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="e2eef-185">Jednak w usługi stanowej, platforma wykonuje dodatkowych działań w Twoim imieniu przed rozpoczęciem wykonywania `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="e2eef-185">However, in a stateful service, the platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="e2eef-186">Te działania mogą obejmować zapewnienie, że Menedżer niezawodnej stanu i niezawodne kolekcji są gotowe do użycia.</span><span class="sxs-lookup"><span data-stu-id="e2eef-186">This work can include ensuring that the Reliable State Manager and Reliable Collections are ready to use.</span></span>

### <a name="reliable-collections-and-the-reliable-state-manager"></a><span data-ttu-id="e2eef-187">Kolekcje niezawodnych i niezawodne Menedżer stanu</span><span class="sxs-lookup"><span data-stu-id="e2eef-187">Reliable Collections and the Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="e2eef-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) jest implementacji słownik, który umożliwia niezawodne przechowywanie stanu usługi.</span><span class="sxs-lookup"><span data-stu-id="e2eef-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use to reliably store state in the service.</span></span> <span data-ttu-id="e2eef-189">Z sieci szkieletowej usług i niezawodne kolekcji można przechowywać danych bezpośrednio w usłudze bez konieczności zewnętrznych magazynu trwałego.</span><span class="sxs-lookup"><span data-stu-id="e2eef-189">With Service Fabric and Reliable Collections, you can store data directly in your service without the need for an external persistent store.</span></span> <span data-ttu-id="e2eef-190">Niezawodne kolekcje danych wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="e2eef-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="e2eef-191">Sieć szkieletowa usług rozwiązanie to tworzenie i zarządzanie wieloma *replik* usługi dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="e2eef-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="e2eef-192">Udostępnia również interfejs API, który abstracts optymalizacji złożoności Zarządzanie tych replik, a ich przejścia stanu.</span><span class="sxs-lookup"><span data-stu-id="e2eef-192">It also provides an API that abstracts away the complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="e2eef-193">Kolekcje niezawodnej może przechowywać żadnych typ architektury .NET, łącznie z niestandardowych typów, za pomocą paru ostrzeżenia:</span><span class="sxs-lookup"><span data-stu-id="e2eef-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="e2eef-194">Usługa sieci szkieletowej udostępnia swój stan wysokiej przez *replikowanie* stanu między węzły i niezawodne kolekcje przechowywania danych na dysku lokalnym na każdej repliki.</span><span class="sxs-lookup"><span data-stu-id="e2eef-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data to local disk on each replica.</span></span> <span data-ttu-id="e2eef-195">To oznacza, że wszystkie zasoby, które są przechowywane w niezawodnej kolekcje muszą zostać *serializacji*.</span><span class="sxs-lookup"><span data-stu-id="e2eef-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="e2eef-196">Domyślnie używają niezawodnej kolekcje [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) serializacji, dlatego ważne jest, aby upewnić się, że Twoje typy są [obsługiwane przez serializator kontraktu danych](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) używając domyślnego elementu serializującego.</span><span class="sxs-lookup"><span data-stu-id="e2eef-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important to make sure that your types are [supported by the Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use the default serializer.</span></span>
* <span data-ttu-id="e2eef-197">Obiekty są replikowane wysokiej dostępności po zatwierdzeniu transakcji na niezawodne kolekcji.</span><span class="sxs-lookup"><span data-stu-id="e2eef-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="e2eef-198">Obiekty przechowywane w niezawodnej kolekcje są przechowywane w lokalnej pamięci w usłudze.</span><span class="sxs-lookup"><span data-stu-id="e2eef-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="e2eef-199">Oznacza to, że masz lokalnego odwołania do obiektu.</span><span class="sxs-lookup"><span data-stu-id="e2eef-199">This means that you have a local reference to the object.</span></span>
  
   <span data-ttu-id="e2eef-200">Należy pamiętać, że nie zmodyfikować lokalnych wystąpień tych obiektów, bez wykonywania operacji update na niezawodne kolekcji w transakcji.</span><span class="sxs-lookup"><span data-stu-id="e2eef-200">It is important that you do not mutate local instances of those objects without performing an update operation on the reliable collection in a transaction.</span></span> <span data-ttu-id="e2eef-201">Jest to spowodowane zmiany do lokalnego wystąpienia obiektów, nie będą automatycznie replikowane.</span><span class="sxs-lookup"><span data-stu-id="e2eef-201">This is because changes to local instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="e2eef-202">Musisz ponownie wstawić obiekt do słownika lub użyj jednej z *aktualizacji* metody w słowniku.</span><span class="sxs-lookup"><span data-stu-id="e2eef-202">You must re-insert the object back into the dictionary or use one of the *update* methods on the dictionary.</span></span>

<span data-ttu-id="e2eef-203">Menedżer niezawodnej stanu zarządza niezawodnej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="e2eef-203">The Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="e2eef-204">Po prostu poproś niezawodnej Menedżer stanu niezawodnej kolekcji o nazwie w dowolnym momencie i w dowolnym miejscu w usłudze.</span><span class="sxs-lookup"><span data-stu-id="e2eef-204">You can simply ask the Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="e2eef-205">Niezawodne Menedżer stanu zapewnia ponownie uzyskać odwołanie.</span><span class="sxs-lookup"><span data-stu-id="e2eef-205">The Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="e2eef-206">Nie zaleca się zapisywania odwołań do kolekcji niezawodnej instancji w elemencie członkowskim klasy zmiennych lub właściwości.</span><span class="sxs-lookup"><span data-stu-id="e2eef-206">We don't recommended that you save references to reliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="e2eef-207">Szczególną uwagę należy upewnić się, że odwołanie jest ustawione na wystąpienie przez cały czas w cyklu życia usługi.</span><span class="sxs-lookup"><span data-stu-id="e2eef-207">Special care must be taken to ensure that the reference is set to an instance at all times in the service lifecycle.</span></span> <span data-ttu-id="e2eef-208">Niezawodne Menedżer stanu obsługuje tę pracę za Ciebie i jest zoptymalizowany do powtarzania wizytach.</span><span class="sxs-lookup"><span data-stu-id="e2eef-208">The Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="e2eef-209">Operacje transakcyjne i asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="e2eef-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="e2eef-210">Kolekcje niezawodnej mają wiele operacji, która ich `System.Collections.Generic` i `System.Collections.Concurrent` odpowiednikami z wyjątkiem LINQ.</span><span class="sxs-lookup"><span data-stu-id="e2eef-210">Reliable Collections have many of the same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="e2eef-211">Operacje na niezawodne kolekcje są asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="e2eef-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="e2eef-212">Jest to spowodowane operacji zapisu z kolekcjami niezawodne wykonywanie operacji We/Wy do replikacji i utrwalić danych na dysku.</span><span class="sxs-lookup"><span data-stu-id="e2eef-212">This is because write operations with Reliable Collections perform I/O operations to replicate and persist data to disk.</span></span>

<span data-ttu-id="e2eef-213">Są niezawodne operacje kolekcji *transakcyjnych*, dzięki czemu można zachować stanu spójne w wielu kolekcjach niezawodnej i operacji.</span><span class="sxs-lookup"><span data-stu-id="e2eef-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="e2eef-214">Może na przykład usuwania z kolejki elementu roboczego z kolejką niezawodne, wykonaj operację i zapisać wynik w słowniku niezawodne, wszystkie w ramach pojedynczej transakcji.</span><span class="sxs-lookup"><span data-stu-id="e2eef-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save the result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="e2eef-215">Jest ona traktowana jako operacją niepodzielną i gwarantuje, że cała operacja zostanie wykonana pomyślnie lub całej operacji cofnie.</span><span class="sxs-lookup"><span data-stu-id="e2eef-215">This is treated as an atomic operation, and it guarantees that either the entire operation will succeed or the entire operation will roll back.</span></span> <span data-ttu-id="e2eef-216">Jeśli błąd wystąpi po dequeue elementu, ale przed zapisaniem wynik, cała transakcja zostanie wycofana i element pozostaje w kolejce do przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="e2eef-216">If an error occurs after you dequeue the item but before you save the result, the entire transaction is rolled back and the item remains in the queue for processing.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="e2eef-217">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e2eef-217">Run the application</span></span>
<span data-ttu-id="e2eef-218">Teraz zwróconych do *HelloWorld* aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2eef-218">We now return to the *HelloWorld* application.</span></span> <span data-ttu-id="e2eef-219">Teraz możesz skompilować i wdrażanie usług.</span><span class="sxs-lookup"><span data-stu-id="e2eef-219">You can now build and deploy your services.</span></span> <span data-ttu-id="e2eef-220">Po naciśnięciu **F5**, aplikacja zostanie utworzony i wdrożyć w klastrze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="e2eef-220">When you press **F5**, your application will be built and deployed to your local cluster.</span></span>

<span data-ttu-id="e2eef-221">Po usługi uruchomione, można przejrzeć wygenerowane zdarzenia funkcji Śledzenie zdarzeń systemu Windows () w **zdarzeń diagnostycznych** okna.</span><span class="sxs-lookup"><span data-stu-id="e2eef-221">After the services start running, you can view the generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="e2eef-222">Należy pamiętać, że są wyświetlone zdarzenia z usługi bezstanowej i usługi stanowej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e2eef-222">Note that the events displayed are from both the stateless service and the stateful service in the application.</span></span> <span data-ttu-id="e2eef-223">W przypadku wstrzymania strumienia, klikając **wstrzymać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e2eef-223">You can pause the stream by clicking the **Pause** button.</span></span> <span data-ttu-id="e2eef-224">Następnie można sprawdzić szczegóły komunikatu rozwijając tej wiadomości.</span><span class="sxs-lookup"><span data-stu-id="e2eef-224">You can then examine the details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="e2eef-225">Przed uruchomieniem aplikacji upewnij się, że masz lokalne działania projektowe klastra z systemem.</span><span class="sxs-lookup"><span data-stu-id="e2eef-225">Before you run the application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="e2eef-226">Zapoznaj się z [Wprowadzenie — przewodnik](service-fabric-get-started.md) informacji na temat konfigurowania środowiska lokalnego.</span><span class="sxs-lookup"><span data-stu-id="e2eef-226">Check out the [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Wyświetl zdarzenia diagnostycznego w programie Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="e2eef-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e2eef-228">Next steps</span></span>
[<span data-ttu-id="e2eef-229">Debugowanie aplikacji sieci szkieletowej usług w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e2eef-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="e2eef-230">Wprowadzenie: usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN</span><span class="sxs-lookup"><span data-stu-id="e2eef-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="e2eef-231">Dowiedz się więcej o niezawodnej kolekcje</span><span class="sxs-lookup"><span data-stu-id="e2eef-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="e2eef-232">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e2eef-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="e2eef-233">Uaktualnianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e2eef-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="e2eef-234">Dokumentacja dla deweloperów dla niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="e2eef-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

