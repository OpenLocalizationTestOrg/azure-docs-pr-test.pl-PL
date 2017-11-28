---
title: "aaaGet pracę z Centrum IoT Azure (Java) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak urządzenia chmury toosend wiadomości tooAzure Centrum IoT przy użyciu IoT zestawy SDK dla języka Java. Utworzyć symulowane urządzenie i tooregister aplikacji usługi, urządzenia, wysyłania wiadomości i odczytywać wiadomości z Centrum IoT."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a><span data-ttu-id="dbeba-104">Połącz przy użyciu języka Java Centrum IoT tooyour urządzenia</span><span class="sxs-lookup"><span data-stu-id="dbeba-104">Connect your device tooyour IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="dbeba-105">Na końcu hello tego samouczka masz trzech aplikacji Java w konsoli:</span><span class="sxs-lookup"><span data-stu-id="dbeba-105">At hello end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="dbeba-106">**Utwórz urządzenie tożsamości**, co powoduje tożsamości urządzenia i skojarzony klucz tooconnect aplikacją urządzenia.</span><span class="sxs-lookup"><span data-stu-id="dbeba-106">**create-device-identity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="dbeba-107">**Odczyt — d2c — liczba komunikatów**, który zawiera dane telemetryczne hello wysyłane przez aplikację na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="dbeba-107">**read-d2c-messages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="dbeba-108">**Symulowane urządzenie**, która łączy się tooyour Centrum IoT z tożsamości urządzenia hello utworzony wcześniej i wysyła komunikat telemetrii co drugi przy użyciu hello MQTT protokołu.</span><span class="sxs-lookup"><span data-stu-id="dbeba-108">**simulated-device**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="dbeba-109">Artykuł Hello [Azure IoT SDK] [ lnk-hub-sdks] zawiera informacje o hello Azure IoT SDK, której można toobuild toorun zarówno aplikacje na urządzeniach i z zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="dbeba-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both apps toorun on devices and your solution back end.</span></span>

<span data-ttu-id="dbeba-110">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="dbeba-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="dbeba-111">Witaj najnowszych [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="dbeba-111">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="dbeba-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="dbeba-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="dbeba-113">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dbeba-113">An active Azure account.</span></span> <span data-ttu-id="dbeba-114">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="dbeba-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="dbeba-115">Jako ostatni krok, zanotuj hello **klucz podstawowy** wartość.</span><span class="sxs-lookup"><span data-stu-id="dbeba-115">As a final step, make a note of hello **Primary key** value.</span></span> <span data-ttu-id="dbeba-116">Następnie kliknij przycisk **punkty końcowe** i hello **zdarzenia** wbudowanym punktem końcowym.</span><span class="sxs-lookup"><span data-stu-id="dbeba-116">Then click **Endpoints** and hello **Events** built-in endpoint.</span></span> <span data-ttu-id="dbeba-117">Na powitania **właściwości** bloku, zanotuj hello **nazwę Centrum zdarzeń zgodnych** i hello **punktu końcowego Centrum zdarzeń zgodnych** adres.</span><span class="sxs-lookup"><span data-stu-id="dbeba-117">On hello **Properties** blade, make a note of hello **Event Hub-compatible name** and hello **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="dbeba-118">Te trzy wartości będą potrzebne podczas tworzenia aplikacji **read-d2c-messages**.</span><span class="sxs-lookup"><span data-stu-id="dbeba-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Blok komunikatów usługi IoT Hub witrynie Azure Portal][6]

<span data-ttu-id="dbeba-120">Utworzono centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="dbeba-120">You have now created your IoT hub.</span></span> <span data-ttu-id="dbeba-121">Masz hello nazwy hosta Centrum IoT, parametry połączenia Centrum IoT, klucz podstawowy Centrum IoT, nazwa zgodnego Centrum zdarzeń i punktu końcowego zgodnego Centrum zdarzeń należy toocomplete w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="dbeba-121">You have hello IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need toocomplete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="dbeba-122">Tworzenie tożsamości urządzenia</span><span class="sxs-lookup"><span data-stu-id="dbeba-122">Create a device identity</span></span>
<span data-ttu-id="dbeba-123">W tej sekcji utworzysz aplikację konsoli języka Java, która tworzy tożsamość urządzenia w rejestrze tożsamości hello w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="dbeba-123">In this section, you create a Java console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="dbeba-124">Urządzenie nie może połączyć tooIoT koncentratora, chyba że jego wpis w rejestrze tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="dbeba-124">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="dbeba-125">Aby uzyskać więcej informacji, zobacz hello **rejestru tożsamości** sekcji hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="dbeba-125">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="dbeba-126">Po uruchomieniu tej aplikacji konsoli, generuje on unikatowy identyfikator urządzenia i tooIoT Centrum wiadomości klucz urządzenia można użyć tooidentify się podczas wysyłania urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="dbeba-126">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="dbeba-127">Utwórz pusty folder o nazwie iot-java-get-started.</span><span class="sxs-lookup"><span data-stu-id="dbeba-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="dbeba-128">W folderze iot-java-get-started hello Utwórz projekt Maven o nazwie **utworzyć urządzenie identity** przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="dbeba-128">In hello iot-java-get-started folder, create a Maven project called **create-device-identity** using hello following command at your command prompt.</span></span> <span data-ttu-id="dbeba-129">Zwróć uwagę, że jest to jedno długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="dbeba-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="dbeba-130">Wierszu polecenia przejdź toohello folderu utworzyć--tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="dbeba-130">At your command prompt, navigate toohello create-device-identity folder.</span></span>

3. <span data-ttu-id="dbeba-131">Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze utwórz urządzenie tożsamości hello i dodaj następujące zależności toohello hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="dbeba-131">Using a text editor, open hello pom.xml file in hello create-device-identity folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="dbeba-132">Ta zależność umożliwia możesz toouse powitania klienta w przypadku usługi iot pakietu w aplikacji:</span><span class="sxs-lookup"><span data-stu-id="dbeba-132">This dependency enables you toouse hello iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="dbeba-133">Możesz sprawdzić hello najnowszą wersję **klienta w przypadku usługi iot** przy użyciu [wyszukiwania Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="dbeba-133">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="dbeba-134">Zapisz i zamknij plik pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="dbeba-134">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="dbeba-135">Za pomocą edytora tekstu, otwórz plik create-device-identity\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="dbeba-135">Using a text editor, open hello create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="dbeba-136">Dodaj następujące hello **zaimportować** instrukcje toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="dbeba-136">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="dbeba-137">Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy, zastępując **{yourhubconnectionstring}** z hello wartość Twojej dostrzeżone wcześniej:</span><span class="sxs-lookup"><span data-stu-id="dbeba-137">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** with hello value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="dbeba-138">Modyfikowanie hello podpis hello **głównego** tooinclude metody hello wyjątków w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="dbeba-138">Modify hello signature of hello **main** method tooinclude hello exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="dbeba-139">Dodaj następującego kodu jako treść hello hello hello **głównego** metody.</span><span class="sxs-lookup"><span data-stu-id="dbeba-139">Add hello following code as hello body of hello **main** method.</span></span> <span data-ttu-id="dbeba-140">Ten kod tworzy urządzenie o nazwie *javadevice* w rejestrze tożsamości usługi IoT Hub, o ile takie już nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="dbeba-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="dbeba-141">Następnie wyświetla hello urządzenia identyfikator i klucz, które są potrzebne później:</span><span class="sxs-lookup"><span data-stu-id="dbeba-141">It then displays hello device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. <span data-ttu-id="dbeba-142">Zapisz i zamknij plik App.java hello.</span><span class="sxs-lookup"><span data-stu-id="dbeba-142">Save and close hello App.java file.</span></span>

11. <span data-ttu-id="dbeba-143">Witaj toobuild **utworzyć--tożsamości urządzenia** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello w folderze utwórz urządzenie tożsamości hello hello:</span><span class="sxs-lookup"><span data-stu-id="dbeba-143">toobuild hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="dbeba-144">Witaj toorun **utworzyć--tożsamości urządzenia** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello w folderze utwórz urządzenie tożsamości hello hello:</span><span class="sxs-lookup"><span data-stu-id="dbeba-144">toorun hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="dbeba-145">Zanotuj hello **identyfikator urządzenia** i **klucza urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="dbeba-145">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="dbeba-146">Należy te wartości później podczas tworzenia aplikacji, która łączy tooIoT koncentratora jako urządzenie.</span><span class="sxs-lookup"><span data-stu-id="dbeba-146">You need these values later when you create an app that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="dbeba-147">Witaj w rejestrze tożsamości Centrum IoT przechowuje dane tylko Centrum IoT toohello bezpiecznego dostępu tooenable tożsamości urządzenia.</span><span class="sxs-lookup"><span data-stu-id="dbeba-147">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="dbeba-148">Urządzenie toouse identyfikatorów i klucze są przechowywane jako poświadczeń zabezpieczeń i flagi włączone/wyłączone, której można toodisable dostępu dla poszczególnych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="dbeba-148">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="dbeba-149">Jeśli Twoja aplikacja powinna toostore inne metadane specyficzne dla urządzenia, należy go użyć magazynu specyficzny dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbeba-149">If your app needs toostore other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="dbeba-150">Aby uzyskać więcej informacji, zobacz hello [Centrum IoT — przewodnik dewelopera][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="dbeba-150">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="dbeba-151">Odbieranie komunikatów z urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="dbeba-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="dbeba-152">W tej sekcji opisano tworzenie aplikacji konsolowej Java, która odczytuje komunikaty z urządzenia do chmury z usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="dbeba-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="dbeba-153">Przedstawia Centrum IoT [Centrum zdarzeń][lnk-event-hubs-overview]-tooenable zgodne punktu końcowego można tooread wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="dbeba-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="dbeba-154">elementy tookeep proste, w tym samouczku tworzy podstawowe reader, który nie jest odpowiedni dla wdrożenia wysokiej przepływności.</span><span class="sxs-lookup"><span data-stu-id="dbeba-154">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="dbeba-155">Witaj [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczek pokazuje, jak urządzenia chmury tooprocess komunikatów na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="dbeba-155">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="dbeba-156">Witaj [Rozpoczynanie pracy z usługą Event Hubs] [ lnk-eventhubs-tutorial] samouczek zawiera dalsze informacje dotyczące sposobu tooprocess komunikaty z usługi Event Hubs i jest toohello odpowiednich punktów końcowych zgodnych z Centrum IoT Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="dbeba-156">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="dbeba-157">Hello punktu końcowego Centrum zdarzeń zgodnych do odczytywania wiadomości urządzenia do chmury zawsze używa protokołu AMQP hello.</span><span class="sxs-lookup"><span data-stu-id="dbeba-157">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="dbeba-158">W folderze iot-java-get-started hello utworzonego w hello *tworzenie tożsamości urządzenia* sekcji, Utwórz projekt Maven o nazwie **odczytu — d2c — liczba komunikatów** przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="dbeba-158">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **read-d2c-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="dbeba-159">Zwróć uwagę, że jest to jedno długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="dbeba-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="dbeba-160">Wierszu polecenia przejdź toohello odczytu — d2c — liczba komunikatów folderu.</span><span class="sxs-lookup"><span data-stu-id="dbeba-160">At your command prompt, navigate toohello read-d2c-messages folder.</span></span>

3. <span data-ttu-id="dbeba-161">Za pomocą edytora tekstu, otwórz plik pom.xml hello na odczyt d2c-wiadomości powitania w folderze i dodaj następujące zależności toohello hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="dbeba-161">Using a text editor, open hello pom.xml file in hello read-d2c-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="dbeba-162">Ta zależność umożliwia toouse powitania klienta eventhubs pakietu w Twojej aplikacji tooread z punktu końcowego Centrum zdarzeń zgodnych hello:</span><span class="sxs-lookup"><span data-stu-id="dbeba-162">This dependency enables you toouse hello eventhubs-client package in your app tooread from hello Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="dbeba-163">Zapisz i zamknij plik pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="dbeba-163">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="dbeba-164">Za pomocą edytora tekstu, otwórz plik read-d2c-messages\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="dbeba-164">Using a text editor, open hello read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="dbeba-165">Dodaj następujące hello **zaimportować** instrukcje toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="dbeba-165">Add hello following **import** statements toohello file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="dbeba-166">Dodaj powitania po toohello zmiennej poziomie klasy **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="dbeba-166">Add hello following class-level variable toohello **App** class.</span></span> <span data-ttu-id="dbeba-167">Zastąp **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, i **{youreventhubcompatiblename}** wartościami hello zanotowany wcześniej:</span><span class="sxs-lookup"><span data-stu-id="dbeba-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with hello values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="dbeba-168">Dodaj następujące hello **receiveMessages** toohello metody **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="dbeba-168">Add hello following **receiveMessages** method toohello **App** class.</span></span> <span data-ttu-id="dbeba-169">Ta metoda tworzy **EventHubClient** wystąpienia tooconnect toohello zgodnego Centrum zdarzeń z punktu końcowego, a następnie asynchronicznie tworzy **PartitionReceiver** tooread wystąpienia z Centrum zdarzeń partycja.</span><span class="sxs-lookup"><span data-stu-id="dbeba-169">This method creates an **EventHubClient** instance tooconnect toohello Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance tooread from an Event Hub partition.</span></span> <span data-ttu-id="dbeba-170">Wykonuje pętlę w sposób ciągły, a drukuje wiadomość hello — szczegóły, aż do zakończenia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="dbeba-170">It loops continuously and prints hello message details until hello app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="dbeba-171">Ta metoda używa filtru podczas tworzenia odbiornika hello tak, aby hello odbiornika odczytuje jedynie tooIoT wiadomości wysłane koncentratora po odbiornika hello zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="dbeba-171">This method uses a filter when it creates hello receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="dbeba-172">Ta technika jest przydatne w środowisku testowym, dzięki czemu bieżącego zestawu wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="dbeba-172">This technique is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="dbeba-173">W środowisku produkcyjnym kod powinien upewnij się, że przetwarza wszystkie wiadomości powitania — Aby uzyskać więcej informacji, zobacz hello [jak tooprocess Centrum IoT urządzenia do chmury wiadomości] [ lnk-process-d2c-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="dbeba-173">In a production environment, your code should make sure that it processes all hello messages - for more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="dbeba-174">Modyfikowanie hello podpis hello **głównego** tooinclude metody hello wyjątek w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="dbeba-174">Modify hello signature of hello **main** method tooinclude hello exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="dbeba-175">Dodaj hello następującego kodu toohello **głównego** metoda hello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="dbeba-175">Add hello following code toohello **main** method in hello **App** class.</span></span> <span data-ttu-id="dbeba-176">Ten kod tworzy dwa hello **EventHubClient** i **PartitionReceiver** wystąpień i umożliwia aplikacji hello tooclose po zakończeniu przetwarzania komunikatów:</span><span class="sxs-lookup"><span data-stu-id="dbeba-176">This code creates hello two **EventHubClient** and **PartitionReceiver** instances and enables you tooclose hello app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="dbeba-177">Ten kod przyjęto założenie, że utworzono Centrum IoT w warstwie (bezpłatnie) hello F1.</span><span class="sxs-lookup"><span data-stu-id="dbeba-177">This code assumes you created your IoT hub in hello F1 (free) tier.</span></span> <span data-ttu-id="dbeba-178">Bezpłatne centrum IoT ma dwie partycje o nazwie „0” i „1”.</span><span class="sxs-lookup"><span data-stu-id="dbeba-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="dbeba-179">Zapisz i zamknij plik App.java hello.</span><span class="sxs-lookup"><span data-stu-id="dbeba-179">Save and close hello App.java file.</span></span>

12. <span data-ttu-id="dbeba-180">Witaj toobuild **odczytu — d2c — liczba komunikatów** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello na odczyt d2c-wiadomości powitania w folderze hello:</span><span class="sxs-lookup"><span data-stu-id="dbeba-180">toobuild hello **read-d2c-messages** app using Maven, execute hello following command at hello command prompt in hello read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="dbeba-181">Tworzenie aplikacji urządzenia</span><span class="sxs-lookup"><span data-stu-id="dbeba-181">Create a device app</span></span>
<span data-ttu-id="dbeba-182">W tej sekcji utworzysz aplikację konsoli języka Java, która symuluje urządzenia, które wysyła Centrum IoT tooan wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="dbeba-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="dbeba-183">W folderze iot-java-get-started hello utworzonego w hello *tworzenie tożsamości urządzenia* sekcji, Utwórz projekt Maven o nazwie **symulowane urządzenie** przy użyciu hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="dbeba-183">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="dbeba-184">Zwróć uwagę, że jest to jedno długie polecenie:</span><span class="sxs-lookup"><span data-stu-id="dbeba-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="dbeba-185">Wierszu polecenia przejdź toohello symulowane urządzenie folderu.</span><span class="sxs-lookup"><span data-stu-id="dbeba-185">At your command prompt, navigate toohello simulated-device folder.</span></span>

3. <span data-ttu-id="dbeba-186">Za pomocą edytora tekstu, otwórz plik pom.xml hello w folderze symulowane urządzenie hello i dodaj następujące zależności toohello hello **zależności** węzła.</span><span class="sxs-lookup"><span data-stu-id="dbeba-186">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="dbeba-187">Ta zależność umożliwia możesz toouse hello Centrum iothub-java-pakietu klienta w Twojej toocommunicate aplikacji z Centrum IoT i tooserialize tooJSON obiektów języka Java:</span><span class="sxs-lookup"><span data-stu-id="dbeba-187">This dependency enables you toouse hello iothub-java-client package in your app toocommunicate with your IoT hub and tooserialize Java objects tooJSON:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="dbeba-188">Możesz sprawdzić hello najnowszą wersję **klienta w przypadku urządzenia iot** przy użyciu [wyszukiwania Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="dbeba-188">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="dbeba-189">Zapisz i zamknij plik pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="dbeba-189">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="dbeba-190">Za pomocą edytora tekstu, otwórz plik simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="dbeba-190">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="dbeba-191">Dodaj następujące hello **zaimportować** instrukcje toohello pliku:</span><span class="sxs-lookup"><span data-stu-id="dbeba-191">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="dbeba-192">Dodaj następujące zmienne klasy toohello hello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="dbeba-192">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="dbeba-193">Zastępowanie **{youriothubname}** z nazwę Centrum IoT i **{yourdevicekey}** o wartości klucza urządzenia hello wygenerowanych w hello *tworzenie tożsamości urządzenia* sekcji:</span><span class="sxs-lookup"><span data-stu-id="dbeba-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="dbeba-194">Ta przykładowa aplikacja używa hello **protokołu** zmiennej podczas tworzenia wystąpień **DeviceClient** obiektu.</span><span class="sxs-lookup"><span data-stu-id="dbeba-194">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="dbeba-195">Można użyć albo toocommunicate protokołu hello, jak MQTT AMQP i HTTP z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="dbeba-195">You can use either hello MQTT, AMQP, or HTTP protocol toocommunicate with IoT Hub.</span></span>

8. <span data-ttu-id="dbeba-196">Dodaj następujące hello zagnieżdżone **TelemetryDataPoint** klasy wewnątrz hello **aplikacji** klasy danych telemetrycznych hello toospecify urządzenie wysyła tooyour Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="dbeba-196">Add hello following nested **TelemetryDataPoint** class inside hello **App** class toospecify hello telemetry data your device sends tooyour IoT hub:</span></span>

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. <span data-ttu-id="dbeba-197">Dodaj następujące hello zagnieżdżone **EventCallback** klasy wewnątrz hello **aplikacji** klasy toodisplay hello potwierdzenia stan hello Centrum IoT zwraca podczas przetwarzania wiadomości powitania urządzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbeba-197">Add hello following nested **EventCallback** class inside hello **App** class toodisplay hello acknowledgement status that hello IoT hub returns when it processes a message from hello device app.</span></span> <span data-ttu-id="dbeba-198">Ta metoda również powiadamia hello wątku głównego w aplikacji hello po przetworzeniu wiadomość hello:</span><span class="sxs-lookup"><span data-stu-id="dbeba-198">This method also notifies hello main thread in hello app when hello message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="dbeba-199">Dodaj następujące hello zagnieżdżone **MessageSender** klasy wewnątrz hello **aplikacji** klasy.</span><span class="sxs-lookup"><span data-stu-id="dbeba-199">Add hello following nested **MessageSender** class inside hello **App** class.</span></span> <span data-ttu-id="dbeba-200">Witaj **Uruchom** metoda w klasie generuje Centrum IoT tooyour toosend danych przykładowych danych telemetrycznych i czeka na potwierdzenie przed wysłaniem hello następny komunikat:</span><span class="sxs-lookup"><span data-stu-id="dbeba-200">hello **run** method in this class generates sample telemetry data toosend tooyour IoT hub and waits for an acknowledgement before sending hello next message:</span></span>

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
            System.out.println("Sending: " + msgStr);
    
            Object lockobj = new Object();
            EventCallback callback = new EventCallback();
            client.sendEventAsync(msg, callback, lockobj);
    
            synchronized (lockobj) {
              lockobj.wait();
            }
            Thread.sleep(1000);
          }
        } catch (InterruptedException e) {
          System.out.println("Finished.");
        }
      }
    }
    ```

    <span data-ttu-id="dbeba-201">Ta metoda wysyła nowy komunikat urządzenia do chmury jednej sekundy po poprzedniej wiadomości powitania potwierdzeniu hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="dbeba-201">This method sends a new device-to-cloud message one second after hello IoT hub acknowledges hello previous message.</span></span> <span data-ttu-id="dbeba-202">wiadomości powitania zawiera obiekt serializacji JSON z hello deviceId i losowo wygenerowane numery toosimulate czujnik temperatury i wilgotności czujnika.</span><span class="sxs-lookup"><span data-stu-id="dbeba-202">hello message contains a JSON-serialized object with hello deviceId and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="dbeba-203">Zastąp hello **głównego** metody za pomocą następującego kodu, która tworzy Centrum IoT wątku toosend wiadomości urządzenia do chmury tooyour hello:</span><span class="sxs-lookup"><span data-stu-id="dbeba-203">Replace hello **main** method with hello following code that creates a thread toosend device-to-cloud messages tooyour IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="dbeba-204">Zapisz i zamknij plik App.java hello.</span><span class="sxs-lookup"><span data-stu-id="dbeba-204">Save and close hello App.java file.</span></span>

13. <span data-ttu-id="dbeba-205">Witaj toobuild **symulowane urządzenie** aplikacji za pomocą programu Maven, wykonaj następujące polecenie w wierszu polecenia hello w folderze symulowane urządzenie hello hello:</span><span class="sxs-lookup"><span data-stu-id="dbeba-205">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="dbeba-206">rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="dbeba-206">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="dbeba-207">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="dbeba-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="dbeba-208">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="dbeba-208">Run hello apps</span></span>

<span data-ttu-id="dbeba-209">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dbeba-209">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="dbeba-210">W wierszu polecenia w folderze d2c odczytu hello uruchom następujące polecenie toobegin monitorowania hello pierwszej partycji w Centrum IoT hello:</span><span class="sxs-lookup"><span data-stu-id="dbeba-210">At a command prompt in hello read-d2c folder, run hello following command toobegin monitoring hello first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Centrum IoT Java usługi aplikacji toomonitor urządzenia do chmury wiadomości][7]

2. <span data-ttu-id="dbeba-212">W wierszu polecenia w folderze symulowane urządzenie hello Uruchom powitania po toobegin polecenie wysyłania Centrum IoT tooyour danych telemetrii:</span><span class="sxs-lookup"><span data-stu-id="dbeba-212">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Centrum IoT Java urządzenia aplikacji toosend urządzenia do chmury wiadomości][8]

3. <span data-ttu-id="dbeba-214">Witaj **użycia** kafelka w hello [portalu Azure] [ lnk-portal] pokazuje hello liczbę komunikatów wysłanych toohello Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="dbeba-214">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Azure portalu użycie kafelka pokazujący liczbę komunikatów wysyłanych tooIoT Centrum][43]

## <a name="next-steps"></a><span data-ttu-id="dbeba-216">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dbeba-216">Next steps</span></span>
<span data-ttu-id="dbeba-217">W tym samouczku został skonfigurowany nowego centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia.</span><span class="sxs-lookup"><span data-stu-id="dbeba-217">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="dbeba-218">Użyto tego urządzenia tożsamości tooenable hello urządzenia aplikacji toosend wiadomości urządzenia do chmury toohello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="dbeba-218">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="dbeba-219">Utworzono aplikację, która wyświetla hello komunikatów odebranych przez Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="dbeba-219">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="dbeba-220">toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="dbeba-220">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="dbeba-221">[Łączenie urządzenia][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="dbeba-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="dbeba-222">[Wprowadzenie do zarządzania urządzeniami][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="dbeba-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="dbeba-223">[Getting started with Azure IoT Edge][lnk-iot-edge] (Rozpoczynanie pracy z usługą Azure IoT Edge)</span><span class="sxs-lookup"><span data-stu-id="dbeba-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="dbeba-224">toolearn tooextend IoT rozwiązanie i procesu urządzenia do chmury wiadomości na dużą skalę, zobacz temat hello [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="dbeba-224">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
