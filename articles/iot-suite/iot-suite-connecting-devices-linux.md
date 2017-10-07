---
title: "aaaConnect urządzenia za pomocą C w systemie Linux | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconnect toohello urządzenia pakiet IoT Azure wstępnie zdalnego rozwiązanie monitorowania przy użyciu Aplikacja napisana w języku C uruchomiony w systemie Linux."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0c7c8039-0bbf-4bb5-9e79-ed8cff433629
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57393817d40d3555177956a01fa71058bc256988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="871c5-103">Połącz z toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie (Linux)</span><span class="sxs-lookup"><span data-stu-id="871c5-103">Connect your device toohello remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="871c5-104">Tworzenie i uruchamianie przykładowych C klient systemu Linux</span><span class="sxs-lookup"><span data-stu-id="871c5-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="871c5-105">Witaj następujące kroki pokazują, jak toocreate aplikacji klienckiej, która komunikuje się z monitorowania zdalnego hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="871c5-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="871c5-106">Ta aplikacja jest napisany w języku C i wbudowane i uruchom na Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="871c5-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="871c5-107">toocomplete tych kroków, należy na urządzenie z systemem Ubuntu wersji 15.04 lub 15.10.</span><span class="sxs-lookup"><span data-stu-id="871c5-107">toocomplete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="871c5-108">Przed kontynuowaniem należy zainstalować pakiety wymagań wstępnych hello na urządzeniu Ubuntu przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="871c5-108">Before proceeding, install hello prerequisite packages on your Ubuntu device using hello following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a><span data-ttu-id="871c5-109">Zainstaluj bibliotek klienckich hello na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="871c5-109">Install hello client libraries on your device</span></span>
<span data-ttu-id="871c5-110">Witaj bibliotek klienckich Centrum IoT Azure są dostępne w pakiecie można zainstalować na urządzeniu Ubuntu przy użyciu hello **stanie get** polecenia.</span><span class="sxs-lookup"><span data-stu-id="871c5-110">hello Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using hello **apt-get** command.</span></span> <span data-ttu-id="871c5-111">Wykonaj następujące kroki tooinstall hello pakiet, który zawiera hello biblioteki klienta Centrum IoT i pliki nagłówkowe na komputerze Ubuntu hello:</span><span class="sxs-lookup"><span data-stu-id="871c5-111">Complete hello following steps tooinstall hello package that contains hello IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="871c5-112">W powłoce Dodaj hello AzureIoT repozytorium tooyour komputera:</span><span class="sxs-lookup"><span data-stu-id="871c5-112">In a shell, add hello AzureIoT repository tooyour computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="871c5-113">Zainstaluj pakiet azure-iot-sdk-c deweloperów hello</span><span class="sxs-lookup"><span data-stu-id="871c5-113">Install hello azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a><span data-ttu-id="871c5-114">Zainstaluj hello analizatora składni Parson JSON</span><span class="sxs-lookup"><span data-stu-id="871c5-114">Install hello Parson JSON parser</span></span>
<span data-ttu-id="871c5-115">powitania klienta Centrum IoT bibliotek używają hello ładunków komunikat tooparse analizator Parson JSON.</span><span class="sxs-lookup"><span data-stu-id="871c5-115">hello IoT Hub client libraries use hello Parson JSON parser tooparse message payloads.</span></span> <span data-ttu-id="871c5-116">Odpowiedniego folderu na komputerze klonowanie repozytorium Parson GitHub hello przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="871c5-116">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="871c5-117">Przygotowanie projektu</span><span class="sxs-lookup"><span data-stu-id="871c5-117">Prepare your project</span></span>
<span data-ttu-id="871c5-118">Na komputerze Ubuntu Utwórz folder o nazwie **zdalnego\_monitorowania**.</span><span class="sxs-lookup"><span data-stu-id="871c5-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="871c5-119">W hello **zdalnego\_monitorowania** folderu:</span><span class="sxs-lookup"><span data-stu-id="871c5-119">In hello **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="871c5-120">Utwórz cztery pliki hello **main.c**, **zdalnego\_monitoring.c**, **zdalnego\_monitoring.h**, i **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="871c5-120">Create hello four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="871c5-121">Utwórz folder o nazwie **parson**.</span><span class="sxs-lookup"><span data-stu-id="871c5-121">Create folder called **parson**.</span></span>

<span data-ttu-id="871c5-122">Skopiuj pliki hello **parson.c** i **parson.h** z lokalną kopię hello Parson repozytorium do hello **zdalnego\_monitorowania parson** folderu.</span><span class="sxs-lookup"><span data-stu-id="871c5-122">Copy hello files **parson.c** and **parson.h** from your local copy of hello Parson repository into hello **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="871c5-123">W edytorze tekstu Otwórz hello **zdalnego\_monitoring.c** pliku.</span><span class="sxs-lookup"><span data-stu-id="871c5-123">In a text editor, open hello **remote\_monitoring.c** file.</span></span> <span data-ttu-id="871c5-124">Dodaj następujące hello `#include` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="871c5-124">Add hello following `#include` statements:</span></span>
   
```
#include "iothubtransportmqtt.h"
#include "schemalib.h"
#include "iothub_client.h"
#include "serializer_devicetwin.h"
#include "schemaserializer.h"
#include "azure_c_shared_utility/threadapi.h"
#include "azure_c_shared_utility/platform.h"
#include "parson.h"
```

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="call-hello-remotemonitoringrun-function"></a><span data-ttu-id="871c5-125">Wywołaj hello zdalnego\_monitorowania\_uruchamiania funkcji</span><span class="sxs-lookup"><span data-stu-id="871c5-125">Call hello remote\_monitoring\_run function</span></span>
<span data-ttu-id="871c5-126">W edytorze tekstu Otwórz hello **remote_monitoring.h** pliku.</span><span class="sxs-lookup"><span data-stu-id="871c5-126">In a text editor, open hello **remote_monitoring.h** file.</span></span> <span data-ttu-id="871c5-127">Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="871c5-127">Add hello following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="871c5-128">W edytorze tekstu Otwórz hello **main.c** pliku.</span><span class="sxs-lookup"><span data-stu-id="871c5-128">In a text editor, open hello **main.c** file.</span></span> <span data-ttu-id="871c5-129">Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="871c5-129">Add hello following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a><span data-ttu-id="871c5-130">Tworzenie i uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="871c5-130">Build and run hello application</span></span>
<span data-ttu-id="871c5-131">Witaj poniższych krokach opisano sposób toouse *CMake* toobuild aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="871c5-131">hello following steps describe how toouse *CMake* toobuild your client application.</span></span>

1. <span data-ttu-id="871c5-132">W edytorze tekstu Otwórz hello **CMakeLists.txt** pliku w hello **remote_monitoring** folderu.</span><span class="sxs-lookup"><span data-stu-id="871c5-132">In a text editor, open hello **CMakeLists.txt** file in hello **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="871c5-133">Dodaj następujące instrukcje toodefine jak hello toobuild aplikacji klienta:</span><span class="sxs-lookup"><span data-stu-id="871c5-133">Add hello following instructions toodefine how toobuild your client application:</span></span>
   
    ```
    macro(compileAsC99)
      if (CMAKE_VERSION VERSION_LESS "3.1")
        if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
          set (CMAKE_C_FLAGS "--std=c99 ${CMAKE_C_FLAGS}")
          set (CMAKE_CXX_FLAGS "--std=c++11 ${CMAKE_CXX_FLAGS}")
        endif()
      else()
        set (CMAKE_C_STANDARD 99)
        set (CMAKE_CXX_STANDARD 11)
      endif()
    endmacro(compileAsC99)

    cmake_minimum_required(VERSION 2.8.11)
    compileAsC99()

    set(AZUREIOT_INC_FOLDER "${CMAKE_SOURCE_DIR}" "${CMAKE_SOURCE_DIR}/parson" "/usr/include/azureiot" "/usr/include/azureiot/inc")

    include_directories(${AZUREIOT_INC_FOLDER})

    set(sample_application_c_files
        ./parson/parson.c
        ./remote_monitoring.c
        ./main.c
    )

    set(sample_application_h_files
        ./parson/parson.h
        ./remote_monitoring.h
    )

    add_executable(sample_app ${sample_application_c_files} ${sample_application_h_files})

    target_link_libraries(sample_app
        serializer
        iothub_client
        iothub_client_mqtt_transport
        aziotsharedutil
        umqtt
        pthread
        curl
        ssl
        crypto
        m
    )
    ```
1. <span data-ttu-id="871c5-134">W hello **remote_monitoring** folderu, Utwórz hello toostore folderu *upewnij* pliki tego CMake generuje, a następnie uruchom hello **cmake** i **należy** polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="871c5-134">In hello **remote_monitoring** folder, create a folder toostore hello *make* files that CMake generates and then run hello **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="871c5-135">Uruchom aplikację kliencką hello i wysyłania danych telemetrycznych tooIoT Centrum:</span><span class="sxs-lookup"><span data-stu-id="871c5-135">Run hello client application and send telemetry tooIoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

