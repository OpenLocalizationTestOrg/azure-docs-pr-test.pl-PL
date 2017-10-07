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
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="2ce8e-103">Eksploruj architektura krawędzi IoT Azure w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="2ce8e-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="2ce8e-104">Jak toorun hello próbki</span><span class="sxs-lookup"><span data-stu-id="2ce8e-104">How toorun hello sample</span></span>

<span data-ttu-id="2ce8e-105">Witaj **build.cmd** skrypt generuje dane wyjściowe w hello **kompilacji** folderu w lokalnej kopii hello **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-105">hello **build.cmd** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="2ce8e-106">Te dane wyjściowe obejmują Witaj dwie krawędzi IoT moduły używane w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="2ce8e-107">Witaj miejsca skryptu kompilacji **logger.dll** w hello **kompilacji\\modułów\\rejestratora\\debugowania** folderu i **hello\_world.dll**  w hello **kompilacji\\modułów\\hello_world\\debugowania** folderu.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-107">hello build script places **logger.dll** in hello **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in hello **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="2ce8e-108">Użyj tych ścieżek dla hello **ścieżka modułu** wartości, jak pokazano w hello następującego pliku ustawień JSON.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-108">Use these paths for hello **module path** values as shown in hello following JSON settings file.</span></span>

<span data-ttu-id="2ce8e-109">Witaj Witaj\_world\_próbki proces trwa hello pliku konfiguracji JSON tooa ścieżkę jako argument wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="2ce8e-110">Witaj następujący przykładowy plik JSON znajduje się w repozytorium SDK hello na **przykłady\\hello\_world\\src\\hello\_world\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-110">hello following example JSON file is provided in hello SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="2ce8e-111">Ta działa plik konfiguracji jest, chyba że zmodyfikujesz hello kompilacji skryptu tooplace hello krawędzi IoT modułów lub przykładowe pliki wykonywalne w lokalizacji innej niż domyślna.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="2ce8e-112">ścieżki modułu Hello są toohello względna katalogu, gdzie hello hello\_world\_znajduje się sample.exe.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-112">hello module paths are relative toohello directory where hello hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="2ce8e-113">przykład Witaj JSON konfiguracji pliku wartości domyślnych toowriting "log.txt" w bieżącym katalogu roboczym.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="2ce8e-114">Przejdź toohello **kompilacji** folderu w katalogu głównym hello kopii lokalnej hello **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="2ce8e-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="2ce8e-115">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2ce8e-115">Run hello following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
