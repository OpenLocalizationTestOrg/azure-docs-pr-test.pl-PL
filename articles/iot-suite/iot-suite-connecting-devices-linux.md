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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a>Połącz z toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie (Linux)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a>Tworzenie i uruchamianie przykładowych C klient systemu Linux
Witaj następujące kroki pokazują, jak toocreate aplikacji klienckiej, która komunikuje się z monitorowania zdalnego hello wstępnie skonfigurowane rozwiązanie. Ta aplikacja jest napisany w języku C i wbudowane i uruchom na Ubuntu Linux.

toocomplete tych kroków, należy na urządzenie z systemem Ubuntu wersji 15.04 lub 15.10. Przed kontynuowaniem należy zainstalować pakiety wymagań wstępnych hello na urządzeniu Ubuntu przy użyciu hello następujące polecenie:

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a>Zainstaluj bibliotek klienckich hello na urządzeniu
Witaj bibliotek klienckich Centrum IoT Azure są dostępne w pakiecie można zainstalować na urządzeniu Ubuntu przy użyciu hello **stanie get** polecenia. Wykonaj następujące kroki tooinstall hello pakiet, który zawiera hello biblioteki klienta Centrum IoT i pliki nagłówkowe na komputerze Ubuntu hello:

1. W powłoce Dodaj hello AzureIoT repozytorium tooyour komputera:
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. Zainstaluj pakiet azure-iot-sdk-c deweloperów hello
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a>Zainstaluj hello analizatora składni Parson JSON
powitania klienta Centrum IoT bibliotek używają hello ładunków komunikat tooparse analizator Parson JSON. Odpowiedniego folderu na komputerze klonowanie repozytorium Parson GitHub hello przy użyciu hello następujące polecenie:

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a>Przygotowanie projektu
Na komputerze Ubuntu Utwórz folder o nazwie **zdalnego\_monitorowania**. W hello **zdalnego\_monitorowania** folderu:

- Utwórz cztery pliki hello **main.c**, **zdalnego\_monitoring.c**, **zdalnego\_monitoring.h**, i **CMakeLists.txt**.
- Utwórz folder o nazwie **parson**.

Skopiuj pliki hello **parson.c** i **parson.h** z lokalną kopię hello Parson repozytorium do hello **zdalnego\_monitorowania parson** folderu.

W edytorze tekstu Otwórz hello **zdalnego\_monitoring.c** pliku. Dodaj następujące hello `#include` instrukcji:
   
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

## <a name="call-hello-remotemonitoringrun-function"></a>Wywołaj hello zdalnego\_monitorowania\_uruchamiania funkcji
W edytorze tekstu Otwórz hello **remote_monitoring.h** pliku. Dodaj hello następującego kodu:

```
void remote_monitoring_run(void);
```

W edytorze tekstu Otwórz hello **main.c** pliku. Dodaj hello następującego kodu:

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a>Tworzenie i uruchamianie aplikacji hello
Witaj poniższych krokach opisano sposób toouse *CMake* toobuild aplikacji klienta.

1. W edytorze tekstu Otwórz hello **CMakeLists.txt** pliku w hello **remote_monitoring** folderu.

1. Dodaj następujące instrukcje toodefine jak hello toobuild aplikacji klienta:
   
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
1. W hello **remote_monitoring** folderu, Utwórz hello toostore folderu *upewnij* pliki tego CMake generuje, a następnie uruchom hello **cmake** i **należy** polecenia w następujący sposób:
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. Uruchom aplikację kliencką hello i wysyłania danych telemetrycznych tooIoT Centrum:
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

