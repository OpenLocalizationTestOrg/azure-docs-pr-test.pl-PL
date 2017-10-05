---
title: "Urządzenia Azure IoT SDK dla języka C | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z urządzeń Azure IoT SDK dla języka C i Dowiedz się, jak tworzyć aplikacje urządzenia, które komunikują się z Centrum IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 459b630f28fe48064f4ba280974f3fdbdb82f0a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="a4754-103">Azure urządzenia IoT zestawu SDK dla języka C</span><span class="sxs-lookup"><span data-stu-id="a4754-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="a4754-104">**Urządzenia Azure IoT SDK** to zestaw bibliotek zaprojektowane w celu uproszczenia procesu wysyłania wiadomości i odbieranie komunikatów z **Centrum IoT Azure** usługi.</span><span class="sxs-lookup"><span data-stu-id="a4754-104">The **Azure IoT device SDK** is a set of libraries designed to simplify the process of sending messages to and receiving messages from the **Azure IoT Hub** service.</span></span> <span data-ttu-id="a4754-105">Istnieją różne odmiany zestawu SDK, każdy przeznaczonych dla określonej platformy, ale w tym artykule opisano **urządzenia Azure IoT SDK dla języka C**.</span><span class="sxs-lookup"><span data-stu-id="a4754-105">There are different variations of the SDK, each targeting a specific platform, but this article describes the **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="a4754-106">Urządzenia Azure IoT SDK dla języka C są zapisywane w ANSI C (C99), aby zmaksymalizować przenoszenia.</span><span class="sxs-lookup"><span data-stu-id="a4754-106">The Azure IoT device SDK for C is written in ANSI C (C99) to maximize portability.</span></span> <span data-ttu-id="a4754-107">Ta funkcja udostępnia biblioteki dobrze nadaje się do działania na wielu platformach i urządzeniach, szczególnie w przypadku, gdy minimalizując dysku i zużycie pamięci jest priorytetem.</span><span class="sxs-lookup"><span data-stu-id="a4754-107">This feature makes the libraries well-suited to operate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="a4754-108">Istnieje szeroka gama platformy, na których zostały przetestowane zestawu SDK (zobacz [Azure certyfikowane dla katalogu urządzenia IoT](https://catalog.azureiotsuite.com/) szczegółowe informacje).</span><span class="sxs-lookup"><span data-stu-id="a4754-108">There are a broad range of platforms on which the SDK has been tested (see the [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="a4754-109">Chociaż ten artykuł zawiera wskazówki przykładowy kod działających na platformie systemu Windows, kod opisane w tym artykule jest identyczna w zakresie obsługiwanych platform.</span><span class="sxs-lookup"><span data-stu-id="a4754-109">Although this article includes walkthroughs of sample code running on the Windows platform, the code described in this article is identical across the range of supported platforms.</span></span>

<span data-ttu-id="a4754-110">Ten artykuł stanowi wprowadzenie do architektury urządzenia Azure IoT SDK dla C. Go pokazano, jak zainicjować biblioteki urządzenia, wysyłania danych do Centrum IoT i otrzymywać wiadomości.</span><span class="sxs-lookup"><span data-stu-id="a4754-110">This article introduces you to the architecture of the Azure IoT device SDK for C. It demonstrates how to initialize the device library, send data to IoT Hub, and receive messages from it.</span></span> <span data-ttu-id="a4754-111">Informacje przedstawione w tym artykule powinny być wystarczające, aby rozpocząć korzystanie z zestawu SDK, ale również zawiera łącza do dodatkowych informacji o bibliotekach.</span><span class="sxs-lookup"><span data-stu-id="a4754-111">The information in this article should be enough to get started using the SDK, but also provides pointers to additional information about the libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="a4754-112">Architektura zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="a4754-112">SDK architecture</span></span>

<span data-ttu-id="a4754-113">Można znaleźć [ **urządzenia Azure IoT SDK dla języka C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repozytorium i wyświetlenia jej szczegółów interfejsu API w [dokumentacja interfejsu API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="a4754-113">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="a4754-114">Najnowszą wersję biblioteki można znaleźć w **wzorca** gałęzi repozytorium:</span><span class="sxs-lookup"><span data-stu-id="a4754-114">The latest version of the libraries can be found in the **master** branch of the repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="a4754-115">Implementacja core zestawu SDK znajduje się w **Centrum iothub\_klienta** folderu, który zawiera implementację najniższy poziom interfejsu API zestawu SDK: **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="a4754-115">The core implementation of the SDK is in the **iothub\_client** folder that contains the implementation of the lowest API layer in the SDK: the **IoTHubClient** library.</span></span> <span data-ttu-id="a4754-116">**IoTHubClient** biblioteka zawiera interfejsy API Implementowanie raw wiadomości wysyłanie komunikatów do Centrum IoT i odbierania wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4754-116">The **IoTHubClient** library contains APIs implementing raw messaging for sending messages to IoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="a4754-117">Korzystając z tej biblioteki, jest odpowiedzialny za wdrażanie serializacji komunikatu, ale inne szczegóły komunikowania się z Centrum IoT są obsługiwane dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="a4754-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="a4754-118">**Serializator** folder zawiera funkcje pomocnicze i przykłady, których pokazano, jak do serializowania danych przed wysłaniem do Centrum IoT Azure za pomocą biblioteki klienta.</span><span class="sxs-lookup"><span data-stu-id="a4754-118">The **serializer** folder contains helper functions and samples that show you how to serialize data before sending to Azure IoT Hub using the client library.</span></span> <span data-ttu-id="a4754-119">Użycie Serializator nie jest obowiązkowe i jest dostępne dla wygody.</span><span class="sxs-lookup"><span data-stu-id="a4754-119">The use of the serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="a4754-120">Aby użyć **serializator** biblioteki, należy zdefiniować modelu, który określa dane do wysłania do Centrum IoT i komunikaty, oczekuje się od niego.</span><span class="sxs-lookup"><span data-stu-id="a4754-120">To use the **serializer** library, you define a model that specifies the data to send to IoT Hub and the messages you expect to receive from it.</span></span> <span data-ttu-id="a4754-121">Po zdefiniowaniu modelu zestaw SDK udostępnia powierzchni interfejsu API, który umożliwia łatwe pracę z urządzenia do chmury i chmury do urządzenia wiadomości bez obaw o szczegóły serializacji.</span><span class="sxs-lookup"><span data-stu-id="a4754-121">Once the model is defined, the SDK provides you with an API surface that enables you to easily work with device-to-cloud and cloud-to-device messages without worrying about the serialization details.</span></span> <span data-ttu-id="a4754-122">Biblioteka jest zależny od innych bibliotek typu open source, które implementują transportu przy użyciu protokołów, takich jak MQTT i protokołu AMQP.</span><span class="sxs-lookup"><span data-stu-id="a4754-122">The library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="a4754-123">**IoTHubClient** biblioteki jest zależny od innych bibliotek typu open source:</span><span class="sxs-lookup"><span data-stu-id="a4754-123">The **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="a4754-124">[Azure C udostępnione narzędzie](https://github.com/Azure/azure-c-shared-utility) biblioteki, która zawiera często używane funkcje podstawowe zadania (na przykład ciągi, manipulowanie listy i we/wy) wymagane przez zestawów SDK C związanych z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a4754-124">The [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="a4754-125">[Azure uAMQP](https://github.com/Azure/azure-uamqp-c) biblioteki, która jest implementacją protokołu AMQP zoptymalizowane pod kątem urządzeń zasobów ograniczone po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="a4754-125">The [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="a4754-126">[Azure uMQTT](https://github.com/Azure/azure-umqtt-c) biblioteki, która jest biblioteką ogólnego przeznaczenia implementacji protokołu MQTT i zoptymalizowany pod kątem urządzeń zasobów ograniczone.</span><span class="sxs-lookup"><span data-stu-id="a4754-126">The [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing the MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="a4754-127">Korzystanie z biblioteki jest łatwiejsze do zrozumienia analizując przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="a4754-127">Use of these libraries is easier to understand by looking at example code.</span></span> <span data-ttu-id="a4754-128">Poniższe sekcje umożliwia przeprowadzenie kilka przykładowych aplikacji, które znajdują się w zestawie SDK.</span><span class="sxs-lookup"><span data-stu-id="a4754-128">The following sections walk you through several of the sample applications that are included in the SDK.</span></span> <span data-ttu-id="a4754-129">W tym przewodniku powinien zapewnić dobrą działanie dla różnych funkcjach warstwy architektury zestawu SDK i wprowadzenie do działania za pośrednictwem interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="a4754-129">This walkthrough should give you a good feel for the various capabilities of the architectural layers of the SDK and an introduction to how the APIs work.</span></span>

## <a name="before-you-run-the-samples"></a><span data-ttu-id="a4754-130">Przed uruchomieniem próbki</span><span class="sxs-lookup"><span data-stu-id="a4754-130">Before you run the samples</span></span>

<span data-ttu-id="a4754-131">Przed uruchomieniem próbek w urządzenia Azure IoT SDK dla języka C, należy najpierw [utworzenia wystąpienia usługi IoT Hub](iot-hub-create-through-portal.md) w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a4754-131">Before you can run the samples in the Azure IoT device SDK for C, you must [create an instance of the IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="a4754-132">Następnie wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a4754-132">Then complete the following tasks:</span></span>

* <span data-ttu-id="a4754-133">Przygotowywanie środowiska projektowego</span><span class="sxs-lookup"><span data-stu-id="a4754-133">Prepare your development environment</span></span>
* <span data-ttu-id="a4754-134">Uzyskaj poświadczenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a4754-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="a4754-135">Przygotowywanie środowiska projektowego</span><span class="sxs-lookup"><span data-stu-id="a4754-135">Prepare your development environment</span></span>

<span data-ttu-id="a4754-136">Pakiety są dostępne dla wspólnego platformy (na przykład NuGet dla systemu Windows lub apt_get Debian i Ubuntu) i przykłady za pomocą tych pakietów, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="a4754-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and the samples use these packages when available.</span></span> <span data-ttu-id="a4754-137">W niektórych przypadkach należy skompilować w zestawie SDK dla lub na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="a4754-137">In some cases, you need to compile the SDK for or on your device.</span></span> <span data-ttu-id="a4754-138">Jeśli potrzebujesz do kompilowania zestawu SDK, zobacz [przygotowywanie środowiska projektowego](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) w repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="a4754-138">If you need to compile the SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in the GitHub repository.</span></span>

<span data-ttu-id="a4754-139">Aby uzyskać przykładowy kod aplikacji, należy pobrać kopię zestawu SDK z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="a4754-139">To obtain the sample application code, download a copy of the SDK from GitHub.</span></span> <span data-ttu-id="a4754-140">Pobierz kopię źródło **wzorca** gałęzi [repozytorium GitHub](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="a4754-140">Get your copy of the source from the **master** branch of the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-the-device-credentials"></a><span data-ttu-id="a4754-141">Uzyskaj poświadczenia urządzenia</span><span class="sxs-lookup"><span data-stu-id="a4754-141">Obtain the device credentials</span></span>

<span data-ttu-id="a4754-142">Teraz, gdy masz przykładowy kod źródłowy następnym etapem jest można pobrać zestawu poświadczeń urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a4754-142">Now that you have the sample source code, the next thing to do is to get a set of device credentials.</span></span> <span data-ttu-id="a4754-143">Urządzenia mogły uzyskiwać dostęp do Centrum IoT najpierw należy dodać urządzenie w rejestrze tożsamości Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4754-143">For a device to be able to access an IoT hub, you must first add the device to the IoT Hub identity registry.</span></span> <span data-ttu-id="a4754-144">Po dodaniu urządzenia możesz pobrać zestaw poświadczeń urządzenia, które należy urządzenia móc połączyć się z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4754-144">When you add your device, you get a set of device credentials that you need for the device to be able to connect to the IoT hub.</span></span> <span data-ttu-id="a4754-145">Przykładowe aplikacje omówiona w następnej sekcji mogą pojawić się te poświadczenia w postaci **ciąg połączenia urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="a4754-145">The sample applications discussed in the next section expect these credentials in the form of a **device connection string**.</span></span>

<span data-ttu-id="a4754-146">Istnieje kilka narzędzi typu open source służących do zarządzania Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4754-146">There are several open source tools to help you manage your IoT hub.</span></span>

* <span data-ttu-id="a4754-147">Aplikacji systemu Windows o nazwie [explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="a4754-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="a4754-148">Wywołuje narzędzie interfejsu wiersza polecenia i platform node.js [explorer Centrum iothub](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="a4754-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="a4754-149">W tym samouczku używana graficznym *explorer urządzenia* narzędzia.</span><span class="sxs-lookup"><span data-stu-id="a4754-149">This tutorial uses the graphical *device explorer* tool.</span></span> <span data-ttu-id="a4754-150">Można również użyć *explorer Centrum iothub* narzędzia, jeśli wolisz za pomocą narzędzia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a4754-150">You can also use the *iothub-explorer* tool if you prefer to use a CLI tool.</span></span>

<span data-ttu-id="a4754-151">Narzędzie explorer urządzenie korzysta z bibliotek usługi Azure IoT do wykonywania różnych funkcji w Centrum IoT, łącznie z dodawaniem urządzeń.</span><span class="sxs-lookup"><span data-stu-id="a4754-151">The device explorer tool uses the Azure IoT service libraries to perform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="a4754-152">Jeśli za pomocą narzędzia Eksplorator urządzenia można dodać urządzenie, możesz uzyskać ciąg połączenia dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a4754-152">If you use the device explorer tool to add a device, you get a connection string for your device.</span></span> <span data-ttu-id="a4754-153">Należy te parametry połączenia do uruchamiania aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="a4754-153">You need this connection string to run the sample applications.</span></span>

<span data-ttu-id="a4754-154">Jeśli nie znasz za pomocą narzędzia Eksplorator urządzenia, Poniższa procedura opisuje jak z niego korzystać, aby dodać urządzenie i uzyskać ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a4754-154">If you're not familiar with the device explorer tool, the following procedure describes how to use it to add a device and obtain a device connection string.</span></span>

<span data-ttu-id="a4754-155">Aby zainstalować narzędzie explorer urządzenia, zobacz [jak używać Eksploratora urządzenia dla urządzeń z Centrum IoT](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="a4754-155">To install the device explorer tool, see [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="a4754-156">Po uruchomieniu programu pojawia się tego interfejsu:</span><span class="sxs-lookup"><span data-stu-id="a4754-156">When you run the program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="a4754-157">Wprowadź użytkownika **parametry połączenia Centrum IoT** w pierwszym polu i kliknij **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="a4754-157">Enter your **IoT Hub Connection String** in the first field and click **Update**.</span></span> <span data-ttu-id="a4754-158">Ten krok konfiguruje narzędzie, dzięki czemu może komunikować się z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4754-158">This step configures the tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="a4754-159">Po skonfigurowaniu parametry połączenia Centrum IoT kliknij **zarządzania** karty:</span><span class="sxs-lookup"><span data-stu-id="a4754-159">When the IoT Hub connection string is configured, click the **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="a4754-160">Ta karta jest, którym zarządzasz urządzeń zarejestrowanych w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4754-160">This tab is where you manage the devices registered in your IoT hub.</span></span>

<span data-ttu-id="a4754-161">Urządzenie można tworzyć przez kliknięcie **Utwórz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a4754-161">You create a device by clicking the **Create** button.</span></span> <span data-ttu-id="a4754-162">Wyświetla okno dialogowe z zestawu kluczy wstępnie wypełnione (podstawowych i pomocniczych).</span><span class="sxs-lookup"><span data-stu-id="a4754-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="a4754-163">Wprowadź **identyfikator urządzenia** , a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a4754-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="a4754-164">Po utworzeniu urządzenia urządzenia Wyświetl listę wszystkich zarejestrowanych urządzeń, w tym utworzonej przed chwilą aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="a4754-164">When the device is created, the Devices list updates with all the registered devices, including the one you just created.</span></span> <span data-ttu-id="a4754-165">Kliknięcie prawym przyciskiem myszy urządzenie nowej pojawić tego menu:</span><span class="sxs-lookup"><span data-stu-id="a4754-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="a4754-166">Jeśli wybierzesz **skopiuj parametry połączenia dla wybranego urządzenia**, ciąg połączenia urządzenia jest kopiowany do Schowka.</span><span class="sxs-lookup"><span data-stu-id="a4754-166">If you choose **Copy connection string for selected device**, the device connection string is copied to the clipboard.</span></span> <span data-ttu-id="a4754-167">Przechowywać kopię ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a4754-167">Keep a copy of the device connection string.</span></span> <span data-ttu-id="a4754-168">Należy go podczas uruchamiania aplikacji przykładowych opisane w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="a4754-168">You need it when running the sample applications described in the following sections.</span></span>

<span data-ttu-id="a4754-169">Po wykonaniu powyższych czynności możesz rozpocząć uruchamianie kodu.</span><span class="sxs-lookup"><span data-stu-id="a4754-169">When you've completed the steps above, you're ready to start running some code.</span></span> <span data-ttu-id="a4754-170">Oba przykłady ma stałą w górnej części plik źródłowy głównego, który umożliwia wprowadzanie parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="a4754-170">Both samples have a constant at the top of the main source file that enables you to enter a connection string.</span></span> <span data-ttu-id="a4754-171">Na przykład odpowiedni wiersz z **Centrum iothub\_klienta\_próbki\_mqtt** aplikacja pojawi się w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="a4754-171">For example, the corresponding line from the **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-the-iothubclient-library"></a><span data-ttu-id="a4754-172">Korzystanie z biblioteki IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="a4754-172">Use the IoTHubClient library</span></span>

<span data-ttu-id="a4754-173">W ramach **Centrum iothub\_klienta** folderu w [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repozytorium, Brak **przykłady** folder, który zawiera aplikację o nazwie **Centrum iothub\_klienta\_próbki\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="a4754-173">Within the **iothub\_client** folder in the [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="a4754-174">Wersja systemu Windows **Centrum iothub\_klienta\_próbki\_mqtt** aplikacji obejmują następujące rozwiązania Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="a4754-174">The Windows version of the **iothub\_client\_sample\_mqtt** application includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="a4754-175">Jeśli w programie Visual Studio 2017 r, możesz otworzyć ten projekt, należy zaakceptować z monitami, aby przekierować projektu do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="a4754-175">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="a4754-176">To rozwiązanie zawiera jeden projekt.</span><span class="sxs-lookup"><span data-stu-id="a4754-176">This solution contains a single project.</span></span> <span data-ttu-id="a4754-177">Istnieją cztery pakiety NuGet zainstalowany w tym rozwiązaniu:</span><span class="sxs-lookup"><span data-stu-id="a4754-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="a4754-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="a4754-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="a4754-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="a4754-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="a4754-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="a4754-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="a4754-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="a4754-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="a4754-182">Należy zawsze **Microsoft.Azure.C.SharedUtility** pakietu podczas pracy z zestawem SDK.</span><span class="sxs-lookup"><span data-stu-id="a4754-182">You always need the **Microsoft.Azure.C.SharedUtility** package when you are working with the SDK.</span></span> <span data-ttu-id="a4754-183">W tym przykładzie korzysta z protokołu MQTT, dlatego należy uwzględnić **Microsoft.Azure.umqtt** i **Microsoft.Azure.IoTHub.MqttTransport** pakietów (są równoważne pakietów dla protokołu AMQP i HTTP).</span><span class="sxs-lookup"><span data-stu-id="a4754-183">This sample uses the MQTT protocol, therefore you must include the **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="a4754-184">Ponieważ w przykładzie użyto **IoTHubClient** biblioteki, należy również uwzględnić **Microsoft.Azure.IoTHub.IoTHubClient** pakietu w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="a4754-184">Because the sample uses the **IoTHubClient** library, you must also include the **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="a4754-185">Można znaleźć implementacji dla przykładowej aplikacji w **Centrum iothub\_klienta\_próbki\_mqtt.c** pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="a4754-185">You can find the implementation for the sample application in the **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="a4754-186">Następujące kroki umożliwiają przeprowadzenie co to są wymagane, aby użyć tej przykładowej aplikacji **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="a4754-186">The following steps use this sample application to walk you through what's required to use the **IoTHubClient** library.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="a4754-187">Zainicjować biblioteki</span><span class="sxs-lookup"><span data-stu-id="a4754-187">Initialize the library</span></span>

> [!NOTE]
> <span data-ttu-id="a4754-188">Przed rozpoczęciem pracy z bibliotekami, może być konieczne zainicjować niektóre specyficzne dla platformy.</span><span class="sxs-lookup"><span data-stu-id="a4754-188">Before you start working with the libraries, you may need to perform some platform-specific initialization.</span></span> <span data-ttu-id="a4754-189">Na przykład jeśli planujesz używać protokołu AMQP w systemie Linux należy zainicjować biblioteki OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="a4754-189">For example, if you plan to use AMQP on Linux you must initialize the OpenSSL library.</span></span> <span data-ttu-id="a4754-190">Przykłady w [repozytorium GitHub](https://github.com/Azure/azure-iot-sdk-c) wywołanie funkcji narzędzia **platformy\_init** kiedy klient uruchamia i Wywołaj **platformy\_deinit**funkcja przed zakończeniem.</span><span class="sxs-lookup"><span data-stu-id="a4754-190">The samples in the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call the utility function **platform\_init** when the client starts and call the **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="a4754-191">Te funkcje są zadeklarowane w pliku nagłówka platform.h.</span><span class="sxs-lookup"><span data-stu-id="a4754-191">These functions are declared in the platform.h header file.</span></span> <span data-ttu-id="a4754-192">Sprawdź definicje tych funkcji dla danej platformy docelowej w [repozytorium](https://github.com/Azure/azure-iot-sdk-c) do określenia, czy muszą zawierać dowolny kod inicjujący specyficzne dla platformy, na kliencie.</span><span class="sxs-lookup"><span data-stu-id="a4754-192">Examine the definitions of these functions for your target platform in the [repository](https://github.com/Azure/azure-iot-sdk-c) to determine whether you need to include any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="a4754-193">Aby rozpocząć pracę z biblioteki, najpierw przydzielić dojścia klienta Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="a4754-193">To start working with the libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="a4754-194">Należy przekazać kopię urządzenia parametry połączenia uzyskane z narzędzia Eksplorator urządzenia do tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a4754-194">You pass a copy of the device connection string you obtained from the device explorer tool to this function.</span></span> <span data-ttu-id="a4754-195">Możesz również określić protokół komunikacji ma być używany.</span><span class="sxs-lookup"><span data-stu-id="a4754-195">You also designate the communications protocol to use.</span></span> <span data-ttu-id="a4754-196">W tym przykładzie użyto MQTT, ale AMQP i HTTP są także opcje.</span><span class="sxs-lookup"><span data-stu-id="a4754-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="a4754-197">Jeśli użytkownik ma prawidłowy **Centrum IOTHUB\_klienta\_obsługi**, możesz uruchomić wywoływania interfejsów API, aby wysyłać i odbierać komunikaty z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4754-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling the APIs to send and receive messages to and from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="a4754-198">Wysyłanie wiadomości</span><span class="sxs-lookup"><span data-stu-id="a4754-198">Send messages</span></span>

<span data-ttu-id="a4754-199">Przykładowa aplikacja konfiguruje pętlę do wysyłania komunikatów do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4754-199">The sample application sets up a loop to send messages to your IoT hub.</span></span> <span data-ttu-id="a4754-200">Poniższy fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="a4754-200">The following snippet:</span></span>

- <span data-ttu-id="a4754-201">Tworzy komunikat.</span><span class="sxs-lookup"><span data-stu-id="a4754-201">Creates a message.</span></span>
- <span data-ttu-id="a4754-202">Dodaje właściwość do wiadomości.</span><span class="sxs-lookup"><span data-stu-id="a4754-202">Adds a property to the message.</span></span>
- <span data-ttu-id="a4754-203">Wysyła komunikat.</span><span class="sxs-lookup"><span data-stu-id="a4754-203">Sends a message.</span></span>

<span data-ttu-id="a4754-204">Najpierw utwórz komunikat:</span><span class="sxs-lookup"><span data-stu-id="a4754-204">First, create a message:</span></span>

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission to IoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="a4754-205">Każdorazowym wysłaniu wiadomości, można określić odwołania do funkcji wywołania zwrotnego, które jest wywoływane, gdy dane są przesyłane.</span><span class="sxs-lookup"><span data-stu-id="a4754-205">Every time you send a message, you specify a reference to a callback function that's invoked when the data is sent.</span></span> <span data-ttu-id="a4754-206">W tym przykładzie jest wywoływana funkcja wywołania zwrotnego **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="a4754-206">In this example, the callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="a4754-207">Poniższy fragment kodu przedstawia tej funkcji wywołania zwrotnego:</span><span class="sxs-lookup"><span data-stu-id="a4754-207">The following snippet shows this callback function:</span></span>

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

<span data-ttu-id="a4754-208">Należy pamiętać, wywołanie **IoTHubMessage\_Destroy** działać po zakończeniu z komunikatem.</span><span class="sxs-lookup"><span data-stu-id="a4754-208">Note the call to the **IoTHubMessage\_Destroy** function when you're done with the message.</span></span> <span data-ttu-id="a4754-209">Ta funkcja zwalnia zasoby przydzielone podczas tworzenia komunikatu.</span><span class="sxs-lookup"><span data-stu-id="a4754-209">This function frees the resources allocated when you created the message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="a4754-210">Odbieranie komunikatów</span><span class="sxs-lookup"><span data-stu-id="a4754-210">Receive messages</span></span>

<span data-ttu-id="a4754-211">Odbieranie wiadomości jest operacja asynchroniczna.</span><span class="sxs-lookup"><span data-stu-id="a4754-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="a4754-212">Najpierw należy zarejestrować wywołania zwrotnego do wywołania, gdy urządzenie otrzyma wiadomość:</span><span class="sxs-lookup"><span data-stu-id="a4754-212">First, you register the callback to invoke when the device receives a message:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

<span data-ttu-id="a4754-213">Ostatni parametr jest typu void wskaźnik do dowolne.</span><span class="sxs-lookup"><span data-stu-id="a4754-213">The last parameter is a void pointer to whatever you want.</span></span> <span data-ttu-id="a4754-214">W przykładzie jest wskaźnik do wartości całkowitej, ale może być wskaźnikiem do bardziej złożonych struktury danych.</span><span class="sxs-lookup"><span data-stu-id="a4754-214">In the sample, it's a pointer to an integer but it could be a pointer to a more complex data structure.</span></span> <span data-ttu-id="a4754-215">Ten parametr umożliwia działanie funkcji wywołania zwrotnego do działania na udostępniania stanu wywołującego tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a4754-215">This parameter enables the callback function to operate on shared state with the caller of this function.</span></span>

<span data-ttu-id="a4754-216">Zarejestrowana funkcja wywołania zwrotnego jest wywoływane, gdy urządzenie otrzyma wiadomość.</span><span class="sxs-lookup"><span data-stu-id="a4754-216">When the device receives a message, the registered callback function is invoked.</span></span> <span data-ttu-id="a4754-217">Ta funkcja wywołania zwrotnego pobiera:</span><span class="sxs-lookup"><span data-stu-id="a4754-217">This callback function retrieves:</span></span>

* <span data-ttu-id="a4754-218">Identyfikator komunikatu i identyfikator korelacji z komunikatu.</span><span class="sxs-lookup"><span data-stu-id="a4754-218">The message id and correlation id from the message.</span></span>
* <span data-ttu-id="a4754-219">Treść komunikatu.</span><span class="sxs-lookup"><span data-stu-id="a4754-219">The message content.</span></span>
* <span data-ttu-id="a4754-220">Wszystkie niestandardowe właściwości z komunikatu.</span><span class="sxs-lookup"><span data-stu-id="a4754-220">Any custom properties from the message.</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable to retrieve the message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive the work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from the message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="a4754-221">Użyj **IoTHubMessage\_GetByteArray** funkcji pobierania wiadomości, który w tym przykładzie jest ciągiem.</span><span class="sxs-lookup"><span data-stu-id="a4754-221">Use the **IoTHubMessage\_GetByteArray** function to retrieve the message, which in this example is a string.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="a4754-222">Odinicjalizuj biblioteki</span><span class="sxs-lookup"><span data-stu-id="a4754-222">Uninitialize the library</span></span>

<span data-ttu-id="a4754-223">Gdy wszystko będzie gotowe, zdarzenia wysyłanie i odbieranie wiadomości, można uninitialize biblioteki IoT.</span><span class="sxs-lookup"><span data-stu-id="a4754-223">When you're done sending events and receiving messages, you can uninitialize the IoT library.</span></span> <span data-ttu-id="a4754-224">Aby to zrobić, należy wydać następujące wywołanie funkcji:</span><span class="sxs-lookup"><span data-stu-id="a4754-224">To do so, issue the following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="a4754-225">To wywołanie zwolni zasoby przydzielone wcześniej przez **IoTHubClient\_CreateFromConnectionString** funkcji.</span><span class="sxs-lookup"><span data-stu-id="a4754-225">This call frees up the resources previously allocated by the **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="a4754-226">Jak widać, jest łatwy do wysyłania i odbierania wiadomości z **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="a4754-226">As you can see, it's easy to send and receive messages with the **IoTHubClient** library.</span></span> <span data-ttu-id="a4754-227">Biblioteka obsługi komunikacji z Centrum IoT, protokół, który ma być używany w tym szczegóły (z perspektywy dewelopera jest opcja prostą konfigurację).</span><span class="sxs-lookup"><span data-stu-id="a4754-227">The library handles the details of communicating with IoT Hub, including which protocol to use (from the perspective of the developer, this is a simple configuration option).</span></span>

<span data-ttu-id="a4754-228">**IoTHubClient** Biblioteka również zapewnia precyzyjną kontrolę nad jak do serializowania danych urządzenie wysyła do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4754-228">The **IoTHubClient** library also provides precise control over how to serialize the data your device sends to IoT Hub.</span></span> <span data-ttu-id="a4754-229">W niektórych przypadkach ten poziom kontroli jest korzyści, ale w innych jest szczegółów implementacji, które nie mają być związane z.</span><span class="sxs-lookup"><span data-stu-id="a4754-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want to be concerned with.</span></span> <span data-ttu-id="a4754-230">Jeśli tak jest, można rozważyć przy użyciu **serializator** biblioteki, który jest opisany w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a4754-230">If that's the case, you might consider using the **serializer** library, which is described in the next section.</span></span>

## <a name="use-the-serializer-library"></a><span data-ttu-id="a4754-231">Korzystanie z biblioteki serializator</span><span class="sxs-lookup"><span data-stu-id="a4754-231">Use the serializer library</span></span>

<span data-ttu-id="a4754-232">Koncepcyjnie **serializator** biblioteki znajduje się nad **IoTHubClient** biblioteki w zestawie SDK.</span><span class="sxs-lookup"><span data-stu-id="a4754-232">Conceptually the **serializer** library sits on top of the **IoTHubClient** library in the SDK.</span></span> <span data-ttu-id="a4754-233">Używa **IoTHubClient** biblioteki podstawowej komunikacji z Centrum IoT, ale zwiększa możliwości modelowania, które okresowo usuwają obciążenie zajmowanie serializacji komunikatu od dewelopera.</span><span class="sxs-lookup"><span data-stu-id="a4754-233">It uses the **IoTHubClient** library for the underlying communication with IoT Hub, but it adds modeling capabilities that remove the burden of dealing with message serialization from the developer.</span></span> <span data-ttu-id="a4754-234">Jak działa ta biblioteka najlepsze dowodzą przykładem.</span><span class="sxs-lookup"><span data-stu-id="a4754-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="a4754-235">Wewnątrz **serializator** folderu w [repozytorium azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c), jest **przykłady** folder, który zawiera aplikację o nazwie **simplesample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="a4754-235">Inside the **serializer** folder in the [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="a4754-236">Wersja systemu Windows w tym przykładzie obejmują następujące rozwiązania Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="a4754-236">The Windows version of this sample includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="a4754-237">Jeśli w programie Visual Studio 2017 r, możesz otworzyć ten projekt, należy zaakceptować z monitami, aby przekierować projektu do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="a4754-237">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="a4754-238">Podobnie jak w poprzednim przykładzie ta obejmuje kilka pakietów NuGet:</span><span class="sxs-lookup"><span data-stu-id="a4754-238">As with the previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="a4754-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="a4754-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="a4754-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="a4754-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="a4754-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="a4754-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="a4754-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="a4754-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="a4754-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="a4754-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="a4754-244">W tym samouczku większość tych pakietów w poprzednim przykładzie, ale **Microsoft.Azure.IoTHub.Serializer** nowego.</span><span class="sxs-lookup"><span data-stu-id="a4754-244">You've seen most of these packages in the previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="a4754-245">Ten pakiet jest wymagany, gdy używasz **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="a4754-245">This package is required when you use the **serializer** library.</span></span>

<span data-ttu-id="a4754-246">Można znaleźć implementacji przykładowej aplikacji w **simplesample\_mqtt.c** pliku.</span><span class="sxs-lookup"><span data-stu-id="a4754-246">You can find the implementation of the sample application in the **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="a4754-247">W poniższych sekcjach opisano części klucza w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="a4754-247">The following sections walk you through the key parts of this sample.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="a4754-248">Zainicjować biblioteki</span><span class="sxs-lookup"><span data-stu-id="a4754-248">Initialize the library</span></span>

<span data-ttu-id="a4754-249">Aby rozpocząć pracę z **serializator** biblioteki, wywołaj inicjowania interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="a4754-249">To start working with the **serializer** library, call the initialization APIs:</span></span>

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

<span data-ttu-id="a4754-250">Wywołanie **serializator\_init** funkcji jednorazowym wywołanie i inicjuje podstawowej biblioteki.</span><span class="sxs-lookup"><span data-stu-id="a4754-250">The call to the **serializer\_init** function is a one-time call and initializes the underlying library.</span></span> <span data-ttu-id="a4754-251">Następnie wywołaj metodę **IoTHubClient\_LL\_CreateFromConnectionString** funkcji, która jest tego samego interfejsu API, jak w **IoTHubClient** próbki.</span><span class="sxs-lookup"><span data-stu-id="a4754-251">Then, you call the **IoTHubClient\_LL\_CreateFromConnectionString** function, which is the same API as in the **IoTHubClient** sample.</span></span> <span data-ttu-id="a4754-252">To wywołanie ustawia parametry połączenia urządzenia (to wywołanie jest również, gdzie możesz wybrać protokół ma być używany).</span><span class="sxs-lookup"><span data-stu-id="a4754-252">This call sets your device connection string (this call is also where you choose the protocol you want to use).</span></span> <span data-ttu-id="a4754-253">W tym przykładzie używa MQTT jako transportu, ale można użyć protokołu AMQP i HTTP.</span><span class="sxs-lookup"><span data-stu-id="a4754-253">This sample uses MQTT as the transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="a4754-254">Na koniec wywołania **Utwórz\_modelu\_wystąpienia** funkcji.</span><span class="sxs-lookup"><span data-stu-id="a4754-254">Finally, call the **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="a4754-255">**WeatherStation** jest przestrzeń nazw modelu i **ContosoAnemometer** jest nazwa modelu.</span><span class="sxs-lookup"><span data-stu-id="a4754-255">**WeatherStation** is the namespace of the model and **ContosoAnemometer** is the name of the model.</span></span> <span data-ttu-id="a4754-256">Utworzone wystąpienie modelu można go uruchomić wysyłania i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="a4754-256">Once the model instance is created, you can use it to start sending and receiving messages.</span></span> <span data-ttu-id="a4754-257">Jednak ważne jest, aby zrozumieć, jakie modelu.</span><span class="sxs-lookup"><span data-stu-id="a4754-257">However, it's important to understand what a model is.</span></span>

### <a name="define-the-model"></a><span data-ttu-id="a4754-258">Zdefiniuj modelu</span><span class="sxs-lookup"><span data-stu-id="a4754-258">Define the model</span></span>

<span data-ttu-id="a4754-259">Model w **serializator** Biblioteka definiuje wiadomości, które urządzenia mogą przesyłać dane do Centrum IoT i komunikaty o nazwie *akcje* w języku modelowania, który może odbierać.</span><span class="sxs-lookup"><span data-stu-id="a4754-259">A model in the **serializer** library defines the messages that your device can send to IoT Hub and the messages, called *actions* in the modeling language, which it can receive.</span></span> <span data-ttu-id="a4754-260">Zdefiniuj modelu przy użyciu zestawu makr C, podobnie jak w **simplesample\_mqtt** aplikacji przykładowej:</span><span class="sxs-lookup"><span data-stu-id="a4754-260">You define a model using a set of C macros as in the **simplesample\_mqtt** sample application:</span></span>

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="a4754-261">**Rozpocząć\_przestrzeni nazw** i **zakończenia\_przestrzeni nazw** makra zarówno przestrzeń nazw modelu jako argument.</span><span class="sxs-lookup"><span data-stu-id="a4754-261">The **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take the namespace of the model as an argument.</span></span> <span data-ttu-id="a4754-262">Oczekuje się, że wszystko między tymi makra jest definicji modelu lub modeli i struktury danych, korzystających z modeli.</span><span class="sxs-lookup"><span data-stu-id="a4754-262">It's expected that anything between these macros is the definition of your model or models, and the data structures that the models use.</span></span>

<span data-ttu-id="a4754-263">W tym przykładzie jest pojedynczego modelu o nazwie **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="a4754-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="a4754-264">Ten model definiuje dwie części danych, które urządzenie może wysyłać do Centrum IoT: **DeviceId** i **prędkość wiatru**.</span><span class="sxs-lookup"><span data-stu-id="a4754-264">This model defines two pieces of data that your device can send to IoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="a4754-265">Definiuje również trzy czynności (wiadomości), które urządzenia mogą odbierać: **TurnFanOn**, **TurnFanOff**, i **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="a4754-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="a4754-266">Każdy element danych ma typ, a każda akcja ma nazwę (i opcjonalnie zestaw parametrów).</span><span class="sxs-lookup"><span data-stu-id="a4754-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="a4754-267">Dane i akcje zdefiniowane w modelu zdefiniuj powierzchni interfejsu API, który służy do wysyłania komunikatów do Centrum IoT i odpowiadać na komunikaty wysyłane do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a4754-267">The data and actions defined in the model define an API surface that you can use to send messages to IoT Hub, and respond to messages sent to the device.</span></span> <span data-ttu-id="a4754-268">Użycie tego modelu najlepiej jest rozpoznawany przez przykładowy.</span><span class="sxs-lookup"><span data-stu-id="a4754-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="a4754-269">Wysyłanie wiadomości</span><span class="sxs-lookup"><span data-stu-id="a4754-269">Send messages</span></span>

<span data-ttu-id="a4754-270">Model Określa dane, które można wysyłać do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4754-270">The model defines the data you can send to IoT Hub.</span></span> <span data-ttu-id="a4754-271">W tym przykładzie to oznacza, jeden z elementów danych dwa zdefiniowane przy użyciu **WITH_DATA** makra.</span><span class="sxs-lookup"><span data-stu-id="a4754-271">In this example, that means one of the two data items defined using the **WITH_DATA** macro.</span></span> <span data-ttu-id="a4754-272">Istnieje kilka czynności wymaganych do wysyłania **DeviceId** i **prędkość wiatru** wartości do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="a4754-272">There are several steps required to send **DeviceId** and **WindSpeed** values to an IoT hub.</span></span> <span data-ttu-id="a4754-273">Pierwsza to ustawić danych, który chcesz wysłać:</span><span class="sxs-lookup"><span data-stu-id="a4754-273">The first is to set the data you want to send:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="a4754-274">Model został zdefiniowany wcześniej służy do ustawiania wartości przez ustawienie członkami **struktury**.</span><span class="sxs-lookup"><span data-stu-id="a4754-274">The model you defined earlier enables you to set the values by setting members of a **struct**.</span></span> <span data-ttu-id="a4754-275">Następnie serializować komunikat, który ma być wysyłane:</span><span class="sxs-lookup"><span data-stu-id="a4754-275">Next, serialize the message you want to send:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed to serialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="a4754-276">Ten kod serializuje urządzenia do chmury w buforze (odwołuje **docelowego**).</span><span class="sxs-lookup"><span data-stu-id="a4754-276">This code serializes the device-to-cloud to a buffer (referenced by **destination**).</span></span> <span data-ttu-id="a4754-277">Następnie wywołuje kod **sendMessage** funkcja do wysyłania komunikatu do Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="a4754-277">The code then invokes the **sendMessage** function to send the message to IoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable to create a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed to hand over the message to IoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted the message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="a4754-278">Drugi do ostatniego parametru metody **IoTHubClient\_LL\_SendEventAsync** jest odwołaniem do funkcji wywołania zwrotnego, które jest wywoływane, gdy dane są pomyślnie wysłane.</span><span class="sxs-lookup"><span data-stu-id="a4754-278">The second to last parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference to a callback function that's called when the data is successfully sent.</span></span> <span data-ttu-id="a4754-279">W tym miejscu jest funkcja wywołania zwrotnego w przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a4754-279">Here's the callback function in the sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="a4754-280">Drugi parametr jest wskaźnik do kontekstu użytkownika; tym samym wskaźnik przekazany do **IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="a4754-280">The second parameter is a pointer to user context; the same pointer passed to **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="a4754-281">W takim przypadku kontekst jest prostego licznika, ale może być dowolny.</span><span class="sxs-lookup"><span data-stu-id="a4754-281">In this case, the context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="a4754-282">To wszystko jest do wysyłania wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="a4754-282">That's all there is to sending device-to-cloud messages.</span></span> <span data-ttu-id="a4754-283">Jedyną operacją, lewo, aby pokrywał jest jak odbierać komunikaty.</span><span class="sxs-lookup"><span data-stu-id="a4754-283">The only thing left to cover is how to receive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="a4754-284">Odbieranie komunikatów</span><span class="sxs-lookup"><span data-stu-id="a4754-284">Receive messages</span></span>

<span data-ttu-id="a4754-285">Odbieranie działa komunikat podobny sposób wiadomości działają w **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="a4754-285">Receiving a message works similarly to the way messages work in the **IoTHubClient** library.</span></span> <span data-ttu-id="a4754-286">Najpierw należy zarejestrować funkcję wywołania zwrotnego komunikat:</span><span class="sxs-lookup"><span data-stu-id="a4754-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable to IoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="a4754-287">Następnie napiszesz funkcja wywołania zwrotnego, które jest wywoływane, gdy wiadomość zostanie odebrana:</span><span class="sxs-lookup"><span data-stu-id="a4754-287">Then, you write the callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="a4754-288">Ten kod jest standardowy — jest taka sama dla dowolnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="a4754-288">This code is boilerplate -- it's the same for any solution.</span></span> <span data-ttu-id="a4754-289">Ta funkcja odbiera wiadomości i zajmuje się rozsyłania jej do odpowiedniej funkcji za pośrednictwem wywołania **EXECUTE\_polecenia**.</span><span class="sxs-lookup"><span data-stu-id="a4754-289">This function receives the message and takes care of routing it to the appropriate function through the call to **EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="a4754-290">Funkcja wywoływana na tym etapie zależy od definicji działań w modelu.</span><span class="sxs-lookup"><span data-stu-id="a4754-290">The function called at this point depends on the definition of the actions in your model.</span></span>

<span data-ttu-id="a4754-291">Po zdefiniowaniu akcji w modelu, musisz zaimplementować funkcję, która jest wywoływana, gdy urządzenie otrzyma odpowiedni komunikat.</span><span class="sxs-lookup"><span data-stu-id="a4754-291">When you define an action in your model, you're required to implement a function that's called when your device receives the corresponding message.</span></span> <span data-ttu-id="a4754-292">Na przykład, jeśli model definiuje tej akcji:</span><span class="sxs-lookup"><span data-stu-id="a4754-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="a4754-293">Zdefiniuj funkcję z tego podpisu:</span><span class="sxs-lookup"><span data-stu-id="a4754-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="a4754-294">Należy zwrócić uwagę, jak nazwa funkcji zgodna z nazwą akcji w modelu, a parametry funkcji takie same parametry określone dla akcji.</span><span class="sxs-lookup"><span data-stu-id="a4754-294">Note how the name of the function matches the name of the action in the model and that the parameters of the function match the parameters specified for the action.</span></span> <span data-ttu-id="a4754-295">Pierwszy parametr jest zawsze wymagane i zawiera wskaźnik do wystąpienia modelu.</span><span class="sxs-lookup"><span data-stu-id="a4754-295">The first parameter is always required and contains a pointer to the instance of your model.</span></span>

<span data-ttu-id="a4754-296">Gdy urządzenie otrzyma wiadomość pasującego do tego podpisu, odpowiednich funkcja jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="a4754-296">When the device receives a message that matches this signature, the corresponding function is called.</span></span> <span data-ttu-id="a4754-297">W związku z tym jako uzupełnienie konieczności dołączania schematyczny kod z **IoTHubMessage**, odbierania wiadomości jest wystarczy zdefiniować funkcję proste dla każdej akcji zdefiniowanych w modelu.</span><span class="sxs-lookup"><span data-stu-id="a4754-297">Therefore, aside from having to include the boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="a4754-298">Odinicjalizuj biblioteki</span><span class="sxs-lookup"><span data-stu-id="a4754-298">Uninitialize the library</span></span>

<span data-ttu-id="a4754-299">Gdy wszystko będzie gotowe, dane wysyłanie i odbieranie wiadomości, można uninitialize biblioteki IoT:</span><span class="sxs-lookup"><span data-stu-id="a4754-299">When you're done sending data and receiving messages, you can uninitialize the IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="a4754-300">Każda z tych trzech funkcji wyrównana z trzech opisanych wcześniej funkcji inicjowania.</span><span class="sxs-lookup"><span data-stu-id="a4754-300">Each of these three functions aligns with the three initialization functions described previously.</span></span> <span data-ttu-id="a4754-301">Te interfejsy API do wywoływania zapewnia zwolnienie wcześniej przydzielone zasoby.</span><span class="sxs-lookup"><span data-stu-id="a4754-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4754-302">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a4754-302">Next Steps</span></span>

<span data-ttu-id="a4754-303">W tym artykule omówione podstawy używania bibliotek w **urządzenia Azure IoT SDK dla języka C**. Go podano za mało informacji, aby zrozumieć, co jest zawarte w zestawie SDK jego architektury i jak rozpocząć pracę z usługą Windows przykłady.</span><span class="sxs-lookup"><span data-stu-id="a4754-303">This article covered the basics of using the libraries in the **Azure IoT device SDK for C**. It provided you with enough information to understand what's included in the SDK, its architecture, and how to get started working with the Windows samples.</span></span> <span data-ttu-id="a4754-304">Kolejnym artykule nadal opis zestawu SDK przez wyjaśniający [więcej informacji na temat biblioteki IoTHubClient](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="a4754-304">The next article continues the description of the SDK by explaining [more about the IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="a4754-305">Aby dowiedzieć się więcej o tworzeniu aplikacji Centrum IoT, zobacz [Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="a4754-305">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="a4754-306">Aby dokładniej analizować możliwości Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="a4754-306">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="a4754-307">[Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="a4754-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
