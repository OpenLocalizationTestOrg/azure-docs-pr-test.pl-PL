---
title: "Podłącz urządzenie za pomocą C w systemie Linux | Dokumentacja firmy Microsoft"
description: "Opisuje sposób podłącz urządzenie do wstępnie pakiet IoT Azure zdalnego monitorowania rozwiązania przy użyciu Aplikacja napisana w języku C uruchomiony w systemie Linux."
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
ms.openlocfilehash: 9adbc9cc13f0b4cafa3a3a7703c46f8085b15232
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="0121e-103">Podłącz urządzenie do zdalnego wstępnie skonfigurowane rozwiązanie monitorowania (Linux)</span><span class="sxs-lookup"><span data-stu-id="0121e-103">Connect your device to the remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="0121e-104">Tworzenie i uruchamianie przykładowych C klient systemu Linux</span><span class="sxs-lookup"><span data-stu-id="0121e-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="0121e-105">Poniższe kroki pokazują, jak utworzyć aplikację klienta, który komunikuje się ze zdalnym wstępnie skonfigurowane rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="0121e-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="0121e-106">Ta aplikacja jest napisany w języku C i wbudowane i uruchom na Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="0121e-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="0121e-107">Aby wykonać te kroki, należy na urządzenie z systemem Ubuntu wersji 15.04 lub 15.10.</span><span class="sxs-lookup"><span data-stu-id="0121e-107">To complete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="0121e-108">Przed kontynuowaniem należy zainstalować wstępnie wymagane pakiety na urządzenie Ubuntu przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0121e-108">Before proceeding, install the prerequisite packages on your Ubuntu device using the following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-the-client-libraries-on-your-device"></a><span data-ttu-id="0121e-109">Zainstaluj biblioteki klienta na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="0121e-109">Install the client libraries on your device</span></span>
<span data-ttu-id="0121e-110">Biblioteki klienta Centrum IoT Azure są dostępne w pakiecie można zainstalować przy użyciu urządzenia Ubuntu **stanie get** polecenia.</span><span class="sxs-lookup"><span data-stu-id="0121e-110">The Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using the **apt-get** command.</span></span> <span data-ttu-id="0121e-111">Wykonaj poniższe kroki, aby zainstalować pakiet, który zawiera Centrum IoT biblioteki i nagłówek pliki klienta na komputerze Ubuntu:</span><span class="sxs-lookup"><span data-stu-id="0121e-111">Complete the following steps to install the package that contains the IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="0121e-112">W powłoce Dodaj repozytorium AzureIoT do komputera:</span><span class="sxs-lookup"><span data-stu-id="0121e-112">In a shell, add the AzureIoT repository to your computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="0121e-113">Zainstaluj pakiet azure-iot-sdk-c deweloperów</span><span class="sxs-lookup"><span data-stu-id="0121e-113">Install the azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-the-parson-json-parser"></a><span data-ttu-id="0121e-114">Zainstaluj analizatora składni Parson JSON</span><span class="sxs-lookup"><span data-stu-id="0121e-114">Install the Parson JSON parser</span></span>
<span data-ttu-id="0121e-115">Centrum IoT bibliotek klienckich użyć analizatora składni Parson JSON do analizowania ładunek komunikatu.</span><span class="sxs-lookup"><span data-stu-id="0121e-115">The IoT Hub client libraries use the Parson JSON parser to parse message payloads.</span></span> <span data-ttu-id="0121e-116">W odpowiednich folderu na komputerze klonowanie repozytorium Parson GitHub przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0121e-116">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="0121e-117">Przygotowanie projektu</span><span class="sxs-lookup"><span data-stu-id="0121e-117">Prepare your project</span></span>
<span data-ttu-id="0121e-118">Na komputerze Ubuntu Utwórz folder o nazwie **zdalnego\_monitorowania**.</span><span class="sxs-lookup"><span data-stu-id="0121e-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="0121e-119">W **zdalnego\_monitorowania** folderu:</span><span class="sxs-lookup"><span data-stu-id="0121e-119">In the **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="0121e-120">Utwórz cztery pliki **main.c**, **zdalnego\_monitoring.c**, **zdalnego\_monitoring.h**, i **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="0121e-120">Create the four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="0121e-121">Utwórz folder o nazwie **parson**.</span><span class="sxs-lookup"><span data-stu-id="0121e-121">Create folder called **parson**.</span></span>

<span data-ttu-id="0121e-122">Skopiuj pliki **parson.c** i **parson.h** z kopii lokalnej do repozytorium Parson **zdalnego\_monitorowania parson** folderu.</span><span class="sxs-lookup"><span data-stu-id="0121e-122">Copy the files **parson.c** and **parson.h** from your local copy of the Parson repository into the **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="0121e-123">W edytorze tekstu Otwórz **zdalnego\_monitoring.c** pliku.</span><span class="sxs-lookup"><span data-stu-id="0121e-123">In a text editor, open the **remote\_monitoring.c** file.</span></span> <span data-ttu-id="0121e-124">Dodaj następujące instrukcje `#include`:</span><span class="sxs-lookup"><span data-stu-id="0121e-124">Add the following `#include` statements:</span></span>
   
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

## <a name="call-the-remotemonitoringrun-function"></a><span data-ttu-id="0121e-125">Wywołanie elementu zdalnego\_monitorowania\_uruchamiania funkcji</span><span class="sxs-lookup"><span data-stu-id="0121e-125">Call the remote\_monitoring\_run function</span></span>
<span data-ttu-id="0121e-126">W edytorze tekstu Otwórz **remote_monitoring.h** pliku.</span><span class="sxs-lookup"><span data-stu-id="0121e-126">In a text editor, open the **remote_monitoring.h** file.</span></span> <span data-ttu-id="0121e-127">Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="0121e-127">Add the following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="0121e-128">W edytorze tekstu Otwórz **main.c** pliku.</span><span class="sxs-lookup"><span data-stu-id="0121e-128">In a text editor, open the **main.c** file.</span></span> <span data-ttu-id="0121e-129">Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="0121e-129">Add the following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-the-application"></a><span data-ttu-id="0121e-130">Kompilowanie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0121e-130">Build and run the application</span></span>
<span data-ttu-id="0121e-131">W poniższych krokach opisano sposób użycia *CMake* do tworzenia aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="0121e-131">The following steps describe how to use *CMake* to build your client application.</span></span>

1. <span data-ttu-id="0121e-132">W edytorze tekstu Otwórz **CMakeLists.txt** w pliku **remote_monitoring** folderu.</span><span class="sxs-lookup"><span data-stu-id="0121e-132">In a text editor, open the **CMakeLists.txt** file in the **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="0121e-133">Dodaj następujące instrukcje, aby zdefiniować sposób kompilowania aplikacji klienta:</span><span class="sxs-lookup"><span data-stu-id="0121e-133">Add the following instructions to define how to build your client application:</span></span>
   
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
1. <span data-ttu-id="0121e-134">W **remote_monitoring** folderu, Utwórz folder do przechowywania *upewnij* pliki, które generuje CMake, a następnie uruchomić **cmake** i **upewnij** polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0121e-134">In the **remote_monitoring** folder, create a folder to store the *make* files that CMake generates and then run the **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="0121e-135">Uruchom aplikację klienta oraz wysyłania danych telemetrycznych do Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="0121e-135">Run the client application and send telemetry to IoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

