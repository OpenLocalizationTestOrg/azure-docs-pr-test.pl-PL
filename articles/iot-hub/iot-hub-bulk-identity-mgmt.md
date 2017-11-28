---
title: "Eksport aaaImport tożsamości urządzenia Azure IoT Hub | Dokumentacja firmy Microsoft"
description: "Jak toouse hello Azure IoT usługi SDK tooperform zbiorcze operacje tooimport rejestru tożsamości hello i eksportowanie tożsamości urządzenia. Operacje importowania Włącz toocreate, aktualizacji i usuwania tożsamości urządzenia w partii."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2ade1494-45ea-46a7-ade7-cf6e11ce62da
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b67777d381e03de05d9c007b5ce6bdaf15bbb8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="fd8f7-104">Zarządzanie tożsamościami urządzenia IoT Hub zbiorcze</span><span class="sxs-lookup"><span data-stu-id="fd8f7-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="fd8f7-105">Każdy Centrum IoT ma rejestru tożsamości w usłudze hello służy toocreate zasobów na urządzenie.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-105">Each IoT hub has an identity registry you can use toocreate per-device resources in hello service.</span></span> <span data-ttu-id="fd8f7-106">Witaj tożsamości rejestru można również toocontrol dostępu toohello uwzględniającym działania urządzenia z punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-106">hello identity registry also enables you toocontrol access toohello device-facing endpoints.</span></span> <span data-ttu-id="fd8f7-107">W tym artykule opisano, jak tooimport i eksportowanie tożsamości urządzenia w zbiorcze tooand z rejestru tożsamości.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-107">This article describes how tooimport and export device identities in bulk tooand from an identity registry.</span></span>

<span data-ttu-id="fd8f7-108">Importowanie i eksportowanie działania mają miejsce w kontekście hello *zadania* pozwalające operacje usługi zbiorcze tooexecute względem Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-108">Import and export operations take place in hello context of *Jobs* that enable you tooexecute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="fd8f7-109">Witaj **RegistryManager** klasa zawiera hello **ExportDevicesAsync** i **ImportDevicesAsync** metody, które używają hello **zadania** Struktura.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-109">hello **RegistryManager** class includes hello **ExportDevicesAsync** and **ImportDevicesAsync** methods that use hello **Job** framework.</span></span> <span data-ttu-id="fd8f7-110">Te metody umożliwiają tooexport, importu i zsynchronizować hello całości rejestru tożsamości Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-110">These methods enable you tooexport, import, and synchronize hello entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="fd8f7-111">Co to są zadania?</span><span class="sxs-lookup"><span data-stu-id="fd8f7-111">What are jobs?</span></span>

<span data-ttu-id="fd8f7-112">Operacje rejestru tożsamości Użyj hello **zadania** systemu hello podczas operacji:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-112">Identity registry operations use hello **Job** system when hello operation:</span></span>

* <span data-ttu-id="fd8f7-113">Jest potencjalnie długi czas wykonywania porównywany toostandard czasu wykonywania operacji.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-113">Has a potentially long execution time compared toostandard run-time operations.</span></span>
* <span data-ttu-id="fd8f7-114">Zwraca dużą ilość danych toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-114">Returns a large amount of data toohello user.</span></span>

<span data-ttu-id="fd8f7-115">Zamiast jednego wywołania interfejsu API Oczekiwanie lub blokowania na powitania wynik operacji hello, tworzy asynchronicznie operację hello **zadania** dla tego Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-115">Instead of a single API call waiting or blocking on hello result of hello operation, hello operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="fd8f7-116">Operacja Hello następnie natychmiast zwraca **JobProperties** obiektu.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-116">hello operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="fd8f7-117">powitania po C# kodu fragment kodu przedstawia sposób toocreate zadania eksportu:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-117">hello following C# code snippet shows how toocreate an export job:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="fd8f7-118">Witaj toouse **RegistryManager** klasy w kodzie C#, Dodaj hello **Microsoft.Azure.Devices** projekt tooyour pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-118">toouse hello **RegistryManager** class in your C# code, add hello **Microsoft.Azure.Devices** NuGet package tooyour project.</span></span> <span data-ttu-id="fd8f7-119">Witaj **RegistryManager** klasa znajduje się w hello **Microsoft.Azure.Devices** przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-119">hello **RegistryManager** class is in hello **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="fd8f7-120">Można użyć hello **RegistryManager** klasy tooquery stan hello hello **zadania** przy użyciu hello zwrócił **JobProperties** metadanych.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-120">You can use hello **RegistryManager** class tooquery hello state of hello **Job** using hello returned **JobProperties** metadata.</span></span>

<span data-ttu-id="fd8f7-121">Witaj poniższy fragment kodu C# przedstawia sposób toopoll toosee co pięć sekund, jeśli hello zadania zakończono wykonywanie:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-121">hello following C# code snippet shows how toopoll every five seconds toosee if hello job has finished executing:</span></span>

```csharp
// Wait until job is finished
while(true)
{
  exportJob = await registryManager.GetJobAsync(exportJob.JobId);
  if (exportJob.Status == JobStatus.Completed || 
      exportJob.Status == JobStatus.Failed ||
      exportJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="export-devices"></a><span data-ttu-id="fd8f7-122">Eksportuj urządzeń</span><span class="sxs-lookup"><span data-stu-id="fd8f7-122">Export devices</span></span>

<span data-ttu-id="fd8f7-123">Użyj hello **ExportDevicesAsync** metody tooexport hello całości IoT hub tożsamości rejestru tooan [usługi Azure Storage](../storage/index.md) przy użyciu kontenera obiektów blob [sygnatura dostępu współdzielonego](../storage/common/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="fd8f7-123">Use hello **ExportDevicesAsync** method tooexport hello entirety of an IoT hub identity registry tooan [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="fd8f7-124">Ta metoda umożliwia toocreate niezawodne kopie zapasowe danych urządzenia w kontenerze obiektów blob, którą kontrolujesz.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-124">This method enables you toocreate reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="fd8f7-125">Witaj **ExportDevicesAsync** wymaga, aby dwa parametry:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-125">hello **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="fd8f7-126">A *ciąg* zawiera identyfikator URI kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="fd8f7-127">Ten identyfikator URI musi zawierać token sygnatury dostępu Współdzielonego, która udziela dostępu do zapisu toohello kontenera.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-127">This URI must contain a SAS token that grants write access toohello container.</span></span> <span data-ttu-id="fd8f7-128">zadanie Hello tworzy blokowych obiektów blob w danych toostore urządzenia eksportu hello serializacji tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-128">hello job creates a block blob in this container toostore hello serialized export device data.</span></span> <span data-ttu-id="fd8f7-129">token sygnatury dostępu Współdzielonego Hello musi zawierać następujące uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-129">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="fd8f7-130">A *logiczna* wskazująca, czy ma klucze uwierzytelniania tooexclude eksportowania danych.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-130">A *boolean* that indicates if you want tooexclude authentication keys from your export data.</span></span> <span data-ttu-id="fd8f7-131">Jeśli **false**, klucze uwierzytelniania znajdują się w danych wyjściowych eksportu.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="fd8f7-132">W przeciwnym razie klucze są eksportowane jako **null**.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="fd8f7-133">Hello poniższy fragment kodu C# przedstawia sposób tooinitiate zadania eksportu zawierający klucze uwierzytelniania urządzenia w hello eksportować dane i następnie sondować zakończenia:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-133">hello following C# code snippet shows how tooinitiate an export job that includes device authentication keys in hello export data and then poll for completion:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);

// Wait until job is finished
while(true)
{
    exportJob = await registryManager.GetJobAsync(exportJob.JobId);
    if (exportJob.Status == JobStatus.Completed || 
        exportJob.Status == JobStatus.Failed ||
        exportJob.Status == JobStatus.Cancelled)
    {
    // Job has finished executing
    break;
    }

    await Task.Delay(TimeSpan.FromSeconds(5));
}
```

<span data-ttu-id="fd8f7-134">Hello zadania są przechowywane jego dane wyjściowe w kontenerze obiektów blob hello podany jako blokowych obiektów blob o nazwie hello **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-134">hello job stores its output in hello provided blob container as a block blob with hello name **devices.txt**.</span></span> <span data-ttu-id="fd8f7-135">dane wyjściowe Hello składa się z danych urządzenia Zserializowany do postaci JSON, jedno urządzenie w jednym wierszu.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-135">hello output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="fd8f7-136">Witaj poniższy przykład przedstawia dane wyjściowe hello:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-136">hello following example shows hello output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Jeśli urządzenie ma dwie danych, Witaj dwie danych również zostaną wyeksportowane wraz z hello danych urządzenia. Witaj poniższy przykład przedstawia tego formatu. <span data-ttu-id="fd8f7-139">Wszystkie dane w wierszu "twinETag" hello, aż do zakończenia hello są dwie danych.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-139">All data from hello "twinETag" line until hello end are twin data.</span></span>

```json
{
   "id":"export-6d84f075-0",
   "eTag":"MQ==",
   "status":"enabled",
   "statusReason":"firstUpdate",
   "authentication":null,
   "twinETag":"AAAAAAAAAAI=",
   "tags":{
      "Location":"LivingRoom"
   },
   "properties":{
      "desired":{
         "Thermostat":{
            "Temperature":75.1,
            "Unit":"F"
         },
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
            "$lastUpdatedVersion":2,
            "Thermostat":{
               "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
               "$lastUpdatedVersion":2,
               "Temperature":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               },
               "Unit":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               }
            }
         },
         "$version":2
      },
      "reported":{
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:51.1309437Z"
         },
         "$version":1
      }
   }
}
```

<span data-ttu-id="fd8f7-140">Jeśli muszą uzyskać dostęp do danych toothis w kodzie, można łatwo deserializacji te dane przy użyciu hello **ExportImportDevice** klasy.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-140">If you need access toothis data in code, you can easily deserialize this data using hello **ExportImportDevice** class.</span></span> <span data-ttu-id="fd8f7-141">Witaj poniższy fragment kodu C# przedstawia sposób informacje o urządzeniu tooread, który został wcześniej wyeksportowany tooa blokowych obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-141">hello following C# code snippet shows how tooread device information that was previously exported tooa block blob:</span></span>

```csharp
var exportedDevices = new List<ExportImportDevice>();

using (var streamReader = new StreamReader(await blob.OpenReadAsync(AccessCondition.GenerateIfExistsCondition(), null, null), Encoding.UTF8))
{
  while (streamReader.Peek() != -1)
  {
    string line = await streamReader.ReadLineAsync();
    var device = JsonConvert.DeserializeObject<ExportImportDevice>(line);
    exportedDevices.Add(device);
  }
}
```

> [!NOTE]
> <span data-ttu-id="fd8f7-142">Można również użyć hello **GetDevicesAsync** metody hello **RegistryManager** toofetch klasy listy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-142">You can also use hello **GetDevicesAsync** method of hello **RegistryManager** class toofetch a list of your devices.</span></span> <span data-ttu-id="fd8f7-143">Jednak takie podejście charakteryzuje się twardych limit 1000 liczby hello obiekty urządzeń, które są zwracane.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-143">However, this approach has a hard cap of 1000 on hello number of device objects that are returned.</span></span> <span data-ttu-id="fd8f7-144">przypadek użycia dla hello oczekiwano Hello **GetDevicesAsync** metoda do rozwoju scenariusze tooaid debugowania i nie jest zalecane w przypadku obciążeń produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-144">hello expected use case for hello **GetDevicesAsync** method is for development scenarios tooaid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="fd8f7-145">Importuj urządzeń</span><span class="sxs-lookup"><span data-stu-id="fd8f7-145">Import devices</span></span>

<span data-ttu-id="fd8f7-146">Witaj **ImportDevicesAsync** metoda hello **RegistryManager** klasa umożliwia tooperform operacji importowania i synchronizacji zbiorczego w rejestrze tożsamości Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-146">hello **ImportDevicesAsync** method in hello **RegistryManager** class enables you tooperform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="fd8f7-147">Podobnie jak hello **ExportDevicesAsync** metoda, hello **ImportDevicesAsync** metoda używa hello **zadania** framework.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-147">Like hello **ExportDevicesAsync** method, hello **ImportDevicesAsync** method uses hello **Job** framework.</span></span>

<span data-ttu-id="fd8f7-148">Zajmie się przy użyciu hello **ImportDevicesAsync** metody, ponieważ w dodanie tooprovisioning nowych urządzeń w rejestrze tożsamości, można również aktualizować i usuwać istniejące urządzenia.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-148">Take care using hello **ImportDevicesAsync** method because in addition tooprovisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="fd8f7-149">Nie można cofnąć operacji importowania.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-149">An import operation cannot be undone.</span></span> <span data-ttu-id="fd8f7-150">Zawsze utworzyć kopię zapasową istniejących danych przy użyciu hello **ExportDevicesAsync** metody kontenera obiektów blob tooanother przed wprowadzeniem zbiorcze zmiany tooyour rejestru tożsamości.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-150">Always back up your existing data using hello **ExportDevicesAsync** method tooanother blob container before you make bulk changes tooyour identity registry.</span></span>

<span data-ttu-id="fd8f7-151">Witaj **ImportDevicesAsync** metoda przyjmuje dwa parametry:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-151">hello **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="fd8f7-152">A *ciąg* zawiera identyfikator URI [usługi Azure Storage](../storage/index.md) obiektu blob kontenera toouse jako *wejściowych* toohello zadania.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container toouse as *input* toohello job.</span></span> <span data-ttu-id="fd8f7-153">Ten identyfikator URI musi zawierać token sygnatury dostępu Współdzielonego, która udziela dostępu do odczytu toohello kontenera.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-153">This URI must contain a SAS token that grants read access toohello container.</span></span> <span data-ttu-id="fd8f7-154">Ten kontener musi zawierać obiektu blob o nazwie hello **devices.txt** zawierający tooimport danych urządzenia hello serializowany w rejestrze tożsamości.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-154">This container must contain a blob with hello name **devices.txt** that contains hello serialized device data tooimport into your identity registry.</span></span> <span data-ttu-id="fd8f7-155">Witaj importowanie danych musi zawierać informacje o urządzeniu w hello JSON tego samego formatu tego hello **ExportImportDevice** podczas tworzenia zadania używa **devices.txt** obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-155">hello import data must contain device information in hello same JSON format that hello **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="fd8f7-156">token sygnatury dostępu Współdzielonego Hello musi zawierać następujące uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-156">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="fd8f7-157">A *ciąg* zawiera identyfikator URI [usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/) obiektu blob kontenera toouse jako *dane wyjściowe* z hello zadania.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container toouse as *output* from hello job.</span></span> <span data-ttu-id="fd8f7-158">Hello zadanie tworzy blokowych obiektów blob w tym toostore kontenera informacje o błędzie z importu ukończyć powitalnych **zadania**.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-158">hello job creates a block blob in this container toostore any error information from hello completed import **Job**.</span></span> <span data-ttu-id="fd8f7-159">token sygnatury dostępu Współdzielonego Hello musi zawierać następujące uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-159">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="fd8f7-160">Witaj dwa parametry może wskazywać toohello tego samego kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-160">hello two parameters can point toohello same blob container.</span></span> <span data-ttu-id="fd8f7-161">Parametry oddzielne Hello po prostu włącz większą kontrolę nad danych jako kontener danych wyjściowych hello wymaga dodatkowych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-161">hello separate parameters simply enable more control over your data as hello output container requires additional permissions.</span></span>

<span data-ttu-id="fd8f7-162">powitania po C# kodu fragment kodu przedstawia sposób tooinitiate zadania importu:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-162">hello following C# code snippet shows how tooinitiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="fd8f7-163">Ta metoda może być również używane tooimport dane hello Witaj dwie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-163">This method can also be used tooimport hello data for hello device twin.</span></span> <span data-ttu-id="fd8f7-164">format Hello hello danych wejściowych jest sama hello jako hello formacie pokazanym na powitania **ExportDevicesAsync** sekcji.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-164">hello format for hello data input is hello same as hello format shown in hello **ExportDevicesAsync** section.</span></span> <span data-ttu-id="fd8f7-165">W ten sposób można ponownie zaimportować hello wyeksportowane dane.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-165">In this way, you can reimport hello exported data.</span></span> <span data-ttu-id="fd8f7-166">Witaj **$metadata** jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-166">hello **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="fd8f7-167">Zachowanie importu</span><span class="sxs-lookup"><span data-stu-id="fd8f7-167">Import behavior</span></span>

<span data-ttu-id="fd8f7-168">Można użyć hello **ImportDevicesAsync** metody tooperform hello następujące zbiorcze operacje w rejestrze tożsamości:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-168">You can use hello **ImportDevicesAsync** method tooperform hello following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="fd8f7-169">Rejestracji zbiorczej nowych urządzeń</span><span class="sxs-lookup"><span data-stu-id="fd8f7-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="fd8f7-170">Zbiorczego usuwania istniejących urządzeń</span><span class="sxs-lookup"><span data-stu-id="fd8f7-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="fd8f7-171">Zbiorcze zmiany stanu (Włączanie lub wyłączanie urządzenia)</span><span class="sxs-lookup"><span data-stu-id="fd8f7-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="fd8f7-172">Zbiorcze przypisania nowych kluczy uwierzytelniania urządzenia</span><span class="sxs-lookup"><span data-stu-id="fd8f7-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="fd8f7-173">Zbiorcze automatyczne ponowne generowanie kluczy uwierzytelniania urządzenia</span><span class="sxs-lookup"><span data-stu-id="fd8f7-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="fd8f7-174">Aktualizację zbiorczą dwie danych</span><span class="sxs-lookup"><span data-stu-id="fd8f7-174">Bulk update of twin data</span></span>

<span data-ttu-id="fd8f7-175">Może wykonywać dowolne kombinacje hello poprzedzających operacji w jednym **ImportDevicesAsync** wywołania.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-175">You can perform any combination of hello preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="fd8f7-176">Na przykład można zarejestrować nowych urządzeń i usuwania lub aktualizacji istniejących urządzeń w hello tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-176">For example, you can register new devices and delete or update existing devices at hello same time.</span></span> <span data-ttu-id="fd8f7-177">Gdy jest używany wraz z hello **ExportDevicesAsync** metody, można całkowicie migracji wszystkich urządzeń z jednego tooanother Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-177">When used along with hello **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub tooanother.</span></span>

<span data-ttu-id="fd8f7-178">Jeśli hello plik importu zawiera dwie metadanych, te metadane zastępuje istniejące metadane dwie hello.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-178">If hello import file includes twin metadata, then this metadata overwrites hello existing twin metadata.</span></span> <span data-ttu-id="fd8f7-179">Jeśli hello plik importu nie zawiera metadanych dwie, następnie tylko hello `lastUpdateTime` metadanych jest aktualizowany przy użyciu hello bieżącego czasu.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-179">If hello import file does not include twin metadata, then only hello `lastUpdateTime` metadata is updated using hello current time.</span></span>

<span data-ttu-id="fd8f7-180">Użyj hello opcjonalne **parametrem importMode** właściwości w danych serializacji importu powitania dla każdego urządzenia toocontrol hello importu procesu na urządzenie.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-180">Use hello optional **importMode** property in hello import serialization data for each device toocontrol hello import process per-device.</span></span> <span data-ttu-id="fd8f7-181">Witaj **parametrem importMode** właściwość ma hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-181">hello **importMode** property has hello following options:</span></span>

| <span data-ttu-id="fd8f7-182">parametrem importMode</span><span class="sxs-lookup"><span data-stu-id="fd8f7-182">importMode</span></span> | <span data-ttu-id="fd8f7-183">Opis</span><span class="sxs-lookup"><span data-stu-id="fd8f7-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fd8f7-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="fd8f7-184">**createOrUpdate**</span></span> |<span data-ttu-id="fd8f7-185">Jeśli urządzenie nie istnieje z hello określony **identyfikator**, nowo jest zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-185">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="fd8f7-186">Jeśli urządzenie hello już istnieje, istniejące informacje zostały zastąpione hello podane dane wejściowe bez względu toohello **ETag** wartość.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-186">If hello device already exists, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br> <span data-ttu-id="fd8f7-187">Hello użytkownika można opcjonalnie określić dwie danych wraz z danymi, hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-187">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="fd8f7-188">Witaj dwie etag, jeśli jest określony, są przetwarzane niezależnie z urządzenia hello etag.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-188">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="fd8f7-189">W przypadku niezgodności z etag Witaj dwie istniejących toohello plik dziennika zostanie zapisany błąd.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-189">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="fd8f7-190">**create**</span><span class="sxs-lookup"><span data-stu-id="fd8f7-190">**create**</span></span> |<span data-ttu-id="fd8f7-191">Jeśli urządzenie nie istnieje z hello określony **identyfikator**, nowo jest zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-191">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="fd8f7-192">Jeśli urządzenie hello już istnieje, toohello plik dziennika zostanie zapisany błąd.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-192">If hello device already exists, an error is written toohello log file.</span></span> <br> <span data-ttu-id="fd8f7-193">Hello użytkownika można opcjonalnie określić dwie danych wraz z danymi, hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-193">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="fd8f7-194">Witaj dwie etag, jeśli jest określony, są przetwarzane niezależnie z urządzenia hello etag.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-194">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="fd8f7-195">W przypadku niezgodności z etag Witaj dwie istniejących toohello plik dziennika zostanie zapisany błąd.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-195">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="fd8f7-196">**Aktualizacja**</span><span class="sxs-lookup"><span data-stu-id="fd8f7-196">**update**</span></span> |<span data-ttu-id="fd8f7-197">Jeśli urządzenie już istnieje z hello określony **identyfikator**, istniejące informacje zostały zastąpione hello podane dane wejściowe bez względu toohello **ETag** wartość.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-197">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="fd8f7-198">Jeśli urządzenie hello nie istnieje, toohello plik dziennika zostanie zapisany błąd.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-198">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="fd8f7-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="fd8f7-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="fd8f7-200">Jeśli urządzenie już istnieje z hello określony **identyfikator**, istniejące informacje zostały zastąpione hello podane dane wejściowe tylko wtedy, gdy istnieje **ETag** zgodne.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-200">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="fd8f7-201">Jeśli urządzenie hello nie istnieje, toohello plik dziennika zostanie zapisany błąd.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-201">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="fd8f7-202">W przypadku **ETag** niezgodności, jest zapisywany błąd toohello pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-202">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> |
| <span data-ttu-id="fd8f7-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="fd8f7-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="fd8f7-204">Jeśli urządzenie nie istnieje z hello określony **identyfikator**, nowo jest zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-204">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="fd8f7-205">Jeśli urządzenie hello już istnieje, istniejące informacje zostały zastąpione hello podane dane wejściowe tylko wtedy, gdy istnieje **ETag** zgodne.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-205">If hello device already exists, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="fd8f7-206">W przypadku **ETag** niezgodności, jest zapisywany błąd toohello pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-206">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> <br> <span data-ttu-id="fd8f7-207">Hello użytkownika można opcjonalnie określić dwie danych wraz z danymi, hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-207">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="fd8f7-208">Witaj dwie etag, jeśli jest określony, są przetwarzane niezależnie z urządzenia hello etag.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-208">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="fd8f7-209">W przypadku niezgodności z etag Witaj dwie istniejących toohello plik dziennika zostanie zapisany błąd.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-209">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="fd8f7-210">**usuwanie**</span><span class="sxs-lookup"><span data-stu-id="fd8f7-210">**delete**</span></span> |<span data-ttu-id="fd8f7-211">Jeśli urządzenie już istnieje z hello określony **identyfikator**, jest usuwany bez względu toohello **ETag** wartość.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-211">If a device already exists with hello specified **id**, it is deleted without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="fd8f7-212">Jeśli urządzenie hello nie istnieje, toohello plik dziennika zostanie zapisany błąd.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-212">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="fd8f7-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="fd8f7-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="fd8f7-214">Jeśli urządzenie już istnieje z hello określony **identyfikator**, jest usuwany, tylko wtedy, gdy istnieje **ETag** zgodne.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-214">If a device already exists with hello specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="fd8f7-215">Jeśli urządzenie hello nie istnieje, toohello plik dziennika zostanie zapisany błąd.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-215">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="fd8f7-216">Jeśli element etag toohello plik dziennika zostanie zapisany błąd.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-216">If there is an ETag mismatch, an error is written toohello log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="fd8f7-217">Jeśli dane serializacji hello nie jawnie definiować **parametrem importMode** flagi dla urządzeń, domyślne zbyt**createOrUpdate** podczas hello operację importowania.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-217">If hello serialization data does not explicitly define an **importMode** flag for a device, it defaults too**createOrUpdate** during hello import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="fd8f7-218">Importuj przykładowe urządzeń — zbiorcze, inicjowanie obsługi administracyjnej urządzeń</span><span class="sxs-lookup"><span data-stu-id="fd8f7-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="fd8f7-219">Witaj poniższy przykład kodu C# ilustruje sposób toogenerate wiele tożsamości urządzenia który:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-219">hello following C# code sample illustrates how toogenerate multiple device identities that:</span></span>

* <span data-ttu-id="fd8f7-220">Zawierają klucze uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-220">Include authentication keys.</span></span>
* <span data-ttu-id="fd8f7-221">Zapis tego urządzenia informacji tooa blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-221">Write that device information tooa block blob.</span></span>
* <span data-ttu-id="fd8f7-222">Importuj hello urządzeń w rejestrze tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-222">Import hello devices into hello identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in hello Microsoft.Azure.Devices.Common namespace
  var deviceToAdd = new ExportImportDevice()
  {
    Id = Guid.NewGuid().ToString(),
    Status = DeviceStatus.Enabled,
    Authentication = new AuthenticationMechanism()
    {
      SymmetricKey = new SymmetricKey()
      {
        PrimaryKey = CryptoKeyGenerator.GenerateKey(32),
        SecondaryKey = CryptoKeyGenerator.GenerateKey(32)
      }
    },
    ImportMode = ImportMode.Create
  };

  // Add device toohello list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write hello list toohello blob
var sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice => sb.AppendLine(serializedDevice));
await blob.DeleteIfExistsAsync();

using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Call import using hello blob tooadd new devices
// Log information related toohello job is written toohello same container
// This normally takes 1 minute per 100 devices
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="fd8f7-223">Przykład urządzeń importu — zbiorczego usuwania</span><span class="sxs-lookup"><span data-stu-id="fd8f7-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="fd8f7-224">Hello poniższy przykład kodu pokazuje sposób toodelete hello urządzeń, które można dodać za pomocą hello powyższego przykładu kodu:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-224">hello following code sample shows you how toodelete hello devices you added using hello previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode toobe Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back tooan ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write hello new import data back toohello block blob
await blob.DeleteIfExistsAsync();
using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Step 3: Call import using hello same blob toodelete all devices
importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="get-hello-container-sas-uri"></a><span data-ttu-id="fd8f7-225">Pobierz kontener hello identyfikatora URI połączenia SAS</span><span class="sxs-lookup"><span data-stu-id="fd8f7-225">Get hello container SAS URI</span></span>

<span data-ttu-id="fd8f7-226">Witaj poniższy przykład kodu pokazuje sposób toogenerate [identyfikatora URI połączenia SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) o odczytu, zapisu i usuwania uprawnień do kontenera obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-226">hello following code sample shows you how toogenerate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set hello expiry time and permissions for hello container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate hello shared access signature on hello container,
  // setting hello constraints directly on hello signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return hello URI string for hello container,
  // including hello SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a><span data-ttu-id="fd8f7-227">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fd8f7-227">Next steps</span></span>

<span data-ttu-id="fd8f7-228">W tym artykule przedstawiono sposób tooperform zbiorcze operacje rejestru tożsamości hello w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="fd8f7-228">In this article, you learned how tooperform bulk operations against hello identity registry in an IoT hub.</span></span> <span data-ttu-id="fd8f7-229">Wykonaj te toolearn łącza więcej informacji na temat zarządzania Centrum IoT Azure:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-229">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="fd8f7-230">[Metryki Centrum IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="fd8f7-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="fd8f7-231">[Operacje monitorowania][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="fd8f7-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="fd8f7-232">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="fd8f7-232">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="fd8f7-233">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="fd8f7-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="fd8f7-234">[Symuluje urządzenia IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="fd8f7-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
