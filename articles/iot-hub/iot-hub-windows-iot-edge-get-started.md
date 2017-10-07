---
title: "aaaGet wprowadzenie do usługi Azure IoT krawędzi (system Windows) | Dokumentacja firmy Microsoft"
description: "Jak toobuild brama brzegowa IoT Azure w systemie Windows komputera i Poznaj podstawowe pojęcia dotyczące usługi Azure IoT krawędzi takie jak moduły i pliki konfiguracyjne w formacie JSON."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 9aff3724-5e4e-40ec-b95a-d00df4f590c5
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5dd13cbfc02eeb55d9f2dbffca5021f2624acf14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a>Eksploruj architektura krawędzi IoT Azure w systemie Windows

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a>Jak toorun hello próbki

Witaj **build.cmd** skrypt generuje dane wyjściowe w hello **kompilacji** folderu w lokalnej kopii hello **krawędzi iot** repozytorium. Te dane wyjściowe obejmują Witaj dwie krawędzi IoT moduły używane w tym przykładzie.

Witaj miejsca skryptu kompilacji **logger.dll** w hello **kompilacji\\modułów\\rejestratora\\debugowania** folderu i **hello\_world.dll**  w hello **kompilacji\\modułów\\hello_world\\debugowania** folderu. Użyj tych ścieżek dla hello **ścieżka modułu** wartości, jak pokazano w hello następującego pliku ustawień JSON.

Witaj Witaj\_world\_próbki proces trwa hello pliku konfiguracji JSON tooa ścieżkę jako argument wiersza polecenia. Witaj następujący przykładowy plik JSON znajduje się w repozytorium SDK hello na **przykłady\\hello\_world\\src\\hello\_world\_win.json**. Ta działa plik konfiguracji jest, chyba że zmodyfikujesz hello kompilacji skryptu tooplace hello krawędzi IoT modułów lub przykładowe pliki wykonywalne w lokalizacji innej niż domyślna.

> [!NOTE]
> ścieżki modułu Hello są toohello względna katalogu, gdzie hello hello\_world\_znajduje się sample.exe. przykład Witaj JSON konfiguracji pliku wartości domyślnych toowriting "log.txt" w bieżącym katalogu roboczym.

```json
{
  "modules": [
    {
      "name": "logger",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
        }
      },
      "args": { "filename": "log.txt" }
    },
    {
      "name": "hello_world",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\hello_world\\Debug\\hello_world.dll"
        }
      },
      "args": null
      }
  ],
  "links": [
    {
      "source": "hello_world",
      "sink": "logger"
    }
  ]
}
```

1. Przejdź toohello **kompilacji** folderu w katalogu głównym hello kopii lokalnej hello **krawędzi iot** repozytorium.

1. Uruchom następujące polecenie hello:

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
