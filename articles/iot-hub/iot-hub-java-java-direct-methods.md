---
title: "Centrum IoT Azure aaaUse bezpośrednie metod (Java) | Dokumentacja firmy Microsoft"
description: "Jak toouse Centrum IoT Azure bezpośrednie metody. Możesz używać urządzenia Azure IoT hello zestawu SDK dla języka Java tooimplement aplikacji symulowane urządzenie, która obejmuje metoda bezpośrednia i hello Azure IoT usługi SDK dla języka Java tooimplement usługi aplikacji, która wywołuje metodę bezpośredniego hello."
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
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a><span data-ttu-id="a3641-104">Użyj metody bezpośredniego (Java)</span><span class="sxs-lookup"><span data-stu-id="a3641-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="a3641-105">W tym samouczku można utworzyć dwie aplikacje konsoli Java:</span><span class="sxs-lookup"><span data-stu-id="a3641-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="a3641-106">**wywołania bezpośrednie — metody**, aplikacji zaplecza Java, która wywołuje metodę w aplikacji symulowane urządzenie hello i wyświetla hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a3641-106">**invoke-direct-method**, a Java back-end app that calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="a3641-107">**Symulowane urządzenie**, która symuluje urządzenie łączące Centrum IoT tooyour z tożsamości urządzenia hello tworzenia aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="a3641-107">**simulated-device**, a Java app that simulates a device connecting tooyour IoT hub with hello device identity you create.</span></span> <span data-ttu-id="a3641-108">Ta aplikacja odpowiada toohello wywoływany bezpośrednio z zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="a3641-108">This app responds toohello direct invoked from hello back end.</span></span>

> [!NOTE]
> <span data-ttu-id="a3641-109">Informacje hello zestawów SDK, której można toobuild toorun aplikacji na urządzeniach i z zaplecza rozwiązania, zobacz [Azure IoT SDK][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="a3641-109">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="a3641-110">toocomplete tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="a3641-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="a3641-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="a3641-111">Java SE 8.</span></span> <br/> <span data-ttu-id="a3641-112">[Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Java w tym samouczku w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="a3641-112">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a3641-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="a3641-113">Maven 3.</span></span>  <br/> <span data-ttu-id="a3641-114">[Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall [Maven] [ lnk-maven] ten samouczek dotyczący systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="a3641-114">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a3641-115">[Środowisko node.js w wersji 0.10.0 lub nowszym](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="a3641-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="a3641-116">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="a3641-116">Create a simulated device app</span></span>

<span data-ttu-id="a3641-117">W tej sekcji utworzysz aplikację konsoli Java, która odpowiada tooa metody wywoływane przez rozwiązania hello zakończenia.</span><span class="sxs-lookup"><span data-stu-id="a3641-117">In this section, you create a Java console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="a3641-118">Utwórz pusty folder o nazwie iot-java bezpośrednio method.</span><span class="sxs-lookup"><span data-stu-id="a3641-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="a3641-119">W folderze iot-java bezpośrednio method hello Utwórz projekt Maven o nazwie **symulowane urządzenie** przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a3641-119">In hello iot-java-direct-method folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="a3641-120">Hello następujące polecenia jest pojedynczą, długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="a3641-120">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="a3641-121">Wierszu polecenia przejdź toohello symulowane urządzenie folderu.</span><span class="sxs-lookup"><span data-stu-id="a3641-121">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="a3641-122">Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze symulowane urządzenie hello i dodaj następujące zależności toohello hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="a3641-122">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="a3641-123">Ta zależność umożliwia możesz toouse powitania klienta w przypadku urządzenia iot pakiet w toocommunicate Twojego aplikacji z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="a3641-123">This dependency enables you toouse hello iot-device-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="a3641-124">Możesz sprawdzić hello najnowszą wersję **klienta w przypadku urządzenia iot** przy użyciu [wyszukiwania Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="a3641-124">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="a3641-125">Dodaj następujące hello **kompilacji** węzła po hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="a3641-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="a3641-126">Ta konfiguracja powoduje, że Maven toouse Java 1,8 toobuild hello aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a3641-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="a3641-127">Zapisz i zamknij plik pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="a3641-127">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="a3641-128">Za pomocą edytora tekstu, otwórz plik simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="a3641-128">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="a3641-129">Dodaj następujące hello **zaimportować** instrukcje toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="a3641-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="a3641-130">Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="a3641-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="a3641-131">Zastępowanie `{youriothubname}` z nazwę Centrum IoT i `{yourdevicekey}` o wartości klucza urządzenia hello wygenerowanych w hello *tworzenie tożsamości urządzenia* sekcji:</span><span class="sxs-lookup"><span data-stu-id="a3641-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="a3641-132">Ta przykładowa aplikacja używa hello **protokołu** zmiennej podczas tworzenia wystąpień **DeviceClient** obiektu.</span><span class="sxs-lookup"><span data-stu-id="a3641-132">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="a3641-133">Obecnie toouse bezpośrednie metody muszą używać protokołu MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="a3641-133">Currently, toouse direct methods you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="a3641-134">tooreturn koncentratora IoT tooyour kod stanu, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="a3641-134">tooreturn a status code tooyour IoT hub, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="a3641-135">toohandle hello bezpośrednie wywołania metod z hello rozwiązania wewnętrznego, Dodaj następujące hello zagnieżdżona klasa toohello **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="a3641-135">toohandle hello direct method invocations from hello solution back end, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="a3641-136">toocreate **DeviceClient** i nasłuchiwania bezpośrednie wywołania metod, dodać **głównego** toohello metody **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="a3641-136">toocreate a **DeviceClient** and listen for direct method invocations, add a **main** method toohello **App** class:</span></span>

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
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="a3641-137">Zapisz i zamknij plik simulated-device\src\main\java\com\mycompany\app\App.java hello</span><span class="sxs-lookup"><span data-stu-id="a3641-137">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="a3641-138">Tworzenie hello **symulowane urządzenie** aplikacji i poprawić błędy.</span><span class="sxs-lookup"><span data-stu-id="a3641-138">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="a3641-139">Wierszu polecenia przejdź folder symulowane urządzenie toohello i hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a3641-139">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="a3641-140">Wywołanie metody bezpośrednio na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="a3641-140">Call a direct method on a device</span></span>

<span data-ttu-id="a3641-141">W tej sekcji utworzysz aplikację konsoli języka Java, która wywołuje metodę bezpośredniego, a następnie wyświetla hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a3641-141">In this section, you create a Java console app that invokes a direct method and then displays hello response.</span></span> <span data-ttu-id="a3641-142">Ta aplikacja konsoli łączy tooyour metoda bezpośrednia hello tooinvoke Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a3641-142">This console app connects tooyour IoT Hub tooinvoke hello direct method.</span></span>

1. <span data-ttu-id="a3641-143">W folderze iot-java bezpośrednio method hello Utwórz projekt Maven o nazwie **invoke bezpośrednio method** przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a3641-143">In hello iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using hello following command at your command prompt.</span></span> <span data-ttu-id="a3641-144">Hello następujące polecenia jest pojedynczą, długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="a3641-144">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="a3641-145">Wierszu polecenia przejdź toohello invoke bezpośrednio method folderu.</span><span class="sxs-lookup"><span data-stu-id="a3641-145">At your command prompt, navigate toohello invoke-direct-method folder.</span></span>

1. <span data-ttu-id="a3641-146">Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze invoke bezpośrednio method hello i dodaj następujące zależności toohello hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="a3641-146">Using a text editor, open hello pom.xml file in hello invoke-direct-method folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="a3641-147">Ta zależność umożliwia możesz toouse hello iot usługi klienta pakietu w Twojej toocommunicate aplikacji z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="a3641-147">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="a3641-148">Możesz sprawdzić hello najnowszą wersję **klienta w przypadku usługi iot** przy użyciu [wyszukiwania Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="a3641-148">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="a3641-149">Dodaj następujące hello **kompilacji** węzła po hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="a3641-149">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="a3641-150">Ta konfiguracja powoduje, że Maven toouse Java 1,8 toobuild hello aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a3641-150">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="a3641-151">Zapisz i zamknij plik pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="a3641-151">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="a3641-152">Za pomocą edytora tekstu, otwórz plik invoke-direct-method\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="a3641-152">Using a text editor, open hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="a3641-153">Dodaj następujące hello **zaimportować** instrukcje toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="a3641-153">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="a3641-154">Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="a3641-154">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="a3641-155">Zastąp `{youriothubconnectionstring}` z parametrów połączenia Centrum IoT zanotowaną w hello *tworzenia Centrum IoT* sekcji:</span><span class="sxs-lookup"><span data-stu-id="a3641-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. <span data-ttu-id="a3641-156">Metoda hello tooinvoke na powitania symulowane urządzenie, Dodaj hello następującego kodu toohello **głównego** metody:</span><span class="sxs-lookup"><span data-stu-id="a3641-156">tooinvoke hello method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="a3641-157">Zapisz i zamknij plik invoke-direct-method\src\main\java\com\mycompany\app\App.java hello</span><span class="sxs-lookup"><span data-stu-id="a3641-157">Save and close hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="a3641-158">Tworzenie hello **invoke bezpośrednio method** aplikacji i poprawić błędy.</span><span class="sxs-lookup"><span data-stu-id="a3641-158">Build hello **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="a3641-159">Wierszu polecenia przejdź toohello invoke bezpośrednio method folder i hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a3641-159">At your command prompt, navigate toohello invoke-direct-method folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="a3641-160">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="a3641-160">Run hello apps</span></span>

<span data-ttu-id="a3641-161">Wszystko jest teraz gotowy toorun hello konsoli aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a3641-161">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="a3641-162">W wierszu polecenia w folderze symulowane urządzenie hello uruchom następujące polecenia toobegin nasłuchiwania dla wywołań metod z Centrum IoT hello:</span><span class="sxs-lookup"><span data-stu-id="a3641-162">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java symulowane urządzenie toolisten aplikacji dla wywołań metod bezpośredniego][8]

1. <span data-ttu-id="a3641-164">W wierszu polecenia w folderze invoke bezpośrednio method hello uruchom następujące polecenie toocall hello metody na symulowane urządzenie z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="a3641-164">At a command prompt in hello invoke-direct-method folder, run hello following command toocall a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Toocall aplikacji usługi Centrum IoT Java metoda bezpośrednia][7]

1. <span data-ttu-id="a3641-166">Symulowane urządzenie Hello odpowiada wywołanie metody bezpośredniego toohello:</span><span class="sxs-lookup"><span data-stu-id="a3641-166">hello simulated device responds toohello direct method call:</span></span>

    ![Wywołanie metody bezpośredniego toohello odpowiada aplikacji symulowane urządzenie Java Centrum IoT][9]

## <a name="next-steps"></a><span data-ttu-id="a3641-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a3641-168">Next steps</span></span>

<span data-ttu-id="a3641-169">W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a3641-169">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="a3641-170">Użyto tego urządzenia tożsamości tooenable hello symulowane urządzenie aplikacji tooreact toomethods wywołana przez hello chmury.</span><span class="sxs-lookup"><span data-stu-id="a3641-170">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="a3641-171">Utworzono aplikację, która wywołuje metody na urządzeniu hello i wyświetla hello odpowiedzi z hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a3641-171">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span>

<span data-ttu-id="a3641-172">tooexplore Zobacz inne scenariusze IoT [Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs].</span><span class="sxs-lookup"><span data-stu-id="a3641-172">tooexplore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="a3641-173">toolearn tooextend IoT metody rozwiązania i harmonogram wywołuje na wielu urządzeniach, zobacz hello [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="a3641-173">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
