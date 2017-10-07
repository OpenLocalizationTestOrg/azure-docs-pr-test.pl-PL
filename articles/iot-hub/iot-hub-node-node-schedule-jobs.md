---
title: "zadania aaaSchedule z Centrum IoT Azure (węzeł) | Dokumentacja firmy Microsoft"
description: "Jak tooschedule Centrum IoT Azure zadania tooinvoke metoda bezpośrednia na wielu urządzeniach. Możesz użyć hello Azure IoT SDK dla środowiska Node.js tooimplement hello symulowane urządzenie aplikacji i zadania hello toorun aplikacji usługi."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a>Zadania harmonogramu i emisji (węzeł)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Centrum IoT Azure jest pełni zarządzaną usługę, która umożliwia toocreate aplikacji zaplecza i zadania Śledź zaplanować i zaktualizować milionów urządzeń.  Zadania mogą być używane dla hello następujące akcje:

* Aktualizowanie żądanych właściwości
* Tagi aktualizacji
* Wywołanie metody bezpośredniego

Koncepcyjnie zadanie opakowuje jedną z następujących czynności i śledzi hello postęp wykonywania pod kątem zestawu urządzeń, jest zdefiniowany przez zapytanie dwie urządzenia.  Na przykład aplikacji zaplecza można użyć tooinvoke zadania metodę ponownego uruchomienia na 10 000 urządzeń, określonych przez zapytanie dwie urządzenia i zaplanowanych w przyszłości.  Tej aplikacji można śledzić postęp, następnie każde z tych urządzeń odbierania i wykonać hello metody ponowny rozruch.

Dowiedz się więcej na temat każdego z tych funkcji w tych artykułach:

* Dwie urządzeń i właściwości: [Rozpoczynanie pracy z urządzenia twins] [ lnk-get-started-twin] i [samouczek: jak urządzenie toouse dwie właściwości][lnk-twin-props]
* bezpośrednie metody: [przewodnik dewelopera Centrum IoT — metody bezpośredniego] [ lnk-dev-methods] i [samouczek: bezpośrednie metody][lnk-c2d-methods]

Ten samouczek przedstawia sposób wykonania następujących czynności:

* Tworzenie aplikacji symulowane urządzenie, który ma bezpośredni metodę, która umożliwia **lockDoor** który może być wywoływany przez zaplecza rozwiązania hello.
* Tworzenie aplikacji konsoli Node.js hello tego wywołania **lockDoor** metoda bezpośrednia w użyciu hello zadania i aktualizacje aplikacji symulowane urządzenie hello żądanego właściwości przy użyciu zadania urządzenia.

Na końcu hello tego samouczka znajdują się dwie aplikacje konsoli Node.js:

**simDevice.js**, która łączy się tooyour Centrum IoT z hello tożsamości urządzenia i odbiera **lockDoor** metoda bezpośrednia.

**scheduleJobService.js**, które wywołuje metoda bezpośrednia hello symulowane urządzenie aplikacji i aktualizacji hello urządzenia przez dwie właściwości żądaną przy użyciu zadania.

toocomplete tego samouczka należy hello następujące:

* Środowisko node.js w wersji 0.12.x lub nowszym <br/>  [Przygotowywanie środowiska projektowego] [ lnk-dev-setup] w tym artykule opisano sposób tooinstall Node.js, w tym samouczku w systemie Windows lub Linux.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Tworzenie aplikacji symulowanego urządzenia
W tej sekcji utworzysz aplikację konsoli Node.js, która odpowiada tooa metoda bezpośrednia wywoływane przez hello chmury, co jest wyzwalane symulowane urządzenie ponowne uruchomienie komputera i zgłosił hello używa właściwości tooenable urządzeń dwie zapytania tooidentify urządzenia, a podczas ich ostatniego ponownego uruchomienia.

1. Utwórz nowy, pusty folder o nazwie **simDevice**.  W hello **simDevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.  Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **simDevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** pakiet SDK urządzenia i **azure-iot urządzenie mqtt** pakiet:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Za pomocą edytora tekstu, Utwórz nową **simDevice.js** pliku w hello **simDevice** folderu.
4. Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **simDevice.js** pliku:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Dodaj **connectionString** zmiennej i korzystać z niego toocreate **klienta** wystąpienia.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Dodaj powitania po hello toohandle funkcja **lockDoor** metody.
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. Dodaj następującego kodu tooregister hello obsługę hello hello **lockDoor** metody.
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. Zapisz i zamknij hello **simDevice.js** pliku.

> [!NOTE]
> rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a>Planowanie zadań dla wywołania metody bezpośredniego i aktualizowanie właściwości dwie urządzenia
W tej sekcji Tworzenie aplikacji konsoli Node.js, który inicjuje zdalnej **lockDoor** na urządzeniu przy użyciu właściwości direct — metoda i aktualizacji hello urządzenia dwie firmy.

1. Utwórz nowy, pusty folder o nazwie **scheduleJobService**.  W hello **scheduleJobService** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.  Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```
2. Z wiersza polecenia w hello **scheduleJobService** folderu, uruchom następujące polecenie tooinstall hello hello **Centrum iothub azure** pakiet SDK urządzenia i **azure-iot urządzenie mqtt**pakietu:
   
    ```
    npm install azure-iothub uuid --save
    ```
3. Za pomocą edytora tekstu, Utwórz nową **scheduleJobService.js** pliku w hello **scheduleJobService** folderu.
4. Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **dmpatterns_gscheduleJobServiceetstarted_service.js** pliku:
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. Dodaj następujące deklaracje zmiennej hello i zastąp symbole zastępcze hello:
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. Dodaj hello następujących funkcji, które będzie używane toomonitor hello wykonanie zadania hello:
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. Dodaj następującego kodu tooschedule hello zadanie, które wywołuje metodę urządzenia hello hello:
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. Dodaj następującego kodu tooschedule hello zadania tooupdate hello urządzenia dwie hello:
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. Zapisz i zamknij hello **scheduleJobService.js** pliku.

## <a name="run-hello-applications"></a>Uruchamianie aplikacji hello
Wszystko jest teraz gotowy toorun hello aplikacji.

1. W wierszu polecenia hello w hello **simDevice** folderu Uruchom hello następujące polecenia toobegin nasłuchiwanie metoda bezpośrednia hello ponowny rozruch.
   
    ```
    node simDevice.js
    ```
2. W wierszu polecenia hello w hello **scheduleJobService** folderu Uruchom hello następujące polecenia tootrigger hello zadania toolock hello drzwi i aktualizacji Witaj dwie
   
    ```
    node scheduleJobService.js
    ```
3. Zostanie wyświetlony hello urządzenia odpowiedzi toohello metoda bezpośrednia hello konsoli.

## <a name="next-steps"></a>Następne kroki
W tym samouczku użyto zadania tooschedule urządzenia tooa metoda bezpośrednia i aktualizacji hello hello urządzenia dwie właściwości.

toocontinue wprowadzenie do korzystania z Centrum IoT i urządzenia zarządzania wzorców, takich jak zdalnego za pośrednictwem aktualizacji oprogramowania układowego lotniczego hello, zobacz:

[Samouczek: Jak toodo oprogramowanie układowe aktualizacji][lnk-fwupdate]

Zobacz toocontinue wprowadzenie do korzystania z Centrum IoT [wprowadzenie do korzystania z usługi Azure IoT krawędzi][lnk-iot-edge].

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
