---
title: "Podłącz urządzenie za pomocą C w systemie Windows | Dokumentacja firmy Microsoft"
description: "Opisuje sposób podłącz urządzenie do wstępnie pakiet IoT Azure zdalnego monitorowania rozwiązania przy użyciu Aplikacja napisana w języku C uruchomiony w systemie Windows."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: d222bcbd64f288d4091acb0ecd2922b9ceee57e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="c6e76-103">Podłącz urządzenie do zdalnego wstępnie skonfigurowane rozwiązanie monitorowania (system Windows)</span><span class="sxs-lookup"><span data-stu-id="c6e76-103">Connect your device to the remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="c6e76-104">Tworzenie rozwiązania próbki C w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="c6e76-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="c6e76-105">Poniższe kroki pokazują, jak utworzyć aplikację klienta, który komunikuje się ze zdalnym wstępnie skonfigurowane rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="c6e76-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="c6e76-106">Ta aplikacja jest napisany w języku C i wbudowane i uruchamianie w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="c6e76-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="c6e76-107">Utwórz projekt starter w programie Visual Studio 2015 lub Visual Studio 2017 i dodawanie pakietów NuGet Centrum IoT urządzenia klienta:</span><span class="sxs-lookup"><span data-stu-id="c6e76-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add the IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="c6e76-108">W programie Visual Studio Utwórz aplikację konsolową C za pomocą programu Visual C++ **aplikacji konsoli Win32** szablonu.</span><span class="sxs-lookup"><span data-stu-id="c6e76-108">In Visual Studio, create a C console application using the Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="c6e76-109">Nazwij projekt **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="c6e76-109">Name the project **RMDevice**.</span></span>
2. <span data-ttu-id="c6e76-110">Na **ustawienia aplikacji** strony **Kreator aplikacji Win32**, upewnij się, że **aplikacja Konsolowa** jest zaznaczone, a następnie usuń zaznaczenie pola wyboru **Prekompilowanego nagłówka** i **sprawdza Security Development Lifecycle (SDL)**.</span><span class="sxs-lookup"><span data-stu-id="c6e76-110">On the **Application Settings** page in the **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="c6e76-111">W **Eksploratora rozwiązań**, Usuń pliki stdafx.h, targetver.h i stdafx.cpp.</span><span class="sxs-lookup"><span data-stu-id="c6e76-111">In **Solution Explorer**, delete the files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="c6e76-112">W **Eksploratora rozwiązań**, Zmień nazwę pliku RMDevice.cpp na RMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="c6e76-112">In **Solution Explorer**, rename the file RMDevice.cpp to RMDevice.c.</span></span>
5. <span data-ttu-id="c6e76-113">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **RMDevice** projektu, a następnie kliknij przycisk **pakiety zarządzania pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c6e76-113">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="c6e76-114">Kliknij przycisk **Przeglądaj**, następnie wyszukaj i zainstaluj następujące pakiety NuGet:</span><span class="sxs-lookup"><span data-stu-id="c6e76-114">Click **Browse**, then search for and install the following NuGet packages:</span></span>
   
   * <span data-ttu-id="c6e76-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="c6e76-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="c6e76-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="c6e76-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="c6e76-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="c6e76-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="c6e76-118">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **RMDevice** projektu, a następnie kliknij przycisk **właściwości** można otworzyć projektu **strony właściwości** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="c6e76-118">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Properties** to open the project's **Property Pages** dialog box.</span></span> <span data-ttu-id="c6e76-119">Aby uzyskać więcej informacji, zobacz [Ustawianie właściwości projektu Visual C++][lnk-c-project-properties].</span><span class="sxs-lookup"><span data-stu-id="c6e76-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="c6e76-120">Kliknij przycisk **konsolidatora** folderu, następnie kliknij przycisk **dane wejściowe** strony właściwości.</span><span class="sxs-lookup"><span data-stu-id="c6e76-120">Click the **Linker** folder, then click the **Input** property page.</span></span>
8. <span data-ttu-id="c6e76-121">Dodaj **crypt32.lib** do **dodatkowe zależności** właściwości.</span><span class="sxs-lookup"><span data-stu-id="c6e76-121">Add **crypt32.lib** to the **Additional Dependencies** property.</span></span> <span data-ttu-id="c6e76-122">Kliknij przycisk **OK** , a następnie **OK** ponownie, aby zapisać wartości właściwości projektu.</span><span class="sxs-lookup"><span data-stu-id="c6e76-122">Click **OK** and then **OK** again to save the project property values.</span></span>

<span data-ttu-id="c6e76-123">Dodaj bibliotekę Parson JSON do **RMDevice** projektu i Dodaj wymagane `#include` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="c6e76-123">Add the Parson JSON library to the **RMDevice** project and add the required `#include` statements:</span></span>

1. <span data-ttu-id="c6e76-124">W odpowiednich folderu na komputerze klonowanie repozytorium Parson GitHub przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="c6e76-124">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="c6e76-125">Skopiuj pliki parson.h i parson.c z lokalną kopię do repozytorium Parson Twojego **RMDevice** folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="c6e76-125">Copy the parson.h and parson.c files from the local copy of the Parson repository to your **RMDevice** project folder.</span></span>

1. <span data-ttu-id="c6e76-126">W programie Visual Studio, kliknij prawym przyciskiem myszy **RMDevice** projektu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="c6e76-126">In Visual Studio, right-click the **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="c6e76-127">W **Dodaj istniejący element** okno dialogowe, wybierz opcję parson.h i parson.c plików **RMDevice** folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="c6e76-127">In the **Add Existing Item** dialog, select the parson.h and parson.c files in the **RMDevice** project folder.</span></span> <span data-ttu-id="c6e76-128">Następnie kliknij przycisk **Dodaj** do dodania tych plików do projektu.</span><span class="sxs-lookup"><span data-stu-id="c6e76-128">Then click **Add** to add these two files to your project.</span></span>

1. <span data-ttu-id="c6e76-129">W programie Visual Studio Otwórz plik RMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="c6e76-129">In Visual Studio, open the RMDevice.c file.</span></span> <span data-ttu-id="c6e76-130">Zastąp istniejące `#include` instrukcje następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="c6e76-130">Replace the existing `#include` statements with the following code:</span></span>
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > <span data-ttu-id="c6e76-131">Teraz możesz sprawdzić, czy projekt ma prawidłowe zależności przez skompilowanie go.</span><span class="sxs-lookup"><span data-stu-id="c6e76-131">Now you can verify that your project has the correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="c6e76-132">Tworzenie i uruchamianie próbki</span><span class="sxs-lookup"><span data-stu-id="c6e76-132">Build and run the sample</span></span>

<span data-ttu-id="c6e76-133">Dodaj kod, aby wywołać **zdalnego\_monitorowania\_Uruchom** funkcji, a następnie skompilować i uruchomić aplikację dla urządzeń.</span><span class="sxs-lookup"><span data-stu-id="c6e76-133">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="c6e76-134">Zastąp **głównego** funkcji z następujący kod, aby wywołać **zdalnego\_monitorowania\_Uruchom** funkcji:</span><span class="sxs-lookup"><span data-stu-id="c6e76-134">Replace the **main** function with following code to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="c6e76-135">Kliknij przycisk **kompilacji** , a następnie **Kompiluj rozwiązanie** do skompilowania aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c6e76-135">Click **Build** and then **Build Solution** to build the device application.</span></span>

1. <span data-ttu-id="c6e76-136">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **RMDevice** projektu, kliknij przycisk **debugowania**, a następnie kliknij przycisk **Start nowe wystąpienie** do uruchomienia przykładu.</span><span class="sxs-lookup"><span data-stu-id="c6e76-136">In **Solution Explorer**, right-click the **RMDevice** project, click **Debug**, and then click **Start new instance** to run the sample.</span></span> <span data-ttu-id="c6e76-137">W konsoli są wyświetlane komunikaty aplikacji wysyła dane telemetryczne próbki do wstępnie skonfigurowane rozwiązanie, otrzymuje wartości żądanej właściwości ustawione na pulpicie nawigacyjnym rozwiązania i odpowiada metody wywoływane z poziomu pulpitu nawigacyjnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c6e76-137">The console displays messages as the application sends sample telemetry to the preconfigured solution, receives desired property values set in the solution dashboard, and responds to methods invoked from the solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
