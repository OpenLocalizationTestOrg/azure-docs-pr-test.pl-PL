---
title: "Tworzenie aplikacji Java z interfejsem Reliable Actors usługi Azure Service Fabric w systemie Linux | Microsoft Docs"
description: "Dowiedz się, jak utworzyć i wdrożyć aplikację Java z elementami Reliable Actors usługi Service Fabric w ciągu pięciu minut."
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
ms.openlocfilehash: baf948587ede31fe3d5b4f6f0981269b4cfe4d3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="9487c-103">Tworzenie pierwszej aplikacji Java z interfejsem Reliable Actors usługi Service Fabric w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="9487c-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9487c-104">C# — Windows</span><span class="sxs-lookup"><span data-stu-id="9487c-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="9487c-105">Java — Linux</span><span class="sxs-lookup"><span data-stu-id="9487c-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="9487c-106">C# — Linux</span><span class="sxs-lookup"><span data-stu-id="9487c-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="9487c-107">Ten przewodnik Szybki start pomaga w ciągu kilku minut utworzyć pierwszą aplikację Java usługi Azure Service Fabric w środowisku projektowym w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="9487c-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="9487c-108">W wyniku pracy z przewodnikiem zostanie utworzona prosta jednousługowa aplikacja Java uruchamiana w lokalnym klastrze projektowym.</span><span class="sxs-lookup"><span data-stu-id="9487c-108">When you are finished, you'll have a simple Java single-service application running on the local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="9487c-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9487c-109">Prerequisites</span></span>
<span data-ttu-id="9487c-110">Przed rozpoczęciem zainstaluj zestaw SDK usługi Service Fabric oraz interfejs wiersza polecenia usługi Service Fabric i skonfiguruj klaster projektowy w [środowisku projektowym w systemie Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9487c-110">Before you get started, install the Service Fabric SDK, the Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="9487c-111">Jeśli używasz systemu Mac OS X, możesz [skonfigurować środowisko deweloperskie systemu Linux na maszynie wirtualnej za pomocą narzędzia Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="9487c-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="9487c-112">Trzeba również zainstalować [interfejs wiersza polecenia usługi Service Fabric](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9487c-112">You will also want to install the [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-the-generators-for-java"></a><span data-ttu-id="9487c-113">Instalowanie i konfigurowanie generatorów dla języka Java</span><span class="sxs-lookup"><span data-stu-id="9487c-113">Install and set up the generators for Java</span></span>
<span data-ttu-id="9487c-114">Usługa Service Fabric udostępnia narzędzia do tworzenia szkieletu, które ułatwiają tworzenie aplikacji Java usługi Service Fabric z poziomu terminalu przy użyciu generatora szablonów Yeoman.</span><span class="sxs-lookup"><span data-stu-id="9487c-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="9487c-115">Wykonaj poniższe kroki, aby upewnić się, że generator szablonów Yeoman usługi Service Fabric dla języka Java działa na Twojej maszynie.</span><span class="sxs-lookup"><span data-stu-id="9487c-115">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="9487c-116">Zainstaluj środowisko NodeJs i menedżera NPM na swojej maszynie</span><span class="sxs-lookup"><span data-stu-id="9487c-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="9487c-117">Zainstaluj generator szablonów [narzędzia Yeoman](http://yeoman.io/) na swoim komputerze z poziomu narzędzia NPM</span><span class="sxs-lookup"><span data-stu-id="9487c-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="9487c-118">Zainstaluj generator aplikacji Java Yeo usługi Service Fabric z poziomu menedżera NPM</span><span class="sxs-lookup"><span data-stu-id="9487c-118">Install the Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-the-application"></a><span data-ttu-id="9487c-119">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="9487c-119">Create the application</span></span>
<span data-ttu-id="9487c-120">Aplikacja usługi Service Fabric zawiera jedną lub więcej usług, a każda z nich pełni określoną rolę w dostarczaniu funkcjonalności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9487c-120">A Service Fabric application contains one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="9487c-121">Generator, który został zainstalowany w ostatniej sekcji, ułatwia utworzenie pierwszej usługi i dodawanie kolejnych w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="9487c-121">The generator you installed in the last section, makes it easy to create your first service and to add more later.</span></span>  <span data-ttu-id="9487c-122">Możesz też tworzyć, kompilować i wdrażać aplikacje Java usługi Service Fabric przy użyciu wtyczki dla środowiska Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9487c-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="9487c-123">Zobacz [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md) (Tworzenie i wdrażanie pierwszej aplikacji Java za pomocą środowiska Eclipse).</span><span class="sxs-lookup"><span data-stu-id="9487c-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="9487c-124">Na potrzeby tego przewodnika Szybki start użyj narzędzia Yeoman, aby utworzyć aplikację z jedną usługą, w której jest przechowywana i pobierana wartość licznika.</span><span class="sxs-lookup"><span data-stu-id="9487c-124">For this quick start, use Yeoman to create an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="9487c-125">Na terminalu wpisz ``yo azuresfjava``.</span><span class="sxs-lookup"><span data-stu-id="9487c-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="9487c-126">Nadaj nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9487c-126">Name your application.</span></span>
3. <span data-ttu-id="9487c-127">Wybierz typ pierwszej usługi i nadaj jej nazwę.</span><span class="sxs-lookup"><span data-stu-id="9487c-127">Choose the type of your first service and name it.</span></span> <span data-ttu-id="9487c-128">Na potrzeby tego samouczka wybierz usługę Reliable Actor Service.</span><span class="sxs-lookup"><span data-stu-id="9487c-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="9487c-129">Aby uzyskać więcej informacji o pozostałych typach usług, zobacz [Service Fabric programming model overview](service-fabric-choose-framework.md) (Omówienie modelu programowania usługi Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="9487c-129">For more information about the other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="9487c-130">![Generator Yeoman usługi Service Fabric dla platformy Java][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="9487c-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-the-application"></a><span data-ttu-id="9487c-131">Kompilowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="9487c-131">Build the application</span></span>
<span data-ttu-id="9487c-132">Szablony generatora Yeoman usługi Service Fabric obejmują skrypt kompilacji dla narzędzia [Gradle](https://gradle.org/), którego można użyć do skompilowania aplikacji z poziomu terminalu.</span><span class="sxs-lookup"><span data-stu-id="9487c-132">The Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use to build the application from the terminal.</span></span>
<span data-ttu-id="9487c-133">Zależności aplikacji Java usługi Service Fabric są pobierane z narzędzia Maven.</span><span class="sxs-lookup"><span data-stu-id="9487c-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="9487c-134">Aby kompilować aplikacje Java usługi Service Fabric i pracować nad nimi, upewnij się, że zainstalowano zestaw JDK i narzędzie Gradle.</span><span class="sxs-lookup"><span data-stu-id="9487c-134">To build and work on the Service Fabric Java applications, you need to ensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="9487c-135">Jeśli ich jeszcze nie zainstalowano, możesz uruchomić następujące polecenia, aby zainstalować zestaw JDK (openjdk-8-jdk) i narzędzie Gradle:</span><span class="sxs-lookup"><span data-stu-id="9487c-135">If not yet installed, you can run the following to install JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="9487c-136">Aby skompilować aplikację i utworzyć jej pakiet, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9487c-136">To build and package the application, run the following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-the-application"></a><span data-ttu-id="9487c-137">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="9487c-137">Deploy the application</span></span>
<span data-ttu-id="9487c-138">Skompilowaną aplikację można wdrożyć w klastrze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="9487c-138">Once the application is built, you can deploy it to the local cluster.</span></span>

1. <span data-ttu-id="9487c-139">Połącz się z lokalnym klastrem usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9487c-139">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="9487c-140">Uruchom skrypt instalacji udostępniony w szablonie, aby skopiować pakiet aplikacji do magazynu obrazów klastra, zarejestrować typ aplikacji i utworzyć wystąpienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9487c-140">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="9487c-141">Wdrażanie skompilowanej aplikacji przebiega tak samo jak w przypadku innych aplikacji usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9487c-141">Deploying the built application is the same as any other Service Fabric application.</span></span> <span data-ttu-id="9487c-142">Szczegółowe instrukcje są dostępne w dokumentacji dotyczącej [zarządzania aplikacją usługi Service Fabric za pomocą interfejsu wiersza polecenia usługi Service Fabric](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="9487c-142">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="9487c-143">Parametry tych poleceń można znaleźć w manifestach wygenerowanych w pakiecie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9487c-143">Parameters to these commands can be found in the generated manifests inside the application package.</span></span>

<span data-ttu-id="9487c-144">Po wdrożeniu aplikacji otwórz przeglądarkę i przejdź do narzędzia [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) pod adresem [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="9487c-144">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="9487c-145">Następnie rozwiń węzeł **Aplikacje** i zwróć uwagę, że istnieje teraz wpis dla danego typu aplikacji i inny wpis dla pierwszego wystąpienia tego typu.</span><span class="sxs-lookup"><span data-stu-id="9487c-145">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

## <a name="start-the-test-client-and-perform-a-failover"></a><span data-ttu-id="9487c-146">Uruchamianie klienta testowego i przechodzenie w tryb failover</span><span class="sxs-lookup"><span data-stu-id="9487c-146">Start the test client and perform a failover</span></span>
<span data-ttu-id="9487c-147">Aktorzy nie pełnią samodzielnie żadnej funkcji. Wymagają wysyłania do nich komunikatów przez inną usługę lub innego klienta.</span><span class="sxs-lookup"><span data-stu-id="9487c-147">Actors do not do anything on their own, they require another service or client to send them messages.</span></span> <span data-ttu-id="9487c-148">Szablon aktora zawiera prosty skrypt testowy, którego można użyć do interakcji z usługą aktora.</span><span class="sxs-lookup"><span data-stu-id="9487c-148">The actor template includes a simple test script that you can use to interact with the actor service.</span></span>

1. <span data-ttu-id="9487c-149">Uruchom skrypt za pomocą narzędzia kontrolnego, aby wyświetlić dane wyjściowe usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="9487c-149">Run the script using the watch utility to see the output of the actor service.</span></span>  <span data-ttu-id="9487c-150">Skrypt testowy wywołuje metodę `setCountAsync()` dla aktora w celu zwiększenia wartości licznika, wywołuje metodę `getCountAsync()` dla aktora w celu pobrania nowej wartości licznika i wyświetla tę wartość w konsoli.</span><span class="sxs-lookup"><span data-stu-id="9487c-150">The test script calls the `setCountAsync()` method on the actor to increment a counter, calls the `getCountAsync()` method on the actor to get the new counter value, and displays that value to the console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="9487c-151">W narzędziu Service Fabric Explorer zlokalizuj węzeł, w którym znajduje się replika podstawowa usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="9487c-151">In Service Fabric Explorer, locate the node hosting the primary replica for the actor service.</span></span> <span data-ttu-id="9487c-152">Na poniższym zrzucie ekranu jest to węzeł 3.</span><span class="sxs-lookup"><span data-stu-id="9487c-152">In the screenshot below, it is node 3.</span></span> <span data-ttu-id="9487c-153">Replika podstawowa usługi obsługuje operacje odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="9487c-153">The primary service replica handles read and write operations.</span></span>  <span data-ttu-id="9487c-154">Zmiany stanu usługi są następnie replikowane w replikach pomocniczych — na poniższym zrzucie ekranu są one uruchomione w węzłach 0 i 1.</span><span class="sxs-lookup"><span data-stu-id="9487c-154">Changes in service state are then replicated out to the secondary replicas, running on nodes 0 and 1 in the screen shot below.</span></span>

    ![Znajdowanie repliki podstawowej w narzędziu Service Fabric Explorer][sfx-primary]

3. <span data-ttu-id="9487c-156">W lokalizacji **Węzły** kliknij węzeł znaleziony w poprzednim kroku, a następnie wybierz pozycję **Dezaktywuj (uruchom ponownie)** z menu Akcje.</span><span class="sxs-lookup"><span data-stu-id="9487c-156">In **Nodes**, click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span></span> <span data-ttu-id="9487c-157">Ta czynność spowoduje ponowne uruchomienie węzła w replice podstawowej usługi i wymuszenie przejścia w tryb failover do jednej z replik pomocniczych uruchomionych w innym węźle.</span><span class="sxs-lookup"><span data-stu-id="9487c-157">This action restarts the node running the primary service replica and forces a failover to one of the secondary replicas running on another node.</span></span>  <span data-ttu-id="9487c-158">Poziom tej repliki pomocniczej zostanie podwyższony do repliki podstawowej, inna replika pomocnicza zostanie utworzona w innym węźle oraz replika podstawowa zacznie obsługiwać operacje odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="9487c-158">That secondary replica is promoted to primary, another secondary replica is created on a different node, and the primary replica begins to take read/write operations.</span></span> <span data-ttu-id="9487c-159">Podczas ponownego uruchamiania węzła należy zwrócić uwagę na dane wyjściowe z klienta testowego oraz to, że licznik będzie nadal się zwiększać niezależnie od trybu failover.</span><span class="sxs-lookup"><span data-stu-id="9487c-159">As the node restarts, watch the output from the test client and note that the counter continues to increment despite the failover.</span></span>

## <a name="remove-the-application"></a><span data-ttu-id="9487c-160">Usuwanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="9487c-160">Remove the application</span></span>
<span data-ttu-id="9487c-161">Użyj skryptu odinstalowania udostępnionego w szablonie, aby usunąć wystąpienie aplikacji, wyrejestrować pakiet aplikacji i usunąć pakiet aplikacji z magazynu obrazów klastra.</span><span class="sxs-lookup"><span data-stu-id="9487c-161">Use the uninstall script provided in the template to delete the application instance, unregister the application package, and remove the application package from the cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="9487c-162">W narzędziu Service Fabric Explorer aplikacja i typ aplikacji nie są już wyświetlane w węźle **Aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9487c-162">In Service Fabric explorer you see that the application and application type no longer appear in the **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="9487c-163">Biblioteki Java usługi Service Fabric w narzędziu Maven</span><span class="sxs-lookup"><span data-stu-id="9487c-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="9487c-164">Biblioteki Java usługi Service Fabric są teraz hostowane w narzędziu Maven.</span><span class="sxs-lookup"><span data-stu-id="9487c-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="9487c-165">Zależności możesz dodać w pliku ``pom.xml`` lub ``build.gradle`` projektów, aby używać bibliotek Java usługi Service Fabric z repozytorium **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="9487c-165">You can add the dependencies in the ``pom.xml`` or ``build.gradle`` of your projects to use Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="9487c-166">Aktorzy</span><span class="sxs-lookup"><span data-stu-id="9487c-166">Actors</span></span>

<span data-ttu-id="9487c-167">Obsługa interfejsu Reliable Actors usługi Service Fabric dla Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9487c-167">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="9487c-168">Usługi</span><span class="sxs-lookup"><span data-stu-id="9487c-168">Services</span></span>

<span data-ttu-id="9487c-169">Obsługa usługi bezstanowej usługi Service Fabric dla Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9487c-169">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="9487c-170">Inne</span><span class="sxs-lookup"><span data-stu-id="9487c-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="9487c-171">Transport</span><span class="sxs-lookup"><span data-stu-id="9487c-171">Transport</span></span>

<span data-ttu-id="9487c-172">Obsługa warstwy transportowej dla aplikacji Java usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9487c-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="9487c-173">Nie trzeba jawnie dodawać tej zależności do aplikacji Reliable Actors lub aplikacji usługi, chyba że programujesz w warstwie transportowej.</span><span class="sxs-lookup"><span data-stu-id="9487c-173">You do not need to explicitly add this dependency to your Reliable Actor or Service applications, unless you program at the transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="9487c-174">Obsługa usługi Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9487c-174">Fabric support</span></span>

<span data-ttu-id="9487c-175">Obsługa na poziomie systemu dla usługi Service Fabric, która komunikuje się z natywnym środowiskiem uruchomieniowym usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9487c-175">System level support for Service Fabric, which talks to native Service Fabric runtime.</span></span> <span data-ttu-id="9487c-176">Nie trzeba jawnie dodawać tej zależności do aplikacji Reliable Actors lub aplikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="9487c-176">You do not need to explicitly add this dependency to your Reliable Actor or Service applications.</span></span> <span data-ttu-id="9487c-177">Jest ona automatycznie pobierana z narzędzia Maven, kiedy uwzględnisz pozostałe powyższe zależności.</span><span class="sxs-lookup"><span data-stu-id="9487c-177">This gets fetched automatically from Maven, when you include the other dependencies above.</span></span>

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

## <a name="migrating-old-service-fabric-java-applications-to-be-used-with-maven"></a><span data-ttu-id="9487c-178">Migrowanie starych aplikacji Java usługi Service Fabric na potrzeby użycia z narzędziem Maven</span><span class="sxs-lookup"><span data-stu-id="9487c-178">Migrating old Service Fabric Java applications to be used with Maven</span></span>
<span data-ttu-id="9487c-179">Ostatnio przenieśliśmy biblioteki Java usługi Service Fabric z zestawu SDK Java usługi Service Fabric do repozytorium narzędzia Maven.</span><span class="sxs-lookup"><span data-stu-id="9487c-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK to Maven repository.</span></span> <span data-ttu-id="9487c-180">Nowe aplikacje generowane za pomocą narzędzia Yeoman lub środowiska Eclipse będą generować najnowsze, zaktualizowane projekty (mogące działać z narzędziem Maven), ale możesz zaktualizować swoje istniejące bezstanowe aplikacje Java lub aplikacje Java aktora usługi Service Fabric, które wcześniej korzystały z zestawu SDK Java usługi Service Fabric, aby używały zależności języka Java usługi Service Fabric z narzędzia Maven.</span><span class="sxs-lookup"><span data-stu-id="9487c-180">While the new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able to work with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using the Service Fabric Java SDK earlier, to use the Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="9487c-181">Wykonaj kroki wymienione [tutaj](service-fabric-migrate-old-javaapp-to-use-maven.md), aby zapewnić działanie Twojej starszej aplikacji z narzędziem Maven.</span><span class="sxs-lookup"><span data-stu-id="9487c-181">Please follow the steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) to ensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9487c-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9487c-182">Next steps</span></span>

* [<span data-ttu-id="9487c-183">Tworzenie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu środowiska Eclipse</span><span class="sxs-lookup"><span data-stu-id="9487c-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="9487c-184">Dowiedz się więcej o usłudze Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="9487c-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="9487c-185">Interact with Service Fabric clusters using the Service Fabric CLI (Interakcja z klastrami usługi Service Fabric przy użyciu interfejsu wiersza polecenia usługi Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="9487c-185">Interact with Service Fabric clusters using the Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="9487c-186">Uzyskaj informacje o [opcjach pomocy technicznej usługi Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="9487c-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="9487c-187">Getting started with Service Fabric CLI (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="9487c-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
