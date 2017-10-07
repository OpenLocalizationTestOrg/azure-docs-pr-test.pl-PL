---
title: "aaaCreate Twojego pierwszego niezawodnej mikrousługi Azure w języku Java | Dokumentacja firmy Microsoft"
description: "Wprowadzenie toocreating aplikację usługi sieć szkieletowa usług Microsoft Azure z usług bezstanowych i stanowych."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="6d1ec-103">Wprowadzenie do usług Reliable Services</span><span class="sxs-lookup"><span data-stu-id="6d1ec-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d1ec-104">C# w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="6d1ec-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="6d1ec-105">Java w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="6d1ec-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="6d1ec-106">W tym artykule opisano podstawy hello Azure Usługa sieci szkieletowej niezawodnej usługi oraz przedstawiono sposób tworzenia i wdrażania prostą aplikację niezawodnej usługi napisane w języku Java.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-106">This article explains hello basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="6d1ec-107">Ten film Microsoft Virtual Academy również przedstawiono toocreate bezstanowej niezawodnej usługi:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="6d1ec-107">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="6d1ec-108">Instalacja i Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="6d1ec-108">Installation and setup</span></span>
<span data-ttu-id="6d1ec-109">Przed rozpoczęciem upewnij się, że masz środowisko projektowania sieci szkieletowej usług hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-109">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="6d1ec-110">Jeśli potrzebujesz tooset go, przejdź do zbyt[wprowadzenie dla komputerów Mac](service-fabric-get-started-mac.md) lub [wprowadzenie w systemie Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6d1ec-110">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="6d1ec-111">Podstawowe pojęcia</span><span class="sxs-lookup"><span data-stu-id="6d1ec-111">Basic concepts</span></span>
<span data-ttu-id="6d1ec-112">tooget pracy z usługami Reliable Services, musisz tylko należy toounderstand kilka podstawowych pojęć:</span><span class="sxs-lookup"><span data-stu-id="6d1ec-112">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="6d1ec-113">**Typ usługi**: jest to implementacji usługi.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="6d1ec-114">Jest on zdefiniowany przez klasę hello pisania, rozszerzający `StatelessService` i innego kodu lub zależności używany, oraz nazwę i numer wersji.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-114">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="6d1ec-115">**Nazwane wystąpienie usługi**: toorun usługi tworzenia nazwanego wystąpienia danego typu usługi znacznie tak, jak utworzyć wystąpienia obiektu typu klasy.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-115">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="6d1ec-116">Wystąpienie usługi są w istocie wystąpieniami klasie usługi, który można zapisać obiektu.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="6d1ec-117">**Host usługi**: hello nazwane wystąpienia usługi, utworzyć toorun potrzeby wewnątrz hosta.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-117">**Service host**: hello named service instances you create need toorun inside a host.</span></span> <span data-ttu-id="6d1ec-118">host usługi Hello jest właśnie procesu, których można uruchomić wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-118">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="6d1ec-119">**Usługa rejestracji**: rejestracji, połączono wszystko.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="6d1ec-120">Witaj typ usługi musi być zarejestrowana z hello sieci szkieletowej usług środowiska uruchomieniowego w usłudze hosta tooallow sieci szkieletowej usług toocreate wystąpień toorun.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-120">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="6d1ec-121">Tworzenie usługi bezstanowej</span><span class="sxs-lookup"><span data-stu-id="6d1ec-121">Create a stateless service</span></span>
<span data-ttu-id="6d1ec-122">Rozpocznij od utworzenia aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="6d1ec-123">Witaj zestawu SDK sieci szkieletowej usług dla systemu Linux zawiera narzędzia Yeoman generator tooprovide hello szkieletów dla aplikacji sieci szkieletowej usług za pomocą usługi bezstanowej.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-123">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="6d1ec-124">Zacznij od uruchomienia hello następujące narzędzia Yeoman polecenia:</span><span class="sxs-lookup"><span data-stu-id="6d1ec-124">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="6d1ec-125">Wykonaj hello instrukcje toocreate **usługi bezstanowej niezawodnej**.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-125">Follow hello instructions toocreate a **Reliable Stateless Service**.</span></span> <span data-ttu-id="6d1ec-126">W tym samouczku aplikacji hello nazwy "HelloWorldApplication" i hello usługi "HelloWorld".</span><span class="sxs-lookup"><span data-stu-id="6d1ec-126">For this tutorial, name hello application "HelloWorldApplication" and hello service "HelloWorld".</span></span> <span data-ttu-id="6d1ec-127">wynik Hello obejmuje katalogów hello `HelloWorldApplication` i `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-127">hello result includes directories for hello `HelloWorldApplication` and `HelloWorld`.</span></span>

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a><span data-ttu-id="6d1ec-128">Wdrożenie usługi hello</span><span class="sxs-lookup"><span data-stu-id="6d1ec-128">Implement hello service</span></span>
<span data-ttu-id="6d1ec-129">Otwórz **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="6d1ec-130">Ta klasa definiuje typ usługi hello i można uruchomić dowolny kod.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-130">This class defines hello service type, and can run any code.</span></span> <span data-ttu-id="6d1ec-131">Interfejs API usługi Hello zawiera dwa punkty wejścia kodu:</span><span class="sxs-lookup"><span data-stu-id="6d1ec-131">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="6d1ec-132">Metoda punktu wejścia otwarty, nazywany `runAsync()`, w którym można rozpocząć wykonywania dowolnych zadań, w tym obciążeń obliczeniowych długotrwałe.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="6d1ec-133">Punkt wejścia komunikacji, gdzie można podłączyć stosu komunikacji wyboru.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="6d1ec-134">Jest to, gdzie można uruchomić odbieranie żądań od użytkowników i innych usług.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="6d1ec-135">W tym samouczku, możemy skupić się na powitania `runAsync()` metoda punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-135">In this tutorial, we focus on hello `runAsync()` entry point method.</span></span> <span data-ttu-id="6d1ec-136">Jest to, gdzie natychmiast można rozpocząć uruchamianie kodu.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="6d1ec-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="6d1ec-137">RunAsync</span></span>
<span data-ttu-id="6d1ec-138">Platforma Hello wywołuje tę metodę, gdy wystąpienie usługi jest tooexecute umieścić i gotowe.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-138">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="6d1ec-139">Dla usługi bezstanowej po prostu oznacza to, gdy wystąpienie usługi hello jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-139">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="6d1ec-140">Token anulowania podano toocoordinate, gdy wystąpienie usługi musi toobe zamknięte.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-140">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="6d1ec-141">W sieci szkieletowej usług ten cykl otwarcie i zamknięcie wystąpienia usługi może wystąpić wiele razy w ciągu okresu istnienia hello hello usługi jako całość.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-141">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="6d1ec-142">Może się to zdarzyć z różnych powodów, w tym:</span><span class="sxs-lookup"><span data-stu-id="6d1ec-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="6d1ec-143">Hello system przenosi swoich wystąpień usługi dla równoważenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-143">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="6d1ec-144">Błędy występują w kodzie.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-144">Faults occur in your code.</span></span>
* <span data-ttu-id="6d1ec-145">Uaktualnianie aplikacji Hello lub systemu.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-145">hello application or system is upgraded.</span></span>
* <span data-ttu-id="6d1ec-146">używany sprzęt Hello ulegnie awarii.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-146">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="6d1ec-147">Aranżacja jest zarządzana przez sieć szkieletowa usług tookeep usługi wysokiej dostępności i nieprawidłowo zrównoważone.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-147">This orchestration is managed by Service Fabric tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="6d1ec-148">`runAsync()`nie zablokować synchronicznie.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="6d1ec-149">Implementacji runAsync powinien zwrócić CompletableFuture tooallow hello środowiska uruchomieniowego toocontinue.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-149">Your implementation of runAsync should return a CompletableFuture tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="6d1ec-150">Jeśli obciążenie musi tooimplement długotrwała zadanie, które należy wykonać wewnątrz hello CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-150">If your workload needs tooimplement a long running task that should be done inside hello CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="6d1ec-151">Anulowanie</span><span class="sxs-lookup"><span data-stu-id="6d1ec-151">Cancellation</span></span>
<span data-ttu-id="6d1ec-152">Anulowanie obciążenie jest współpracy wysiłku, zorkiestrowana przez hello podany token anulowania.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-152">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="6d1ec-153">Hello system oczekuje tooend Twojego zadania (przez pomyślne zakończenie anulowania lub fault) przed przesyłane w.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-153">hello system waits for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="6d1ec-154">Jest ważne toohonor hello anulowania tokenu, Zakończ wszelkie pracy i zamknięcie `runAsync()` tak szybko jak to możliwe, gdy hello system żądań anulowania.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-154">It is important toohonor hello cancellation token, finish any work, and exit `runAsync()` as quickly as possible when hello system requests cancellation.</span></span> <span data-ttu-id="6d1ec-155">Witaj poniższym przykładzie pokazano, jak toohandle zdarzenia anulowania:</span><span class="sxs-lookup"><span data-stu-id="6d1ec-155">hello following example demonstrates how toohandle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a><span data-ttu-id="6d1ec-156">Rejestracja usługi</span><span class="sxs-lookup"><span data-stu-id="6d1ec-156">Service registration</span></span>
<span data-ttu-id="6d1ec-157">Środowisko uruchomieniowe usługi sieć szkieletowa hello musi być zarejestrowany typów usług.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-157">Service types must be registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="6d1ec-158">Typ usługi Hello jest zdefiniowany w hello `ServiceManifest.xml` i klasie usługi, który implementuje `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-158">hello service type is defined in hello `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="6d1ec-159">Rejestracja usługi jest wykonywane w hello proces główny punkt wejścia.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-159">Service registration is performed in hello process main entry point.</span></span> <span data-ttu-id="6d1ec-160">W tym przykładzie hello jest główny punkt wejścia procesu `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="6d1ec-160">In this example, hello process main entry point is `HelloWorldServiceHost.java`:</span></span>

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="6d1ec-161">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="6d1ec-161">Run hello application</span></span>

<span data-ttu-id="6d1ec-162">Witaj narzędzia Yeoman szkieletów zawiera narzędzia gradle skryptu toobuild hello aplikacji i bash skrypty toodeploy i Usuń aplikację.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-162">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="6d1ec-163">Aplikacja hello toorun, pierwsza aplikacja hello kompilacji z narzędziem gradle:</span><span class="sxs-lookup"><span data-stu-id="6d1ec-163">toorun hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="6d1ec-164">Daje to pakiet aplikacji sieci szkieletowej usług, które można wdrożyć przy użyciu interfejsu wiersza polecenia usługi sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="6d1ec-165">Wdrażanie z sieci szkieletowej usług interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="6d1ec-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="6d1ec-166">skrypt install.sh Hello zawiera hello niezbędne usługi sieci szkieletowej interfejsu wiersza polecenia polecenia toodeploy hello pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-166">hello install.sh script contains hello necessary Service Fabric CLI commands toodeploy hello application package.</span></span> <span data-ttu-id="6d1ec-167">Uruchamianie aplikacji hello toodeploy skryptu install.sh.</span><span class="sxs-lookup"><span data-stu-id="6d1ec-167">Run the install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="6d1ec-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d1ec-168">Next steps</span></span>

* [<span data-ttu-id="6d1ec-169">Getting started with Service Fabric CLI (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="6d1ec-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
