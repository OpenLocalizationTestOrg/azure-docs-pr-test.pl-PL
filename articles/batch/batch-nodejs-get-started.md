---
title: "aaaTutorial — Biblioteka klienta użyj hello partii zadań Azure dla środowiska Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się hello podstawowych pojęciach dotyczących partii zadań Azure i utworzenie rozwiązania do prostych przy użyciu środowiska Node.js."
services: batch
author: shwetams
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: nodejs
ms.topic: hero-article
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: shwetams
ms.openlocfilehash: d2b0ecbe764e7100affd7b02839aef3077b073cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a>Wprowadzenie do zestawu SDK usługi Batch dla środowiska Node.js

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Dowiedz się hello podstawy tworzenia klienta przy użyciu środowiska Node.js [Azure partii Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/). W tym artykule poznamy scenariusz dotyczący aplikacji usługi Batch i sposób jej konfigurowania przy użyciu klienta Node.js.  

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule założono, że masz praktyczną wiedzę dotyczącą języka Node.js oraz znasz system Linux. Przyjęto założenie, że masz konto platformy Azure Instalatorowi dostępu prawa toocreate partii i usługi magazynu.

Firma Microsoft zaleca odczytu [omówienie techniczne usługi partia zadań Azure](batch-technical-overview.md) przed przejściem przez hello kroki opisane w tym artykule.

## <a name="hello-tutorial-scenario"></a>Scenariusz samouczek Hello
Daj nam poznać hello partii przepływ pracy scenariusza. Mamy prostego skryptu napisane w języku Python, który pobiera csv wszystkie pliki z kontenera magazynu obiektów Blob platformy Azure i konwertuje je tooJSON. tooprocess konta magazynu wielu kontenerów równolegle, możemy wdrożyć skryptu hello Azure wsadowym.

## <a name="azure-batch-architecture"></a>Architektura usługi Azure Batch
Witaj Poniższy diagram przedstawia sposób mogą być skalowane skrypt w języku Python hello przy użyciu partii zadań Azure i klienta środowiska Node.js.

![Scenariusze dotyczące usługi Azure Batch](./media/batch-nodejs-get-started/BatchScenario.png)

powitania klienta node.js wdraża zadania wsadowego z przygotowanie zadania (szczegółowo omówiono później) i zestaw zadań, w zależności od hello liczba kontenerów w hello konta magazynu. Skrypty hello można pobrać z repozytorium github hello.

* [Klient Node.js](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [Przygotowanie skryptów powłoki zadań](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [Procesor tooJSON csv Python](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> powitania klienta Node.js łącza hello określony nie zawiera toobe kod wdrożony jako aplikacja funkcji platformy Azure. Toohello następujące linki do instrukcji toocreate, co może się odwoływać.
> - [Create function app](../azure-functions/functions-create-first-azure-function.md) (Tworzenie aplikacji funkcji)
> - [Create timer trigger function](../azure-functions/functions-bindings-timer.md) (Tworzenie funkcji wyzwalanej czasomierzem)
>
>

## <a name="build-hello-application"></a>Tworzenie aplikacji hello

Teraz Poinformuj nas wykonaj proces hello krok po kroku do tworzenia powitania klienta Node.js:

### <a name="step-1-install-azure-batch-sdk"></a>Krok 1. Instalowanie zestawu SDK usługi Azure Batch

Należy zainstalować zestaw SDK usługi partia zadań Azure dla środowiska Node.js przy użyciu polecenia install npm hello.

`npm install azure-batch`

To polecenie instaluje najnowszą wersję hello węzła partii zadań azure SDK.

>[!Tip]
> W aplikacji funkcji platformy Azure, można przejść za poleceń instalacji npm hello toorun kartę Ustawienia "Konsoli Kudu" hello Azure funkcji. W tym wielkość tooinstall zestawu SDK usługi partia zadań Azure dla środowiska Node.js.
>
>

### <a name="step-2-create-an-azure-batch-account"></a>Krok 2. Tworzenie konta usługi Azure Batch

Można go utworzyć, korzystając z hello [portalu Azure](batch-account-create-portal.md) lub z wiersza polecenia ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).

Poniżej przedstawiono toocreate polecenia hello, jeden za pomocą wiersza polecenia platformy Azure.

Utwórz grupę zasobów, Pomiń ten krok, jeśli masz już konto, w którym ma hello toocreate konta usługi partia zadań:

`az group create -n "<resource-group-name>" -l "<location>"`

Następnie utwórz konto usługi Azure Batch.

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

Każde konto usługi Batch ma odpowiadające mu klucze dostępu. Klucze te są toocreate wymagane dalsze zasobów konta usługi partia zadań Azure. Dobrym rozwiązaniem w środowisku produkcyjnym jest toostore usługi Azure Key Vault toouse tych kluczy. Następnie można utworzyć usługi głównej aplikacji hello. Za pomocą tej aplikacji hello główna usługi można utworzyć kluczy token tooaccess OAuth z hello magazynu kluczy.

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

Skopiuj i Zapisz hello toobe klucza używane w kolejnych krokach hello.

### <a name="step-3-create-an-azure-batch-service-client"></a>Krok 3. Tworzenie klienta usługi Azure Batch
Poniższy fragment kodu najpierw importuje moduł Node.js partii zadań azure hello, a następnie tworzy klienta usługi partia zadań. Należy toofirst utworzyć obiekt SharedKeyCredentials kluczem hello partii konta kopiowane z hello w poprzednim kroku.

```nodejs
// Initializing Azure Batch variables

var batch = require('azure-batch');

var accountName = '<azure-batch-account-name>';

var accountKey = '<account-key-downloaded>';

var accountUrl = '<account-url>'

// Create Batch credentials object using account name and account key

var credentials = new batch.SharedKeyCredentials(accountName,accountKey);

// Create Batch service client

var batch_client = new batch.ServiceClient(credentials,accountUrl);

```

Hello identyfikator URI usługi partia zadań Azure można znaleźć na karcie Przegląd hello hello portalu Azure. Jest w formacie hello:

`https://accountname.location.batch.azure.com`

Można znaleźć toohello zrzut ekranu:

![Identyfikator URI usługi Azure Batch](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a>Krok 4. Tworzenie puli usługi Azure Batch
Pula usługi Azure Batch składa się z wielu maszyn wirtualnych (znanych także jako węzły usługi Batch). Usługa partia zadań Azure wdraża hello zadania na tych węzłach i zarządza nimi. Można określić następujące parametry konfiguracji pulę hello.

* Typ obrazu maszyny wirtualnej
* Rozmiar węzłów maszyny wirtualnej
* Liczba węzłów maszyny wirtualnej

> [!Tip]
> Hello rozmiaru i liczby węzłów maszyny wirtualnej dużej mierze zależą hello liczba zadań, które mają toorun w równoległej, a także samo zadanie hello. Zaleca się testowanie toodetermine hello idealne liczby i rozmiaru.
>
>

Witaj poniższy fragment kodu tworzy hello obiektów parametru konfiguracji.

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating hello VM configuration object with hello SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting hello VM size tooStandard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in hello pool too4
var numVMs = 4
```

> [!Tip]
> Aby hello listę dostępnych dla partii zadań Azure i ich identyfikatorów jednostki SKU obrazów maszyny Wirtualnej systemu Linux, zobacz [listy obrazów maszyny wirtualnej](batch-linux-nodes.md#list-of-virtual-machine-images).
>
>

Konfiguracja puli hello jest zdefiniowany, można tworzyć hello puli partii zadań Azure. Hello polecenia puli partii tworzy węzły maszyny wirtualnej platformy Azure i przygotować je toobe tooreceive gotowe zadania tooexecute. Każda pula powinna mieć unikatowy identyfikator, który będzie potrzebny w kolejnych krokach samouczka.

Witaj następującego fragmentu kodu tworzy puli partii zadań Azure.

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

Możesz sprawdzić stan powitania po utworzeniu puli hello i sprawdź, czy stan hello jest "active" przed przejściem dalej z przesyłaniem puli toothat zadania.

```nodejs
var cloudPool = batch_client.pool.get(poolid,function(error,result,request,response){
        if(error == null)
        {

            if(result.state == "active")
            {
                console.log("Pool is active");
            }
        }
        else
        {
            if(error.statusCode==404)
            {
                console.log("Pool not found yet returned 404...");    

            }
            else
            {
                console.log("Error occurred while retrieving pool data");
            }
        }
        });
```

Poniżej znajduje się obiekt wyniku próbki zwracane przez funkcję pool.get hello.

```
{ id: 'processcsv_201721152',
  displayName: 'processcsv_201721152',
  url: 'https://<batch-account-name>.centralus.batch.azure.com/pools/processcsv_201721152',
  eTag: '<eTag>',
  lastModified: 2017-03-27T10:28:02.398Z,
  creationTime: 2017-03-27T10:28:02.398Z,
  state: 'active',
  stateTransitionTime: 2017-03-27T10:28:02.398Z,
  allocationState: 'resizing',
  allocationStateTransitionTime: 2017-03-27T10:28:02.398Z,
  vmSize: 'standard_a1',
  virtualMachineConfiguration:
   { imageReference:
      { publisher: 'Canonical',
        offer: 'UbuntuServer',
        sku: '14.04.2-LTS',
        version: 'latest' },
     nodeAgentSKUId: 'batch.node.ubuntu 14.04' },
  resizeTimeout:
   { [Number: 900000]
     _milliseconds: 900000,
     _days: 0,
     _months: 0,
     _data:
      { milliseconds: 0,
        seconds: 0,
        minutes: 15,
        hours: 0,
        days: 0,
        months: 0,
        years: 0 },
     _locale:
      Locale {
        _calendar: [Object],
        _longDateFormat: [Object],
        _invalidDate: 'Invalid date',
        ordinal: [Function: ordinal],
        _ordinalParse: /\d{1,2}(th|st|nd|rd)/,
        _relativeTime: [Object],
        _months: [Object],
        _monthsShort: [Object],
        _week: [Object],
        _weekdays: [Object],
        _weekdaysMin: [Object],
        _weekdaysShort: [Object],
        _meridiemParse: /[ap]\.?m?\.?/i,
        _abbr: 'en',
        _config: [Object],
        _ordinalParseLenient: /\d{1,2}(th|st|nd|rd)|\d{1,2}/ } },
  currentDedicated: 0,
  targetDedicated: 4,
  enableAutoScale: false,
  enableInterNodeCommunication: false,
  maxTasksPerNode: 1,
  taskSchedulingPolicy: { nodeFillType: 'Spread' } }
```


### <a name="step-4-submit-an-azure-batch-job"></a>Krok 4. Przesyłanie zadania usługi Azure Batch
Zadanie usługi Azure Batch jest logiczną grupą podobnych zadań podrzędnych. W naszym scenariuszu jest "Proces tooJSON csv". Każde przedstawione tutaj zadanie podrzędne może przetwarzać pliki csv zawarte we wszystkich kontenerach usługi Azure Storage.

Te zadania będą uruchamiane równolegle i wdrażane na wielu węzłach zorkiestrowana przez usługi partia zadań Azure hello.

> [!Tip]
> Można użyć hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) właściwości toospecify maksymalna liczba zadań, które można uruchomić jednocześnie w jednym węźle.
>
>

#### <a name="preparation-task"></a>Zadanie podrzędne przygotowania

węzły maszyny Wirtualnej Hello tworzone są puste Ubuntu węzłów. Często konieczne tooinstall zestaw programów jako warunki wstępne.
Zazwyczaj dla systemu Linux węzłów może mieć skrypt powłoki, który instaluje hello wymagania wstępne, przed hello zadania rzeczywistego uruchamiania. Jednak może to być dowolny inny programowalny i wykonywalny skrypt.
Witaj [skryptu powłoki](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) w tym przykładzie instaluje narzędzie pip Python i hello zestawu SDK usługi Magazyn Azure dla języka Python.

Możesz przekazać skrypt hello na konto magazynu Azure i generowania skryptu hello tooaccess identyfikatora URI połączenia SAS. Ten proces można również zautomatyzować, używając hello zestawu Node.js SDK usługi Magazyn Azure.

> [!Tip]
> Zadanie przygotowanie zadania działa tylko na powitania węzłach maszyny Wirtualnej, których hello konkretne zadanie wymaga toorun. Jeśli chcesz toobe wymagania wstępne zainstalowane we wszystkich węzłach, niezależnie od zadania hello, które będą uruchamiane w nim, można użyć hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) właściwości podczas dodawania puli. Możesz użyć powitania po definicji zadania przygotowanie odwołania.
>
>

Przygotowanie zadania jest określana podczas przesyłania hello zadania partii zadań Azure. Poniżej są hello parametry konfiguracji zadania przygotowania:

* **Identyfikator**: Unikatowy identyfikator hello przygotowanie zadania
* **commandLine**: plik wykonywalny zadania hello tooexecute wiersza polecenia
* **resourceFiles**: Tablica obiektów zawierających szczegóły dotyczące plików potrzebne toobe pobierane dla toorun tego zadania.  Poniżej przedstawiono dostępne opcje
    - blobSource: hello identyfikatora URI połączenia SAS hello pliku
    - Ścieżka pliku: toodownload ścieżka lokalna i Zapisz plik hello
    - fileMode: dotyczy wyłącznie węzłów systemu Linux, opcja fileMode jest w formacie ósemkowym i domyślnie ma wartość 0770
* **waitForSuccess**: zestaw tootrue, hello zadanie nie zostanie uruchomione na przygotowanie niepowodzeń zadań
* **runElevated**: ustaw ją tootrue, jeśli zadanie hello toorun wymagane są podniesione uprawnienia.

Poniższy fragment kodu przedstawia hello przygotowanie zadania skryptu konfiguracji próbki:

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

Jeśli nie ma żadnych toobe wymagania wstępne zainstalowane dla Twojego toorun zadań, możesz pominąć hello przygotowanie zadania. Następujący kod tworzy zadanie o nazwie wyświetlanej „process csv files” (konwertowanie plików csv).

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job toohello pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a>Krok 5. Przesyłanie zadań podrzędnych usługi Azure Batch do zadania

Po utworzeniu zadania konwertującego pliki csv można utworzyć dla niego zadania podrzędne. Zakładając, że mamy cztery kontenery, będziemy mieć cztery zadania toocreate, po jednej dla każdego kontenera.

Jeśli przyjrzymy się hello [skrypt w języku Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), przyjmuje dwa parametry:

* Nazwa kontenera: hello pliki toodownload kontenera magazynu z
* wzorzec: opcjonalny parametr wzorca nazwy plików

Zakładając, że mamy cztery kontenery "con1", "con2", "con3", "con4" poniższy kod przedstawia przesyłanie dla zadań toohello partii zadań Azure zadania "proces csv" utworzony wcześniej.

```nodejs
// storing container names in an array
var container_list = ["con1","con2","con3","con4"]
    container_list.forEach(function(val,index){           

           var container_name = val;
           var taskID = container_name + "_process";
           var task_config = {id:taskID,displayName:'process csv in ' + container_name,commandLine:'python processcsv.py --container ' + container_name,resourceFiles:[{'blobSource':'<blob SAS URI>','filePath':'processcsv.py'}]}
           var task = batch_client.task.add(poolid,task_config,function(error,result){
                if(error != null)
                {
                    console.log(error.response);     
                }
                else
                {
                    console.log("Task for container : " + container_name + "submitted successfully");
                }



           });

    });
```

Kod Hello dodaje wielu zadań toohello puli. I poszczególnych zadań hello jest wykonywana w węźle hello puli maszyny wirtualne utworzone. Jeśli hello liczba zadań przekracza hello liczbę maszyn wirtualnych w puli lub hello właściwości maxTasksPerNode, zadania hello poczekaj, aż węzeł ma zostać udostępnione. Takie ograniczenia są zapewniane przez usługę Azure Batch automatycznie.

Hello portal przedstawiono szczegółowe widoki na powitania zadania i stany zadania. Można również użyć listy hello i uzyskać funkcje w hello węzła zestawu SDK platformy Azure. Szczegółowe informacje znajdują się w dokumentacji hello [łącze](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).

## <a name="next-steps"></a>Następne kroki

- Przejrzyj hello [funkcji partii omówienie Azure](batch-api-basics.md) artykułu, w którym firma Microsoft zaleca, jeśli masz nową usługę toohello.
- Zobacz hello [odwołania Node.js partii](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) hello tooexplore interfejsu API partii.

