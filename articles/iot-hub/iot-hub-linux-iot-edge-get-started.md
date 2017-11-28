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
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="1a560-103">Eksplorowanie architektury usługi Azure IoT Edge w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="1a560-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="1a560-104">Jak toorun hello próbki</span><span class="sxs-lookup"><span data-stu-id="1a560-104">How toorun hello sample</span></span>

<span data-ttu-id="1a560-105">Witaj **build.sh** skrypt generuje dane wyjściowe w hello **kompilacji** folderu w lokalnej kopii hello **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="1a560-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="1a560-106">Te dane wyjściowe obejmują Witaj dwie krawędzi IoT moduły używane w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="1a560-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="1a560-107">Witaj miejsca skryptu kompilacji **liblogger.so** w hello **kompilacji/moduły/rejestratora/** folderu i **libhello\_world.so** w hello **kompilacji / Moduły/hello_world/** folderu.</span><span class="sxs-lookup"><span data-stu-id="1a560-107">hello build script places **liblogger.so** in hello **build/modules/logger/** folder and **libhello\_world.so** in hello **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="1a560-108">Użyj tych ścieżek dla hello **ścieżka modułu** wartości, jak pokazano w hello następującego przykładowego pliku ustawień JSON.</span><span class="sxs-lookup"><span data-stu-id="1a560-108">Use these paths for hello **module path** values as shown in hello following example JSON settings file.</span></span>

<span data-ttu-id="1a560-109">Witaj Witaj\_world\_próbki proces trwa hello ścieżki tooa JSON konfiguracji pliku argumentu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="1a560-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file a command-line argument.</span></span> <span data-ttu-id="1a560-110">Witaj następujący przykładowy plik JSON znajduje się w repozytorium SDK hello na **przykłady/hello\_world/src/hello\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="1a560-110">hello following example JSON file is provided in hello SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="1a560-111">Ta działa plik konfiguracji jest, chyba że zmodyfikujesz hello kompilacji skryptu tooplace hello krawędzi IoT modułów lub przykładowe pliki wykonywalne w lokalizacji innej niż domyślna.</span><span class="sxs-lookup"><span data-stu-id="1a560-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="1a560-112">Hello modułu jest ścieżek względnych toohello bieżący katalog roboczy, z jakiej lokalizacji hello hello\_world\_przykładowy plik wykonywalny jest uruchomiona, nie hello katalogu zawierającego hello pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="1a560-112">hello module paths are relative toohello current working directory from where hello hello\_world\_sample executable is launched, not hello directory where hello executable is located.</span></span> <span data-ttu-id="1a560-113">przykład Witaj JSON konfiguracji pliku wartości domyślnych toowriting "log.txt" w bieżącym katalogu roboczym.</span><span class="sxs-lookup"><span data-stu-id="1a560-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="1a560-114">Przejdź toohello **kompilacji** folderu w katalogu głównym hello kopii lokalnej hello **krawędzi iot** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="1a560-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="1a560-115">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="1a560-115">Run hello following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

