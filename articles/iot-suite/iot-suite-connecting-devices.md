---
title: "aaaConnect urządzenia za pomocą C w systemie Windows | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconnect toohello urządzenia pakiet IoT Azure wstępnie zdalnego rozwiązanie monitorowania przy użyciu Aplikacja napisana w języku C uruchomiony w systemie Windows."
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
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="42c9b-103">Połącz z toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie (system Windows)</span><span class="sxs-lookup"><span data-stu-id="42c9b-103">Connect your device toohello remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="42c9b-104">Tworzenie rozwiązania próbki C w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="42c9b-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="42c9b-105">Witaj następujące kroki pokazują, jak toocreate aplikacji klienckiej, która komunikuje się z monitorowania zdalnego hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="42c9b-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="42c9b-106">Ta aplikacja jest napisany w języku C i wbudowane i uruchamianie w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="42c9b-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="42c9b-107">Utwórz projekt starter w programie Visual Studio 2015 lub Visual Studio 2017 i dodawanie pakietów NuGet hello Centrum IoT urządzenia klienta:</span><span class="sxs-lookup"><span data-stu-id="42c9b-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add hello IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="42c9b-108">W programie Visual Studio Utwórz aplikację konsolową C za pomocą hello Visual C++ **aplikacji konsoli Win32** szablonu.</span><span class="sxs-lookup"><span data-stu-id="42c9b-108">In Visual Studio, create a C console application using hello Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="42c9b-109">Nazwa projektu hello **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="42c9b-109">Name hello project **RMDevice**.</span></span>
2. <span data-ttu-id="42c9b-110">Na powitania **ustawienia aplikacji** strony w hello **Kreator aplikacji Win32**, upewnij się, że **aplikacja Konsolowa** jest zaznaczone, a następnie usuń zaznaczenie pola wyboru **Prekompilowanego nagłówek** i **sprawdza Security Development Lifecycle (SDL)**.</span><span class="sxs-lookup"><span data-stu-id="42c9b-110">On hello **Application Settings** page in hello **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="42c9b-111">W **Eksploratora rozwiązań**, usunąć hello pliki stdafx.h, targetver.h i stdafx.cpp.</span><span class="sxs-lookup"><span data-stu-id="42c9b-111">In **Solution Explorer**, delete hello files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="42c9b-112">W **Eksploratora rozwiązań**, Zmień nazwę hello pliku RMDevice.cpp tooRMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="42c9b-112">In **Solution Explorer**, rename hello file RMDevice.cpp tooRMDevice.c.</span></span>
5. <span data-ttu-id="42c9b-113">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy na powitania **RMDevice** projektu, a następnie kliknij przycisk **pakiety zarządzania pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="42c9b-113">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="42c9b-114">Kliknij przycisk **Przeglądaj**, następnie wyszukaj i zainstaluj następujące pakiety NuGet hello:</span><span class="sxs-lookup"><span data-stu-id="42c9b-114">Click **Browse**, then search for and install hello following NuGet packages:</span></span>
   
   * <span data-ttu-id="42c9b-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="42c9b-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="42c9b-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="42c9b-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="42c9b-117">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="42c9b-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="42c9b-118">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy na powitania **RMDevice** projektu, a następnie kliknij przycisk **właściwości** tooopen hello projektu **strony właściwości**okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="42c9b-118">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Properties** tooopen hello project's **Property Pages** dialog box.</span></span> <span data-ttu-id="42c9b-119">Aby uzyskać więcej informacji, zobacz [Ustawianie właściwości projektu Visual C++][lnk-c-project-properties].</span><span class="sxs-lookup"><span data-stu-id="42c9b-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="42c9b-120">Kliknij przycisk hello **konsolidatora** folderu, kliknij przycisk hello **danych wejściowych** strony właściwości.</span><span class="sxs-lookup"><span data-stu-id="42c9b-120">Click hello **Linker** folder, then click hello **Input** property page.</span></span>
8. <span data-ttu-id="42c9b-121">Dodaj **crypt32.lib** toohello **dodatkowe zależności** właściwości.</span><span class="sxs-lookup"><span data-stu-id="42c9b-121">Add **crypt32.lib** toohello **Additional Dependencies** property.</span></span> <span data-ttu-id="42c9b-122">Kliknij przycisk **OK** , a następnie **OK** ponownie toosave hello projektu wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="42c9b-122">Click **OK** and then **OK** again toosave hello project property values.</span></span>

<span data-ttu-id="42c9b-123">Dodaj hello Parson JSON biblioteki toohello **RMDevice** projektu i dodać hello wymagane `#include` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="42c9b-123">Add hello Parson JSON library toohello **RMDevice** project and add hello required `#include` statements:</span></span>

1. <span data-ttu-id="42c9b-124">Odpowiedniego folderu na komputerze klonowanie repozytorium Parson GitHub hello przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="42c9b-124">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="42c9b-125">Skopiuj pliki parson.h i parson.c hello z lokalną kopię hello Parson repozytorium tooyour hello **RMDevice** folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="42c9b-125">Copy hello parson.h and parson.c files from hello local copy of hello Parson repository tooyour **RMDevice** project folder.</span></span>

1. <span data-ttu-id="42c9b-126">W programie Visual Studio, kliknij prawym przyciskiem myszy hello **RMDevice** projektu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="42c9b-126">In Visual Studio, right-click hello **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="42c9b-127">W hello **Dodaj istniejący element** okno dialogowe, wybierz hello parson.h i parson.c plików w hello **RMDevice** folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="42c9b-127">In hello **Add Existing Item** dialog, select hello parson.h and parson.c files in hello **RMDevice** project folder.</span></span> <span data-ttu-id="42c9b-128">Następnie kliknij przycisk **Dodaj** tooadd tych dwóch plików tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="42c9b-128">Then click **Add** tooadd these two files tooyour project.</span></span>

1. <span data-ttu-id="42c9b-129">W programie Visual Studio Otwórz plik RMDevice.c hello.</span><span class="sxs-lookup"><span data-stu-id="42c9b-129">In Visual Studio, open hello RMDevice.c file.</span></span> <span data-ttu-id="42c9b-130">Zamień istniejące hello `#include` instrukcji z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="42c9b-130">Replace hello existing `#include` statements with hello following code:</span></span>
   
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
    > <span data-ttu-id="42c9b-131">Teraz możesz sprawdzić, czy projekt ma prawidłowe zależności hello przez skompilowanie go.</span><span class="sxs-lookup"><span data-stu-id="42c9b-131">Now you can verify that your project has hello correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="42c9b-132">Tworzenie i uruchamianie przykładowych hello</span><span class="sxs-lookup"><span data-stu-id="42c9b-132">Build and run hello sample</span></span>

<span data-ttu-id="42c9b-133">Dodaj kod tooinvoke hello **zdalnego\_monitorowania\_Uruchom** funkcji, a następnie skompilować i uruchomić aplikację dla urządzeń hello.</span><span class="sxs-lookup"><span data-stu-id="42c9b-133">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="42c9b-134">Zastąp hello **głównego** funkcji z następującego kodu tooinvoke hello **zdalnego\_monitorowania\_Uruchom** funkcji:</span><span class="sxs-lookup"><span data-stu-id="42c9b-134">Replace hello **main** function with following code tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="42c9b-135">Kliknij przycisk **kompilacji** , a następnie **Kompiluj rozwiązanie** toobuild hello urządzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42c9b-135">Click **Build** and then **Build Solution** toobuild hello device application.</span></span>

1. <span data-ttu-id="42c9b-136">W **Eksploratora rozwiązań**, powitania kliknij prawym przyciskiem myszy **RMDevice** projektu, kliknij przycisk **debugowania**, a następnie kliknij przycisk **Start nowe wystąpienie** toorun hello przykład.</span><span class="sxs-lookup"><span data-stu-id="42c9b-136">In **Solution Explorer**, right-click hello **RMDevice** project, click **Debug**, and then click **Start new instance** toorun hello sample.</span></span> <span data-ttu-id="42c9b-137">Hello konsoli są wyświetlane komunikaty hello aplikacja wyśle przykładowe dane telemetryczne toohello wstępnie skonfigurowane rozwiązanie, otrzymuje wartości żądanej właściwości ustawione na pulpicie nawigacyjnym rozwiązania hello i odpowiada toomethods wywoływane z poziomu pulpitu nawigacyjnego hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="42c9b-137">hello console displays messages as hello application sends sample telemetry toohello preconfigured solution, receives desired property values set in hello solution dashboard, and responds toomethods invoked from hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
