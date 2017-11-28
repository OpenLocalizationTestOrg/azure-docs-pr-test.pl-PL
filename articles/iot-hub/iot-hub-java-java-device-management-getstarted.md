---
title: "aaaGet wprowadzenie do zarządzania urządzeniami Centrum IoT Azure (Java) | Dokumentacja firmy Microsoft"
description: "Jak tooinitiate zarządzania urządzenia Azure IoT Hub toouse urządzenie zdalne ponowny rozruch. Możesz używać urządzenia Azure IoT hello zestawu SDK dla języka Java tooimplement aplikacji symulowane urządzenie, która obejmuje metoda bezpośrednia i hello Azure IoT usługi SDK dla języka Java tooimplement usługi aplikacji, która wywołuje metodę bezpośredniego hello."
services: iot-hub
documentationcenter: .java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 7aaeda9d4ff7002e5c66adfd61e2dfd5bcea964f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="8b33a-104">Wprowadzenie do zarządzania urządzeniami (Java)</span><span class="sxs-lookup"><span data-stu-id="8b33a-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="8b33a-105">Ten samouczek przedstawia sposób wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="8b33a-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="8b33a-106">Użyj hello toocreate portalu Azure IoT Hub i Utwórz tożsamość urządzenia w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="8b33a-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="8b33a-107">Utwórz aplikację symulowane urządzenie, która implementuje urządzenie hello tooreboot metoda bezpośrednia.</span><span class="sxs-lookup"><span data-stu-id="8b33a-107">Create a simulated device app that implements a direct method tooreboot hello device.</span></span> <span data-ttu-id="8b33a-108">Bezpośrednie metody są wywoływane z hello chmury.</span><span class="sxs-lookup"><span data-stu-id="8b33a-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="8b33a-109">Utwórz aplikację, która wywołuje metodę hello ponowny rozruch bezpośrednio w aplikacji symulowane urządzenie hello za pośrednictwem Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="8b33a-109">Create an app that invokes hello reboot direct method in hello simulated device app through your IoT hub.</span></span> <span data-ttu-id="8b33a-110">Tej aplikacji, a następnie hello zgłoszone właściwości z hello toosee urządzeń po zakończeniu operacji ponownego rozruchu hello monitorów.</span><span class="sxs-lookup"><span data-stu-id="8b33a-110">This app then monitors hello reported properties from hello device toosee when hello reboot operation is complete.</span></span>

<span data-ttu-id="8b33a-111">Na końcu hello tego samouczka znajdują się dwie aplikacje konsoli Java:</span><span class="sxs-lookup"><span data-stu-id="8b33a-111">At hello end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="8b33a-112">**Symulowane urządzenie**.</span><span class="sxs-lookup"><span data-stu-id="8b33a-112">**simulated-device**.</span></span> <span data-ttu-id="8b33a-113">Ta aplikacja:</span><span class="sxs-lookup"><span data-stu-id="8b33a-113">This app:</span></span>

* <span data-ttu-id="8b33a-114">Centrum IoT tooyour łączy się z usługą tożsamości urządzenia hello utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="8b33a-114">Connects tooyour IoT hub with hello device identity created earlier.</span></span>
* <span data-ttu-id="8b33a-115">Odbiera wywołanie metody bezpośredniego ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="8b33a-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="8b33a-116">Symuluje ponowny rozruch komputera fizycznego.</span><span class="sxs-lookup"><span data-stu-id="8b33a-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="8b33a-117">Raporty hello czasu ostatniego ponownego uruchomienia hello za pośrednictwem właściwości zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="8b33a-117">Reports hello time of hello last reboot through a reported property.</span></span>

<span data-ttu-id="8b33a-118">**ponowne uruchomienie wyzwalacza**.</span><span class="sxs-lookup"><span data-stu-id="8b33a-118">**trigger-reboot**.</span></span> <span data-ttu-id="8b33a-119">Ta aplikacja:</span><span class="sxs-lookup"><span data-stu-id="8b33a-119">This app:</span></span>

* <span data-ttu-id="8b33a-120">Wywołuje metodę bezpośrednio w aplikacji symulowane urządzenie hello.</span><span class="sxs-lookup"><span data-stu-id="8b33a-120">Calls a direct method in hello simulated device app.</span></span>
* <span data-ttu-id="8b33a-121">Wyświetla hello odpowiedzi toohello wywołanie metody bezpośredniego wysyłane przez hello symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="8b33a-121">Displays hello response toohello direct method call sent by hello simulated device</span></span>
* <span data-ttu-id="8b33a-122">Wyświetla hello zaktualizowane zgłosił właściwości.</span><span class="sxs-lookup"><span data-stu-id="8b33a-122">Displays hello updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="8b33a-123">Informacje hello zestawów SDK, której można toobuild toorun aplikacji na urządzeniach i z zaplecza rozwiązania, zobacz [Azure IoT SDK][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="8b33a-123">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="8b33a-124">toocomplete tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="8b33a-124">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="8b33a-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="8b33a-125">Java SE 8.</span></span> <br/> <span data-ttu-id="8b33a-126">[Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Java w tym samouczku w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="8b33a-126">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="8b33a-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="8b33a-127">Maven 3.</span></span>  <br/> <span data-ttu-id="8b33a-128">[Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall [Maven] [ lnk-maven] ten samouczek dotyczący systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="8b33a-128">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="8b33a-129">[Środowisko node.js w wersji 0.10.0 lub nowszym](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="8b33a-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="8b33a-130">Wyzwalacz zdalnego ponownego uruchomienia na urządzeniu hello za pomocą bezpośrednich — metoda</span><span class="sxs-lookup"><span data-stu-id="8b33a-130">Trigger a remote reboot on hello device using a direct method</span></span>

<span data-ttu-id="8b33a-131">W tej sekcji tworzenia aplikacji konsoli Java który:</span><span class="sxs-lookup"><span data-stu-id="8b33a-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="8b33a-132">Wywołuje metodę bezpośredniego ponowny rozruch hello w hello symulowane urządzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8b33a-132">Invokes hello reboot direct method in hello simulated device app.</span></span>
1. <span data-ttu-id="8b33a-133">Wyświetla hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="8b33a-133">Displays hello response.</span></span>
1. <span data-ttu-id="8b33a-134">Ankiety hello zgłosił przesyłanych z hello toodetermine urządzeń po zakończeniu ponownego rozruchu hello właściwości.</span><span class="sxs-lookup"><span data-stu-id="8b33a-134">Polls hello reported properties sent from hello device toodetermine when hello reboot is complete.</span></span>

<span data-ttu-id="8b33a-135">Ta aplikacja konsoli łączy tooyour Centrum IoT metoda bezpośrednia hello tooinvoke i hello odczytu zgłoszone właściwości.</span><span class="sxs-lookup"><span data-stu-id="8b33a-135">This console app connects tooyour IoT Hub tooinvoke hello direct method and read hello reported properties.</span></span>

1. <span data-ttu-id="8b33a-136">Utwórz pusty folder o nazwie dm-get-started.</span><span class="sxs-lookup"><span data-stu-id="8b33a-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="8b33a-137">W folderze dm-get-started hello Utwórz projekt Maven o nazwie **ponowne uruchomienie wyzwalacza** przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="8b33a-137">In hello dm-get-started folder, create a Maven project called **trigger-reboot** using hello following command at your command prompt.</span></span> <span data-ttu-id="8b33a-138">Oto Hello polecenia jednej, długi:</span><span class="sxs-lookup"><span data-stu-id="8b33a-138">hello following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="8b33a-139">Wierszu polecenia przejdź toohello ponowne uruchomienie wyzwalacza folderu.</span><span class="sxs-lookup"><span data-stu-id="8b33a-139">At your command prompt, navigate toohello trigger-reboot folder.</span></span>

1. <span data-ttu-id="8b33a-140">Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze ponowne uruchomienie wyzwalacza hello i dodaj następujące zależności toohello hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="8b33a-140">Using a text editor, open hello pom.xml file in hello trigger-reboot folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="8b33a-141">Ta zależność umożliwia możesz toouse hello iot usługi klienta pakietu w Twojej toocommunicate aplikacji z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="8b33a-141">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="8b33a-142">Możesz sprawdzić hello najnowszą wersję **klienta w przypadku usługi iot** przy użyciu [wyszukiwania Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="8b33a-142">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="8b33a-143">Dodaj następujące hello **kompilacji** węzła po hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="8b33a-143">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="8b33a-144">Ta konfiguracja powoduje, że Maven toouse Java 1,8 toobuild hello aplikacji:</span><span class="sxs-lookup"><span data-stu-id="8b33a-144">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="8b33a-145">Zapisz i zamknij plik pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="8b33a-145">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="8b33a-146">Za pomocą edytora tekstu, otwórz plik źródłowy trigger-reboot\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="8b33a-146">Using a text editor, open hello trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="8b33a-147">Dodaj następujące hello **zaimportować** instrukcje toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="8b33a-147">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. <span data-ttu-id="8b33a-148">Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="8b33a-148">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="8b33a-149">Zastąp `{youriothubconnectionstring}` z parametrów połączenia Centrum IoT zanotowaną w hello *tworzenia Centrum IoT* sekcji:</span><span class="sxs-lookup"><span data-stu-id="8b33a-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="8b33a-150">tooimplement wątku, który odczytuje hello zgłosił właściwości z dwie urządzenia hello co 10 sekund, Dodaj hello zagnieżdżona klasa toohello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="8b33a-150">tooimplement a thread that reads hello reported properties from hello device twin every 10 seconds, add hello following nested class toohello **App** class:</span></span>

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="8b33a-151">Metoda bezpośrednia ponowny rozruch hello tooinvoke na powitania symulowane urządzenie, Dodaj hello następującego kodu toohello **głównego** metody:</span><span class="sxs-lookup"><span data-stu-id="8b33a-151">tooinvoke hello reboot direct method on hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="8b33a-152">toostart hello wątku toopoll hello zgłoszone właściwości z hello symulowane urządzenie, należy dodać hello następującego kodu toohello **głównego** metody:</span><span class="sxs-lookup"><span data-stu-id="8b33a-152">toostart hello thread toopoll hello reported properties from hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="8b33a-153">tooenable toostop hello aplikacji, Dodaj hello następującego kodu toohello **głównego** metody:</span><span class="sxs-lookup"><span data-stu-id="8b33a-153">tooenable you toostop hello app, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="8b33a-154">Zapisz i zamknij plik trigger-reboot\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="8b33a-154">Save and close hello trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="8b33a-155">Tworzenie hello **ponowne uruchomienie wyzwalacza** aplikacji zaplecza i poprawić błędy.</span><span class="sxs-lookup"><span data-stu-id="8b33a-155">Build hello **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="8b33a-156">Wierszu polecenia przejdź toohello ponowne uruchomienie wyzwalacza folder i hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="8b33a-156">At your command prompt, navigate toohello trigger-reboot folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="8b33a-157">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="8b33a-157">Create a simulated device app</span></span>

<span data-ttu-id="8b33a-158">W tej sekcji utworzysz aplikację konsoli języka Java, która symuluje urządzenia.</span><span class="sxs-lookup"><span data-stu-id="8b33a-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="8b33a-159">Aplikacja Hello nasłuchuje wywołanie metody bezpośredniego ponowny rozruch hello z Centrum IoT i natychmiast odpowiada toothat wywołania.</span><span class="sxs-lookup"><span data-stu-id="8b33a-159">hello app listens for hello reboot direct method call from your IoT hub and immediately responds toothat call.</span></span> <span data-ttu-id="8b33a-160">Witaj aplikacji, a następnie sen jakiś czas toosimulate hello ponowne uruchomienie procesu przed użyciem hello toonotify zgłoszone właściwości **ponowne uruchomienie wyzwalacza** zaplecza aplikacji hello ponowne uruchomienie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="8b33a-160">hello app then sleeps for a while toosimulate hello reboot process before it uses a reported property toonotify hello **trigger-reboot** back-end app that hello reboot is complete.</span></span>

1. <span data-ttu-id="8b33a-161">W folderze dm-get-started hello Utwórz projekt Maven o nazwie **symulowane urządzenie** przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="8b33a-161">In hello dm-get-started folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="8b33a-162">następujące Hello jest poleceniem jednej, długi:</span><span class="sxs-lookup"><span data-stu-id="8b33a-162">hello following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="8b33a-163">Wierszu polecenia przejdź toohello symulowane urządzenie folderu.</span><span class="sxs-lookup"><span data-stu-id="8b33a-163">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="8b33a-164">Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze symulowane urządzenie hello i dodaj następujące zależności toohello hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="8b33a-164">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="8b33a-165">Ta zależność umożliwia możesz toouse hello iot usługi klienta pakietu w Twojej toocommunicate aplikacji z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="8b33a-165">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="8b33a-166">Możesz sprawdzić hello najnowszą wersję **klienta w przypadku urządzenia iot** przy użyciu [wyszukiwania Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="8b33a-166">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="8b33a-167">Dodaj następujące hello **kompilacji** węzła po hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="8b33a-167">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="8b33a-168">Ta konfiguracja powoduje, że Maven toouse Java 1,8 toobuild hello aplikacji:</span><span class="sxs-lookup"><span data-stu-id="8b33a-168">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="8b33a-169">Zapisz i zamknij plik pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="8b33a-169">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="8b33a-170">Za pomocą edytora tekstu, otwórz plik źródłowy simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="8b33a-170">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="8b33a-171">Dodaj następujące hello **zaimportować** instrukcje toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="8b33a-171">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. <span data-ttu-id="8b33a-172">Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="8b33a-172">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="8b33a-173">Zastąp `{yourdeviceconnectionstring}` przy użyciu parametrów połączenia urządzenia hello zanotowaną w hello *tworzenie tożsamości urządzenia* sekcji:</span><span class="sxs-lookup"><span data-stu-id="8b33a-173">Replace `{yourdeviceconnectionstring}` with hello device connection string you noted in hello *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="8b33a-174">tooimplement obsługi wywołania zwrotnego, metoda bezpośrednia zdarzeń stanu, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="8b33a-174">tooimplement a callback handler for direct method status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="8b33a-175">tooimplement obsługi wywołania zwrotnego dla zdarzeń urządzenia dwie stanu, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="8b33a-175">tooimplement a callback handler for device twin status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="8b33a-176">tooimplement obsługi wywołania zwrotnego dla właściwości zdarzenia, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="8b33a-176">tooimplement a callback handler for property events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. <span data-ttu-id="8b33a-177">tooimplement wątku toosimulate hello urządzenia ponownego uruchomienia komputera, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="8b33a-177">tooimplement a thread toosimulate hello device reboot, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="8b33a-178">Wątek Hello zostanie uśpiony na pięć sekund, a następnie ustawia hello **lastReboot** zgłoszonych właściwości:</span><span class="sxs-lookup"><span data-stu-id="8b33a-178">hello thread sleeps for five seconds and then sets hello **lastReboot** reported property:</span></span>

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="8b33a-179">Metoda bezpośrednia hello tooimplement na urządzeniu hello, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="8b33a-179">tooimplement hello direct method on hello device, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="8b33a-180">Gdy aplikacja symulowane hello odbiera toohello wywołania **ponowny rozruch** metoda bezpośrednia zwraca obiekt wywołujący toohello potwierdzenia i następnie uruchamia hello tooprocess wątku ponownego rozruchu:</span><span class="sxs-lookup"><span data-stu-id="8b33a-180">When hello simulated app receives a call toohello **reboot** direct method, it returns an acknowledgement toohello caller and then starts a thread tooprocess hello reboot:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. <span data-ttu-id="8b33a-181">Modyfikowanie hello podpis hello **głównego** hello toothrow metody następujące wyjątki:</span><span class="sxs-lookup"><span data-stu-id="8b33a-181">Modify hello signature of hello **main** method toothrow hello following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="8b33a-182">tooinstantiate **DeviceClient**, Dodaj hello następującego kodu toohello **głównego** metody:</span><span class="sxs-lookup"><span data-stu-id="8b33a-182">tooinstantiate a **DeviceClient**, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="8b33a-183">toostart nasłuchiwania dla wywołań metod bezpośrednie dodawanie hello następującego kodu toohello **głównego** metody:</span><span class="sxs-lookup"><span data-stu-id="8b33a-183">toostart listening for direct method calls, add hello following code toohello **main** method:</span></span>

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed toodirect methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="8b33a-184">tooshut dół hello symulator urządzeń, Dodaj hello następującego kodu toohello **głównego** metody:</span><span class="sxs-lookup"><span data-stu-id="8b33a-184">tooshut down hello device simulator, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="8b33a-185">Zapisz i zamknij plik simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="8b33a-185">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="8b33a-186">Tworzenie hello **symulowane urządzenie** aplikacji zaplecza i poprawić błędy.</span><span class="sxs-lookup"><span data-stu-id="8b33a-186">Build hello **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="8b33a-187">Wierszu polecenia przejdź folder symulowane urządzenie toohello i hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="8b33a-187">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="8b33a-188">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="8b33a-188">Run hello apps</span></span>

<span data-ttu-id="8b33a-189">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8b33a-189">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="8b33a-190">W wierszu polecenia w folderze symulowane urządzenie hello uruchom następujące polecenia toobegin nasłuchiwania dla wywołań metod ponowny rozruch z Centrum IoT hello:</span><span class="sxs-lookup"><span data-stu-id="8b33a-190">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java symulowane urządzenie toolisten aplikacji dla wywołań metod bezpośredniego ponowny rozruch][1]

1. <span data-ttu-id="8b33a-192">W wierszu polecenia w folderze ponowne uruchomienie wyzwalacza hello Uruchom hello, wykonując polecenie toocall hello ponowny rozruch metody na symulowane urządzenie z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="8b33a-192">At a command prompt in hello trigger-reboot folder, run hello following command toocall hello reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java usługi aplikacji toocall hello ponowny rozruch direct — metoda][2]

1. <span data-ttu-id="8b33a-194">Symulowane urządzenie Hello odpowiada wywołanie metody bezpośredniego ponowny rozruch toohello:</span><span class="sxs-lookup"><span data-stu-id="8b33a-194">hello simulated device responds toohello reboot direct method call:</span></span>

    ![Wywołanie metody bezpośredniego toohello odpowiada aplikacji symulowane urządzenie Java Centrum IoT][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22