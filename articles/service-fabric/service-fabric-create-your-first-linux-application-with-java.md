---
title: "aaaCreate aplikacji Java niezawodnej podmiotów sieć szkieletowa usług Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i wdrożenie aplikacji Java sieci szkieletowej usług niezawodnej złośliwych użytkowników w ciągu pięciu minut."
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="94447-103">Tworzenie pierwszej aplikacji Java z interfejsem Reliable Actors usługi Service Fabric w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="94447-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="94447-104">C# — Windows</span><span class="sxs-lookup"><span data-stu-id="94447-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="94447-105">Java — Linux</span><span class="sxs-lookup"><span data-stu-id="94447-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="94447-106">C# — Linux</span><span class="sxs-lookup"><span data-stu-id="94447-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="94447-107">Ten przewodnik Szybki start pomaga w ciągu kilku minut utworzyć pierwszą aplikację Java usługi Azure Service Fabric w środowisku projektowym w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="94447-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="94447-108">Gdy skończysz, będziesz mieć prostą aplikację usługi pojedynczej Java uruchomionych na powitania lokalnego klastra projektowego.</span><span class="sxs-lookup"><span data-stu-id="94447-108">When you are finished, you'll have a simple Java single-service application running on hello local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="94447-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="94447-109">Prerequisites</span></span>
<span data-ttu-id="94447-110">Przed rozpoczęciem pracy Zainstaluj hello zestawu SDK usług sieci szkieletowej, hello usługi sieci szkieletowej interfejsu wiersza polecenia, a konfiguracja klastra Programowanie w Twojej [środowisko projektowe Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="94447-110">Before you get started, install hello Service Fabric SDK, hello Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="94447-111">Jeśli używasz systemu Mac OS X, możesz [skonfigurować środowisko deweloperskie systemu Linux na maszynie wirtualnej za pomocą narzędzia Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="94447-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="94447-112">Ma również tooinstall hello [interfejsu wiersza polecenia usługi sieć szkieletowa](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="94447-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-hello-generators-for-java"></a><span data-ttu-id="94447-113">Instalowanie i konfigurowanie hello generatory dla języka Java</span><span class="sxs-lookup"><span data-stu-id="94447-113">Install and set up hello generators for Java</span></span>
<span data-ttu-id="94447-114">Usługa Service Fabric udostępnia narzędzia do tworzenia szkieletu, które ułatwiają tworzenie aplikacji Java usługi Service Fabric z poziomu terminalu przy użyciu generatora szablonów Yeoman.</span><span class="sxs-lookup"><span data-stu-id="94447-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="94447-115">Wykonaj kroki hello poniżej tooensure ma generatora narzędzia yeoman szablonu usługi sieć szkieletowa hello for Java działa na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="94447-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="94447-116">Zainstaluj środowisko NodeJs i menedżera NPM na swojej maszynie</span><span class="sxs-lookup"><span data-stu-id="94447-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="94447-117">Zainstaluj generator szablonów [narzędzia Yeoman](http://yeoman.io/) na swoim komputerze z poziomu narzędzia NPM</span><span class="sxs-lookup"><span data-stu-id="94447-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="94447-118">Zainstaluj generator aplikacji usługi sieci szkieletowej Yeo Java hello z pakietu NPM</span><span class="sxs-lookup"><span data-stu-id="94447-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a><span data-ttu-id="94447-119">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="94447-119">Create hello application</span></span>
<span data-ttu-id="94447-120">Aplikacja usługi Service Fabric zawiera jeden lub więcej usług, a każda z określoną rolę w dostarczaniu funkcjonalności aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="94447-120">A Service Fabric application contains one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="94447-121">generator Hello zainstalowane w ostatniej sekcji hello umożliwia łatwe toocreate pierwszą usługi i tooadd więcej później.</span><span class="sxs-lookup"><span data-stu-id="94447-121">hello generator you installed in hello last section, makes it easy toocreate your first service and tooadd more later.</span></span>  <span data-ttu-id="94447-122">Możesz też tworzyć, kompilować i wdrażać aplikacje Java usługi Service Fabric przy użyciu wtyczki dla środowiska Eclipse.</span><span class="sxs-lookup"><span data-stu-id="94447-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="94447-123">Zobacz [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md) (Tworzenie i wdrażanie pierwszej aplikacji Java za pomocą środowiska Eclipse).</span><span class="sxs-lookup"><span data-stu-id="94447-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="94447-124">Dla tego szybki start Użyj narzędzia Yeoman toocreate aplikacji za pomocą jednej usługi, która przechowuje i pobiera wartość licznika.</span><span class="sxs-lookup"><span data-stu-id="94447-124">For this quick start, use Yeoman toocreate an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="94447-125">Na terminalu wpisz ``yo azuresfjava``.</span><span class="sxs-lookup"><span data-stu-id="94447-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="94447-126">Nadaj nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94447-126">Name your application.</span></span>
3. <span data-ttu-id="94447-127">Wybierz typ hello pierwszej usługi i nadaj jej nazwę.</span><span class="sxs-lookup"><span data-stu-id="94447-127">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="94447-128">Na potrzeby tego samouczka wybierz usługę Reliable Actor Service.</span><span class="sxs-lookup"><span data-stu-id="94447-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="94447-129">Aby uzyskać więcej informacji na temat hello innych typów usług, zobacz [usługi sieć szkieletowa omówienie modelu programowania](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="94447-129">For more information about hello other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="94447-130">![Generator Yeoman usługi Service Fabric dla platformy Java][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="94447-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="94447-131">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="94447-131">Build hello application</span></span>
<span data-ttu-id="94447-132">Hello narzędzia usługi sieć szkieletowa Yeoman szablony obejmują skryptu kompilacji dla [Gradle](https://gradle.org/), który można użyć aplikacji hello toobuild z hello terminala.</span><span class="sxs-lookup"><span data-stu-id="94447-132">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span>
<span data-ttu-id="94447-133">Zależności aplikacji Java usługi Service Fabric są pobierane z narzędzia Maven.</span><span class="sxs-lookup"><span data-stu-id="94447-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="94447-134">toobuild i pracy w aplikacji Java sieci szkieletowej usług hello należy tooensure, że masz JDK i zainstalowane narzędzia Gradle.</span><span class="sxs-lookup"><span data-stu-id="94447-134">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="94447-135">Jeśli nie został jeszcze zainstalowany, możesz uruchomić hello tooinstall JDK(openjdk-8-jdk) i Gradle -</span><span class="sxs-lookup"><span data-stu-id="94447-135">If not yet installed, you can run hello following tooinstall JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="94447-136">toobuild i pakietów hello aplikacji, uruchom następujące hello:</span><span class="sxs-lookup"><span data-stu-id="94447-136">toobuild and package hello application, run hello following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="94447-137">Wdrażanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="94447-137">Deploy hello application</span></span>
<span data-ttu-id="94447-138">Po utworzeniu aplikacji hello można wdrożyć klaster lokalny toohello.</span><span class="sxs-lookup"><span data-stu-id="94447-138">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="94447-139">Połącz toohello lokalnego klastra usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="94447-139">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="94447-140">Uruchom skrypt instalacji hello hello szablonu toocopy aplikacji hello pakietu magazynu obrazu klastra toohello, Rejestracja typu aplikacji hello, i Utwórz wystąpienie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="94447-140">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="94447-141">Wdrażanie aplikacji hello wbudowane jest hello takie same jak innych aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="94447-141">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="94447-142">Zobacz dokumentację hello [Zarządzanie aplikacją sieci szkieletowej usług z hello interfejsu wiersza polecenia usługi sieć szkieletowa](service-fabric-application-lifecycle-sfctl.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="94447-142">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="94447-143">Parametry toothese polecenia można znaleźć w manifestach hello generowane w pakiecie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="94447-143">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="94447-144">Po wdrożeniu aplikacji hello, otwórz przeglądarkę i przejdź do [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) w [http://localhost: 19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="94447-144">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="94447-145">Następnie rozwiń hello **aplikacji** węzeł i zwróć uwagę, że istnieją teraz wpis dla danego typu aplikacji i drugi dla hello pierwsze wystąpienie tego typu.</span><span class="sxs-lookup"><span data-stu-id="94447-145">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="94447-146">Uruchomić klienta testowego hello i przejściu w tryb failover</span><span class="sxs-lookup"><span data-stu-id="94447-146">Start hello test client and perform a failover</span></span>
<span data-ttu-id="94447-147">Złośliwych użytkowników nie rób nic na ich własnych, wymagają innego toosend usługi lub klienta ich wiadomości.</span><span class="sxs-lookup"><span data-stu-id="94447-147">Actors do not do anything on their own, they require another service or client toosend them messages.</span></span> <span data-ttu-id="94447-148">Szablon aktora Hello zawiera skrypt prosty test przy użyciu usługi aktora hello można toointeract.</span><span class="sxs-lookup"><span data-stu-id="94447-148">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="94447-149">Uruchom skrypt hello przy użyciu hello czujki narzędzie toosee hello dane wyjściowe hello usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="94447-149">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>  <span data-ttu-id="94447-150">skrypt testu Hello wywołuje hello `setCountAsync()` hello wywołania metod na powitania aktora tooincrement licznika, `getCountAsync()` metody na powitania aktora tooget hello nowa wartość licznika i wyświetla, które wartość toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="94447-150">hello test script calls hello `setCountAsync()` method on hello actor tooincrement a counter, calls hello `getCountAsync()` method on hello actor tooget hello new counter value, and displays that value toohello console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="94447-151">W narzędziu Service Fabric Explorer Znajdź hello węzła hostingu hello repliki podstawowej dla usługi aktora hello.</span><span class="sxs-lookup"><span data-stu-id="94447-151">In Service Fabric Explorer, locate hello node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="94447-152">W poniższym zrzucie ekranu hello jest węzeł 3.</span><span class="sxs-lookup"><span data-stu-id="94447-152">In hello screenshot below, it is node 3.</span></span> <span data-ttu-id="94447-153">uchwyty replika podstawowa usługa Hello operacje odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="94447-153">hello primary service replica handles read and write operations.</span></span>  <span data-ttu-id="94447-154">Zmiany stanu usługi są następnie replikowane limit toohello replikach pomocniczych, uruchomione w węzłach 0 i 1 na ekranie powitania zrzut poniżej.</span><span class="sxs-lookup"><span data-stu-id="94447-154">Changes in service state are then replicated out toohello secondary replicas, running on nodes 0 and 1 in hello screen shot below.</span></span>

    ![Znajdowanie hello repliki podstawowej w narzędziu Service Fabric Explorer][sfx-primary]

3. <span data-ttu-id="94447-156">W **węzłów**, kliknij węzeł hello można znaleźć w poprzednim kroku hello, a następnie wybierz **Dezaktywuj (ponowne uruchomienie)** z menu Akcje hello.</span><span class="sxs-lookup"><span data-stu-id="94447-156">In **Nodes**, click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="94447-157">Ta akcja uruchamia ponownie węzeł hello działa replika podstawowa usługa hello i wymusza tooone trybu failover, hello replik pomocniczych uruchomiona w innym węźle.</span><span class="sxs-lookup"><span data-stu-id="94447-157">This action restarts hello node running hello primary service replica and forces a failover tooone of hello secondary replicas running on another node.</span></span>  <span data-ttu-id="94447-158">Tej repliki pomocniczej jest awansowana tooprimary innej repliki pomocniczej jest tworzona na inny węzeł i repliki podstawowej hello rozpoczyna tootake operacji odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="94447-158">That secondary replica is promoted tooprimary, another secondary replica is created on a different node, and hello primary replica begins tootake read/write operations.</span></span> <span data-ttu-id="94447-159">Podczas ponownego uruchamiania hello węzła, obejrzyj dane wyjściowe hello powitania klienta testowego i Uwaga tego licznika hello nadal tooincrement pomimo hello trybu failover.</span><span class="sxs-lookup"><span data-stu-id="94447-159">As hello node restarts, watch hello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="remove-hello-application"></a><span data-ttu-id="94447-160">Usuwanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="94447-160">Remove hello application</span></span>
<span data-ttu-id="94447-161">Użyj hello Odinstaluj skryptu wystąpienia aplikacji hello hello szablonu toodelete wyrejestrować pakiet aplikacji hello i usuwanie pakietu aplikacji hello z magazynu obrazu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="94447-161">Use hello uninstall script provided in hello template toodelete hello application instance, unregister hello application package, and remove hello application package from hello cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="94447-162">W narzędziu Service Fabric explorer widać, że aplikacja hello i typu aplikacji nie są widoczne w hello **aplikacji** węzła.</span><span class="sxs-lookup"><span data-stu-id="94447-162">In Service Fabric explorer you see that hello application and application type no longer appear in hello **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="94447-163">Biblioteki Java usługi Service Fabric w narzędziu Maven</span><span class="sxs-lookup"><span data-stu-id="94447-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="94447-164">Biblioteki Java usługi Service Fabric są teraz hostowane w narzędziu Maven.</span><span class="sxs-lookup"><span data-stu-id="94447-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="94447-165">Można dodać zależności hello hello ``pom.xml`` lub ``build.gradle`` z bibliotek usługi sieć szkieletowa Java toouse projektów z **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="94447-165">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="94447-166">Aktorzy</span><span class="sxs-lookup"><span data-stu-id="94447-166">Actors</span></span>

<span data-ttu-id="94447-167">Obsługa interfejsu Reliable Actors usługi Service Fabric dla Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94447-167">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="94447-168">Usługi</span><span class="sxs-lookup"><span data-stu-id="94447-168">Services</span></span>

<span data-ttu-id="94447-169">Obsługa usługi bezstanowej usługi Service Fabric dla Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94447-169">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="94447-170">Inne</span><span class="sxs-lookup"><span data-stu-id="94447-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="94447-171">Transport</span><span class="sxs-lookup"><span data-stu-id="94447-171">Transport</span></span>

<span data-ttu-id="94447-172">Obsługa warstwy transportowej dla aplikacji Java usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="94447-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="94447-173">Nie trzeba tooexplicitly dodawać tej zależności tooyour niezawodnego aktora lub aplikacje usług, chyba że program na powitania warstwy transportowej.</span><span class="sxs-lookup"><span data-stu-id="94447-173">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="94447-174">Obsługa usługi Service Fabric</span><span class="sxs-lookup"><span data-stu-id="94447-174">Fabric support</span></span>

<span data-ttu-id="94447-175">System poziomu obsługę sieci szkieletowej usług, który zawiera środowisko uruchomieniowe usługi sieć szkieletowa toonative.</span><span class="sxs-lookup"><span data-stu-id="94447-175">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="94447-176">Nie trzeba tooexplicitly Dodawanie tej zależności tooyour niezawodnego aktora lub aplikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="94447-176">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="94447-177">Pobiera pobrania automatycznie z Maven, po dołączeniu hello innych zależności powyżej.</span><span class="sxs-lookup"><span data-stu-id="94447-177">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="94447-178">Migrowanie starego toobe aplikacji Java sieci szkieletowej usług używany z Maven</span><span class="sxs-lookup"><span data-stu-id="94447-178">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="94447-179">Biblioteki usługi sieć szkieletowa Java niedawno został przeniesiony z repozytorium tooMaven zestawu SDK Java sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="94447-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="94447-180">Gdy hello nowe aplikacje, które można wygenerować za pomocą narzędzia Yeoman lub Eclipse, spowoduje wygenerowanie najnowsze zaktualizowane projekty (które będą mogli toowork z Maven), można aktualizacji istniejącej sieci szkieletowej usług bezstanowych lub aplikacji Java aktora, które były używane hello usługi Sieć szkieletowa zestawu Java SDK wcześniej, zależności usługi sieci szkieletowej Java hello toouse z Maven.</span><span class="sxs-lookup"><span data-stu-id="94447-180">While hello new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="94447-181">Wykonaj kroki hello wymienione [tutaj](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure starszych aplikacji współdziała z Maven.</span><span class="sxs-lookup"><span data-stu-id="94447-181">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94447-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="94447-182">Next steps</span></span>

* [<span data-ttu-id="94447-183">Tworzenie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu środowiska Eclipse</span><span class="sxs-lookup"><span data-stu-id="94447-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="94447-184">Dowiedz się więcej o usłudze Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="94447-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="94447-185">Interakcji z klastrami usługi sieć szkieletowa usług za pomocą hello usługi sieci szkieletowej interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="94447-185">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="94447-186">Uzyskaj informacje o [opcjach pomocy technicznej usługi Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="94447-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="94447-187">Getting started with Service Fabric CLI (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="94447-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
