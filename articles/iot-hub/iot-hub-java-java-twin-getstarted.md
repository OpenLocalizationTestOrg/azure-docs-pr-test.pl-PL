---
title: "aaaGet wprowadzenie twins urządzenia Azure IoT Hub (Java) | Dokumentacja firmy Microsoft"
description: "Jak tooadd twins urządzenia Azure IoT Hub toouse tagów, a następnie użyj zapytania Centrum IoT. Używasz urządzenia Azure IoT hello zestawu SDK dla języka Java tooimplement hello urządzenia aplikacji i hello Azure IoT usługi SDK dla języka Java tooimplement aplikacji usługi, który dodaje znaczniki hello i uruchamia hello zapytania Centrum IoT."
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
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: 25f6fc81471d59c62bcdc3766bb5c33f5733c930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="26d8f-104">Rozpoczynanie pracy z urządzenia twins (Java)</span><span class="sxs-lookup"><span data-stu-id="26d8f-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="26d8f-105">W tym samouczku można utworzyć dwie aplikacje konsoli Java:</span><span class="sxs-lookup"><span data-stu-id="26d8f-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="26d8f-106">**Dodaj tag query**, aplikacji zaplecza Java, która dodaje znaczniki i zapytanie twins urządzenia.</span><span class="sxs-lookup"><span data-stu-id="26d8f-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="26d8f-107">**Symulowane urządzenie**, że łączące Centrum IoT tooyour i raporty stanu łączności za pomocą właściwości zgłoszone aplikacji Java urządzenia.</span><span class="sxs-lookup"><span data-stu-id="26d8f-107">**simulated-device**, a Java device app that that connects tooyour IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="26d8f-108">Artykuł Hello [Azure IoT SDK](iot-hub-devguide-sdks.md) informacje na temat hello Azure IoT SDK służy toobuild zarówno urządzenia, jak i zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="26d8f-108">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

<span data-ttu-id="26d8f-109">toocomplete tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="26d8f-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="26d8f-110">Witaj najnowszych [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="26d8f-110">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="26d8f-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="26d8f-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="26d8f-112">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="26d8f-112">An active Azure account.</span></span> <span data-ttu-id="26d8f-113">(Jeśli nie masz konta, możesz utworzyć [bezpłatne konto](http://azure.microsoft.com/pricing/free-trial/) w zaledwie kilka minut.)</span><span class="sxs-lookup"><span data-stu-id="26d8f-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="26d8f-114">Jeśli wolisz tożsamości urządzenia hello toocreate programowo, przeczytaj hello odpowiedniej sekcji w hello [połączenia przy użyciu języka Java Centrum IoT urządzenia tooyour](iot-hub-java-java-getstarted.md#create-a-device-identity) artykułu.</span><span class="sxs-lookup"><span data-stu-id="26d8f-114">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="26d8f-115">Tworzenie aplikacji usługi hello</span><span class="sxs-lookup"><span data-stu-id="26d8f-115">Create hello service app</span></span>

<span data-ttu-id="26d8f-116">W tej sekcji utworzysz aplikację Java dodające metadanych lokalizacji dwie tag toohello urządzenie w Centrum IoT skojarzone z **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="26d8f-116">In this section, you create a Java app that adds location metadata as a tag toohello device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="26d8f-117">Aplikacja Hello najpierw wysyła zapytanie Centrum IoT dla urządzeń znajdujących się w hello USA, a następnie dla urządzeń, które zgłosiły połączenia sieci komórkowej.</span><span class="sxs-lookup"><span data-stu-id="26d8f-117">hello app first queries IoT hub for devices located in hello US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="26d8f-118">Na komputerze deweloperskim, należy utworzyć pusty folder o nazwie `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="26d8f-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="26d8f-119">W hello `iot-java-twin-getstarted` folderu, Utwórz projekt Maven o nazwie **Dodaj tag query** przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="26d8f-119">In hello `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using hello following command at your command prompt.</span></span> <span data-ttu-id="26d8f-120">Zwróć uwagę, że jest to jedno długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="26d8f-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="26d8f-121">Wierszu polecenia przejdź toohello `add-tags-query` folderu.</span><span class="sxs-lookup"><span data-stu-id="26d8f-121">At your command prompt, navigate toohello `add-tags-query` folder.</span></span>

1. <span data-ttu-id="26d8f-122">Za pomocą edytora tekstu, otwórz hello `pom.xml` pliku w hello `add-tags-query` folderu i dodaj następujące zależności toohello hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="26d8f-122">Using a text editor, open hello `pom.xml` file in hello `add-tags-query` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="26d8f-123">Ta zależność umożliwia toouse hello **klienta w przypadku usługi iot** pakiet w Twojej toocommunicate aplikacji z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="26d8f-123">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="26d8f-124">Możesz sprawdzić hello najnowszą wersję **klienta w przypadku usługi iot** przy użyciu [wyszukiwania Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="26d8f-124">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="26d8f-125">Dodaj następujące hello **kompilacji** węzła po hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="26d8f-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="26d8f-126">Ta konfiguracja powoduje, że Maven toouse Java 1,8 toobuild hello aplikacji:</span><span class="sxs-lookup"><span data-stu-id="26d8f-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="26d8f-127">Zapisz i zamknij hello `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="26d8f-127">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="26d8f-128">Za pomocą edytora tekstu, otwórz hello `add-tags-query\src\main\java\com\mycompany\app\App.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="26d8f-128">Using a text editor, open hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="26d8f-129">Dodaj następujące hello **zaimportować** instrukcje toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="26d8f-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="26d8f-130">Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="26d8f-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="26d8f-131">Zastąp `{youriothubconnectionstring}` z parametrów połączenia Centrum IoT zanotowaną w hello *tworzenia Centrum IoT* sekcji:</span><span class="sxs-lookup"><span data-stu-id="26d8f-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="26d8f-132">Aktualizacja hello **głównego** następujące hello tooinclude podpis metody `throws` klauzuli:</span><span class="sxs-lookup"><span data-stu-id="26d8f-132">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="26d8f-133">Dodaj hello następującego kodu toohello **głównego** hello toocreate — metoda **DeviceTwin** i **DeviceTwinDevice** obiektów.</span><span class="sxs-lookup"><span data-stu-id="26d8f-133">Add hello following code toohello **main** method toocreate hello **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="26d8f-134">Witaj **DeviceTwin** obiektu obsługuje hello komunikację z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="26d8f-134">hello **DeviceTwin** object handles hello communication with your IoT hub.</span></span> <span data-ttu-id="26d8f-135">Witaj **DeviceTwinDevice** obiekt reprezentuje Witaj dwie urządzenia z jego właściwości i tagi:</span><span class="sxs-lookup"><span data-stu-id="26d8f-135">hello **DeviceTwinDevice** object represents hello device twin with its properties and tags:</span></span>

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="26d8f-136">Dodaj następujące hello `try/catch` zablokować toohello **głównego** metody:</span><span class="sxs-lookup"><span data-stu-id="26d8f-136">Add hello following `try/catch` block toohello **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="26d8f-137">Witaj tooupdate **region** i **roślin** hello następującego kodu w hello Dodaj tagi dwie urządzeń w Twojej dwie urządzenia `try` bloku:</span><span class="sxs-lookup"><span data-stu-id="26d8f-137">tooupdate hello **region** and **plant** device twin tags in your device twin, add hello following code in hello `try` block:</span></span>

    ```java
    // Get hello device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from hello existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create hello tags and attach them toohello DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update hello device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve hello device twin with hello tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. <span data-ttu-id="26d8f-138">tooquery hello urządzenia twins w Centrum IoT, Dodaj hello następującego kodu toohello `try` blok po kodzie hello dodanym w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="26d8f-138">tooquery hello device twins in IoT hub, add hello following code toohello `try` block after hello code you added in hello previous step.</span></span> <span data-ttu-id="26d8f-139">Kod Hello uruchamia dwa zapytania.</span><span class="sxs-lookup"><span data-stu-id="26d8f-139">hello code runs two queries.</span></span> <span data-ttu-id="26d8f-140">Każde zapytanie zwraca maksymalnie 100 urządzeń:</span><span class="sxs-lookup"><span data-stu-id="26d8f-140">Each query returns a maximum of 100 devices:</span></span>

    ```java
    // Query hello device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct hello query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run hello query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct hello query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run hello query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. <span data-ttu-id="26d8f-141">Zapisz i zamknij hello `add-tags-query\src\main\java\com\mycompany\app\App.java` pliku</span><span class="sxs-lookup"><span data-stu-id="26d8f-141">Save and close hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="26d8f-142">Tworzenie hello **Dodaj tag query** aplikacji i poprawić błędy.</span><span class="sxs-lookup"><span data-stu-id="26d8f-142">Build hello **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="26d8f-143">Wierszu polecenia przejdź toohello `add-tags-query` folder i hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="26d8f-143">At your command prompt, navigate toohello `add-tags-query` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="26d8f-144">Tworzenie aplikacji urządzenia</span><span class="sxs-lookup"><span data-stu-id="26d8f-144">Create a device app</span></span>

<span data-ttu-id="26d8f-145">W tej sekcji utworzysz aplikację konsoli języka Java, która ustawia wartości właściwości zgłoszone wysyłany tooIoT Centrum.</span><span class="sxs-lookup"><span data-stu-id="26d8f-145">In this section, you create a Java console app that sets a reported property value that is sent tooIoT Hub.</span></span>

1. <span data-ttu-id="26d8f-146">W hello `iot-java-twin-getstarted` folderu, Utwórz projekt Maven o nazwie **symulowane urządzenie** przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="26d8f-146">In hello `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="26d8f-147">Zwróć uwagę, że jest to jedno długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="26d8f-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="26d8f-148">Wierszu polecenia przejdź toohello `simulated-device` folderu.</span><span class="sxs-lookup"><span data-stu-id="26d8f-148">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="26d8f-149">Za pomocą edytora tekstu, otwórz hello `pom.xml` pliku w hello `simulated-device` folderu i dodaj następujące zależności toohello hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="26d8f-149">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="26d8f-150">Ta zależność umożliwia toouse hello **klienta w przypadku urządzenia iot** pakiet w Twojej toocommunicate aplikacji z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="26d8f-150">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="26d8f-151">Możesz sprawdzić hello najnowszą wersję **klienta w przypadku urządzenia iot** przy użyciu [wyszukiwania Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="26d8f-151">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="26d8f-152">Dodaj następujące hello **kompilacji** węzła po hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="26d8f-152">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="26d8f-153">Ta konfiguracja powoduje, że Maven toouse Java 1,8 toobuild hello aplikacji:</span><span class="sxs-lookup"><span data-stu-id="26d8f-153">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="26d8f-154">Zapisz i zamknij hello `pom.xml` pliku.</span><span class="sxs-lookup"><span data-stu-id="26d8f-154">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="26d8f-155">Za pomocą edytora tekstu, otwórz hello `simulated-device\src\main\java\com\mycompany\app\App.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="26d8f-155">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="26d8f-156">Dodaj następujące hello **zaimportować** instrukcje toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="26d8f-156">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="26d8f-157">Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="26d8f-157">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="26d8f-158">Zastępowanie `{youriothubname}` z nazwę Centrum IoT i `{yourdevicekey}` o wartości klucza urządzenia hello wygenerowanych w hello *tworzenie tożsamości urządzenia* sekcji:</span><span class="sxs-lookup"><span data-stu-id="26d8f-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="26d8f-159">Ta przykładowa aplikacja używa hello **protokołu** zmiennej podczas tworzenia wystąpień **DeviceClient** obiektu.</span><span class="sxs-lookup"><span data-stu-id="26d8f-159">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="26d8f-160">Obecnie toouse dwie funkcji urządzenia muszą używać protokołu MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="26d8f-160">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="26d8f-161">Dodaj hello następującego kodu toohello **głównego** metodę:</span><span class="sxs-lookup"><span data-stu-id="26d8f-161">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="26d8f-162">Utwórz toocommunicate klienta urządzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="26d8f-162">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="26d8f-163">Utwórz **urządzenia** toostore hello urządzenia dwie właściwości obiektu.</span><span class="sxs-lookup"><span data-stu-id="26d8f-163">Create a **Device** object toostore hello device twin properties.</span></span>

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object toostore hello device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed too" + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="26d8f-164">Dodaj hello następującego kodu toohello **głównego** toocreate — metoda **connectivityType** zgłosił właściwości, a następnie wysłać je tooIoT Centrum:</span><span class="sxs-lookup"><span data-stu-id="26d8f-164">Add hello following code toohello **main** method toocreate a **connectivityType** reported property and send it tooIoT Hub:</span></span>

    ```java
    try {
      // Open hello DeviceClient and start hello device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it tooyour IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="26d8f-165">Dodaj kod zakończenia toohello hello hello **głównego** metody.</span><span class="sxs-lookup"><span data-stu-id="26d8f-165">Add hello following code toohello end of hello **main** method.</span></span> <span data-ttu-id="26d8f-166">Oczekiwanie na powitania **Enter** klucz umożliwia czas stanu hello tooreport Centrum IoT hello urządzenia dwie czynności:</span><span class="sxs-lookup"><span data-stu-id="26d8f-166">Waiting for hello **Enter** key allows time for IoT Hub tooreport hello status of hello device twin operations:</span></span>

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="26d8f-167">Zapisz i zamknij hello `simulated-device\src\main\java\com\mycompany\app\App.java` pliku.</span><span class="sxs-lookup"><span data-stu-id="26d8f-167">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="26d8f-168">Tworzenie hello **symulowane urządzenie** aplikacji i poprawić błędy.</span><span class="sxs-lookup"><span data-stu-id="26d8f-168">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="26d8f-169">Wierszu polecenia przejdź toohello `simulated-device` folder i hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="26d8f-169">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="26d8f-170">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="26d8f-170">Run hello apps</span></span>

<span data-ttu-id="26d8f-171">Wszystko jest teraz gotowy toorun hello konsoli aplikacji.</span><span class="sxs-lookup"><span data-stu-id="26d8f-171">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="26d8f-172">W wierszu polecenia w hello `add-tags-query` folderu, uruchom następujące polecenie toorun hello hello **Dodaj tag query** usługi aplikacji:</span><span class="sxs-lookup"><span data-stu-id="26d8f-172">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java usługi aplikacji tooupdate wartości tagów i uruchamianie zapytań urządzenia](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="26d8f-174">Zostanie wyświetlony hello **roślin** i **region** tagi dodane dwie urządzenia toohello.</span><span class="sxs-lookup"><span data-stu-id="26d8f-174">You can see hello **plant** and **region** tags added toohello device twin.</span></span> <span data-ttu-id="26d8f-175">Hello pierwsza kwerenda zwraca urządzenia, ale hello drugi nie.</span><span class="sxs-lookup"><span data-stu-id="26d8f-175">hello first query returns your device, but hello second does not.</span></span>

1. <span data-ttu-id="26d8f-176">W wierszu polecenia w hello `simulated-device` folderu, uruchom następujące polecenie tooadd hello hello **connectivityType** zgłosił dwie urządzenia toohello właściwości:</span><span class="sxs-lookup"><span data-stu-id="26d8f-176">At a command prompt in hello `simulated-device` folder, run hello following command tooadd hello **connectivityType** reported property toohello device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![powitania klienta urządzenia dodaje hello ** connectivityType ** zgłosił właściwości](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="26d8f-178">W wierszu polecenia w hello `add-tags-query` folderu, uruchom następujące polecenie toorun hello hello **Dodaj tag query** usługi aplikacji po raz drugi:</span><span class="sxs-lookup"><span data-stu-id="26d8f-178">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centrum IoT Java usługi aplikacji tooupdate wartości tagów i uruchamianie zapytań urządzenia](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="26d8f-180">Teraz urządzenia wysłał hello **connectivityType** tooIoT właściwości koncentratora, hello drugiego zapytania zwraca urządzenie.</span><span class="sxs-lookup"><span data-stu-id="26d8f-180">Now your device has sent hello **connectivityType** property tooIoT Hub, hello second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26d8f-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="26d8f-181">Next steps</span></span>

<span data-ttu-id="26d8f-182">W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia.</span><span class="sxs-lookup"><span data-stu-id="26d8f-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="26d8f-183">Dodaje metadane urządzenia jako tagi z aplikacji zaplecza i zapisane urządzenia tooreport urządzenia łączności informacji o aplikacji w Witaj dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="26d8f-183">You added device metadata as tags from a back-end app, and wrote a device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="26d8f-184">Również wiesz, jak tooquery hello przy użyciu języka zapytań Centrum IoT przypominającego SQL hello dwie informacje o urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="26d8f-184">You also learned how tooquery hello device twin information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="26d8f-185">Hello Użyj następujących zasobów toolearn jak do:</span><span class="sxs-lookup"><span data-stu-id="26d8f-185">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="26d8f-186">Wysłać dane telemetryczne z urządzenia z hello [Rozpoczynanie pracy z Centrum IoT](iot-hub-java-java-getstarted.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="26d8f-186">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="26d8f-187">Kontrolowanie urządzenia interakcyjne (takich jak włączanie wentylator z aplikacji kontrolowane przez użytkownika) z hello [metody bezpośredniego](iot-hub-java-java-direct-methods.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="26d8f-187">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
