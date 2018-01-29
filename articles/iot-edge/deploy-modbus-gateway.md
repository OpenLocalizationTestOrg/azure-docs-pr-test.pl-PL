---
title: "Wdrażanie protokołu Modbus w usłudze Azure IoT Edge | Microsoft Docs"
description: "Zezwalanie urządzeniom korzystających z protokołu Modbus TCP na komunikację z usługą Azure IoT Hub poprzez utworzenie urządzenia bramy usługi IoT Edge"
services: iot-Edge
documentationcenter: 
author: kgremban
manager: timlt
editor: chrisgmsft
ms.assetid: 
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2017
ms.author: kgremban
ms.custom: 
ms.openlocfilehash: e239bde48c3da0d899e3c78bdd39f520c4128b95
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="connect-modbus-tcp-devices-through-an-iot-edge-device-gateway---preview"></a>Łączenie urządzeń Modbus TCP za pośrednictwem bramy urządzeń usługi IoT Edge — wersja zapoznawcza

Jeśli chcesz połączyć urządzenia IoT korzystające z protokołów Modbus TCP lub RTU z centrum usługi Azure IoT, użyj urządzenia IoT Edge jako bramy. Urządzenie bramy odczytuje dane z urządzeń korzystających z protokołu Modbus, a następnie przekazuje te dane do chmury przy użyciu obsługiwanego protokołu. 

![Urządzenia korzystające z protokołu Modbus łączą się z usługą IoT Hub za pośrednictwem bramy granicznej](./media/deploy-modbus-gateway/diagram.png)

W tym artykule opisano sposób tworzenia własnego obrazu kontenera dla modułu Modbus (można też użyć wstępnie utworzonej próbki), a następnie wdrożenia go do urządzenia usługi IoT Edge, które będzie pełnić rolę bramy. 

W tym artykule założono, że użytkownik korzysta z protokołu Modbus TCP. Aby uzyskać więcej informacji o sposobie konfigurowania modułu na potrzeby obsługi protokołu Modbus RTU, zobacz projekt [Moduł Azure IoT Edge Modbus](https://github.com/Azure/iot-edge-modbus) w witrynie Github. 

## <a name="prerequisites"></a>Wymagania wstępne
* Urządzenie usługi Azure IoT Edge. Aby skorzystać z przewodnika dotyczącego konfiguracji takiego urządzenia, zobacz [Wdrażanie usługi Azure IoT Edge na symulowanym urządzeniu w systemie Windows](tutorial-simulate-device-windows.md) lub [Linux](tutorial-simulate-device-linux.md). 
* Parametry połączenia klucza podstawowego dla urządzenia usługi IoT Edge.
* Fizyczne lub symulowane urządzenie Modbus obsługujące protokół Modbus TCP.

## <a name="prepare-a-modbus-container"></a>Przygotowanie kontenera Modbus

Jeśli chcesz przetestować funkcje bramy Modbus, firma Microsoft przygotowała przykładowy moduł, którego możesz użyć. Aby użyć przykładowego modułu, przejdź do sekcji [Uruchamianie rozwiązania](#run-the-solution) i wprowadź następujący identyfikator URI obrazu: 

```URL
microsoft/azureiotedge-modbus-tcp:1.0-preview
```

Jeśli chcesz utworzyć własny moduł i dostosować go pod kątem środowiska użytkownika, istnieje projekt [Moduł Azure IoT Edge Modbus](https://github.com/Azure/iot-edge-modbus) typu open source w witrynie Github. Wykonaj instrukcje zawarte w tym projekcie, aby utworzyć własny obraz kontenera. Jeśli tworzysz własny obraz kontenera, zobacz [Opracowanie i wdrożenie modułu IoT Edge w języku C#](tutorial-csharp-module.md), aby uzyskać instrukcje dotyczące publikowania obrazów kontenera w rejestrze oraz wdrażania niestandardowego modułu na urządzeniu. 


## <a name="run-the-solution"></a>Uruchamianie rozwiązania
1. W witrynie [Azure Portal](https://portal.azure.com/) przejdź do centrum IoT Hub.
2. Przejdź do pozycji **IoT Edge (wersja zapoznawcza)** i wybierz urządzenie usługi IoT Edge.
3. Wybierz opcję **Ustaw moduły**.
4. Dodaj moduł Modbus:
   1. Wybierz opcję **Dodaj moduł IoT Edge**.
   2. W polu **Nazwa** wpisz „modbus”.
   3. W polu **Obraz** wprowadź identyfikator URI obrazu przykładowego kontenera: `microsoft/azureiotedge-modbus-tcp:1.0-preview`.
   4. Zaznacz pole **Włącz**, aby zaktualizować żądane właściwości bliźniaczego modułu.
   5. Skopiuj następujące dane JSON do pola tekstowego. Zmień wartość atrybutu **SlaveConnection** na adres IPv4 urządzenia Modbus.

      ```JSON
      {  
        "properties.desired":{  
          "PublishInterval":"2000",
          "SlaveConfigs":{  
            "Slave01":{  
              "SlaveConnection":"<IPV4 address>",
              "HwId":"PowerMeter-0a:01:01:01:01:01",
              "Operations":{  
                "Op01":{  
                  "PollingInterval": "1000",
                  "UnitId":"1",
                  "StartAddress":"400001",
                  "Count":"2",
                  "DisplayName":"Voltage"
                }
              }
            }
          }
        }
      }
      ```

   6. Wybierz pozycję **Zapisz**.
5. W kroku **Dodawanie modułów** wybierz opcję **Dalej**.
7. W kroku **Określanie tras** skopiuj następujące dane JSON do pola tekstowego. Ta trasa wysyła wszystkie komunikaty zebrane przez moduł Modbus do centrum IoT Hub. W tej trasie „modbusOutput” jest punktem końcowym, którego moduł Modbus używa do wydawania danych, a „upstream” jest specjalną lokalizacją docelową, która nakazuje centrum Edge Hub wysyłanie komunikatów do centrum IoT Hub. 
   ```JSON
   {
    "routes": {
      "modbusToIoTHub":"FROM /messages/modules/modbus/outputs/modbusOutput INTO $upstream"
    }
   }
   ```

8. Wybierz opcję **Dalej**. 
9. W kroku **Przegląd szablonu** wybierz opcję **Prześlij**. 
10. Wróć do strony szczegółów urządzenia i wybierz opcję **Odśwież**. Nowy moduł **modbus** powinien zostać uruchomiony wraz ze środowiskiem uruchomieniowym usługi IoT Edge.

## <a name="view-data"></a>Wyświetlanie danych
Wyświetlanie danych przechodzących przez moduł modbus:
```cmd/sh
docker logs -f modbus
```

Możesz też wyświetlić telemetrię wysyłaną przez urządzenie przy użyciu [narzędzia eksploratora centrum IoT Hub](https://github.com/azure/iothub-explorer). 

## <a name="next-steps"></a>Następne kroki

- Aby dowiedzieć się więcej o tym, jak urządzenia usługi IoT Edge mogą pełnić rolę bram, zobacz [Tworzenie urządzenia usługi IoT Edge, które będzie pełnić rolę przezroczystej bramy](how-to-create-transparent-gateway.md)
- Aby uzyskać więcej informacji o działaniu modułów usługi IoT Edge, zobacz [Opis modułów usługi Azure IoT Edge](iot-edge-modules.md)