## <a name="create-a-simulated-device-app"></a>Tworzenie aplikacji symulowanego urządzenia
W tej sekcji omówiono następujące zagadnienia:

* Tworzenie aplikacji konsoli Node.js, które odpowiada metoda bezpośrednia tooa wywoływane przez hello chmury
* Wyzwalanie symulowanej aktualizacji oprogramowania układowego
* Hello używany zgłaszane właściwości tooenable urządzeń dwie zapytania tooidentify urządzenia i kiedy zostały ukończone ostatniej aktualizacji oprogramowania układowego

Krok 1: Tworzenie pustego folderu o nazwie **manageddevice**.  W hello **manageddevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia. Zaakceptuj wszystkie domyślne hello:
   
    ```
    npm init
    ```

Krok 2: W oknie wiersza polecenia w hello **manageddevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** i **azure-iot urządzenie mqtt** urządzenia Zestaw SDK pakietów:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

Krok 3: Za pomocą edytora tekstu, Utwórz **dmpatterns_fwupdate_device.js** pliku w hello **manageddevice** folderu.

Krok 4: Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **dmpatterns_fwupdate_device.js** pliku:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
Krok 5: Dodawanie **connectionString** zmiennej i korzystać z niego toocreate **klienta** wystąpienia. Zastąp hello `{yourdeviceconnectionstring}` symbol zastępczy parametrów połączenia hello należy wcześniej zanotowano w sekcji "Tworzenie tożsamości urządzenia" hello wcześniej:
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

Krok 6: Dodaj hello funkcja, która jest tooupdate używany zgłaszane właściwości:
   
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

Krok 7: Dodawanie hello następujące funkcje, które symulować pobierania i stosowania obrazu oprogramowania układowego hello:
   
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

Krok 8: Dodanie powitania po funkcji stan aktualizacji oprogramowania układowego hello aktualizacje za pośrednictwem hello zbyt zgłosił właściwości**oczekiwania**. Zazwyczaj urządzenia zostaną poinformowani o dostępnych aktualizacjach i określonej przez administratora zasad powoduje hello urządzenia toostart pobierania i stosowania aktualizacji hello. Ta funkcja jest gdzie hello tooenable logiki, który należy uruchamiać zasad. Dla uproszczenia hello przykładowy oczekuje na cztery sekund przed kontynuowaniem toodownload hello oprogramowania układowego obrazu:
   
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

Krok 9: Dodaj powitania po funkcji stan aktualizacji oprogramowania układowego hello aktualizacje za pośrednictwem hello zbyt zgłosił właściwości**pobierania**. Witaj funkcja następnie symuluje pobierania oprogramowania układowego i na koniec aktualizacje hello tooeither stan aktualizacji oprogramowania układowego **downloadFailed** lub **downloadComplete**:
   
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

Krok 10: Dodaj powitania po funkcji stan aktualizacji oprogramowania układowego hello aktualizacje za pośrednictwem hello zbyt zgłosił właściwości**stosowania**. Witaj funkcja następnie symuluje stosowania obrazu oprogramowania układowego hello i ostatecznie aktualizacje hello tooeither stan aktualizacji oprogramowania układowego **applyFailed** lub **applyComplete**:
    
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

Krok 11: Dodaj następujące hello funkcji hello tego dojścia **firmwareUpdate** metoda bezpośrednia i oprogramowanie układowe wieloetapowym hello inicjuje proces aktualizacji:
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond hello cloud app for hello direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get hello parameter from hello body of hello method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain hello device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start hello multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

Krok 12: Na koniec należy dodać następującego kodu, który łączy się z Centrum IoT tooyour hello:
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect tooIotHub client');
      }  else {
        console.log('Client connected tooIoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych](https://msdn.microsoft.com/library/hh675232.aspx).
> 
> 