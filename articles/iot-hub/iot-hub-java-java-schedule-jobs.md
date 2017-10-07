---
title: zadania aaaSchedule z Centrum IoT Azure (Java) | Dokumentacja firmy Microsoft
description: "Jak tooschedule Centrum IoT Azure zadania tooinvoke metoda bezpośrednia i ustaw odpowiednie właściwości na wielu urządzeniach. Możesz używać urządzenia Azure IoT hello zestawu SDK dla języka Java tooimplement hello symulowane urządzenie aplikacji i hello Azure IoT usługa zestawu SDK dla języka Java tooimplement zadania hello toorun aplikacji usługi."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dobett
ms.openlocfilehash: b1b05fa56c3ce96af0b33d4cca0dd54da0f4e927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="f837a-104">Zadania harmonogramu i emisji (Java)</span><span class="sxs-lookup"><span data-stu-id="f837a-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="f837a-105">Użyj Centrum IoT Azure tooschedule i Śledź zadań aktualizowanych milionów urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f837a-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="f837a-106">Należy użyć zadania, aby:</span><span class="sxs-lookup"><span data-stu-id="f837a-106">Use jobs to:</span></span>

* <span data-ttu-id="f837a-107">Aktualizowanie żądanych właściwości</span><span class="sxs-lookup"><span data-stu-id="f837a-107">Update desired properties</span></span>
* <span data-ttu-id="f837a-108">Tagi aktualizacji</span><span class="sxs-lookup"><span data-stu-id="f837a-108">Update tags</span></span>
* <span data-ttu-id="f837a-109">Wywołanie metody bezpośredniego</span><span class="sxs-lookup"><span data-stu-id="f837a-109">Invoke direct methods</span></span>

<span data-ttu-id="f837a-110">Zadanie opakowuje jedną z następujących czynności i śledzi hello wykonywania z zestawem urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f837a-110">A job wraps one of these actions and tracks hello execution against a set of devices.</span></span> <span data-ttu-id="f837a-111">Zapytanie dwie urządzenia definiuje hello zbiór urządzeń, które wykonuje zadanie hello przed.</span><span class="sxs-lookup"><span data-stu-id="f837a-111">A device twin query defines hello set of devices hello job executes against.</span></span> <span data-ttu-id="f837a-112">Na przykład aplikacji zaplecza można użyć zadania tooinvoke metoda bezpośrednia na 10 000 urządzeń, które wykonuje ponowny rozruch hello urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f837a-112">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="f837a-113">Określ zestaw hello urządzeń za pomocą kwerendy dwie urządzenia i zaplanować hello toorun zadania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="f837a-113">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="f837a-114">postęp śledzi zadania Hello jako każdego urządzenia hello odbierania i wykonaj metoda bezpośrednia hello ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="f837a-114">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="f837a-115">toolearn więcej informacji na temat każdego z tych funkcji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="f837a-115">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="f837a-116">Dwie urządzeń i właściwości: [wprowadzenie twins urządzenia](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="f837a-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="f837a-117">Bezpośrednie metody: [przewodnik dewelopera Centrum IoT — metody bezpośredniego](iot-hub-devguide-direct-methods.md) i [samouczek: bezpośrednie metody](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="f837a-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="f837a-118">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="f837a-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="f837a-119">Tworzenie aplikacji urządzenia implementujący bezpośredniego metodę o nazwie **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="f837a-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="f837a-120">Aplikacja urządzenia Hello również odbiera zmiany żądanej właściwości z hello zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f837a-120">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="f837a-121">Tworzenie aplikacji zaplecza, która tworzy hello toocall zadania **lockDoor** metoda bezpośrednia na wielu urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="f837a-121">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="f837a-122">Inne zadanie wysyła żądanej właściwości aktualizuje toomultiple urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f837a-122">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="f837a-123">Na końcu hello tego samouczka masz urządzenie aplikację konsoli języka java i zaplecza aplikacji konsoli java:</span><span class="sxs-lookup"><span data-stu-id="f837a-123">At hello end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="f837a-124">**Symulowane urządzenie** który łączy Centrum IoT tooyour, implementuje hello **lockDoor** bezpośrednie — metoda i uchwytów potrzebne zmiany właściwości.</span><span class="sxs-lookup"><span data-stu-id="f837a-124">**simulated-device** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="f837a-125">**Harmonogram zadań** wykorzystujące hello toocall zadania **lockDoor** właściwości na wielu urządzeniach potrzeby bezpośredniego metoda i aktualizacji dwie hello w urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="f837a-125">**schedule-jobs** that use jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="f837a-126">Artykuł Hello [Azure IoT SDK](iot-hub-devguide-sdks.md) informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f837a-126">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f837a-127">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f837a-127">Prerequisites</span></span>

<span data-ttu-id="f837a-128">toocomplete tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="f837a-128">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="f837a-129">Witaj najnowszych [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="f837a-129">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="f837a-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="f837a-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="f837a-131">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f837a-131">An active Azure account.</span></span> <span data-ttu-id="f837a-132">(Jeśli nie masz konta, możesz utworzyć [bezpłatne konto](http://azure.microsoft.com/pricing/free-trial/) w zaledwie kilka minut.)</span><span class="sxs-lookup"><span data-stu-id="f837a-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="f837a-133">Jeśli wolisz tożsamości urządzenia hello toocreate programowo, przeczytaj hello odpowiedniej sekcji w hello [połączenia przy użyciu języka Java Centrum IoT urządzenia tooyour](iot-hub-java-java-getstarted.md#create-a-device-identity) artykułu.</span><span class="sxs-lookup"><span data-stu-id="f837a-133">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="f837a-134">Można również użyć hello [explorer Centrum iothub](https://github.com/Azure/iothub-explorer) tooadd narzędzia Centrum IoT tooyour urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f837a-134">You can also use hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool tooadd a device tooyour IoT hub.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="f837a-135">Tworzenie aplikacji usługi hello</span><span class="sxs-lookup"><span data-stu-id="f837a-135">Create hello service app</span></span>

<span data-ttu-id="f837a-136">W tej sekcji służy do tworzenia aplikacji konsoli Java, który używa zadań:</span><span class="sxs-lookup"><span data-stu-id="f837a-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="f837a-137">Wywołaj hello **lockDoor** metoda bezpośrednia na wielu urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="f837a-137">Call hello **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="f837a-138">Wyślij odpowiednie właściwości toomultiple urządzeń.</span><span class="sxs-lookup"><span data-stu-id="f837a-138">Send desired properties toomultiple devices.</span></span>

<span data-ttu-id="f837a-139">Aplikacja hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="f837a-139">toocreate hello app:</span></span>

1. <span data-ttu-id="f837a-140">Na komputerze deweloperskim, należy utworzyć pusty folder o nazwie `iot-java-schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="f837a-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="f837a-141">W hello `iot-java-schedule-jobs` folderu, Utwórz projekt Maven o nazwie **harmonogram zadań** przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f837a-141">In hello `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using hello following command at your command prompt.</span></span> <span data-ttu-id="f837a-142">Zwróć uwagę, że jest to jedno długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="f837a-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="f837a-143">Wierszu polecenia przejdź toohello `schedule-jobs` folderu.</span><span class="sxs-lookup"><span data-stu-id="f837a-143">At your command prompt, navigate toohello `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="f837a-144">Za pomocą edytora tekstu, otwórz hello `pom.xml` pliku w hello `schedule-jobs` folderu i dodaj następujące zależności toohello hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="f837a-144">Using a text editor, open hello `pom.xml` file in hello `schedule-jobs` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="f837a-145">Ta zależność umożliwia toouse hello **klienta w przypadku usługi iot** pakiet w Twojej toocommunicate aplikacji z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="f837a-145">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="f837a-146">Możesz sprawdzić hello najnowszą wersję **klienta w przypadku usługi iot** przy użyciu [wyszukiwania Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="f837a-146">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="f837a-147">Dodaj następujące hello **kompilacji** węzła po hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="f837a-147">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="f837a-148">Ta konfiguracja powoduje, że Maven toouse Java 1,8 toobuild hello aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f837a-148">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="f837a-149">Zapisz i zamknij hello `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="f837a-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="f837a-150">Za pomocą edytora tekstu, otwórz hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="f837a-150">Using a text editor, open hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="f837a-151">Dodaj następujące hello **zaimportować** instrukcje toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="f837a-151">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Pair;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Query;
    import com.microsoft.azure.sdk.iot.service.devicetwin.SqlQuery;
    import com.microsoft.azure.sdk.iot.service.jobs.JobClient;
    import com.microsoft.azure.sdk.iot.service.jobs.JobResult;
    import com.microsoft.azure.sdk.iot.service.jobs.JobStatus;

    import java.util.Date;
    import java.time.Instant;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.UUID;
    ```

1. <span data-ttu-id="f837a-152">Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="f837a-152">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="f837a-153">Zastąp `{youriothubconnectionstring}` z parametrów połączenia Centrum IoT zanotowaną w hello *tworzenia Centrum IoT* sekcji:</span><span class="sxs-lookup"><span data-stu-id="f837a-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="f837a-154">Dodaj następujące metody toohello hello **aplikacji** tooschedule klasy hello tooupdate zadania **budynku** i **Floor** żądanego właściwości w Witaj dwie urządzenia:</span><span class="sxs-lookup"><span data-stu-id="f837a-154">Add hello following method toohello **App** class tooschedule a job tooupdate hello **Building** and **Floor** desired properties in hello device twin:</span></span>

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule hello update twin job toorun now
      // against a single device
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleUpdateTwin(jobId, 
          "deviceId='" + deviceId + "'",
          twin,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling desired properties job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    }
    ```

1. <span data-ttu-id="f837a-155">tooschedule hello toocall zadania **lockDoor** metody, Dodaj następujące metody toohello hello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="f837a-155">tooschedule a job toocall hello **lockDoor** method, add hello following method toohello **App** class:</span></span>

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now toocall hello lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set too5 seconds.
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleDeviceMethod(jobId,
          "deviceId='" + deviceId + "'",
          "lockDoor",
          5L, 5L, null,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling direct method job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    };
    ```

1. <span data-ttu-id="f837a-156">toomonitor zadania, Dodaj następujące metody toohello hello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="f837a-156">toomonitor a job, add hello following method toohello **App** class:</span></span>

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check hello job result until it's completed
        while(jobResult.getJobStatus() != JobStatus.completed)
        {
          Thread.sleep(100);
          jobResult = jobClient.getJob(jobId);
          System.out.println("Status " + jobResult.getJobStatus() + " for job " + jobId);
        }
        System.out.println("Final status " + jobResult.getJobStatus() + " for job " + jobId);
      } catch (Exception e) {
        System.out.println("Exception monitoring job: " + jobId);
        System.out.println(e.getMessage());
        return;
      }
    }
    ```

1. <span data-ttu-id="f837a-157">tooquery hello informacji o zadaniach hello uruchomienia, Dodaj hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="f837a-157">tooquery for hello details of hello jobs you ran, add hello following method:</span></span>

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using hello time hello jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over hello list of jobs and print hello details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. <span data-ttu-id="f837a-158">Aktualizacja hello **głównego** następujące hello tooinclude podpis metody `throws` klauzuli:</span><span class="sxs-lookup"><span data-stu-id="f837a-158">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="f837a-159">monitor i toorun dwa zadania sekwencyjnie, Dodaj hello następującego kodu toohello **głównego** metody:</span><span class="sxs-lookup"><span data-stu-id="f837a-159">toorun and monitor two jobs sequentially, add hello following code toohello **main** method:</span></span>

    ```java
    // Record hello start time
    String start = Instant.now().toString();

    // Create JobClient
    JobClient jobClient = JobClient.createFromConnectionString(iotHubConnectionString);
    System.out.println("JobClient created with success");

    // Schedule twin job desired properties
    // Maximum concurrent jobs is 1 for Free and S1 tiers
    String desiredPropertiesJobId = "DPCMD" + UUID.randomUUID();
    scheduleJobSetDesiredProperties(jobClient, desiredPropertiesJobId);
    monitorJob(jobClient, desiredPropertiesJobId);

    // Schedule twin job direct method
    String directMethodJobId = "DMCMD" + UUID.randomUUID();
    scheduleJobCallDirectMethod(jobClient, directMethodJobId);
    monitorJob(jobClient, directMethodJobId);

    // Run a query tooshow hello job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. <span data-ttu-id="f837a-160">Zapisz i zamknij hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` pliku</span><span class="sxs-lookup"><span data-stu-id="f837a-160">Save and close hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="f837a-161">Tworzenie hello **harmonogram zadań** aplikacji i poprawić błędy.</span><span class="sxs-lookup"><span data-stu-id="f837a-161">Build hello **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="f837a-162">Wierszu polecenia przejdź toohello `schedule-jobs` folder i hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f837a-162">At your command prompt, navigate toohello `schedule-jobs` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="f837a-163">Tworzenie aplikacji urządzenia</span><span class="sxs-lookup"><span data-stu-id="f837a-163">Create a device app</span></span>

<span data-ttu-id="f837a-164">W tej sekcji utworzysz aplikację konsoli języka Java, która uchwytów hello żądanej właściwości wysyłane z Centrum IoT i implementuje wywołanie metody bezpośredniego hello.</span><span class="sxs-lookup"><span data-stu-id="f837a-164">In this section, you create a Java console app that handles hello desired properties sent from IoT Hub and implements hello direct method call.</span></span>

1. <span data-ttu-id="f837a-165">W hello `iot-java-schedule-jobs` folderu, Utwórz projekt Maven o nazwie **symulowane urządzenie** przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f837a-165">In hello `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="f837a-166">Zwróć uwagę, że jest to jedno długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="f837a-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="f837a-167">Wierszu polecenia przejdź toohello `simulated-device` folderu.</span><span class="sxs-lookup"><span data-stu-id="f837a-167">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="f837a-168">Za pomocą edytora tekstu, otwórz hello `pom.xml` pliku w hello `simulated-device` folderu i dodaj następujące zależności toohello hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="f837a-168">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="f837a-169">Ta zależność umożliwia toouse hello **klienta w przypadku urządzenia iot** pakiet w Twojej toocommunicate aplikacji z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="f837a-169">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="f837a-170">Możesz sprawdzić hello najnowszą wersję **klienta w przypadku urządzenia iot** przy użyciu [wyszukiwania Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="f837a-170">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="f837a-171">Dodaj następujące hello **kompilacji** węzła po hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="f837a-171">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="f837a-172">Ta konfiguracja powoduje, że Maven toouse Java 1,8 toobuild hello aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f837a-172">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="f837a-173">Zapisz i zamknij hello `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="f837a-173">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="f837a-174">Za pomocą edytora tekstu, otwórz hello `simulated-device\src\main\java\com\mycompany\app\App.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="f837a-174">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="f837a-175">Dodaj następujące hello **zaimportować** instrukcje toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="f837a-175">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="f837a-176">Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="f837a-176">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="f837a-177">Zastępowanie `{youriothubname}` z nazwę Centrum IoT i `{yourdevicekey}` o wartości klucza urządzenia hello wygenerowanych w hello *tworzenie tożsamości urządzenia* sekcji:</span><span class="sxs-lookup"><span data-stu-id="f837a-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="f837a-178">Ta przykładowa aplikacja używa hello **protokołu** zmiennej podczas tworzenia wystąpień **DeviceClient** obiektu.</span><span class="sxs-lookup"><span data-stu-id="f837a-178">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="f837a-179">Obecnie toouse dwie funkcji urządzenia muszą używać protokołu MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="f837a-179">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="f837a-180">tooprint urządzenia dwie powiadomienia toohello konsoli, należy dodać następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="f837a-180">tooprint device twin notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="f837a-181">tooprint bezpośrednie toohello powiadomienia metody konsoli, należy dodać następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="f837a-181">tooprint direct method notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="f837a-182">toohandle wywołania metody bezpośrednio z Centrum IoT, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="f837a-182">toohandle direct method calls from IoT Hub, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for direct method calls from IoT Hub
    protected static class DirectMethodCallback
        implements DeviceMethodCallback {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context) {
        DeviceMethodData deviceMethodData;
        switch (methodName) {
          case "lockDoor": {
            System.out.println("Executing direct method: " + methodName);
            deviceMethodData = new DeviceMethodData(METHOD_SUCCESS, "Executed direct method " + methodName);
            break;
          }
          default: {
            deviceMethodData = new DeviceMethodData(METHOD_NOT_DEFINED, "Not defined direct method " + methodName);
          }
        }
        // Notify IoT Hub of result
        return deviceMethodData;
      }
    }
    ```

1. <span data-ttu-id="f837a-183">Aktualizacja hello **głównego** następujące hello tooinclude podpis metody `throws` klauzuli:</span><span class="sxs-lookup"><span data-stu-id="f837a-183">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="f837a-184">Dodaj hello następującego kodu toohello **głównego** metodę:</span><span class="sxs-lookup"><span data-stu-id="f837a-184">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="f837a-185">Utwórz toocommunicate klienta urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f837a-185">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="f837a-186">Utwórz **urządzenia** toostore hello urządzenia dwie właściwości obiektu.</span><span class="sxs-lookup"><span data-stu-id="f837a-186">Create a **Device** object toostore hello device twin properties.</span></span>

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object toomanage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="f837a-187">toostart hello urządzenia klienta usługi, dodać hello następującego kodu toohello **głównego** metody:</span><span class="sxs-lookup"><span data-stu-id="f837a-187">toostart hello device client services, add hello following code toohello **main** method:</span></span>

    ```java
    try {
      // Open hello DeviceClient
      // Start hello device twin services
      // Subscribe toodirect method calls
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
    } catch (Exception e) {
      System.out.println("Exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.closeNow();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="f837a-188">toowait dla hello użytkownika toopress hello **Enter** klucza przed zamknięciem, należy dodać kodu zakończenia toohello hello hello **głównego** metody:</span><span class="sxs-lookup"><span data-stu-id="f837a-188">toowait for hello user toopress hello **Enter** key before shutting down, add hello following code toohello end of hello **main** method:</span></span>

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="f837a-189">Zapisz i zamknij hello `simulated-device\src\main\java\com\mycompany\app\App.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="f837a-189">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="f837a-190">Tworzenie hello **symulowane urządzenie** aplikacji i poprawić błędy.</span><span class="sxs-lookup"><span data-stu-id="f837a-190">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="f837a-191">Wierszu polecenia przejdź toohello `simulated-device` folder i hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f837a-191">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="f837a-192">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="f837a-192">Run hello apps</span></span>

<span data-ttu-id="f837a-193">Wszystko jest teraz gotowy toorun hello konsoli aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f837a-193">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="f837a-194">W wierszu polecenia w hello `simulated-device` folderu, uruchom następujące polecenie toostart hello aplikacji urządzenia nasłuchiwanie zmian żądanej właściwości i wywołania metody bezpośredniego hello:</span><span class="sxs-lookup"><span data-stu-id="f837a-194">At a command prompt in hello `simulated-device` folder, run hello following command toostart hello device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Uruchamia powitania klienta urządzenia](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="f837a-196">W wierszu polecenia w hello `schedule-jobs` folderu, uruchom następujące polecenie toorun hello hello **harmonogram zadań** usługi aplikacji toorun dwa zadania.</span><span class="sxs-lookup"><span data-stu-id="f837a-196">At a command prompt in hello `schedule-jobs` folder, run hello following command toorun hello **schedule-jobs** service app toorun two jobs.</span></span> <span data-ttu-id="f837a-197">Hello najpierw ustawia wartości właściwości hello potrzebne, wywołania drugiej hello hello metoda bezpośrednia:</span><span class="sxs-lookup"><span data-stu-id="f837a-197">hello first sets hello desired property values, hello second calls hello direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java usługi aplikacji tworzy dwa zadania](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="f837a-199">aplikacji urządzenia Hello obsługuje hello potrzebne zmiany właściwości i wywołanie metody bezpośredniego hello:</span><span class="sxs-lookup"><span data-stu-id="f837a-199">hello device app handles hello desired property change and hello direct method call:</span></span>

    ![zmiany toohello odpowiada powitania klienta urządzenia](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="f837a-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f837a-201">Next steps</span></span>

<span data-ttu-id="f837a-202">W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f837a-202">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="f837a-203">Utworzono aplikacji zaplecza toorun dwa zadania.</span><span class="sxs-lookup"><span data-stu-id="f837a-203">You created a back-end app toorun two jobs.</span></span> <span data-ttu-id="f837a-204">Hello pierwszego zadania ustawić wartości żądanej właściwości, a zadanie drugi hello wywołana metoda bezpośrednia.</span><span class="sxs-lookup"><span data-stu-id="f837a-204">hello first job set desired property values, and hello second job called a direct method.</span></span>

<span data-ttu-id="f837a-205">Hello Użyj następujących zasobów toolearn jak do:</span><span class="sxs-lookup"><span data-stu-id="f837a-205">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="f837a-206">Wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT](iot-hub-java-java-getstarted.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="f837a-206">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="f837a-207">Kontrolowanie urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika) z hello [metody bezpośredniego](iot-hub-java-java-direct-methods.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="f837a-207">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
