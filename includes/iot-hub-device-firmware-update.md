## <a name="create-a-simulated-device-app"></a><span data-ttu-id="a5b82-101">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="a5b82-101">Create a simulated device app</span></span>
<span data-ttu-id="a5b82-102">W tej sekcji omówiono następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="a5b82-102">In this section, you:</span></span>

* <span data-ttu-id="a5b82-103">Tworzenie aplikacji konsolowej Node.js, która reaguje na metodę bezpośrednią wywołaną przez chmurę</span><span class="sxs-lookup"><span data-stu-id="a5b82-103">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="a5b82-104">Wyzwalanie symulowanej aktualizacji oprogramowania układowego</span><span class="sxs-lookup"><span data-stu-id="a5b82-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="a5b82-105">Włączanie zapytań bliźniaczych reprezentacji urządzeń przy użyciu zgłoszonych właściwości w celu zidentyfikowania urządzeń i ustalenia, kiedy ostatnio przeprowadzono na nich aktualizację oprogramowania układowego</span><span class="sxs-lookup"><span data-stu-id="a5b82-105">Use the reported properties to enable device twin queries to identify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="a5b82-106">Krok 1: Tworzenie pustego folderu o nazwie **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="a5b82-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="a5b82-107">W folderze **manageddevice** utwórz plik package.json przy użyciu następującego polecenia z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a5b82-107">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="a5b82-108">Zaakceptuj wszystkie ustawienia domyślne:</span><span class="sxs-lookup"><span data-stu-id="a5b82-108">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="a5b82-109">Krok 2: W oknie wiersza polecenia w **manageddevice** folderu, uruchom następujące polecenie, aby zainstalować **azure iot urządzenia** i **azure-iot urządzenie mqtt** SDK urządzenia pakiety:</span><span class="sxs-lookup"><span data-stu-id="a5b82-109">Step 2: At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="a5b82-110">Krok 3: Za pomocą edytora tekstu, Utwórz **dmpatterns_fwupdate_device.js** w pliku **manageddevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="a5b82-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in the **manageddevice** folder.</span></span>

<span data-ttu-id="a5b82-111">Krok 4: Dodaj następujące "wymagane" instrukcje na początku **dmpatterns_fwupdate_device.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="a5b82-111">Step 4: Add the following 'require' statements at the start of the **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="a5b82-112">Krok 5: Dodawanie **connectionString** zmiennej i użyj go, aby utworzyć **klienta** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="a5b82-112">Step 5: Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="a5b82-113">Zamień symbol zastępczy `{yourdeviceconnectionstring}` na parametry połączenia zanotowane wcześniej w sekcji „Tworzenie tożsamości urządzenia”:</span><span class="sxs-lookup"><span data-stu-id="a5b82-113">Replace the `{yourdeviceconnectionstring}` placeholder with the connection string you previously made a note of in the "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="a5b82-114">Krok 6: Dodawanie następujących funkcji, która jest używana do aktualizacji właściwości zgłoszone:</span><span class="sxs-lookup"><span data-stu-id="a5b82-114">Step 6: Add the following function that is used to update reported properties:</span></span>
   
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

<span data-ttu-id="a5b82-115">Krok 7: Dodawanie następujących funkcji symulujących pobierania i stosowania obrazu oprogramowania układowego:</span><span class="sxs-lookup"><span data-stu-id="a5b82-115">Step 7: Add the following functions that simulate downloading and applying the firmware image:</span></span>
   
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

<span data-ttu-id="a5b82-116">Krok 8: Dodaj następującą funkcję, która aktualizuje stan aktualizacji oprogramowania układowego za pośrednictwem właściwości zgłoszony do **oczekiwania**.</span><span class="sxs-lookup"><span data-stu-id="a5b82-116">Step 8: Add the following function that updates the firmware update status through the reported properties to **waiting**.</span></span> <span data-ttu-id="a5b82-117">Zazwyczaj urządzenia otrzymują informacje o dostępnej aktualizacji, a zasady określone przez administratora powodują, że urządzenie zaczyna pobierać i stosować aktualizację.</span><span class="sxs-lookup"><span data-stu-id="a5b82-117">Typically, devices are informed of an available update and an administrator defined policy causes the device to start downloading and applying the update.</span></span> <span data-ttu-id="a5b82-118">To w tej funkcji powinna zostać uruchomiona logika włączająca te zasady.</span><span class="sxs-lookup"><span data-stu-id="a5b82-118">This function is where the logic to enable that policy should run.</span></span> <span data-ttu-id="a5b82-119">Dla uproszczenia próbki czeka na cztery sekund przed kontynuowaniem pobranie obrazu oprogramowania układowego:</span><span class="sxs-lookup"><span data-stu-id="a5b82-119">For simplicity, the sample waits for four seconds before proceeding to download the firmware image:</span></span>
   
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

<span data-ttu-id="a5b82-120">Krok 9: Dodaj następującą funkcję, która aktualizuje stan aktualizacji oprogramowania układowego za pośrednictwem właściwości zgłoszony do **pobierania**.</span><span class="sxs-lookup"><span data-stu-id="a5b82-120">Step 9: Add the following function that updates the firmware update status through the reported properties to **downloading**.</span></span> <span data-ttu-id="a5b82-121">Następnie funkcja symuluje pobieranie oprogramowania układowego i aktualizuje stan aktualizacji oprogramowania na **downloadFailed** lub **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="a5b82-121">The function then simulates a firmware download and finally updates the firmware update status to either **downloadFailed** or **downloadComplete**:</span></span>
   
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

<span data-ttu-id="a5b82-122">Krok 10: Dodaj następującą funkcję, która aktualizuje stan aktualizacji oprogramowania układowego za pośrednictwem właściwości zgłoszony do **stosowania**.</span><span class="sxs-lookup"><span data-stu-id="a5b82-122">Step 10: Add the following function that updates the firmware update status through the reported properties to **applying**.</span></span> <span data-ttu-id="a5b82-123">Następnie funkcja symuluje stosowanie obrazu oprogramowania układowego i aktualizuje stan aktualizacji oprogramowania na **applyFailed** lub **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="a5b82-123">The function then simulates applying the firmware image and finally updates the firmware update status to either **applyFailed** or **applyComplete**:</span></span>
    
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

<span data-ttu-id="a5b82-124">Krok 11: Dodaj następująca funkcja, która obsługuje **firmwareUpdate** metoda bezpośrednia i inicjuje procesu aktualizacji oprogramowania układowego wieloetapowym:</span><span class="sxs-lookup"><span data-stu-id="a5b82-124">Step 11: Add the following function that handles the **firmwareUpdate** direct method and initiates the multi-stage firmware update process:</span></span>
    
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

<span data-ttu-id="a5b82-125">Krok 12: Na koniec należy dodać następujący kod, który łączy się z Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="a5b82-125">Step 12: Finally, add the following code that connects to your IoT hub:</span></span>
    
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
> <span data-ttu-id="a5b82-126">Dla uproszczenia ten samouczek nie zawiera opisu wdrożenia żadnych zasad ponawiania.</span><span class="sxs-lookup"><span data-stu-id="a5b82-126">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="a5b82-127">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN [obsługi błędów przejściowych](https://msdn.microsoft.com/library/hh675232.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5b82-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 