## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b13dc-101">Tworzenie aplikacji symulowanego urządzenia</span><span class="sxs-lookup"><span data-stu-id="b13dc-101">Create a simulated device app</span></span>
<span data-ttu-id="b13dc-102">W tej sekcji omówiono następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="b13dc-102">In this section, you:</span></span>

* <span data-ttu-id="b13dc-103">Tworzenie aplikacji konsoli Node.js, które odpowiada metoda bezpośrednia tooa wywoływane przez hello chmury</span><span class="sxs-lookup"><span data-stu-id="b13dc-103">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="b13dc-104">Wyzwalanie symulowanej aktualizacji oprogramowania układowego</span><span class="sxs-lookup"><span data-stu-id="b13dc-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="b13dc-105">Hello używany zgłaszane właściwości tooenable urządzeń dwie zapytania tooidentify urządzenia i kiedy zostały ukończone ostatniej aktualizacji oprogramowania układowego</span><span class="sxs-lookup"><span data-stu-id="b13dc-105">Use hello reported properties tooenable device twin queries tooidentify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="b13dc-106">Krok 1: Tworzenie pustego folderu o nazwie **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="b13dc-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="b13dc-107">W hello **manageddevice** folderu, Utwórz plik package.json za pomocą hello następujące polecenie z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b13dc-107">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="b13dc-108">Zaakceptuj wszystkie domyślne hello:</span><span class="sxs-lookup"><span data-stu-id="b13dc-108">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="b13dc-109">Krok 2: W oknie wiersza polecenia w hello **manageddevice** folderu, uruchom następujące polecenie tooinstall hello hello **azure iot urządzenia** i **azure-iot urządzenie mqtt** urządzenia Zestaw SDK pakietów:</span><span class="sxs-lookup"><span data-stu-id="b13dc-109">Step 2: At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="b13dc-110">Krok 3: Za pomocą edytora tekstu, Utwórz **dmpatterns_fwupdate_device.js** pliku w hello **manageddevice** folderu.</span><span class="sxs-lookup"><span data-stu-id="b13dc-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in hello **manageddevice** folder.</span></span>

<span data-ttu-id="b13dc-111">Krok 4: Dodaj następujące hello "Wymagaj" instrukcje na początku hello hello **dmpatterns_fwupdate_device.js** pliku:</span><span class="sxs-lookup"><span data-stu-id="b13dc-111">Step 4: Add hello following 'require' statements at hello start of hello **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="b13dc-112">Krok 5: Dodawanie **connectionString** zmiennej i korzystać z niego toocreate **klienta** wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="b13dc-112">Step 5: Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="b13dc-113">Zastąp hello `{yourdeviceconnectionstring}` symbol zastępczy parametrów połączenia hello należy wcześniej zanotowano w sekcji "Tworzenie tożsamości urządzenia" hello wcześniej:</span><span class="sxs-lookup"><span data-stu-id="b13dc-113">Replace hello `{yourdeviceconnectionstring}` placeholder with hello connection string you previously made a note of in hello "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="b13dc-114">Krok 6: Dodaj hello funkcja, która jest tooupdate używany zgłaszane właściwości:</span><span class="sxs-lookup"><span data-stu-id="b13dc-114">Step 6: Add hello following function that is used tooupdate reported properties:</span></span>
   
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

<span data-ttu-id="b13dc-115">Krok 7: Dodawanie hello następujące funkcje, które symulować pobierania i stosowania obrazu oprogramowania układowego hello:</span><span class="sxs-lookup"><span data-stu-id="b13dc-115">Step 7: Add hello following functions that simulate downloading and applying hello firmware image:</span></span>
   
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

<span data-ttu-id="b13dc-116">Krok 8: Dodanie powitania po funkcji stan aktualizacji oprogramowania układowego hello aktualizacje za pośrednictwem hello zbyt zgłosił właściwości**oczekiwania**.</span><span class="sxs-lookup"><span data-stu-id="b13dc-116">Step 8: Add hello following function that updates hello firmware update status through hello reported properties too**waiting**.</span></span> <span data-ttu-id="b13dc-117">Zazwyczaj urządzenia zostaną poinformowani o dostępnych aktualizacjach i określonej przez administratora zasad powoduje hello urządzenia toostart pobierania i stosowania aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="b13dc-117">Typically, devices are informed of an available update and an administrator defined policy causes hello device toostart downloading and applying hello update.</span></span> <span data-ttu-id="b13dc-118">Ta funkcja jest gdzie hello tooenable logiki, który należy uruchamiać zasad.</span><span class="sxs-lookup"><span data-stu-id="b13dc-118">This function is where hello logic tooenable that policy should run.</span></span> <span data-ttu-id="b13dc-119">Dla uproszczenia hello przykładowy oczekuje na cztery sekund przed kontynuowaniem toodownload hello oprogramowania układowego obrazu:</span><span class="sxs-lookup"><span data-stu-id="b13dc-119">For simplicity, hello sample waits for four seconds before proceeding toodownload hello firmware image:</span></span>
   
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

<span data-ttu-id="b13dc-120">Krok 9: Dodaj powitania po funkcji stan aktualizacji oprogramowania układowego hello aktualizacje za pośrednictwem hello zbyt zgłosił właściwości**pobierania**.</span><span class="sxs-lookup"><span data-stu-id="b13dc-120">Step 9: Add hello following function that updates hello firmware update status through hello reported properties too**downloading**.</span></span> <span data-ttu-id="b13dc-121">Witaj funkcja następnie symuluje pobierania oprogramowania układowego i na koniec aktualizacje hello tooeither stan aktualizacji oprogramowania układowego **downloadFailed** lub **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="b13dc-121">hello function then simulates a firmware download and finally updates hello firmware update status tooeither **downloadFailed** or **downloadComplete**:</span></span>
   
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

<span data-ttu-id="b13dc-122">Krok 10: Dodaj powitania po funkcji stan aktualizacji oprogramowania układowego hello aktualizacje za pośrednictwem hello zbyt zgłosił właściwości**stosowania**.</span><span class="sxs-lookup"><span data-stu-id="b13dc-122">Step 10: Add hello following function that updates hello firmware update status through hello reported properties too**applying**.</span></span> <span data-ttu-id="b13dc-123">Witaj funkcja następnie symuluje stosowania obrazu oprogramowania układowego hello i ostatecznie aktualizacje hello tooeither stan aktualizacji oprogramowania układowego **applyFailed** lub **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="b13dc-123">hello function then simulates applying hello firmware image and finally updates hello firmware update status tooeither **applyFailed** or **applyComplete**:</span></span>
    
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

<span data-ttu-id="b13dc-124">Krok 11: Dodaj następujące hello funkcji hello tego dojścia **firmwareUpdate** metoda bezpośrednia i oprogramowanie układowe wieloetapowym hello inicjuje proces aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="b13dc-124">Step 11: Add hello following function that handles hello **firmwareUpdate** direct method and initiates hello multi-stage firmware update process:</span></span>
    
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

<span data-ttu-id="b13dc-125">Krok 12: Na koniec należy dodać następującego kodu, który łączy się z Centrum IoT tooyour hello:</span><span class="sxs-lookup"><span data-stu-id="b13dc-125">Step 12: Finally, add hello following code that connects tooyour IoT hub:</span></span>
    
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
> <span data-ttu-id="b13dc-126">rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="b13dc-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b13dc-127">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych](https://msdn.microsoft.com/library/hh675232.aspx).</span><span class="sxs-lookup"><span data-stu-id="b13dc-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 