---
title: "aaaCreate Twojego pierwszego na podstawie aktora Azure mikrousługi w języku Java | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki tworzenia, debugowania i wdrażania prostego usługi aktora na podstawie przy użyciu usługi sieci szkieletowej Reliable Actors hello."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="a7594-103">Wprowadzenie do korzystania z Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="a7594-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7594-104">C# w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="a7594-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="a7594-105">Java w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="a7594-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="a7594-106">W tym artykule opisano podstawy hello Azure Service Fabric Reliable Actors oraz przedstawiono sposób tworzenia i wdrażania prostą aplikację niezawodnego aktora w języku Java.</span><span class="sxs-lookup"><span data-stu-id="a7594-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="a7594-107">Instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="a7594-107">Installation and setup</span></span>
<span data-ttu-id="a7594-108">Przed rozpoczęciem upewnij się, że masz środowisko projektowania sieci szkieletowej usług hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a7594-108">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="a7594-109">Jeśli potrzebujesz tooset go, przejdź do zbyt[wprowadzenie dla komputerów Mac](service-fabric-get-started-mac.md) lub [wprowadzenie w systemie Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a7594-109">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="a7594-110">Podstawowe pojęcia</span><span class="sxs-lookup"><span data-stu-id="a7594-110">Basic concepts</span></span>
<span data-ttu-id="a7594-111">wprowadzenie Reliable Actors, możesz tylko tooget należy toounderstand kilka podstawowych pojęć:</span><span class="sxs-lookup"><span data-stu-id="a7594-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="a7594-112">**Usługa aktora**.</span><span class="sxs-lookup"><span data-stu-id="a7594-112">**Actor service**.</span></span> <span data-ttu-id="a7594-113">Reliable Actors są popakowane w niezawodnej usługi, które można wdrożyć w infrastrukturze sieci szkieletowej usług hello.</span><span class="sxs-lookup"><span data-stu-id="a7594-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="a7594-114">Wystąpienia aktora zostaną aktywowane w wystąpieniu usługi o nazwie.</span><span class="sxs-lookup"><span data-stu-id="a7594-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="a7594-115">**Rejestracja aktora**.</span><span class="sxs-lookup"><span data-stu-id="a7594-115">**Actor registration**.</span></span> <span data-ttu-id="a7594-116">Jako z usługami Reliable Services, usługi niezawodnego aktora musi toobe zarejestrowane ze środowiskiem uruchomieniowym usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="a7594-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="a7594-117">Ponadto typ aktora hello musi toobe zarejestrowany hello aktora w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="a7594-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="a7594-118">**Interfejs aktora**.</span><span class="sxs-lookup"><span data-stu-id="a7594-118">**Actor interface**.</span></span> <span data-ttu-id="a7594-119">Interfejs aktora Hello jest używany toodefine jednoznacznie interfejs publiczny aktora.</span><span class="sxs-lookup"><span data-stu-id="a7594-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="a7594-120">W terminologii modelu niezawodnego aktora hello hello aktora interfejs definiuje hello typów komunikatów, które hello aktora można zrozumieć i przetworzyć.</span><span class="sxs-lookup"><span data-stu-id="a7594-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="a7594-121">Interfejs aktora Hello jest używany przez innych uczestników i aplikacje klienckie zbyt "Wyślij" (asynchronicznie) aktora toohello wiadomości.</span><span class="sxs-lookup"><span data-stu-id="a7594-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="a7594-122">Reliable Actors można zaimplementować wiele interfejsów.</span><span class="sxs-lookup"><span data-stu-id="a7594-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="a7594-123">**Klasa ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="a7594-123">**ActorProxy class**.</span></span> <span data-ttu-id="a7594-124">Hello ActorProxy klasy jest używany przez klienta tooinvoke aplikacji hello metod udostępnianych za pośrednictwem interfejsu aktora hello.</span><span class="sxs-lookup"><span data-stu-id="a7594-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="a7594-125">Witaj klasy ActorProxy zawiera dwie ważne funkcje:</span><span class="sxs-lookup"><span data-stu-id="a7594-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="a7594-126">Rozpoznawanie nazw: jest w stanie toolocate hello aktora w klastrze hello (Znajdź hello węzeł klastra hello, w którym jest hostowany).</span><span class="sxs-lookup"><span data-stu-id="a7594-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="a7594-127">Obsługa błąd: można ponowić próbę wywołania metody i ponownie rozwiązania lokalizacji aktora powitania po, na przykład błąd, który wymaga toobe aktora hello przeniesiony tooanother węzła w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="a7594-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="a7594-128">następujące reguły, które odnoszą się interfejsów tooactor Hello są warto zauważyć:</span><span class="sxs-lookup"><span data-stu-id="a7594-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="a7594-129">Metody interfejsu aktora nie może być przeciążony.</span><span class="sxs-lookup"><span data-stu-id="a7594-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="a7594-130">Interfejs aktora metody nie może mieć wychodzących, ref lub parametrów opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="a7594-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="a7594-131">Interfejsy ogólne nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a7594-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="a7594-132">Tworzenie usługi aktora</span><span class="sxs-lookup"><span data-stu-id="a7594-132">Create an actor service</span></span>
<span data-ttu-id="a7594-133">Rozpocznij od utworzenia nowej aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="a7594-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="a7594-134">Witaj zestawu SDK sieci szkieletowej usług dla systemu Linux zawiera narzędzia Yeoman generator tooprovide hello szkieletów dla aplikacji sieci szkieletowej usług za pomocą usługi bezstanowej.</span><span class="sxs-lookup"><span data-stu-id="a7594-134">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="a7594-135">Zacznij od uruchomienia hello następujące narzędzia Yeoman polecenia:</span><span class="sxs-lookup"><span data-stu-id="a7594-135">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="a7594-136">Wykonaj hello instrukcje toocreate **niezawodnej usługi aktora**.</span><span class="sxs-lookup"><span data-stu-id="a7594-136">Follow hello instructions toocreate a **Reliable Actor Service**.</span></span> <span data-ttu-id="a7594-137">W tym samouczku nazwa hello aplikacji "HelloWorldActorApplication" i hello aktora "HelloWorldActor."</span><span class="sxs-lookup"><span data-stu-id="a7594-137">For this tutorial, name hello application "HelloWorldActorApplication" and hello actor "HelloWorldActor."</span></span> <span data-ttu-id="a7594-138">zostanie utworzony po szkieletów Hello:</span><span class="sxs-lookup"><span data-stu-id="a7594-138">hello following scaffolding will be created:</span></span>

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="a7594-139">Niezawodne złośliwych użytkowników podstawowych bloków konstrukcyjnych</span><span class="sxs-lookup"><span data-stu-id="a7594-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="a7594-140">podstawowe pojęcia dotyczące Hello opisanych wcześniej przetłumaczenie hello podstawowe bloki konstrukcyjne usługi niezawodnego aktora.</span><span class="sxs-lookup"><span data-stu-id="a7594-140">hello basic concepts described earlier translate into hello basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="a7594-141">Interfejs aktora</span><span class="sxs-lookup"><span data-stu-id="a7594-141">Actor interface</span></span>
<span data-ttu-id="a7594-142">Zawiera definicję interfejsu hello hello aktora.</span><span class="sxs-lookup"><span data-stu-id="a7594-142">This contains hello interface definition for hello actor.</span></span> <span data-ttu-id="a7594-143">Ten interfejs definiuje kontrakt aktora hello, który jest współużytkowany przez hello aktora implementacji i klientom Witaj wywoływania aktora hello, dlatego zazwyczaj ułatwia wykrywanie toodefine w miejscu, które jest oddzielić od hello aktora implementacji i może być współużytkowane przez wiele innych usługi lub aplikacje klienckie.</span><span class="sxs-lookup"><span data-stu-id="a7594-143">This interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in a place that is separate from hello actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="a7594-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="a7594-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="a7594-145">Usługa aktora</span><span class="sxs-lookup"><span data-stu-id="a7594-145">Actor service</span></span>
<span data-ttu-id="a7594-146">Zawiera to implementacja aktora i kod rejestracji aktora.</span><span class="sxs-lookup"><span data-stu-id="a7594-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="a7594-147">Klasa aktora Hello implementuje interfejs aktora hello.</span><span class="sxs-lookup"><span data-stu-id="a7594-147">hello actor class implements hello actor interface.</span></span> <span data-ttu-id="a7594-148">Jest to, gdzie aktora sieci działa jej.</span><span class="sxs-lookup"><span data-stu-id="a7594-148">This is where your actor does its work.</span></span>

<span data-ttu-id="a7594-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="a7594-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a><span data-ttu-id="a7594-150">Rejestracja aktora</span><span class="sxs-lookup"><span data-stu-id="a7594-150">Actor registration</span></span>
<span data-ttu-id="a7594-151">Usługa aktora Hello musi być zarejestrowany w środowisku uruchomieniowym usługi sieć szkieletowa hello typ usługi.</span><span class="sxs-lookup"><span data-stu-id="a7594-151">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="a7594-152">W celu dla hello toorun usługi aktora swoich wystąpień aktora, danego typu aktora również musi być zarejestrowany hello usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="a7594-152">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="a7594-153">Witaj `ActorRuntime` metoda rejestracji wykonuje tej pracy dla osób.</span><span class="sxs-lookup"><span data-stu-id="a7594-153">hello `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="a7594-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="a7594-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a><span data-ttu-id="a7594-155">Klient testowy</span><span class="sxs-lookup"><span data-stu-id="a7594-155">Test client</span></span>
<span data-ttu-id="a7594-156">To jest aplikacją kliencką prosty test można uruchomić osobno z tootest aplikacji usługi sieć szkieletowa hello usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="a7594-156">This is a simple test client application you can run separately from hello Service Fabric application tootest your actor service.</span></span> <span data-ttu-id="a7594-157">To jest przykład gdzie hello ActorProxy może być używane tooactivate i komunikować się z wystąpieniami aktora.</span><span class="sxs-lookup"><span data-stu-id="a7594-157">This is an example of where hello ActorProxy can be used tooactivate and communicate with actor instances.</span></span> <span data-ttu-id="a7594-158">Pobierz nie wdrożone przy użyciu usługi.</span><span class="sxs-lookup"><span data-stu-id="a7594-158">It does not get deployed with your service.</span></span>

### <a name="hello-application"></a><span data-ttu-id="a7594-159">Aplikacja Hello</span><span class="sxs-lookup"><span data-stu-id="a7594-159">hello application</span></span>
<span data-ttu-id="a7594-160">Ponadto pakiety aplikacji hello hello usługi aktora i innych usług, dodawany w hello przyszłych razem dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a7594-160">Finally, hello application packages hello actor service and any other services you might add in hello future together for deployment.</span></span> <span data-ttu-id="a7594-161">Zawiera on hello *ApplicationManifest.xml* i symbole zastępcze dla pakietu z hello aktora.</span><span class="sxs-lookup"><span data-stu-id="a7594-161">It contains hello *ApplicationManifest.xml* and place holders for hello actor service package.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="a7594-162">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="a7594-162">Run hello application</span></span>

<span data-ttu-id="a7594-163">Witaj narzędzia Yeoman szkieletów zawiera narzędzia gradle skryptu toobuild hello aplikacji i bash skrypty toodeploy i Usuń aplikację.</span><span class="sxs-lookup"><span data-stu-id="a7594-163">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="a7594-164">Aplikacja hello toodeploy, pierwsza aplikacja hello kompilacji z narzędziem gradle:</span><span class="sxs-lookup"><span data-stu-id="a7594-164">toodeploy hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="a7594-165">Spowoduje to utworzenie pakietu aplikacji sieci szkieletowej usług, które można wdrożyć przy użyciu narzędzi interfejsu wiersza polecenia usługi sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="a7594-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="a7594-166">Wdrażanie usługi sieci szkieletowej interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="a7594-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="a7594-167">skrypt install.sh Hello zawiera hello niezbędne usługi sieci szkieletowej interfejsu wiersza polecenia (sfctl) polecenia toodeploy hello pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a7594-167">hello install.sh script contains hello necessary Service Fabric CLI (sfctl) commands toodeploy hello application package.</span></span>
<span data-ttu-id="a7594-168">Uruchom hello install.sh skryptu toodeploy hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a7594-168">Run hello install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="a7594-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a7594-169">Next steps</span></span>

* [<span data-ttu-id="a7594-170">Getting started with Service Fabric CLI (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="a7594-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
