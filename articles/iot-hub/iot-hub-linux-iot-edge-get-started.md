---
title: "aaaGet wprowadzenie do usługi Azure IoT krawędzi (Linux) | Dokumentacja firmy Microsoft"
description: "Jak toobuild bramy w systemie Linux maszyny i Poznaj podstawowe pojęcia dotyczące usługi Azure IoT krawędzi takie jak moduły i pliki konfiguracyjne w formacie JSON."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: cf537bdd-2352-4bb1-96cd-a283fcd3d6cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40aa9c8ddca6a974c361cbb0b453c7d0ddc71b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a>Eksplorowanie architektury usługi Azure IoT Edge w systemie Linux

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>Jak toorun hello próbki

Witaj **build.sh** skrypt generuje dane wyjściowe w hello **kompilacji** folderu w lokalnej kopii hello **krawędzi iot** repozytorium. Te dane wyjściowe obejmują Witaj dwie krawędzi IoT moduły używane w tym przykładzie.

Witaj miejsca skryptu kompilacji **liblogger.so** w hello **kompilacji/moduły/rejestratora/** folderu i **libhello\_world.so** w hello **kompilacji / Moduły/hello_world/** folderu. Użyj tych ścieżek dla hello **ścieżka modułu** wartości, jak pokazano w hello następującego przykładowego pliku ustawień JSON.

Witaj Witaj\_world\_próbki proces trwa hello ścieżki tooa JSON konfiguracji pliku argumentu wiersza polecenia. Witaj następujący przykładowy plik JSON znajduje się w repozytorium SDK hello na **przykłady/hello\_world/src/hello\_world\_lin.json**. Ta działa plik konfiguracji jest, chyba że zmodyfikujesz hello kompilacji skryptu tooplace hello krawędzi IoT modułów lub przykładowe pliki wykonywalne w lokalizacji innej niż domyślna.

> [!NOTE]
> Hello modułu jest ścieżek względnych toohello bieżący katalog roboczy, z jakiej lokalizacji hello hello\_world\_przykładowy plik wykonywalny jest uruchomiona, nie hello katalogu zawierającego hello pliku wykonywalnego. przykład Witaj JSON konfiguracji pliku wartości domyślnych toowriting "log.txt" w bieżącym katalogu roboczym.

```json
{
    "modules" :
    [
        {
            "name" : "logger",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args" : {"filename":"log.txt"}
        },
        {
            "name" : "hello_world",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/hello_world/libhello_world.so"
            }
            },
            "args" : null
        }
    ],
    "links":
    [
        {
            "source": "hello_world",
            "sink": "logger"
        }
    ]
}
```

1. Przejdź toohello **kompilacji** folderu w katalogu głównym hello kopii lokalnej hello **krawędzi iot** repozytorium.

1. Uruchom następujące polecenie hello:

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

