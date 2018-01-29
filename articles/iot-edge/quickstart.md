---
title: "Szybki Start Azure IoT krawędzi + Windows | Dokumentacja firmy Microsoft"
description: "Wypróbować usługę Azure IoT krawędzi, uruchamiając analytics na urządzeniu symulowane krawędzi"
services: iot-edge
keywords: 
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 11/15/2017
ms.topic: article
ms.service: iot-edge
ms.openlocfilehash: 17675f870a015e86f98bf286a9b1c2bbc05c16cd
ms.sourcegitcommit: 933af6219266cc685d0c9009f533ca1be03aa5e9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2017
---
# <a name="quickstart-deploy-your-first-iot-edge-module-from-the-azure-portal-to-a-windows-device---preview"></a>Szybki Start: Wdrażanie modułu pierwszy krawędzi IoT z portalu Azure do urządzenia z systemem Windows — w wersji preview

W tym Szybki Start Użyj interfejsu chmury Azure IoT krawędzi do zdalnego wdrożenia kodu wbudowane urządzenia IoT. Aby wykonać to zadanie, należy najpierw użyć urządzenia z systemem Windows do symulacji urządzenia IoT, następnie można wdrożyć modułu do niego.

Jeśli nie masz aktywnych subskrypcji platformy Azure, Utwórz [bezpłatne konto] [ lnk-account] przed rozpoczęciem.

## <a name="prerequisites"></a>Wymagania wstępne

Ten samouczek zakłada, że używasz komputera lub maszyny wirtualnej z systemem Windows do symulacji urządzenia Internetu rzeczy. Jeśli korzystasz z systemu Windows na maszynie wirtualnej, należy włączyć [zagnieżdżonych wirtualizacji] [ lnk-nested] i przydziel co najmniej 2 GB pamięci RAM. 

1. Upewnij się, że używasz wersji systemu Windows:
   * Windows 10 
   * Windows Server
2. Zainstaluj [Docker dla systemu Windows] [ lnk-docker] i upewnij się, że jest uruchomiona.
3. Zainstaluj [Python 2.7 w systemie Windows] [ lnk-python] i upewnij się, możesz użyć polecenia pip.
4. Uruchom następujące polecenie, aby pobrać skryptu kontroli IoT krawędzi.

   ```
   pip install -U azure-iot-edge-runtime-ctl
   ```

> [!NOTE]
> Kontenery systemu Windows lub Linux kontenerów, można uruchomić Azure IoT krawędzi. Aby użyć kontenery systemu Windows, należy uruchomić:
>    * Windows 10 twórców spadku zaktualizować, lub
>    * Windows Server (kompilacja 16299) 1709, lub
>    * Windows IoT Core (16299 kompilacji) na urządzenia z systemem x64
>
> Dla systemu Windows IoT Core, postępuj zgodnie z instrukcjami [zainstaluj środowisko uruchomieniowe IoT Edge w systemie Windows IoT Core][lnk-install-iotcore]. W przeciwnym razie po prostu [skonfigurować Docker na używanie kontenerów Windows][lnk-docker-containers]i opcjonalnie zweryfikować Twoje wymagania wstępne przy użyciu następującego polecenia programu powershell:
>    ```
>    Invoke-Expression (Invoke-WebRequest -useb https://aka.ms/iotedgewin)
>    ```

## <a name="create-an-iot-hub-with-azure-cli"></a>Tworzenie Centrum IoT z wiersza polecenia platformy Azure

Utwórz Centrum IoT w Twojej subskrypcji platformy Azure. Poziom wolnego Centrum IoT działa w przypadku tego przewodnika Szybki Start. Jeśli używano Centrum IoT w przeszłości i już koncentratora wolnego utworzony, można pominąć tę sekcję i przejdź do [zarejestrować urządzenia IoT][anchor-register]. Każda subskrypcja może mieć tylko jeden bezpłatne Centrum IoT. 

1. Zaloguj się w witrynie [Azure Portal][lnk-portal]. 
1. Wybierz **powłoki chmury** przycisku. 

   ![Przycisk powłoki w chmurze][1]

1. Utwórz grupę zasobów. Poniższy kod tworzy grupę zasobów o nazwie **IoTEdge** w **zachodnie stany USA** regionu:

   ```azurecli
   az group create --name IoTEdge --location westus
   ```

1. Utwórz Centrum IoT w nowej grupy zasobów. Poniższy kod tworzy bezpłatny **F1** koncentratora o nazwie **MyIotHub** w grupie zasobów **IoTEdge**:

   ```azurecli
   az iot hub create --resource-group IoTEdge --name MyIotHub --sku F1 
   ```

## <a name="register-an-iot-edge-device"></a>Zarejestruj urządzenia IoT

[!INCLUDE [iot-edge-register-device](../../includes/iot-edge-register-device.md)]

## <a name="configure-the-iot-edge-runtime"></a>Konfigurowanie środowiska uruchomieniowego krawędzi IoT

Środowisko uruchomieniowe krawędzi IoT jest wdrażana na wszystkich urządzeniach IoT krawędzi. Zawiera dwa moduły. Najpierw agenta krawędzi IoT ułatwia wdrażanie i monitorowanie modułów na urządzeniu IoT krawędzi. Po drugie Centrum IoT krawędzi zarządza komunikacji między modułami na urządzeniu IoT krawędzi i między urządzeniami a Centrum IoT. 

Konfigurowanie środowiska uruchomieniowego z parametrów połączenia urządzenia IoT krawędzi z poprzedniej sekcji.

```
iotedgectl setup --connection-string "{device connection string}" --auto-cert-gen-force-no-passwords
```

Uruchom środowisko uruchomieniowe.

```
iotedgectl start
```

Sprawdź Docker, aby zobaczyć, czy agent krawędzi IoT jest uruchomiony jako moduł.

```
docker ps
```

![Zobacz edgeAgent w Docker](./media/tutorial-simulate-device-windows/docker-ps.png)

## <a name="deploy-a-module"></a>Wdrażanie modułu

[!INCLUDE [iot-edge-deploy-module](../../includes/iot-edge-deploy-module.md)]

## <a name="view-generated-data"></a>Widok wygenerowany danych

W tego przewodnika Szybki Start utworzyć nowe urządzenie brzegowe IoT, a na nim zainstalowany środowiska uruchomieniowego IoT krawędzi. Następnie użyto portalu Azure do umieszczenia krawędzi IoT modułu do uruchomienia na urządzeniu bez konieczności zmiany na urządzeniu. W takim przypadku moduł, który zostanie przypisany tworzy dane środowiska, używanego programu samouczków. 

Otwórz wiersz polecenia na komputerze z uruchomionym symulowane urządzenie ponownie. Upewnij się, że moduł wdrożonych w chmurze jest uruchomiona na urządzeniu IoT krawędzi. 

```cmd
docker ps
```

![Wyświetl trzech modułów na urządzeniu](./media/tutorial-simulate-device-windows/docker-ps2.png)

Wyświetl komunikaty wysyłane z modułu tempSensor do chmury. 

```cmd
docker logs -f tempSensor
```

![Wyświetlanie danych z modułu](./media/tutorial-simulate-device-windows/docker-logs.png)

Można również wyświetlić dane telemetryczne, wysyła urządzenia przy użyciu [narzędzia explorer Centrum IoT][lnk-iothub-explorer]. 
## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Podczas tworzenia Centrum IoT nie są już potrzebne, można użyć [usuwania Centrum iot az] [ lnk-delete] polecenie, aby usunąć zasób i wszystkie skojarzone z nią urządzenia:

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

## <a name="next-steps"></a>Następne kroki

Wiesz, jak wdrożyć moduł krawędzi IoT urządzenia IoT. Teraz spróbuj wdrażanie różnych typów usług Azure modułów, dzięki czemu można analizować dane na krawędzi. 

* [Wdrażanie funkcji platformy Azure jako moduł](tutorial-deploy-function.md)
* [Wdrażanie usługi Azure Stream Analytics jako modułu](tutorial-deploy-stream-analytics.md)
* [Wdrożyć własny kod jako moduł](tutorial-csharp-module.md)


<!-- Images -->
[1]: ./media/quickstart/cloud-shell.png

<!-- Links -->
[lnk-docker]: https://docs.docker.com/docker-for-windows/install/ 
[lnk-docker-containers]: https://docs.microsoft.com/virtualization/windowscontainers/quick-start/quick-start-windows-10#2-switch-to-windows-containers
[lnk-python]: https://www.python.org/downloads/
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-account]: https://azure.microsoft.com/free
[lnk-portal]: https://portal.azure.com
[lnk-nested]: https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization
[lnk-delete]: https://docs.microsoft.com/cli/azure/iot/hub?view=azure-cli-latest#az_iot_hub_delete
[lnk-install-iotcore]: how-to-install-iot-core.md

<!-- Anchor links -->
[anchor-register]: #register-an-iot-edge-device
