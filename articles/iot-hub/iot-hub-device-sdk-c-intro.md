---
title: "aaaThe urządzenia Azure IoT SDK dla języka C | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z hello urządzenia Azure IoT SDK dla języka C i Dowiedz się, jak toocreate aplikacji dla urządzeń, które do komunikacji z Centrum IoT."
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
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="ebd79-103">Azure urządzenia IoT zestawu SDK dla języka C</span><span class="sxs-lookup"><span data-stu-id="ebd79-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="ebd79-104">Witaj **urządzenia Azure IoT SDK** to zestaw bibliotek zaprojektowane toosimplify hello proces wysyłania wiadomości tooand odbieranie wiadomości z hello **Centrum IoT Azure** usługi.</span><span class="sxs-lookup"><span data-stu-id="ebd79-104">hello **Azure IoT device SDK** is a set of libraries designed toosimplify hello process of sending messages tooand receiving messages from hello **Azure IoT Hub** service.</span></span> <span data-ttu-id="ebd79-105">Istnieją możliwych kombinacji hello SDK każdego przeznaczonych dla określonej platformy, ale w tym artykule opisano hello **urządzenia Azure IoT SDK dla języka C**.</span><span class="sxs-lookup"><span data-stu-id="ebd79-105">There are different variations of hello SDK, each targeting a specific platform, but this article describes hello **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="ebd79-106">Hello urządzenia Azure IoT SDK dla języka C są zapisywane w przenośność toomaximize ANSI C (C99).</span><span class="sxs-lookup"><span data-stu-id="ebd79-106">hello Azure IoT device SDK for C is written in ANSI C (C99) toomaximize portability.</span></span> <span data-ttu-id="ebd79-107">Ta funkcja umożliwia hello bibliotek toooperate dobrze nadaje się na wielu platformach i urządzeniach, szczególnie w przypadku, gdy minimalizując dysku i zużycie pamięci jest priorytetem.</span><span class="sxs-lookup"><span data-stu-id="ebd79-107">This feature makes hello libraries well-suited toooperate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="ebd79-108">Istnieje szeroka gama platformy, na których hello został przetestowany zestaw SDK (zobacz hello [Azure certyfikowane dla katalogu urządzenia IoT](https://catalog.azureiotsuite.com/) szczegółowe informacje).</span><span class="sxs-lookup"><span data-stu-id="ebd79-108">There are a broad range of platforms on which hello SDK has been tested (see hello [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="ebd79-109">Chociaż ten artykuł zawiera wskazówki przykładowy kod działających na platformie Windows hello, kod hello opisane w tym artykule jest identyczna w zakresie hello obsługiwanych platform.</span><span class="sxs-lookup"><span data-stu-id="ebd79-109">Although this article includes walkthroughs of sample code running on hello Windows platform, hello code described in this article is identical across hello range of supported platforms.</span></span>

<span data-ttu-id="ebd79-110">W tym artykule przedstawiono toohello architektury urządzenia Azure IoT hello zestawu SDK dla C. Pokazano go, jak wysyłać dane tooIoT Centrum tooinitialize hello urządzenia biblioteki, i otrzymywać wiadomości.</span><span class="sxs-lookup"><span data-stu-id="ebd79-110">This article introduces you toohello architecture of hello Azure IoT device SDK for C. It demonstrates how tooinitialize hello device library, send data tooIoT Hub, and receive messages from it.</span></span> <span data-ttu-id="ebd79-111">Hello informacje w tym artykule powinien być wystarczająco dużo tooget uruchomiony przy użyciu hello zestawu SDK, ale także wskaźniki tooadditional informacje o bibliotekach hello.</span><span class="sxs-lookup"><span data-stu-id="ebd79-111">hello information in this article should be enough tooget started using hello SDK, but also provides pointers tooadditional information about hello libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="ebd79-112">Architektura zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="ebd79-112">SDK architecture</span></span>

<span data-ttu-id="ebd79-113">Można znaleźć hello [ **urządzenia Azure IoT SDK dla języka C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub repozytorium i Wyświetl szczegóły hello interfejsu API w hello [dokumentacja interfejsu API C](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="ebd79-113">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="ebd79-114">najnowszą wersję Hello hello bibliotek można znaleźć w hello **wzorca** gałęzi repozytorium hello:</span><span class="sxs-lookup"><span data-stu-id="ebd79-114">hello latest version of hello libraries can be found in hello **master** branch of hello repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="ebd79-115">Witaj core implementacja hello zestawu SDK jest w hello **Centrum iothub\_klienta** folderu, który zawiera implementację hello hello najniższy poziom interfejsu API zestawu SDK hello: hello **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="ebd79-115">hello core implementation of hello SDK is in hello **iothub\_client** folder that contains hello implementation of hello lowest API layer in hello SDK: hello **IoTHubClient** library.</span></span> <span data-ttu-id="ebd79-116">Witaj **IoTHubClient** biblioteka zawiera interfejsy API Implementowanie raw wiadomości do wysyłania wiadomości tooIoT koncentratora i odbieranie komunikatów z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ebd79-116">hello **IoTHubClient** library contains APIs implementing raw messaging for sending messages tooIoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="ebd79-117">Korzystając z tej biblioteki, jest odpowiedzialny za wdrażanie serializacji komunikatu, ale inne szczegóły komunikowania się z Centrum IoT są obsługiwane dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="ebd79-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="ebd79-118">Witaj **serializator** folder zawiera funkcje pomocnicze i przykłady, które pokazują, jak tooserialize danych przed wysłaniem przy użyciu Centrum IoT tooAzure hello biblioteki klienta.</span><span class="sxs-lookup"><span data-stu-id="ebd79-118">hello **serializer** folder contains helper functions and samples that show you how tooserialize data before sending tooAzure IoT Hub using hello client library.</span></span> <span data-ttu-id="ebd79-119">Użycie Hello hello Serializator nie jest obowiązkowe i jest dostępne dla wygody.</span><span class="sxs-lookup"><span data-stu-id="ebd79-119">hello use of hello serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="ebd79-120">Witaj toouse **serializator** biblioteki, należy zdefiniować modelu, który określa danych toosend tooIoT koncentratora i hello wiadomości powitania oczekiwać tooreceive od niego.</span><span class="sxs-lookup"><span data-stu-id="ebd79-120">toouse hello **serializer** library, you define a model that specifies hello data toosend tooIoT Hub and hello messages you expect tooreceive from it.</span></span> <span data-ttu-id="ebd79-121">Po modelu hello jest zdefiniowany, hello zestaw SDK umożliwia powierzchni interfejsu API, która umożliwia tooeasily pracy z urządzenia do chmury i komunikaty chmury do urządzenia, nie martwiąc się o hello szczegóły serializacji.</span><span class="sxs-lookup"><span data-stu-id="ebd79-121">Once hello model is defined, hello SDK provides you with an API surface that enables you tooeasily work with device-to-cloud and cloud-to-device messages without worrying about hello serialization details.</span></span> <span data-ttu-id="ebd79-122">Biblioteka Hello jest zależny od innych bibliotek typu open source, które implementują transportu przy użyciu protokołów, takich jak MQTT i protokołu AMQP.</span><span class="sxs-lookup"><span data-stu-id="ebd79-122">hello library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="ebd79-123">Witaj **IoTHubClient** biblioteki jest zależny od innych bibliotek typu open source:</span><span class="sxs-lookup"><span data-stu-id="ebd79-123">hello **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="ebd79-124">Witaj [Azure C udostępnione narzędzie](https://github.com/Azure/azure-c-shared-utility) biblioteki, która zawiera często używane funkcje podstawowe zadania (na przykład ciągi, manipulowanie listy i we/wy) wymagane przez zestawów SDK C związanych z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd79-124">hello [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="ebd79-125">Witaj [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) biblioteki, która jest implementacją protokołu AMQP zoptymalizowane pod kątem urządzeń zasobów ograniczone po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="ebd79-125">hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="ebd79-126">Witaj [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) biblioteki, która jest biblioteką ogólnego przeznaczenia implementacji protokołu MQTT hello i zoptymalizowany pod kątem urządzeń zasobów ograniczone.</span><span class="sxs-lookup"><span data-stu-id="ebd79-126">hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing hello MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="ebd79-127">Te biblioteki jest łatwiejsze toounderstand analizując przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="ebd79-127">Use of these libraries is easier toounderstand by looking at example code.</span></span> <span data-ttu-id="ebd79-128">następujące sekcje Hello umożliwia przeprowadzenie kilka hello przykładowej aplikacji, które znajdują się w hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="ebd79-128">hello following sections walk you through several of hello sample applications that are included in hello SDK.</span></span> <span data-ttu-id="ebd79-129">W tym przewodniku powinien zapewnić jest dobrą działanie hello różnych funkcjach warstwy architektury hello hello zestawu SDK i powitalne toohow wprowadzenie pracy interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="ebd79-129">This walkthrough should give you a good feel for hello various capabilities of hello architectural layers of hello SDK and an introduction toohow hello APIs work.</span></span>

## <a name="before-you-run-hello-samples"></a><span data-ttu-id="ebd79-130">Przed uruchomieniem hello próbek</span><span class="sxs-lookup"><span data-stu-id="ebd79-130">Before you run hello samples</span></span>

<span data-ttu-id="ebd79-131">Przed uruchomieniem hello próbek w hello urządzenia Azure IoT SDK dla języka C, należy najpierw [Utwórz wystąpienie hello usługi IoT Hub](iot-hub-create-through-portal.md) w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd79-131">Before you can run hello samples in hello Azure IoT device SDK for C, you must [create an instance of hello IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="ebd79-132">Następnie ukończyć powitalnych następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="ebd79-132">Then complete hello following tasks:</span></span>

* <span data-ttu-id="ebd79-133">Przygotowywanie środowiska projektowego</span><span class="sxs-lookup"><span data-stu-id="ebd79-133">Prepare your development environment</span></span>
* <span data-ttu-id="ebd79-134">Uzyskaj poświadczenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ebd79-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="ebd79-135">Przygotowywanie środowiska projektowego</span><span class="sxs-lookup"><span data-stu-id="ebd79-135">Prepare your development environment</span></span>

<span data-ttu-id="ebd79-136">Pakiety są dostępne dla wspólnego platformy (na przykład NuGet dla systemu Windows lub apt_get Debian i Ubuntu) i przykłady hello za pomocą tych pakietów, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="ebd79-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and hello samples use these packages when available.</span></span> <span data-ttu-id="ebd79-137">W niektórych przypadkach należy hello toocompile zestawu SDK dla lub na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="ebd79-137">In some cases, you need toocompile hello SDK for or on your device.</span></span> <span data-ttu-id="ebd79-138">Jeśli potrzebujesz hello toocompile zestawu SDK, zobacz [przygotowywanie środowiska projektowego](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) w repozytorium GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="ebd79-138">If you need toocompile hello SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in hello GitHub repository.</span></span>

<span data-ttu-id="ebd79-139">tooobtain hello przykładowy kod aplikacji, Pobierz kopię hello SDK z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="ebd79-139">tooobtain hello sample application code, download a copy of hello SDK from GitHub.</span></span> <span data-ttu-id="ebd79-140">Pobierz kopię hello źródła z hello **wzorca** gałęzi hello [repozytorium GitHub](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="ebd79-140">Get your copy of hello source from hello **master** branch of hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-hello-device-credentials"></a><span data-ttu-id="ebd79-141">Uzyskaj poświadczenia urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="ebd79-141">Obtain hello device credentials</span></span>

<span data-ttu-id="ebd79-142">Teraz, gdy masz hello przykładowy kod źródłowy dalej toodo operacją hello jest tooget zestaw poświadczeń, urządzenie.</span><span class="sxs-lookup"><span data-stu-id="ebd79-142">Now that you have hello sample source code, hello next thing toodo is tooget a set of device credentials.</span></span> <span data-ttu-id="ebd79-143">Dla urządzenia toobe stanie tooaccess Centrum IoT najpierw należy dodać hello urządzenia toohello w rejestrze tożsamości Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ebd79-143">For a device toobe able tooaccess an IoT hub, you must first add hello device toohello IoT Hub identity registry.</span></span> <span data-ttu-id="ebd79-144">Po dodaniu urządzenia otrzymasz zestaw poświadczeń urządzenia, wymagane dla Centrum IoT toohello toobe tooconnect stanie hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ebd79-144">When you add your device, you get a set of device credentials that you need for hello device toobe able tooconnect toohello IoT hub.</span></span> <span data-ttu-id="ebd79-145">Hello przykładowe aplikacje omówiona w następnej sekcji hello mogą pojawić się te poświadczenia w postaci hello **ciąg połączenia urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="ebd79-145">hello sample applications discussed in hello next section expect these credentials in hello form of a **device connection string**.</span></span>

<span data-ttu-id="ebd79-146">Istnieje kilka toohelp narzędzi typu open source, zarządzanie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ebd79-146">There are several open source tools toohelp you manage your IoT hub.</span></span>

* <span data-ttu-id="ebd79-147">Aplikacji systemu Windows o nazwie [explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="ebd79-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="ebd79-148">Wywołuje narzędzie interfejsu wiersza polecenia i platform node.js [explorer Centrum iothub](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="ebd79-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="ebd79-149">W tym samouczku używana hello graficznego *explorer urządzenia* narzędzia.</span><span class="sxs-lookup"><span data-stu-id="ebd79-149">This tutorial uses hello graphical *device explorer* tool.</span></span> <span data-ttu-id="ebd79-150">Można również użyć hello *explorer Centrum iothub* narzędzia, jeśli wolisz toouse narzędzia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="ebd79-150">You can also use hello *iothub-explorer* tool if you prefer toouse a CLI tool.</span></span>

<span data-ttu-id="ebd79-151">Narzędzie explorer urządzenia Hello używa tooperform bibliotek usługi Azure IoT hello różnych funkcji w Centrum IoT, łącznie z dodawaniem urządzeń.</span><span class="sxs-lookup"><span data-stu-id="ebd79-151">hello device explorer tool uses hello Azure IoT service libraries tooperform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="ebd79-152">Jeśli używasz hello urządzenia explorer narzędzia tooadd urządzenia, możesz uzyskać ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ebd79-152">If you use hello device explorer tool tooadd a device, you get a connection string for your device.</span></span> <span data-ttu-id="ebd79-153">Należy to połączenie ciąg toorun hello przykładowe aplikacje.</span><span class="sxs-lookup"><span data-stu-id="ebd79-153">You need this connection string toorun hello sample applications.</span></span>

<span data-ttu-id="ebd79-154">Jeśli nie znasz za pomocą narzędzia Eksplorator hello urządzenia, hello procedury w tym artykule opisano sposób toouse on tooadd urządzenie i uzyskać ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ebd79-154">If you're not familiar with hello device explorer tool, hello following procedure describes how toouse it tooadd a device and obtain a device connection string.</span></span>

<span data-ttu-id="ebd79-155">Narzędzie explorer tooinstall hello urządzenia, zobacz [jak toouse hello Explorer urządzenia dla urządzeń z Centrum IoT](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="ebd79-155">tooinstall hello device explorer tool, see [How toouse hello Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="ebd79-156">Po uruchomieniu hello program, zostanie wyświetlony ten interfejs:</span><span class="sxs-lookup"><span data-stu-id="ebd79-156">When you run hello program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="ebd79-157">Wprowadź użytkownika **parametry połączenia Centrum IoT** w hello pierwsze pole i kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="ebd79-157">Enter your **IoT Hub Connection String** in hello first field and click **Update**.</span></span> <span data-ttu-id="ebd79-158">Ten krok obejmuje skonfigurowanie narzędzia hello tak, aby umożliwić komunikację z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ebd79-158">This step configures hello tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="ebd79-159">Po skonfigurowaniu hello parametry połączenia Centrum IoT kliknij hello **zarządzania** karty:</span><span class="sxs-lookup"><span data-stu-id="ebd79-159">When hello IoT Hub connection string is configured, click hello **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="ebd79-160">Ta karta jest, którym zarządzasz hello urządzeń zarejestrowanych w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ebd79-160">This tab is where you manage hello devices registered in your IoT hub.</span></span>

<span data-ttu-id="ebd79-161">Urządzenie można tworzyć przez kliknięcie hello **Utwórz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ebd79-161">You create a device by clicking hello **Create** button.</span></span> <span data-ttu-id="ebd79-162">Wyświetla okno dialogowe z zestawu kluczy wstępnie wypełnione (podstawowych i pomocniczych).</span><span class="sxs-lookup"><span data-stu-id="ebd79-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="ebd79-163">Wprowadź **identyfikator urządzenia** , a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ebd79-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="ebd79-164">Po utworzeniu urządzenia hello urządzeń hello Wyświetl listę wszystkich hello zarejestrowanych urządzeń, takich jak hello utworzony co aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="ebd79-164">When hello device is created, hello Devices list updates with all hello registered devices, including hello one you just created.</span></span> <span data-ttu-id="ebd79-165">Kliknięcie prawym przyciskiem myszy urządzenie nowej pojawić tego menu:</span><span class="sxs-lookup"><span data-stu-id="ebd79-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="ebd79-166">Jeśli wybierzesz **skopiuj parametry połączenia dla wybranego urządzenia**, ciąg połączenia urządzenia hello jest skopiowany toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="ebd79-166">If you choose **Copy connection string for selected device**, hello device connection string is copied toohello clipboard.</span></span> <span data-ttu-id="ebd79-167">Przechowywać kopię ciąg połączenia urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="ebd79-167">Keep a copy of hello device connection string.</span></span> <span data-ttu-id="ebd79-168">Należy go podczas uruchamiania aplikacji przykładowych hello opisanego w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="ebd79-168">You need it when running hello sample applications described in hello following sections.</span></span>

<span data-ttu-id="ebd79-169">Po ukończeniu powyższych kroków hello, wszystko jest gotowe toostart uruchamiania kodu.</span><span class="sxs-lookup"><span data-stu-id="ebd79-169">When you've completed hello steps above, you're ready toostart running some code.</span></span> <span data-ttu-id="ebd79-170">Oba przykłady ma stałą u góry hello hello główne źródło pliku, który umożliwia tooenter ciąg połączenia.</span><span class="sxs-lookup"><span data-stu-id="ebd79-170">Both samples have a constant at hello top of hello main source file that enables you tooenter a connection string.</span></span> <span data-ttu-id="ebd79-171">Na przykład Witaj odpowiedni wiersz z hello **Centrum iothub\_klienta\_próbki\_mqtt** aplikacja pojawi się w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="ebd79-171">For example, hello corresponding line from hello **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a><span data-ttu-id="ebd79-172">Użyj hello IoTHubClient biblioteki</span><span class="sxs-lookup"><span data-stu-id="ebd79-172">Use hello IoTHubClient library</span></span>

<span data-ttu-id="ebd79-173">W ramach hello **Centrum iothub\_klienta** folderu w hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repozytorium, Brak **przykłady** folder, który zawiera aplikację o nazwie **Centrum iothub\_klienta\_próbki\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="ebd79-173">Within hello **iothub\_client** folder in hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="ebd79-174">Wersja Windows Hello hello **Centrum iothub\_klienta\_próbki\_mqtt** aplikacja zawiera hello następujące rozwiązania Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ebd79-174">hello Windows version of hello **iothub\_client\_sample\_mqtt** application includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="ebd79-175">Po otwarciu tego projektu w programie Visual Studio 2017 zaakceptować hello monity tooretarget hello projektu toohello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="ebd79-175">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="ebd79-176">To rozwiązanie zawiera jeden projekt.</span><span class="sxs-lookup"><span data-stu-id="ebd79-176">This solution contains a single project.</span></span> <span data-ttu-id="ebd79-177">Istnieją cztery pakiety NuGet zainstalowany w tym rozwiązaniu:</span><span class="sxs-lookup"><span data-stu-id="ebd79-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="ebd79-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="ebd79-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="ebd79-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="ebd79-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="ebd79-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="ebd79-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="ebd79-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="ebd79-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="ebd79-182">Należy zawsze hello **Microsoft.Azure.C.SharedUtility** pakietu podczas pracy z hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="ebd79-182">You always need hello **Microsoft.Azure.C.SharedUtility** package when you are working with hello SDK.</span></span> <span data-ttu-id="ebd79-183">Ten przykład wykorzystuje protokół MQTT hello, w związku z tym musi zawierać hello **Microsoft.Azure.umqtt** i **Microsoft.Azure.IoTHub.MqttTransport** pakietów (są równoważne pakietów dla protokołu AMQP i HTTP ).</span><span class="sxs-lookup"><span data-stu-id="ebd79-183">This sample uses hello MQTT protocol, therefore you must include hello **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="ebd79-184">Ponieważ hello w przykładzie użyto hello **IoTHubClient** biblioteki, musi także obejmować hello **Microsoft.Azure.IoTHub.IoTHubClient** pakietu w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="ebd79-184">Because hello sample uses hello **IoTHubClient** library, you must also include hello **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="ebd79-185">Implementacja hello hello przykładowej aplikacji można znaleźć w hello **Centrum iothub\_klienta\_próbki\_mqtt.c** pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="ebd79-185">You can find hello implementation for hello sample application in hello **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="ebd79-186">Witaj następujące kroki używać tej przykładowej aplikacji toowalk przez co wymagane toouse hello **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="ebd79-186">hello following steps use this sample application toowalk you through what's required toouse hello **IoTHubClient** library.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="ebd79-187">Zainicjowanie biblioteki hello</span><span class="sxs-lookup"><span data-stu-id="ebd79-187">Initialize hello library</span></span>

> [!NOTE]
> <span data-ttu-id="ebd79-188">Przed rozpoczęciem pracy z bibliotekami hello może być konieczne tooperform inicjowania niektóre specyficzne dla platformy.</span><span class="sxs-lookup"><span data-stu-id="ebd79-188">Before you start working with hello libraries, you may need tooperform some platform-specific initialization.</span></span> <span data-ttu-id="ebd79-189">Na przykład jeśli planujesz toouse AMQP w systemie Linux należy zainicjować biblioteki OpenSSL hello.</span><span class="sxs-lookup"><span data-stu-id="ebd79-189">For example, if you plan toouse AMQP on Linux you must initialize hello OpenSSL library.</span></span> <span data-ttu-id="ebd79-190">Witaj próbek w hello [repozytorium GitHub](https://github.com/Azure/azure-iot-sdk-c) wywołania funkcji narzędzia hello **platformy\_init** po hello uruchamia klienta i Wywołaj hello **platformy\_deinit**  funkcja przed zakończeniem.</span><span class="sxs-lookup"><span data-stu-id="ebd79-190">hello samples in hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call hello utility function **platform\_init** when hello client starts and call hello **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="ebd79-191">Te funkcje są zadeklarowane w pliku nagłówka platform.h hello.</span><span class="sxs-lookup"><span data-stu-id="ebd79-191">These functions are declared in hello platform.h header file.</span></span> <span data-ttu-id="ebd79-192">Sprawdź hello definicji funkcji dla danej platformy docelowej w hello [repozytorium](https://github.com/Azure/azure-iot-sdk-c) toodetermine tego, czy należy tooinclude dowolny kod inicjujący specyficzne dla platformy, na kliencie.</span><span class="sxs-lookup"><span data-stu-id="ebd79-192">Examine hello definitions of these functions for your target platform in hello [repository](https://github.com/Azure/azure-iot-sdk-c) toodetermine whether you need tooinclude any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="ebd79-193">Praca z bibliotekami hello toostart najpierw przydzielić dojścia klienta Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="ebd79-193">toostart working with hello libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="ebd79-194">Należy przekazać kopię ciąg połączenia urządzenia hello uzyskane z hello urządzenia explorer narzędzia toothis funkcji.</span><span class="sxs-lookup"><span data-stu-id="ebd79-194">You pass a copy of hello device connection string you obtained from hello device explorer tool toothis function.</span></span> <span data-ttu-id="ebd79-195">Możesz też określić hello komunikacji protokołu toouse.</span><span class="sxs-lookup"><span data-stu-id="ebd79-195">You also designate hello communications protocol toouse.</span></span> <span data-ttu-id="ebd79-196">W tym przykładzie użyto MQTT, ale AMQP i HTTP są także opcje.</span><span class="sxs-lookup"><span data-stu-id="ebd79-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="ebd79-197">Jeśli użytkownik ma prawidłowy **Centrum IOTHUB\_klienta\_obsługi**, można uruchomić wywoływania hello toosend interfejsów API i odbieranie wiadomości tooand z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ebd79-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling hello APIs toosend and receive messages tooand from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="ebd79-198">Wysyłanie wiadomości</span><span class="sxs-lookup"><span data-stu-id="ebd79-198">Send messages</span></span>

<span data-ttu-id="ebd79-199">Centrum IoT pętli toosend wiadomości tooyour ustawia Hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ebd79-199">hello sample application sets up a loop toosend messages tooyour IoT hub.</span></span> <span data-ttu-id="ebd79-200">Witaj następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="ebd79-200">hello following snippet:</span></span>

- <span data-ttu-id="ebd79-201">Tworzy komunikat.</span><span class="sxs-lookup"><span data-stu-id="ebd79-201">Creates a message.</span></span>
- <span data-ttu-id="ebd79-202">Dodaje komunikat toohello właściwości.</span><span class="sxs-lookup"><span data-stu-id="ebd79-202">Adds a property toohello message.</span></span>
- <span data-ttu-id="ebd79-203">Wysyła komunikat.</span><span class="sxs-lookup"><span data-stu-id="ebd79-203">Sends a message.</span></span>

<span data-ttu-id="ebd79-204">Najpierw utwórz komunikat:</span><span class="sxs-lookup"><span data-stu-id="ebd79-204">First, create a message:</span></span>

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
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="ebd79-205">Każdorazowym wysłaniu wiadomości, można określić funkcję wywołania zwrotnego tooa odwołanie, które jest wywoływane, gdy hello dane są wysyłane.</span><span class="sxs-lookup"><span data-stu-id="ebd79-205">Every time you send a message, you specify a reference tooa callback function that's invoked when hello data is sent.</span></span> <span data-ttu-id="ebd79-206">W tym przykładzie jest wywoływana funkcja wywołania zwrotnego hello **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="ebd79-206">In this example, hello callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="ebd79-207">powitania po fragment kodu przedstawia tej funkcji wywołania zwrotnego:</span><span class="sxs-lookup"><span data-stu-id="ebd79-207">hello following snippet shows this callback function:</span></span>

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

<span data-ttu-id="ebd79-208">Należy zwrócić uwagę hello wywołania toohello **IoTHubMessage\_Destroy** działać po zakończeniu wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="ebd79-208">Note hello call toohello **IoTHubMessage\_Destroy** function when you're done with hello message.</span></span> <span data-ttu-id="ebd79-209">Ta funkcja zwalnia zasoby hello przydzielone podczas tworzenia wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="ebd79-209">This function frees hello resources allocated when you created hello message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="ebd79-210">Odbieranie komunikatów</span><span class="sxs-lookup"><span data-stu-id="ebd79-210">Receive messages</span></span>

<span data-ttu-id="ebd79-211">Odbieranie wiadomości jest operacja asynchroniczna.</span><span class="sxs-lookup"><span data-stu-id="ebd79-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="ebd79-212">Po pierwsze zarejestrujesz tooinvoke wywołania zwrotnego hello odebrania wiadomość hello urządzenia:</span><span class="sxs-lookup"><span data-stu-id="ebd79-212">First, you register hello callback tooinvoke when hello device receives a message:</span></span>

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

<span data-ttu-id="ebd79-213">Ostatni parametr Hello jest toowhatever void wskaźnika, który ma.</span><span class="sxs-lookup"><span data-stu-id="ebd79-213">hello last parameter is a void pointer toowhatever you want.</span></span> <span data-ttu-id="ebd79-214">W przykładowym hello jest liczba całkowita tooan wskaźnika, ale można jej tooa wskaźnika bardziej złożonych struktury danych.</span><span class="sxs-lookup"><span data-stu-id="ebd79-214">In hello sample, it's a pointer tooan integer but it could be a pointer tooa more complex data structure.</span></span> <span data-ttu-id="ebd79-215">Ten parametr umożliwia toooperate funkcja wywołania zwrotnego hello na udostępniania stanu wywołującego hello tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ebd79-215">This parameter enables hello callback function toooperate on shared state with hello caller of this function.</span></span>

<span data-ttu-id="ebd79-216">Gdy hello urządzenie odbiera wiadomości, hello zarejestrowana funkcja wywołania zwrotnego jest wywoływany.</span><span class="sxs-lookup"><span data-stu-id="ebd79-216">When hello device receives a message, hello registered callback function is invoked.</span></span> <span data-ttu-id="ebd79-217">Ta funkcja wywołania zwrotnego pobiera:</span><span class="sxs-lookup"><span data-stu-id="ebd79-217">This callback function retrieves:</span></span>

* <span data-ttu-id="ebd79-218">Identyfikator wiadomości powitania i identyfikator korelacji z wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="ebd79-218">hello message id and correlation id from hello message.</span></span>
* <span data-ttu-id="ebd79-219">zawartość wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="ebd79-219">hello message content.</span></span>
* <span data-ttu-id="ebd79-220">Wszystkie niestandardowe właściwości z wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="ebd79-220">Any custom properties from hello message.</span></span>

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
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
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

<span data-ttu-id="ebd79-221">Użyj hello **IoTHubMessage\_GetByteArray** wiadomości powitania tooretrieve funkcja, której wartość jest ciągiem.</span><span class="sxs-lookup"><span data-stu-id="ebd79-221">Use hello **IoTHubMessage\_GetByteArray** function tooretrieve hello message, which in this example is a string.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="ebd79-222">Odinicjalizuj hello biblioteki</span><span class="sxs-lookup"><span data-stu-id="ebd79-222">Uninitialize hello library</span></span>

<span data-ttu-id="ebd79-223">Po zakończeniu wysyłania zdarzeń i odbieranie wiadomości, można uninitialize hello IoT biblioteki.</span><span class="sxs-lookup"><span data-stu-id="ebd79-223">When you're done sending events and receiving messages, you can uninitialize hello IoT library.</span></span> <span data-ttu-id="ebd79-224">toodo wystawiania, powitania po wywołaniu funkcji:</span><span class="sxs-lookup"><span data-stu-id="ebd79-224">toodo so, issue hello following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="ebd79-225">To wywołanie zwolni zasoby hello przydzielona wcześniej przez hello **IoTHubClient\_CreateFromConnectionString** funkcji.</span><span class="sxs-lookup"><span data-stu-id="ebd79-225">This call frees up hello resources previously allocated by hello **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="ebd79-226">Jak widać, jest łatwe toosend i odbieranie komunikatów za pomocą hello **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="ebd79-226">As you can see, it's easy toosend and receive messages with hello **IoTHubClient** library.</span></span> <span data-ttu-id="ebd79-227">Witaj biblioteki obsługuje szczegóły hello komunikowania się z Centrum IoT, które toouse protokołu w tym (względem hello dewelopera hello jest opcja prostą konfigurację).</span><span class="sxs-lookup"><span data-stu-id="ebd79-227">hello library handles hello details of communicating with IoT Hub, including which protocol toouse (from hello perspective of hello developer, this is a simple configuration option).</span></span>

<span data-ttu-id="ebd79-228">Witaj **IoTHubClient** Biblioteka również zapewnia precyzyjną kontrolę nad jak tooserialize hello dane urządzenie wysyła tooIoT koncentratora.</span><span class="sxs-lookup"><span data-stu-id="ebd79-228">hello **IoTHubClient** library also provides precise control over how tooserialize hello data your device sends tooIoT Hub.</span></span> <span data-ttu-id="ebd79-229">W niektórych przypadkach ten poziom kontroli jest korzyści, ale w innych jest szczegółów implementacji, które nie mają toobe zajęto się.</span><span class="sxs-lookup"><span data-stu-id="ebd79-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want toobe concerned with.</span></span> <span data-ttu-id="ebd79-230">Jeśli to hello case, warto rozważyć przy użyciu hello **serializator** biblioteki, który jest opisany w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="ebd79-230">If that's hello case, you might consider using hello **serializer** library, which is described in hello next section.</span></span>

## <a name="use-hello-serializer-library"></a><span data-ttu-id="ebd79-231">Użyj hello serializator biblioteki</span><span class="sxs-lookup"><span data-stu-id="ebd79-231">Use hello serializer library</span></span>

<span data-ttu-id="ebd79-232">Koncepcyjnie hello **serializator** biblioteki znajduje się na szczycie hello **IoTHubClient** biblioteki w hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="ebd79-232">Conceptually hello **serializer** library sits on top of hello **IoTHubClient** library in hello SDK.</span></span> <span data-ttu-id="ebd79-233">Używa hello **IoTHubClient** biblioteki hello bazowy komunikacji z Centrum IoT, ale dodaje modelowania możliwości, które usunąć obciążenia hello postępowania z serializacji komunikatu z hello developer.</span><span class="sxs-lookup"><span data-stu-id="ebd79-233">It uses hello **IoTHubClient** library for hello underlying communication with IoT Hub, but it adds modeling capabilities that remove hello burden of dealing with message serialization from hello developer.</span></span> <span data-ttu-id="ebd79-234">Jak działa ta biblioteka najlepsze dowodzą przykładem.</span><span class="sxs-lookup"><span data-stu-id="ebd79-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="ebd79-235">Witaj wewnątrz **serializator** folderu w hello [repozytorium azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c), jest **przykłady** folder, który zawiera aplikację o nazwie **simplesample \_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="ebd79-235">Inside hello **serializer** folder in hello [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="ebd79-236">wersja systemu Windows Hello tego przykładu obejmuje hello następujące rozwiązania Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ebd79-236">hello Windows version of this sample includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="ebd79-237">Po otwarciu tego projektu w programie Visual Studio 2017 zaakceptować hello monity tooretarget hello projektu toohello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="ebd79-237">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="ebd79-238">Podobnie jak w przypadku hello poprzedni przykład, ta obejmuje kilka pakietów NuGet:</span><span class="sxs-lookup"><span data-stu-id="ebd79-238">As with hello previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="ebd79-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="ebd79-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="ebd79-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="ebd79-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="ebd79-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="ebd79-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="ebd79-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="ebd79-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="ebd79-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="ebd79-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="ebd79-244">W tym samouczku większość tych pakietów hello powyższego przykładu, ale **Microsoft.Azure.IoTHub.Serializer** nowego.</span><span class="sxs-lookup"><span data-stu-id="ebd79-244">You've seen most of these packages in hello previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="ebd79-245">Ten pakiet jest wymagany, gdy używasz hello **serializator** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="ebd79-245">This package is required when you use hello **serializer** library.</span></span>

<span data-ttu-id="ebd79-246">Implementacja hello hello przykładowej aplikacji można znaleźć w hello **simplesample\_mqtt.c** pliku.</span><span class="sxs-lookup"><span data-stu-id="ebd79-246">You can find hello implementation of hello sample application in hello **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="ebd79-247">Hello następnych sekcjach opisano części klucza hello tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="ebd79-247">hello following sections walk you through hello key parts of this sample.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="ebd79-248">Zainicjowanie biblioteki hello</span><span class="sxs-lookup"><span data-stu-id="ebd79-248">Initialize hello library</span></span>

<span data-ttu-id="ebd79-249">Praca z hello toostart **serializator** biblioteki, inicjowanie hello wywołania interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="ebd79-249">toostart working with hello **serializer** library, call hello initialization APIs:</span></span>

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

<span data-ttu-id="ebd79-250">Witaj wywołania toohello **serializator\_init** funkcja jest wywołaniem jednorazowe i inicjuje hello podstawowej biblioteki.</span><span class="sxs-lookup"><span data-stu-id="ebd79-250">hello call toohello **serializer\_init** function is a one-time call and initializes hello underlying library.</span></span> <span data-ttu-id="ebd79-251">Następnie wywołaj metodę hello **IoTHubClient\_LL\_CreateFromConnectionString** funkcji, która jest hello tego samego interfejsu API tak jak hello **IoTHubClient** próbki.</span><span class="sxs-lookup"><span data-stu-id="ebd79-251">Then, you call hello **IoTHubClient\_LL\_CreateFromConnectionString** function, which is hello same API as in hello **IoTHubClient** sample.</span></span> <span data-ttu-id="ebd79-252">To wywołanie ustawia parametry połączenia urządzenia (to wywołanie jest również, gdzie należy wybrać protokół hello ma toouse).</span><span class="sxs-lookup"><span data-stu-id="ebd79-252">This call sets your device connection string (this call is also where you choose hello protocol you want toouse).</span></span> <span data-ttu-id="ebd79-253">W tym przykładzie używa MQTT jako hello transportu, ale można użyć protokołu AMQP i HTTP.</span><span class="sxs-lookup"><span data-stu-id="ebd79-253">This sample uses MQTT as hello transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="ebd79-254">Na koniec wywołania hello **Utwórz\_modelu\_wystąpienia** funkcji.</span><span class="sxs-lookup"><span data-stu-id="ebd79-254">Finally, call hello **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="ebd79-255">**WeatherStation** jest przestrzenią nazw hello hello modelu i **ContosoAnemometer** jest nazwą hello hello modelu.</span><span class="sxs-lookup"><span data-stu-id="ebd79-255">**WeatherStation** is hello namespace of hello model and **ContosoAnemometer** is hello name of hello model.</span></span> <span data-ttu-id="ebd79-256">Po utworzeniu hello wystąpienie modelu, można użyć toostart wysyłania i odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="ebd79-256">Once hello model instance is created, you can use it toostart sending and receiving messages.</span></span> <span data-ttu-id="ebd79-257">Jest jednak toounderstand ważne jest jakie modelu.</span><span class="sxs-lookup"><span data-stu-id="ebd79-257">However, it's important toounderstand what a model is.</span></span>

### <a name="define-hello-model"></a><span data-ttu-id="ebd79-258">Zdefiniuj hello modelu</span><span class="sxs-lookup"><span data-stu-id="ebd79-258">Define hello model</span></span>

<span data-ttu-id="ebd79-259">Model w hello **serializator** Biblioteka definiuje wiadomości powitania, które urządzenie może wysyłać tooIoT koncentratora i hello, o nazwie *akcje* w hello język, który może odbierać modelowania.</span><span class="sxs-lookup"><span data-stu-id="ebd79-259">A model in hello **serializer** library defines hello messages that your device can send tooIoT Hub and hello messages, called *actions* in hello modeling language, which it can receive.</span></span> <span data-ttu-id="ebd79-260">Zdefiniuj modelu przy użyciu zestawu makr C jak hello **simplesample\_mqtt** aplikacji przykładowej:</span><span class="sxs-lookup"><span data-stu-id="ebd79-260">You define a model using a set of C macros as in hello **simplesample\_mqtt** sample application:</span></span>

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

<span data-ttu-id="ebd79-261">Hello **rozpocząć\_przestrzeni nazw** i **zakończenia\_przestrzeni nazw** makra zarówno zająć hello przestrzeń nazw modelu hello jako argument.</span><span class="sxs-lookup"><span data-stu-id="ebd79-261">hello **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take hello namespace of hello model as an argument.</span></span> <span data-ttu-id="ebd79-262">Oczekuje się, że wszystko między tymi makra jest hello definicji modelu lub modeli i struktury danych hello korzystających z modeli hello.</span><span class="sxs-lookup"><span data-stu-id="ebd79-262">It's expected that anything between these macros is hello definition of your model or models, and hello data structures that hello models use.</span></span>

<span data-ttu-id="ebd79-263">W tym przykładzie jest pojedynczego modelu o nazwie **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="ebd79-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="ebd79-264">Ten model definiuje dwie części danych, czy urządzenie może wysyłać tooIoT Centrum: **DeviceId** i **prędkość wiatru**.</span><span class="sxs-lookup"><span data-stu-id="ebd79-264">This model defines two pieces of data that your device can send tooIoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="ebd79-265">Definiuje również trzy czynności (wiadomości), które urządzenia mogą odbierać: **TurnFanOn**, **TurnFanOff**, i **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="ebd79-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="ebd79-266">Każdy element danych ma typ, a każda akcja ma nazwę (i opcjonalnie zestaw parametrów).</span><span class="sxs-lookup"><span data-stu-id="ebd79-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="ebd79-267">Hello danych i akcje zdefiniowane w modelu hello definiują powierzchni interfejsu API Użyj toosend wiadomości tooIoT koncentratora, a urządzenie toohello toomessages wysyłane odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ebd79-267">hello data and actions defined in hello model define an API surface that you can use toosend messages tooIoT Hub, and respond toomessages sent toohello device.</span></span> <span data-ttu-id="ebd79-268">Użycie tego modelu najlepiej jest rozpoznawany przez przykładowy.</span><span class="sxs-lookup"><span data-stu-id="ebd79-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="ebd79-269">Wysyłanie wiadomości</span><span class="sxs-lookup"><span data-stu-id="ebd79-269">Send messages</span></span>

<span data-ttu-id="ebd79-270">Hello model definiuje hello danych, możesz wysłać tooIoT koncentratora.</span><span class="sxs-lookup"><span data-stu-id="ebd79-270">hello model defines hello data you can send tooIoT Hub.</span></span> <span data-ttu-id="ebd79-271">W tym przykładzie, oznacza to, co hello dwa elementy danych zdefiniowany przy użyciu hello **WITH_DATA** makra.</span><span class="sxs-lookup"><span data-stu-id="ebd79-271">In this example, that means one of hello two data items defined using hello **WITH_DATA** macro.</span></span> <span data-ttu-id="ebd79-272">Istnieje kilka czynności, wymagane toosend **DeviceId** i **prędkość wiatru** Centrum IoT tooan wartości.</span><span class="sxs-lookup"><span data-stu-id="ebd79-272">There are several steps required toosend **DeviceId** and **WindSpeed** values tooan IoT hub.</span></span> <span data-ttu-id="ebd79-273">Hello jest najpierw tooset hello dane, które mają toosend:</span><span class="sxs-lookup"><span data-stu-id="ebd79-273">hello first is tooset hello data you want toosend:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="ebd79-274">Hello model został zdefiniowany wcześniej pozwala tooset hello wartości przez ustawienie członkami **struktury**.</span><span class="sxs-lookup"><span data-stu-id="ebd79-274">hello model you defined earlier enables you tooset hello values by setting members of a **struct**.</span></span> <span data-ttu-id="ebd79-275">Następnie serializować wiadomość hello, które chcesz toosend:</span><span class="sxs-lookup"><span data-stu-id="ebd79-275">Next, serialize hello message you want toosend:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="ebd79-276">Ten kod serializuje hello buforu tooa urządzenia do chmury (odwołuje **docelowego**).</span><span class="sxs-lookup"><span data-stu-id="ebd79-276">This code serializes hello device-to-cloud tooa buffer (referenced by **destination**).</span></span> <span data-ttu-id="ebd79-277">Kod Hello następnie wywołuje hello **sendMessage** funkcji tooIoT wiadomość hello toosend Centrum:</span><span class="sxs-lookup"><span data-stu-id="ebd79-277">hello code then invokes hello **sendMessage** function toosend hello message tooIoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="ebd79-278">Witaj drugi parametr toolast **IoTHubClient\_LL\_SendEventAsync** jest odwołanie funkcji wywołania zwrotnego tooa jest wywoływane, gdy dane hello jest pomyślnie wysłane.</span><span class="sxs-lookup"><span data-stu-id="ebd79-278">hello second toolast parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference tooa callback function that's called when hello data is successfully sent.</span></span> <span data-ttu-id="ebd79-279">W tym miejscu jest funkcja wywołania zwrotnego hello w przykładowym hello:</span><span class="sxs-lookup"><span data-stu-id="ebd79-279">Here's hello callback function in hello sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="ebd79-280">drugi parametr Hello jest kontekst toouser wskaźnika; Witaj tego samego wskaźnik przekazany za**IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="ebd79-280">hello second parameter is a pointer toouser context; hello same pointer passed too**IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="ebd79-281">W takim przypadku kontekst hello jest prostego licznika, ale może być dowolny.</span><span class="sxs-lookup"><span data-stu-id="ebd79-281">In this case, hello context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="ebd79-282">To wszystko jest toosending wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="ebd79-282">That's all there is toosending device-to-cloud messages.</span></span> <span data-ttu-id="ebd79-283">Witaj tylko po lewej toocover jest to, jak tooreceive wiadomości.</span><span class="sxs-lookup"><span data-stu-id="ebd79-283">hello only thing left toocover is how tooreceive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="ebd79-284">Odbieranie komunikatów</span><span class="sxs-lookup"><span data-stu-id="ebd79-284">Receive messages</span></span>

<span data-ttu-id="ebd79-285">Odbieranie wiadomości działa podobnie sposób toohello komunikatów działa w hello **IoTHubClient** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="ebd79-285">Receiving a message works similarly toohello way messages work in hello **IoTHubClient** library.</span></span> <span data-ttu-id="ebd79-286">Najpierw należy zarejestrować funkcję wywołania zwrotnego komunikat:</span><span class="sxs-lookup"><span data-stu-id="ebd79-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="ebd79-287">Następnie napiszesz hello funkcja wywołania zwrotnego, które jest wywoływane, gdy wiadomość zostanie odebrana:</span><span class="sxs-lookup"><span data-stu-id="ebd79-287">Then, you write hello callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
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

<span data-ttu-id="ebd79-288">Ten kod jest standardowy — ma hello takie same dla dowolnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ebd79-288">This code is boilerplate -- it's hello same for any solution.</span></span> <span data-ttu-id="ebd79-289">Ta funkcja odbiera wiadomości powitania i zajmuje się rozsyłania jej toohello odpowiednią funkcję za pomocą wywołania hello zbyt**EXECUTE\_polecenia**.</span><span class="sxs-lookup"><span data-stu-id="ebd79-289">This function receives hello message and takes care of routing it toohello appropriate function through hello call too**EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="ebd79-290">wywołana funkcja Hello na tym etapie zależy od definicji hello hello działań w modelu.</span><span class="sxs-lookup"><span data-stu-id="ebd79-290">hello function called at this point depends on hello definition of hello actions in your model.</span></span>

<span data-ttu-id="ebd79-291">Po zdefiniowaniu akcji w modelu jest wymagana tooimplement funkcję, która jest wywoływana, gdy urządzenie otrzyma odpowiednia wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="ebd79-291">When you define an action in your model, you're required tooimplement a function that's called when your device receives hello corresponding message.</span></span> <span data-ttu-id="ebd79-292">Na przykład, jeśli model definiuje tej akcji:</span><span class="sxs-lookup"><span data-stu-id="ebd79-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="ebd79-293">Zdefiniuj funkcję z tego podpisu:</span><span class="sxs-lookup"><span data-stu-id="ebd79-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="ebd79-294">Należy zwrócić uwagę, jak nazwa hello funkcji hello odpowiada nazwie hello hello akcji w modelu hello a hello parametry funkcji hello są takie same parametry hello określone dla akcji hello.</span><span class="sxs-lookup"><span data-stu-id="ebd79-294">Note how hello name of hello function matches hello name of hello action in hello model and that hello parameters of hello function match hello parameters specified for hello action.</span></span> <span data-ttu-id="ebd79-295">pierwszy parametr Hello jest zawsze wymagane i zawiera wskaźnik toohello wystąpienie modelu.</span><span class="sxs-lookup"><span data-stu-id="ebd79-295">hello first parameter is always required and contains a pointer toohello instance of your model.</span></span>

<span data-ttu-id="ebd79-296">Witaj urządzenie otrzyma wiadomość pasującego do tego podpisu, jest nazywany hello odpowiednich funkcji.</span><span class="sxs-lookup"><span data-stu-id="ebd79-296">When hello device receives a message that matches this signature, hello corresponding function is called.</span></span> <span data-ttu-id="ebd79-297">W związku z tym jako uzupełnienie o tooinclude hello schematyczny kod z **IoTHubMessage**, odbierania wiadomości jest wystarczy zdefiniować funkcję proste dla każdej akcji zdefiniowanych w modelu.</span><span class="sxs-lookup"><span data-stu-id="ebd79-297">Therefore, aside from having tooinclude hello boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="ebd79-298">Odinicjalizuj hello biblioteki</span><span class="sxs-lookup"><span data-stu-id="ebd79-298">Uninitialize hello library</span></span>

<span data-ttu-id="ebd79-299">Po zakończeniu wysyłania danych i odbierania wiadomości, można uninitialize hello IoT biblioteki:</span><span class="sxs-lookup"><span data-stu-id="ebd79-299">When you're done sending data and receiving messages, you can uninitialize hello IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="ebd79-300">Każda z tych trzech funkcji wyrównana z hello trzech funkcji inicjowania opisanych powyżej.</span><span class="sxs-lookup"><span data-stu-id="ebd79-300">Each of these three functions aligns with hello three initialization functions described previously.</span></span> <span data-ttu-id="ebd79-301">Te interfejsy API do wywoływania zapewnia zwolnienie wcześniej przydzielone zasoby.</span><span class="sxs-lookup"><span data-stu-id="ebd79-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebd79-302">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ebd79-302">Next Steps</span></span>

<span data-ttu-id="ebd79-303">W tym artykule omówione podstawy hello przy użyciu bibliotek hello hello **urządzenia Azure IoT SDK dla języka C**. On udostępniony za mało toounderstand informacji dostępnych w hello zestawu SDK, jego architektury i jak tooget pracę z hello przykładów Windows.</span><span class="sxs-lookup"><span data-stu-id="ebd79-303">This article covered hello basics of using hello libraries in hello **Azure IoT device SDK for C**. It provided you with enough information toounderstand what's included in hello SDK, its architecture, and how tooget started working with hello Windows samples.</span></span> <span data-ttu-id="ebd79-304">kolejnym artykule Hello nadal hello opis hello zestawu SDK przez wyjaśniający [więcej informacji na temat biblioteki IoTHubClient hello](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="ebd79-304">hello next article continues hello description of hello SDK by explaining [more about hello IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="ebd79-305">toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz hello [Azure IoT SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="ebd79-305">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="ebd79-306">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="ebd79-306">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ebd79-307">[Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="ebd79-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
