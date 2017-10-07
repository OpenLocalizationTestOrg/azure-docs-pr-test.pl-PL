---
title: "aaaCreate Twojego pierwszego na podstawie aktora Azure mikrousługi w języku C# | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki tworzenia, debugowania i wdrażania prostego usługi aktora na podstawie przy użyciu usługi sieci szkieletowej Reliable Actors hello."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="6551b-103">Wprowadzenie do korzystania z Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="6551b-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6551b-104">C# w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="6551b-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="6551b-105">Java w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="6551b-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="6551b-106">W tym artykule opisano podstawy hello Azure Service Fabric Reliable Actors oraz przeprowadzi Cię przez proces tworzenia, debugowania i wdrażanie prostej aplikacji niezawodnego aktora w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6551b-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="6551b-107">Instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="6551b-107">Installation and setup</span></span>
<span data-ttu-id="6551b-108">Przed rozpoczęciem upewnij się, że masz środowisko projektowania sieci szkieletowej usług hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6551b-108">Before you start, ensure that you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="6551b-109">Jeśli potrzebujesz tooset go, zobaczyć szczegółowe instrukcje dotyczące [jak tooset się środowisko projektowe hello](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6551b-109">If you need tooset it up, see detailed instructions on [how tooset up hello development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="6551b-110">Podstawowe pojęcia</span><span class="sxs-lookup"><span data-stu-id="6551b-110">Basic concepts</span></span>
<span data-ttu-id="6551b-111">wprowadzenie Reliable Actors, możesz tylko tooget należy toounderstand kilka podstawowych pojęć:</span><span class="sxs-lookup"><span data-stu-id="6551b-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="6551b-112">**Usługa aktora**.</span><span class="sxs-lookup"><span data-stu-id="6551b-112">**Actor service**.</span></span> <span data-ttu-id="6551b-113">Reliable Actors są popakowane w niezawodnej usługi, które można wdrożyć w infrastrukturze sieci szkieletowej usług hello.</span><span class="sxs-lookup"><span data-stu-id="6551b-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="6551b-114">Wystąpienia aktora zostaną aktywowane w wystąpieniu usługi o nazwie.</span><span class="sxs-lookup"><span data-stu-id="6551b-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="6551b-115">**Rejestracja aktora**.</span><span class="sxs-lookup"><span data-stu-id="6551b-115">**Actor registration**.</span></span> <span data-ttu-id="6551b-116">Jako z usługami Reliable Services, usługi niezawodnego aktora musi toobe zarejestrowane ze środowiskiem uruchomieniowym usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="6551b-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="6551b-117">Ponadto typ aktora hello musi toobe zarejestrowany hello aktora w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="6551b-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="6551b-118">**Interfejs aktora**.</span><span class="sxs-lookup"><span data-stu-id="6551b-118">**Actor interface**.</span></span> <span data-ttu-id="6551b-119">Interfejs aktora Hello jest używany toodefine jednoznacznie interfejs publiczny aktora.</span><span class="sxs-lookup"><span data-stu-id="6551b-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="6551b-120">W terminologii modelu niezawodnego aktora hello hello aktora interfejs definiuje hello typów komunikatów, które hello aktora można zrozumieć i przetworzyć.</span><span class="sxs-lookup"><span data-stu-id="6551b-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="6551b-121">Interfejs aktora Hello jest używany przez innych uczestników i aplikacje klienckie zbyt "Wyślij" (asynchronicznie) aktora toohello wiadomości.</span><span class="sxs-lookup"><span data-stu-id="6551b-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="6551b-122">Reliable Actors można zaimplementować wiele interfejsów.</span><span class="sxs-lookup"><span data-stu-id="6551b-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="6551b-123">**Klasa ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="6551b-123">**ActorProxy class**.</span></span> <span data-ttu-id="6551b-124">Hello ActorProxy klasy jest używany przez klienta tooinvoke aplikacji hello metod udostępnianych za pośrednictwem interfejsu aktora hello.</span><span class="sxs-lookup"><span data-stu-id="6551b-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="6551b-125">Witaj klasy ActorProxy zawiera dwie ważne funkcje:</span><span class="sxs-lookup"><span data-stu-id="6551b-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="6551b-126">Rozpoznawanie nazw: jest w stanie toolocate hello aktora w klastrze hello (Znajdź hello węzeł klastra hello, w którym jest hostowany).</span><span class="sxs-lookup"><span data-stu-id="6551b-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="6551b-127">Obsługa błąd: można ponowić próbę wywołania metody i ponownie rozwiązania lokalizacji aktora powitania po, na przykład błąd, który wymaga toobe aktora hello przeniesiony tooanother węzła w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="6551b-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="6551b-128">następujące reguły, które odnoszą się interfejsów tooactor Hello są warto zauważyć:</span><span class="sxs-lookup"><span data-stu-id="6551b-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="6551b-129">Metody interfejsu aktora nie może być przeciążony.</span><span class="sxs-lookup"><span data-stu-id="6551b-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="6551b-130">Interfejs aktora metody nie może mieć wychodzących, ref lub parametrów opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="6551b-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="6551b-131">Interfejsy ogólne nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="6551b-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="6551b-132">Utwórz nowy projekt w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6551b-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="6551b-133">Uruchom program Visual Studio 2015 lub Visual Studio 2017 jako administrator, a następnie utwórz nowy projekt aplikacji sieci szkieletowej usług:</span><span class="sxs-lookup"><span data-stu-id="6551b-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Narzędzia usługi sieć szkieletowa usług dla programu Visual Studio — nowy projekt][1]

<span data-ttu-id="6551b-135">Okno dialogowe dalej hello można wybrać typ hello projektu, które mają toocreate.</span><span class="sxs-lookup"><span data-stu-id="6551b-135">In hello next dialog box, you can choose hello type of project that you want toocreate.</span></span>

![Szablony projektu sieci szkieletowej usług][5]

<span data-ttu-id="6551b-137">Dla projektu HelloWorld hello Użyjmy hello usługi Reliable Actors sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="6551b-137">For hello HelloWorld project, let's use hello Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="6551b-138">Po utworzeniu rozwiązania hello powinny być widoczne następujące struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6551b-138">After you have created hello solution, you should see hello following structure:</span></span>

![Struktury projektu sieci szkieletowej usług][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="6551b-140">Niezawodne złośliwych użytkowników podstawowych bloków konstrukcyjnych</span><span class="sxs-lookup"><span data-stu-id="6551b-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="6551b-141">Typowe rozwiązania Reliable Actors składa się z trzech projektów:</span><span class="sxs-lookup"><span data-stu-id="6551b-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="6551b-142">**Projekt aplikacji Hello (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="6551b-142">**hello application project (MyActorApplication)**.</span></span> <span data-ttu-id="6551b-143">Jest to projekt hello wszystkich usług hello razem wdrożenia pakietów.</span><span class="sxs-lookup"><span data-stu-id="6551b-143">This is hello project that packages all of hello services together for deployment.</span></span> <span data-ttu-id="6551b-144">Zawiera on hello *ApplicationManifest.xml* i skrypty programu PowerShell do zarządzania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6551b-144">It contains hello *ApplicationManifest.xml* and PowerShell scripts for managing hello application.</span></span>
* <span data-ttu-id="6551b-145">**Projekt interfejsu Hello (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="6551b-145">**hello interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="6551b-146">Jest to projekt hello, który zawiera definicję interfejsu hello hello aktora.</span><span class="sxs-lookup"><span data-stu-id="6551b-146">This is hello project that contains hello interface definition for hello actor.</span></span> <span data-ttu-id="6551b-147">W projekcie MyActor.Interfaces hello można zdefiniować hello interfejsów, które będą używane przez uczestników hello hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6551b-147">In hello MyActor.Interfaces project, you can define hello interfaces that will be used by hello actors in hello solution.</span></span> <span data-ttu-id="6551b-148">Interfejsów aktora można zdefiniować w każdym projekcie z żadną nazwą, jednak hello interfejs definiuje hello aktora kontraktu, który jest współużytkowany przez implementację aktora hello i klientów hello wywoływania aktora hello, dlatego zazwyczaj ułatwia wykrywanie toodefine w zestawie, do którego jest oddzielić od hello aktora implementacji i może być współużytkowane przez wiele innych projektów.</span><span class="sxs-lookup"><span data-stu-id="6551b-148">Your actor interfaces can be defined in any project with any name, however hello interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in an assembly that is separate from hello actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="6551b-149">**projekt usługi aktora Hello (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="6551b-149">**hello actor service project (MyActor)**.</span></span> <span data-ttu-id="6551b-150">To jest hello projektu używany toodefine hello usługi sieć szkieletowa jest będzie toohost hello aktora.</span><span class="sxs-lookup"><span data-stu-id="6551b-150">This is hello project used toodefine hello Service Fabric service that is going toohost hello actor.</span></span> <span data-ttu-id="6551b-151">Zawiera ona wdrożenia hello hello aktora.</span><span class="sxs-lookup"><span data-stu-id="6551b-151">It contains hello implementation of hello actor.</span></span> <span data-ttu-id="6551b-152">Implementacja aktora jest klasa, która pochodzi z typu podstawowego hello `Actor` i implementuje hello interfejsów, które są zdefiniowane w projekcie MyActor.Interfaces hello.</span><span class="sxs-lookup"><span data-stu-id="6551b-152">An actor implementation is a class that derives from hello base type `Actor` and implements hello interface(s) that are defined in hello MyActor.Interfaces project.</span></span> <span data-ttu-id="6551b-153">Klasa aktora musi także implementować konstruktora akceptującego `ActorService` wystąpienia i `ActorId` i przekazuje je toohello podstawowej `Actor` klasy.</span><span class="sxs-lookup"><span data-stu-id="6551b-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them toohello base `Actor` class.</span></span> <span data-ttu-id="6551b-154">Dzięki temu iniekcji zależności konstruktora zależności platformy.</span><span class="sxs-lookup"><span data-stu-id="6551b-154">This allows for constructor dependency injection of platform dependencies.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

<span data-ttu-id="6551b-155">Usługa aktora Hello musi być zarejestrowany w środowisku uruchomieniowym usługi sieć szkieletowa hello typ usługi.</span><span class="sxs-lookup"><span data-stu-id="6551b-155">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="6551b-156">W celu dla hello toorun usługi aktora swoich wystąpień aktora, danego typu aktora również musi być zarejestrowany hello usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="6551b-156">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="6551b-157">Witaj `ActorRuntime` metoda rejestracji wykonuje tej pracy dla osób.</span><span class="sxs-lookup"><span data-stu-id="6551b-157">hello `ActorRuntime` registration method performs this work for actors.</span></span>

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

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

<span data-ttu-id="6551b-158">Jeśli masz tylko jedną definicję aktora w przypadku uruchomienia nowego projektu programu Visual Studio, rejestracja hello jest domyślnie włączone w hello kod, który generuje Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6551b-158">If you start from a new project in Visual Studio and you have only one actor definition, hello registration is included by default in hello code that Visual Studio generates.</span></span> <span data-ttu-id="6551b-159">Po zdefiniowaniu innych uczestników w usłudze hello należy tooadd hello aktora rejestracji przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="6551b-159">If you define other actors in hello service, you need tooadd hello actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="6551b-160">Witaj środowisko uruchomieniowe usługi sieć szkieletowa podmiotów emituje niektóre [zdarzenia i liczniki wydajności związane z metody tooactor](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="6551b-160">hello Service Fabric Actors runtime emits some [events and performance counters related tooactor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="6551b-161">Są one przydatne w Diagnostyka i monitorowanie wydajności.</span><span class="sxs-lookup"><span data-stu-id="6551b-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="6551b-162">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="6551b-162">Debugging</span></span>
<span data-ttu-id="6551b-163">Witaj usługi Service Fabric tools dla Visual Studio obsługuje debugowania na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="6551b-163">hello Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="6551b-164">Możesz uruchomić sesję debugowania hello naciskać klawisz F5.</span><span class="sxs-lookup"><span data-stu-id="6551b-164">You can start a debugging session by hitting hello F5 key.</span></span> <span data-ttu-id="6551b-165">Visual Studio kompiluje (w razie potrzeby) pakietów.</span><span class="sxs-lookup"><span data-stu-id="6551b-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="6551b-166">Również wdraża aplikację hello na powitania lokalnego klastra usługi sieć szkieletowa usług i dołącza debuger hello.</span><span class="sxs-lookup"><span data-stu-id="6551b-166">It also deploys hello application on hello local Service Fabric cluster and attaches hello debugger.</span></span>

<span data-ttu-id="6551b-167">Podczas procesu wdrażania hello, możesz wyświetlić postęp hello na powitania **dane wyjściowe** okna.</span><span class="sxs-lookup"><span data-stu-id="6551b-167">During hello deployment process, you can see hello progress in hello **Output** window.</span></span>

![Okno danych wyjściowych debugowania sieci szkieletowej usług][3]

## <a name="next-steps"></a><span data-ttu-id="6551b-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6551b-169">Next steps</span></span>
<span data-ttu-id="6551b-170">Dowiedz się więcej o [wykorzystania platformy Service Fabric hello Reliable Actors](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="6551b-170">Learn more about [how Reliable Actors use hello Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
