## <a name="create-a-simulated-device-app"></a>Tworzenie aplikacji symulowanego urządzenia
W tej sekcji omówiono następujące zagadnienia:

* Tworzenie aplikacji konsolowej Node.js, która reaguje na metodę bezpośrednią wywołaną przez chmurę
* Wyzwalanie symulowanej aktualizacji oprogramowania układowego
* Włączanie zapytań bliźniaczych reprezentacji urządzeń przy użyciu zgłoszonych właściwości w celu zidentyfikowania urządzeń i ustalenia, kiedy ostatnio przeprowadzono na nich aktualizację oprogramowania układowego

Krok 1: Tworzenie pustego folderu o nazwie **manageddevice**.  W folderze **manageddevice** utwórz plik package.json przy użyciu następującego polecenia z poziomu wiersza polecenia. Zaakceptuj wszystkie ustawienia domyślne:
   
    ```
    npm init
    ```

Krok 2: W oknie wiersza polecenia w **manageddevice** folderu, uruchom następujące polecenie, aby zainstalować **azure iot urządzenia** i **azure-iot urządzenie mqtt** SDK urządzenia pakiety:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

Krok 3: Za pomocą edytora tekstu, Utwórz **dmpatterns_fwupdate_device.js** w pliku **manageddevice** folderu.

Krok 4: Dodaj następujące "wymagane" instrukcje na początku **dmpatterns_fwupdate_device.js** pliku:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
Krok 5: Dodawanie **connectionString** zmiennej i użyj go, aby utworzyć **klienta** wystąpienia. Zamień symbol zastępczy `{yourdeviceconnectionstring}` na parametry połączenia zanotowane wcześniej w sekcji „Tworzenie tożsamości urządzenia”:
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

Krok 6: Dodawanie następujących funkcji, która jest używana do aktualizacji właściwości zgłoszone:
   
    ```
    var reportFWUpdateThroughTwin = function(twin, firmwareUpdateValue) {
      var patch = {
          iothubDM : {
            firmwareUpdate : firmwareUpdateValue
          }
      };
   
      twin.properties.reported.update(patch, function(err) {
        if (err) throw err;
        console.log('twin state reported: ' + firmwareUpdateValue.status);
      });
    };
    ```

Krok 7: Dodawanie następujących funkcji symulujących pobierania i stosowania obrazu oprogramowania układowego:
   
    ```
    var simulateDownloadImage = function(imageUrl, callback) {
      var error = null;
      var image = "[fake image data]";
   
      console.log("Downloading image from " + imageUrl);
   
      callback(error, image);
    }
   
    var simulateApplyImage = function(imageData, callback) {
      var error = null;
   
      if (!imageData) {
        error = {message: 'Apply image failed because of missing image data.'};
      }
   
      callback(error);
    }
    ```

Krok 8: Dodaj następującą funkcję, która aktualizuje stan aktualizacji oprogramowania układowego za pośrednictwem właściwości zgłoszony do **oczekiwania**. Zazwyczaj urządzenia otrzymują informacje o dostępnej aktualizacji, a zasady określone przez administratora powodują, że urządzenie zaczyna pobierać i stosować aktualizację. To w tej funkcji powinna zostać uruchomiona logika włączająca te zasady. Dla uproszczenia próbki czeka na cztery sekund przed kontynuowaniem pobranie obrazu oprogramowania układowego:
   
    ```
    var waitToDownload = function(twin, fwPackageUriVal, callback) {
      var now = new Date();
   
      reportFWUpdateThroughTwin(twin, {
        fwPackageUri: fwPackageUriVal,
        status: 'waiting',
        error : null,
        startedWaitingTime : now.toISOString()
      });
      setTimeout(callback, 4000);
    };
    ```

Krok 9: Dodaj następującą funkcję, która aktualizuje stan aktualizacji oprogramowania układowego za pośrednictwem właściwości zgłoszony do **pobierania**. Następnie funkcja symuluje pobieranie oprogramowania układowego i aktualizuje stan aktualizacji oprogramowania na **downloadFailed** lub **downloadComplete**:
   
    ```
    var downloadImage = function(twin, fwPackageUriVal, callback) {
      var now = new Date();   
   
      reportFWUpdateThroughTwin(twin, {
        status: 'downloading',
      });
   
      setTimeout(function() {
        // Simulate download
        simulateDownloadImage(fwPackageUriVal, function(err, image) {
   
          if (err)
          {
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadfailed',
              error: {
                code: error_code,
                message: error_message,
              }
            });
          }
          else {        
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadComplete',
              downloadCompleteTime: now.toISOString(),
            });
   
            setTimeout(function() { callback(image); }, 4000);   
          }
        });
   
      }, 4000);
    }
    ```

Krok 10: Dodaj następującą funkcję, która aktualizuje stan aktualizacji oprogramowania układowego za pośrednictwem właściwości zgłoszony do **stosowania**. Następnie funkcja symuluje stosowanie obrazu oprogramowania układowego i aktualizuje stan aktualizacji oprogramowania na **applyFailed** lub **applyComplete**:
    
    ```
    var applyImage = function(twin, imageData, callback) {
      var now = new Date();   
    
      reportFWUpdateThroughTwin(twin, {
        status: 'applying',
        startedApplyingImage : now.toISOString()
      });
    
      setTimeout(function() {
    
        // Simulate apply firmware image
        simulateApplyImage(imageData, function(err) {
          if (err) {
            reportFWUpdateThroughTwin(twin, {
              status: 'applyFailed',
              error: {
                code: err.error_code,
                message: err.error_message,
              }
            });
          } else { 
            reportFWUpdateThroughTwin(twin, {
              status: 'applyComplete',
              lastFirmwareUpdate: now.toISOString()
            });    
    
          }
        });
    
        setTimeout(callback, 4000);
    
      }, 4000);
    }
    ```

Krok 11: Dodaj następująca funkcja, która obsługuje **firmwareUpdate** metoda bezpośrednia i inicjuje procesu aktualizacji oprogramowania układowego wieloetapowym:
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond the cloud app for the direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response to method \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get the parameter from the body of the method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain the device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start the multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

Krok 12: Na koniec należy dodać następujący kod, który łączy się z Centrum IoT:
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect to IotHub client');
      }  else {
        console.log('Client connected to IoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> Dla uproszczenia ten samouczek nie zawiera opisu wdrożenia żadnych zasad ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN [obsługi błędów przejściowych](https://msdn.microsoft.com/library/hh675232.aspx).
> 
> 