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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a>Połącz z toohello urządzenie zdalne monitorowanie wstępnie skonfigurowane rozwiązanie (system Windows)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a>Tworzenie rozwiązania próbki C w systemie Windows
Witaj następujące kroki pokazują, jak toocreate aplikacji klienckiej, która komunikuje się z monitorowania zdalnego hello wstępnie skonfigurowane rozwiązanie. Ta aplikacja jest napisany w języku C i wbudowane i uruchamianie w systemie Windows.

Utwórz projekt starter w programie Visual Studio 2015 lub Visual Studio 2017 i dodawanie pakietów NuGet hello Centrum IoT urządzenia klienta:

1. W programie Visual Studio Utwórz aplikację konsolową C za pomocą hello Visual C++ **aplikacji konsoli Win32** szablonu. Nazwa projektu hello **RMDevice**.
2. Na powitania **ustawienia aplikacji** strony w hello **Kreator aplikacji Win32**, upewnij się, że **aplikacja Konsolowa** jest zaznaczone, a następnie usuń zaznaczenie pola wyboru **Prekompilowanego nagłówek** i **sprawdza Security Development Lifecycle (SDL)**.
3. W **Eksploratora rozwiązań**, usunąć hello pliki stdafx.h, targetver.h i stdafx.cpp.
4. W **Eksploratora rozwiązań**, Zmień nazwę hello pliku RMDevice.cpp tooRMDevice.c.
5. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy na powitania **RMDevice** projektu, a następnie kliknij przycisk **pakiety zarządzania pakietami NuGet**. Kliknij przycisk **Przeglądaj**, następnie wyszukaj i zainstaluj następujące pakiety NuGet hello:
   
   * Microsoft.Azure.IoTHub.Serializer
   * Microsoft.Azure.IoTHub.IoTHubClient
   * Microsoft.Azure.IoTHub.MqttTransport
6. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy na powitania **RMDevice** projektu, a następnie kliknij przycisk **właściwości** tooopen hello projektu **strony właściwości**okno dialogowe. Aby uzyskać więcej informacji, zobacz [Ustawianie właściwości projektu Visual C++][lnk-c-project-properties]. 
7. Kliknij przycisk hello **konsolidatora** folderu, kliknij przycisk hello **danych wejściowych** strony właściwości.
8. Dodaj **crypt32.lib** toohello **dodatkowe zależności** właściwości. Kliknij przycisk **OK** , a następnie **OK** ponownie toosave hello projektu wartości właściwości.

Dodaj hello Parson JSON biblioteki toohello **RMDevice** projektu i dodać hello wymagane `#include` instrukcji:

1. Odpowiedniego folderu na komputerze klonowanie repozytorium Parson GitHub hello przy użyciu hello następujące polecenie:

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. Skopiuj pliki parson.h i parson.c hello z lokalną kopię hello Parson repozytorium tooyour hello **RMDevice** folderu projektu.

1. W programie Visual Studio, kliknij prawym przyciskiem myszy hello **RMDevice** projektu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **istniejący element**.

1. W hello **Dodaj istniejący element** okno dialogowe, wybierz hello parson.h i parson.c plików w hello **RMDevice** folderu projektu. Następnie kliknij przycisk **Dodaj** tooadd tych dwóch plików tooyour projektu.

1. W programie Visual Studio Otwórz plik RMDevice.c hello. Zamień istniejące hello `#include` instrukcji z hello następującego kodu:
   
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
    > Teraz możesz sprawdzić, czy projekt ma prawidłowe zależności hello przez skompilowanie go.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Tworzenie i uruchamianie przykładowych hello

Dodaj kod tooinvoke hello **zdalnego\_monitorowania\_Uruchom** funkcji, a następnie skompilować i uruchomić aplikację dla urządzeń hello.

1. Zastąp hello **głównego** funkcji z następującego kodu tooinvoke hello **zdalnego\_monitorowania\_Uruchom** funkcji:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Kliknij przycisk **kompilacji** , a następnie **Kompiluj rozwiązanie** toobuild hello urządzenia aplikacji.

1. W **Eksploratora rozwiązań**, powitania kliknij prawym przyciskiem myszy **RMDevice** projektu, kliknij przycisk **debugowania**, a następnie kliknij przycisk **Start nowe wystąpienie** toorun hello przykład. Hello konsoli są wyświetlane komunikaty hello aplikacja wyśle przykładowe dane telemetryczne toohello wstępnie skonfigurowane rozwiązanie, otrzymuje wartości żądanej właściwości ustawione na pulpicie nawigacyjnym rozwiązania hello i odpowiada toomethods wywoływane z poziomu pulpitu nawigacyjnego hello rozwiązania.

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
