---
title: "Aktualizacja oprogramowania układowego aaaDevice z Centrum IoT Azure (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak zaktualizować toouse zarządzania urządzeniami w usłudze Azure IoT Hub tooinitiate oprogramowanie układowe urządzenia. Używasz hello Azure IoT SDK dla środowiska Node.js tooimplement aplikacji symulowane urządzenie i aplikacji usługi, która wyzwala hello aktualizacji oprogramowania układowego."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a>Użyj tooinitiate zarządzania urządzenia aktualizacji oprogramowania układowego urządzenia (węzeł/węzeł)
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Wprowadzenie
W hello [wprowadzenie do zarządzania urządzeniami] [ lnk-dm-getstarted] samouczku przedstawiono sposób toouse hello [dwie urządzenia] [ lnk-devtwin] i [bezpośredniego metody] [ lnk-c2dmethod] tooremotely podstawowych ponownego uruchamiania urządzenia. Ten samouczek używa hello tego samego Centrum IoT elementów podstawowych i zawiera wskazówki i pokazuje, jak toodo end-to-end symulowane aktualizacji oprogramowania układowego.  Ten wzorzec jest używany podczas wdrażania aktualizacji oprogramowania układowego hello hello Intel Edison urządzenia próbki.

Ten samouczek przedstawia sposób wykonania następujących czynności:

* Tworzenie aplikacji konsoli Node.js, który wywołuje metodę bezpośredniego firmwareUpdate hello w hello symulowane urządzenie aplikacji za pośrednictwem Centrum IoT.
* Tworzenie aplikacji symulowane urządzenie, który implementuje **firmwareUpdate** metoda bezpośrednia. Ta metoda inicjuje procesem wieloetapowym, która oczekuje toodownload hello oprogramowania układowego obrazu, pobierze obraz oprogramowania układowego hello i finally stosuje hello oprogramowania układowego obrazu. Podczas każdego etapu aktualizacji hello hello urządzenie używa hello zgłoszony tooreport właściwości w toku.

Na końcu hello tego samouczka znajdują się dwie aplikacje konsoli Node.js:

**dmpatterns_fwupdate_service.js**, która wywołuje metodę bezpośrednio w aplikacji hello symulowane urządzenie Wyświetla hello odpowiedzi i okresowo (co 500 MS.) hello wyświetla zaktualizowane zgłoszone właściwości.

**dmpatterns_fwupdate_device.js**, o tożsamości urządzenia hello utworzony wcześniej, który łączy Centrum IoT tooyour odbiera firmwareUpdate metoda bezpośrednia, jest uruchamiany za pośrednictwem toosimulate wielu stanu procesu aktualizacji oprogramowania układowego łącznie: Oczekiwanie na powitania Obraz Pobierz pobierania nowy obraz powitania i na koniec stosowania hello obrazu.

toocomplete tego samouczka należy hello następujące:

* Środowisko node.js w wersji 0.12.x lub nowszym <br/>  [Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Node.js, w tym samouczku w systemie Windows lub Linux.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

Wykonaj hello [wprowadzenie do zarządzania urządzeniami](iot-hub-node-node-device-management-get-started.md) artykułu toocreate Centrum IoT i pobrać parametry połączenia Centrum IoT.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Wyzwalanie aktualizacji oprogramowania układowego zdalnego na urządzeniu hello za pomocą bezpośrednich — metoda
W tej sekcji utworzysz aplikację konsoli Node.js, która inicjuje aktualizacji oprogramowania układowego zdalnego na urządzeniu. Aplikacja Hello korzysta z aktualizacją hello tooinitiate metoda bezpośrednia i używa urządzenia dwie zapytania tooperiodically Pobierz hello stan aktualizacji oprogramowania układowego active hello.

1. Utwórz pusty folder o nazwie **triggerfwupdateondevice**.  W hello **triggerfwupdateondevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.  Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **triggerfwupdateondevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot koncentrator** i **azure-iot urządzenie mqtt** urządzenia Zestaw SDK pakietów:
   
    ```
    npm install azure-iothub --save
    ```
3. Za pomocą edytora tekstu, Utwórz **dmpatterns_getstarted_service.js** pliku w hello **triggerfwupdateondevice** folderu.
4. Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **dmpatterns_getstarted_service.js** pliku:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Dodaj następujące deklaracje zmiennej hello i zastąp symbole zastępcze hello:
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. Dodaj następujący hello funkcji toofind i wyświetlenia wartości hello hello firmwareUpdate zgłosił właściwości.
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. Dodaj powitania po funkcja tooinvoke hello firmwareUpdate metody tooreboot hello docelowe urządzenie:
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. Na koniec Dodaj następujące hello funkcji sekwencja aktualizacji oprogramowania układowego hello toostart toocode i rozpoczęcia okresowo wyświetlania hello zgłoszonych właściwości:
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. Zapisz i zamknij hello **dmpatterns_fwupdate_service.js** pliku.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Uruchamianie aplikacji hello
Wszystko jest teraz gotowy toorun hello aplikacji.

1. W wierszu polecenia hello w hello **manageddevice** folderu Uruchom hello następujące polecenia toobegin nasłuchiwanie metoda bezpośrednia hello ponowny rozruch.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. W wierszu polecenia hello w hello **triggerfwupdateondevice** folderu, uruchom następujące polecenie tootrigger hello zdalnego hello ponownie i zapytania dla hello urządzenia dwie toofind hello ostatniego ponownego rozruchu czasu.
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. Zostanie wyświetlony hello urządzenia odpowiedzi toohello metoda bezpośrednia hello konsoli.

## <a name="next-steps"></a>Następne kroki
W tym samouczku używana metoda bezpośrednia tootrigger zdalnej aktualizacji oprogramowania układowego na urządzeniach i hello używany zgłaszane postęp hello toofollow właściwości aktualizacji oprogramowania układowego hello.

toolearn tooextend IoT metody rozwiązania i harmonogram wywołuje na wielu urządzeniach, zobacz hello [emisji zadania i harmonogramu] [ lnk-tutorial-jobs] samouczka.

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
