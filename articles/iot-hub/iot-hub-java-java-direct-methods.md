---
title: "Centrum IoT Azure bezpośredniego metody (Java) | Dokumentacja firmy Microsoft"
description: "Jak używać bezpośrednich metod Centrum IoT Azure. Przy użyciu urządzenia Azure IoT SDK dla języka Java aplikacji symulowane urządzenie, która zawiera metoda bezpośrednia i usługę Azure IoT SDK dla języka Java, aby zaimplementować aplikację usługi, która wywołuje metodę bezpośredniego."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6243a1a8cc971c53c797182b2beb6f594d2ac5f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-direct-methods-java"></a><span data-ttu-id="ed827-104">Użyj metody bezpośredniego (Java)</span><span class="sxs-lookup"><span data-stu-id="ed827-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="ed827-105">W tym samouczku można utworzyć dwie aplikacje konsoli Java:</span><span class="sxs-lookup"><span data-stu-id="ed827-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="ed827-106">**wywołania bezpośrednie — metody**, aplikacji wewnętrznych Java, która wywołuje metodę w aplikacji symulowane urządzenie i wyświetla odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ed827-106">**invoke-direct-method**, a Java back-end app that calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="ed827-107">**Symulowane urządzenie**, aplikacji Java, która symuluje urządzenia nawiązywanie połączeń z Centrum IoT z tożsamości urządzenia można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="ed827-107">**simulated-device**, a Java app that simulates a device connecting to your IoT hub with the device identity you create.</span></span> <span data-ttu-id="ed827-108">Ta aplikacja odpowiada bezpośrednio wywołać z poziomu wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="ed827-108">This app responds to the direct invoked from the back end.</span></span>

> [!NOTE]
> <span data-ttu-id="ed827-109">Aby uzyskać informacji na temat zestawów SDK, które służy do tworzenia aplikacji do uruchamiania na urządzeniach i z zaplecza rozwiązania, zobacz [Azure IoT SDK][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="ed827-109">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="ed827-110">Do ukończenia tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ed827-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="ed827-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="ed827-111">Java SE 8.</span></span> <br/> <span data-ttu-id="ed827-112">W artykule [Prepare your development environment][lnk-dev-setup] (Przygotowanie środowiska projektowego) opisano, jak zainstalować środowisko Java na potrzeby tego samouczka w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="ed827-112">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="ed827-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="ed827-113">Maven 3.</span></span>  <br/> <span data-ttu-id="ed827-114">W artykule [Prepare your development environment][lnk-dev-setup] (Przygotowanie środowiska projektowego) opisano, jak zainstalować środowisko [Maven][lnk-maven] na potrzeby tego samouczka w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="ed827-114">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="ed827-115">[Środowisko node.js w wersji 0.10.0 lub nowszym](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="ed827-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="ed827-116">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="ed827-116">Create a simulated device app</span></span>

<span data-ttu-id="ed827-117">W tej sekcji utworzysz aplikację konsoli języka Java odpowiadający do metody wywoływane przez rozwiązania zakończenia.</span><span class="sxs-lookup"><span data-stu-id="ed827-117">In this section, you create a Java console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="ed827-118">Utwórz pusty folder o nazwie iot-java bezpośrednio method.</span><span class="sxs-lookup"><span data-stu-id="ed827-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="ed827-119">W folderze iot-java bezpośrednio method, Utwórz projekt Maven o nazwie **symulowane urządzenie** przy użyciu następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="ed827-119">In the iot-java-direct-method folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="ed827-120">Polecenie jest pojedynczą, długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="ed827-120">The following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="ed827-121">W wierszu polecenia przejdź do folderu simulated-device.</span><span class="sxs-lookup"><span data-stu-id="ed827-121">At your command prompt, navigate to the simulated-device folder.</span></span>

1. <span data-ttu-id="ed827-122">Za pomocą edytora tekstów otwórz plik pom.xml w folderze simulated-device i dodaj następujące zależności do węzła **zależności**.</span><span class="sxs-lookup"><span data-stu-id="ed827-122">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="ed827-123">Ta zależność umożliwia za pomocą pakietu klienta w przypadku urządzenia iot w aplikacji do komunikowania się z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="ed827-123">This dependency enables you to use the iot-device-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ed827-124">Możesz sprawdzić dostępność najnowszej wersji pakietu **iot-device-client** za pomocą [funkcji wyszukiwania narzędzia Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="ed827-124">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="ed827-125">Dodaj następujące **kompilacji** węzła po **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="ed827-125">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="ed827-126">Ta konfiguracja powoduje, że Maven na potrzeby tworzenia aplikacji Java 1.8:</span><span class="sxs-lookup"><span data-stu-id="ed827-126">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="ed827-127">Zapisz i zamknij plik pom.xml.</span><span class="sxs-lookup"><span data-stu-id="ed827-127">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="ed827-128">Za pomocą edytora tekstów otwórz plik simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="ed827-128">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="ed827-129">Dodaj do pliku następujące instrukcje **importowania**:</span><span class="sxs-lookup"><span data-stu-id="ed827-129">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="ed827-130">Dodaj następujące zmienne na poziomie klasy do klasy **App**.</span><span class="sxs-lookup"><span data-stu-id="ed827-130">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="ed827-131">Zastępowanie `{youriothubname}` z nazwę Centrum IoT i `{yourdevicekey}` kluczem urządzenia wartość, zostanie wygenerowany w *tworzenie tożsamości urządzenia* sekcji:</span><span class="sxs-lookup"><span data-stu-id="ed827-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="ed827-132">Ta przykładowa aplikacja używa zmiennej **protocol** podczas tworzenia wystąpienia obiektu **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="ed827-132">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="ed827-133">Obecnie bezpośredniego metod musi używać protokołu MQTT.</span><span class="sxs-lookup"><span data-stu-id="ed827-133">Currently, to use direct methods you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="ed827-134">Aby przywrócić Centrum IoT kod stanu, Dodaj następujące zagnieżdżona klasa na **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="ed827-134">To return a status code to your IoT hub, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded to device method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="ed827-135">Do obsługi wywołań metody bezpośrednio z zaplecza rozwiązania, należy dodać następujące zagnieżdżona klasa na **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="ed827-135">To handle the direct method invocations from the solution back end, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
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

1. <span data-ttu-id="ed827-136">Aby utworzyć **DeviceClient** i nasłuchiwania bezpośrednie wywołania metod, Dodaj **głównego** metodę **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="ed827-136">To create a **DeviceClient** and listen for direct method invocations, add a **main** method to the **App** class:</span></span>

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed to direct methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key to exit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="ed827-137">Zapisz i zamknij plik simulated-device\src\main\java\com\mycompany\app\App.java</span><span class="sxs-lookup"><span data-stu-id="ed827-137">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="ed827-138">Tworzenie **symulowane urządzenie** aplikacji i poprawić błędy.</span><span class="sxs-lookup"><span data-stu-id="ed827-138">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="ed827-139">Wierszu polecenia przejdź do folderu symulowane urządzenie, a następnie uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ed827-139">At your command prompt, navigate to the simulated-device folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="ed827-140">Wywołanie metody bezpośrednio na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="ed827-140">Call a direct method on a device</span></span>

<span data-ttu-id="ed827-141">W tej sekcji utworzysz aplikację konsoli języka Java, która wywołuje metodę bezpośredniego, a następnie wyświetla odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ed827-141">In this section, you create a Java console app that invokes a direct method and then displays the response.</span></span> <span data-ttu-id="ed827-142">Łączy się Centrum IoT można wywołać metody bezpośrednio z tej aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="ed827-142">This console app connects to your IoT Hub to invoke the direct method.</span></span>

1. <span data-ttu-id="ed827-143">W folderze iot-java bezpośrednio method, Utwórz projekt Maven o nazwie **invoke bezpośrednio method** za pomocą następującego polecenia z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="ed827-143">In the iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using the following command at your command prompt.</span></span> <span data-ttu-id="ed827-144">Polecenie jest pojedynczą, długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="ed827-144">The following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="ed827-145">Wierszu polecenia przejdź do folderu metody invoke bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="ed827-145">At your command prompt, navigate to the invoke-direct-method folder.</span></span>

1. <span data-ttu-id="ed827-146">Za pomocą edytora tekstu, otwórz plik pom.xml w folderze metody invoke bezpośredniego i dodaj następujące zależności do **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="ed827-146">Using a text editor, open the pom.xml file in the invoke-direct-method folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="ed827-147">Ta zależność umożliwia za pomocą pakietu iot usługi klienta w aplikacji do komunikowania się z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="ed827-147">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="ed827-148">Możesz sprawdzić dostępność najnowszej wersji pakietu **iot-service-client** za pomocą [funkcji wyszukiwania narzędzia Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="ed827-148">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="ed827-149">Dodaj następujące **kompilacji** węzła po **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="ed827-149">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="ed827-150">Ta konfiguracja powoduje, że Maven na potrzeby tworzenia aplikacji Java 1.8:</span><span class="sxs-lookup"><span data-stu-id="ed827-150">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="ed827-151">Zapisz i zamknij plik pom.xml.</span><span class="sxs-lookup"><span data-stu-id="ed827-151">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="ed827-152">Za pomocą edytora tekstu, otwórz plik invoke-direct-method\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="ed827-152">Using a text editor, open the invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="ed827-153">Dodaj do pliku następujące instrukcje **importowania**:</span><span class="sxs-lookup"><span data-stu-id="ed827-153">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="ed827-154">Dodaj następujące zmienne na poziomie klasy do klasy **App**.</span><span class="sxs-lookup"><span data-stu-id="ed827-154">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="ed827-155">Zastąp `{youriothubconnectionstring}` z wymienionych w ciągu połączenia Centrum IoT *tworzenia Centrum IoT* sekcji:</span><span class="sxs-lookup"><span data-stu-id="ed827-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line to be written";
    ```

1. <span data-ttu-id="ed827-156">Aby wywołać metodę na symulowane urządzenie, Dodaj następujący kod do **głównego** metody:</span><span class="sxs-lookup"><span data-stu-id="ed827-156">To invoke the method on the simulated device, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="ed827-157">Zapisz i zamknij plik invoke-direct-method\src\main\java\com\mycompany\app\App.java</span><span class="sxs-lookup"><span data-stu-id="ed827-157">Save and close the invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="ed827-158">Tworzenie **invoke bezpośrednio method** aplikacji i poprawić błędy.</span><span class="sxs-lookup"><span data-stu-id="ed827-158">Build the **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="ed827-159">Wiersz polecenia przejdź do folderu metody invoke bezpośrednio i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ed827-159">At your command prompt, navigate to the invoke-direct-method folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="ed827-160">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="ed827-160">Run the apps</span></span>

<span data-ttu-id="ed827-161">Teraz można przystąpić do uruchomienia aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="ed827-161">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="ed827-162">W wierszu polecenia w folderze symulowane urządzenie uruchom następujące polecenie, aby rozpocząć nasłuchiwania dla wywołań metod z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="ed827-162">At a command prompt in the simulated-device folder, run the following command to begin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java symulowane urządzenie aplikacji do nasłuchiwania dla wywołań metod bezpośredniego][8]

1. <span data-ttu-id="ed827-164">W wierszu polecenia w folderze metody invoke bezpośrednio uruchom następujące polecenie, aby wywołać metodę na symulowane urządzenie z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="ed827-164">At a command prompt in the invoke-direct-method folder, run the following command to call a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java usługi aplikacji, aby wywołać metodę bezpośredniego][7]

1. <span data-ttu-id="ed827-166">Symulowane urządzenie odpowiada na wywołanie metody bezpośrednie:</span><span class="sxs-lookup"><span data-stu-id="ed827-166">The simulated device responds to the direct method call:</span></span>

    ![Centrum IoT Java symulowane urządzenie aplikacji odpowiada na wywołanie bezpośrednie — metoda][9]

## <a name="next-steps"></a><span data-ttu-id="ed827-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ed827-168">Next steps</span></span>

<span data-ttu-id="ed827-169">W tym samouczku opisano konfigurowanie nowego centrum IoT Hub w witrynie Azure Portal, a następnie tworzenie tożsamości urządzenia w rejestrze tożsamości centrum.</span><span class="sxs-lookup"><span data-stu-id="ed827-169">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="ed827-170">Tej tożsamości urządzenia są używane do włączenia aplikacji symulowane urządzenie zareagować na metody wywoływane przez chmurę.</span><span class="sxs-lookup"><span data-stu-id="ed827-170">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="ed827-171">Utworzono aplikację, która wywołuje metody na urządzeniu i wyświetla odpowiedzi z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ed827-171">You also created an app that invokes methods on the device and displays the response from the device.</span></span>

<span data-ttu-id="ed827-172">Aby zapoznać się z innymi scenariuszami IoT, zobacz [Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs].</span><span class="sxs-lookup"><span data-stu-id="ed827-172">To explore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="ed827-173">Aby dowiedzieć się, jak rozszerzyć IoT, Twoje rozwiązanie i harmonogram metoda wywołuje na wielu urządzeniach, zobacz [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="ed827-173">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
