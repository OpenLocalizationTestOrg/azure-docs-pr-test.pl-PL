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
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a>Zarządzanie tożsamościami urządzenia IoT Hub zbiorcze

Każdy Centrum IoT ma rejestru tożsamości w usłudze hello służy toocreate zasobów na urządzenie. Witaj tożsamości rejestru można również toocontrol dostępu toohello uwzględniającym działania urządzenia z punktów końcowych. W tym artykule opisano, jak tooimport i eksportowanie tożsamości urządzenia w zbiorcze tooand z rejestru tożsamości.

Importowanie i eksportowanie działania mają miejsce w kontekście hello *zadania* pozwalające operacje usługi zbiorcze tooexecute względem Centrum IoT.

Witaj **RegistryManager** klasa zawiera hello **ExportDevicesAsync** i **ImportDevicesAsync** metody, które używają hello **zadania** Struktura. Te metody umożliwiają tooexport, importu i zsynchronizować hello całości rejestru tożsamości Centrum IoT.

## <a name="what-are-jobs"></a>Co to są zadania?

Operacje rejestru tożsamości Użyj hello **zadania** systemu hello podczas operacji:

* Jest potencjalnie długi czas wykonywania porównywany toostandard czasu wykonywania operacji.
* Zwraca dużą ilość danych toohello użytkownika.

Zamiast jednego wywołania interfejsu API Oczekiwanie lub blokowania na powitania wynik operacji hello, tworzy asynchronicznie operację hello **zadania** dla tego Centrum IoT. Operacja Hello następnie natychmiast zwraca **JobProperties** obiektu.

powitania po C# kodu fragment kodu przedstawia sposób toocreate zadania eksportu:

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> Witaj toouse **RegistryManager** klasy w kodzie C#, Dodaj hello **Microsoft.Azure.Devices** projekt tooyour pakietu NuGet. Witaj **RegistryManager** klasa znajduje się w hello **Microsoft.Azure.Devices** przestrzeni nazw.

Można użyć hello **RegistryManager** klasy tooquery stan hello hello **zadania** przy użyciu hello zwrócił **JobProperties** metadanych.

Witaj poniższy fragment kodu C# przedstawia sposób toopoll toosee co pięć sekund, jeśli hello zadania zakończono wykonywanie:

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

## <a name="export-devices"></a>Eksportuj urządzeń

Użyj hello **ExportDevicesAsync** metody tooexport hello całości IoT hub tożsamości rejestru tooan [usługi Azure Storage](../storage/index.md) przy użyciu kontenera obiektów blob [sygnatura dostępu współdzielonego](../storage/common/storage-security-guide.md#data-plane-security).

Ta metoda umożliwia toocreate niezawodne kopie zapasowe danych urządzenia w kontenerze obiektów blob, którą kontrolujesz.

Witaj **ExportDevicesAsync** wymaga, aby dwa parametry:

* A *ciąg* zawiera identyfikator URI kontenera obiektów blob. Ten identyfikator URI musi zawierać token sygnatury dostępu Współdzielonego, która udziela dostępu do zapisu toohello kontenera. zadanie Hello tworzy blokowych obiektów blob w danych toostore urządzenia eksportu hello serializacji tego kontenera. token sygnatury dostępu Współdzielonego Hello musi zawierać następujące uprawnienia:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* A *logiczna* wskazująca, czy ma klucze uwierzytelniania tooexclude eksportowania danych. Jeśli **false**, klucze uwierzytelniania znajdują się w danych wyjściowych eksportu. W przeciwnym razie klucze są eksportowane jako **null**.

Hello poniższy fragment kodu C# przedstawia sposób tooinitiate zadania eksportu zawierający klucze uwierzytelniania urządzenia w hello eksportować dane i następnie sondować zakończenia:

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

Hello zadania są przechowywane jego dane wyjściowe w kontenerze obiektów blob hello podany jako blokowych obiektów blob o nazwie hello **devices.txt**. dane wyjściowe Hello składa się z danych urządzenia Zserializowany do postaci JSON, jedno urządzenie w jednym wierszu.

Witaj poniższy przykład przedstawia dane wyjściowe hello:

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Jeśli urządzenie ma dwie danych, Witaj dwie danych również zostaną wyeksportowane wraz z hello danych urządzenia. Witaj poniższy przykład przedstawia tego formatu. Wszystkie dane w wierszu "twinETag" hello, aż do zakończenia hello są dwie danych.

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

Jeśli muszą uzyskać dostęp do danych toothis w kodzie, można łatwo deserializacji te dane przy użyciu hello **ExportImportDevice** klasy. Witaj poniższy fragment kodu C# przedstawia sposób informacje o urządzeniu tooread, który został wcześniej wyeksportowany tooa blokowych obiektów blob:

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
> Można również użyć hello **GetDevicesAsync** metody hello **RegistryManager** toofetch klasy listy urządzeń. Jednak takie podejście charakteryzuje się twardych limit 1000 liczby hello obiekty urządzeń, które są zwracane. przypadek użycia dla hello oczekiwano Hello **GetDevicesAsync** metoda do rozwoju scenariusze tooaid debugowania i nie jest zalecane w przypadku obciążeń produkcyjnych.

## <a name="import-devices"></a>Importuj urządzeń

Witaj **ImportDevicesAsync** metoda hello **RegistryManager** klasa umożliwia tooperform operacji importowania i synchronizacji zbiorczego w rejestrze tożsamości Centrum IoT. Podobnie jak hello **ExportDevicesAsync** metoda, hello **ImportDevicesAsync** metoda używa hello **zadania** framework.

Zajmie się przy użyciu hello **ImportDevicesAsync** metody, ponieważ w dodanie tooprovisioning nowych urządzeń w rejestrze tożsamości, można również aktualizować i usuwać istniejące urządzenia.

> [!WARNING]
> Nie można cofnąć operacji importowania. Zawsze utworzyć kopię zapasową istniejących danych przy użyciu hello **ExportDevicesAsync** metody kontenera obiektów blob tooanother przed wprowadzeniem zbiorcze zmiany tooyour rejestru tożsamości.

Witaj **ImportDevicesAsync** metoda przyjmuje dwa parametry:

* A *ciąg* zawiera identyfikator URI [usługi Azure Storage](../storage/index.md) obiektu blob kontenera toouse jako *wejściowych* toohello zadania. Ten identyfikator URI musi zawierać token sygnatury dostępu Współdzielonego, która udziela dostępu do odczytu toohello kontenera. Ten kontener musi zawierać obiektu blob o nazwie hello **devices.txt** zawierający tooimport danych urządzenia hello serializowany w rejestrze tożsamości. Witaj importowanie danych musi zawierać informacje o urządzeniu w hello JSON tego samego formatu tego hello **ExportImportDevice** podczas tworzenia zadania używa **devices.txt** obiektu blob. token sygnatury dostępu Współdzielonego Hello musi zawierać następujące uprawnienia:

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* A *ciąg* zawiera identyfikator URI [usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/) obiektu blob kontenera toouse jako *dane wyjściowe* z hello zadania. Hello zadanie tworzy blokowych obiektów blob w tym toostore kontenera informacje o błędzie z importu ukończyć powitalnych **zadania**. token sygnatury dostępu Współdzielonego Hello musi zawierać następujące uprawnienia:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> Witaj dwa parametry może wskazywać toohello tego samego kontenera obiektów blob. Parametry oddzielne Hello po prostu włącz większą kontrolę nad danych jako kontener danych wyjściowych hello wymaga dodatkowych uprawnień.

powitania po C# kodu fragment kodu przedstawia sposób tooinitiate zadania importu:

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

Ta metoda może być również używane tooimport dane hello Witaj dwie urządzenia. format Hello hello danych wejściowych jest sama hello jako hello formacie pokazanym na powitania **ExportDevicesAsync** sekcji. W ten sposób można ponownie zaimportować hello wyeksportowane dane. Witaj **$metadata** jest opcjonalna.

## <a name="import-behavior"></a>Zachowanie importu

Można użyć hello **ImportDevicesAsync** metody tooperform hello następujące zbiorcze operacje w rejestrze tożsamości:

* Rejestracji zbiorczej nowych urządzeń
* Zbiorczego usuwania istniejących urządzeń
* Zbiorcze zmiany stanu (Włączanie lub wyłączanie urządzenia)
* Zbiorcze przypisania nowych kluczy uwierzytelniania urządzenia
* Zbiorcze automatyczne ponowne generowanie kluczy uwierzytelniania urządzenia
* Aktualizację zbiorczą dwie danych

Może wykonywać dowolne kombinacje hello poprzedzających operacji w jednym **ImportDevicesAsync** wywołania. Na przykład można zarejestrować nowych urządzeń i usuwania lub aktualizacji istniejących urządzeń w hello tym samym czasie. Gdy jest używany wraz z hello **ExportDevicesAsync** metody, można całkowicie migracji wszystkich urządzeń z jednego tooanother Centrum IoT.

Jeśli hello plik importu zawiera dwie metadanych, te metadane zastępuje istniejące metadane dwie hello. Jeśli hello plik importu nie zawiera metadanych dwie, następnie tylko hello `lastUpdateTime` metadanych jest aktualizowany przy użyciu hello bieżącego czasu.

Użyj hello opcjonalne **parametrem importMode** właściwości w danych serializacji importu powitania dla każdego urządzenia toocontrol hello importu procesu na urządzenie. Witaj **parametrem importMode** właściwość ma hello następujące opcje:

| parametrem importMode | Opis |
| --- | --- |
| **createOrUpdate** |Jeśli urządzenie nie istnieje z hello określony **identyfikator**, nowo jest zarejestrowany. <br/>Jeśli urządzenie hello już istnieje, istniejące informacje zostały zastąpione hello podane dane wejściowe bez względu toohello **ETag** wartość. <br> Hello użytkownika można opcjonalnie określić dwie danych wraz z danymi, hello urządzenia. Witaj dwie etag, jeśli jest określony, są przetwarzane niezależnie z urządzenia hello etag. W przypadku niezgodności z etag Witaj dwie istniejących toohello plik dziennika zostanie zapisany błąd. |
| **create** |Jeśli urządzenie nie istnieje z hello określony **identyfikator**, nowo jest zarejestrowany. <br/>Jeśli urządzenie hello już istnieje, toohello plik dziennika zostanie zapisany błąd. <br> Hello użytkownika można opcjonalnie określić dwie danych wraz z danymi, hello urządzenia. Witaj dwie etag, jeśli jest określony, są przetwarzane niezależnie z urządzenia hello etag. W przypadku niezgodności z etag Witaj dwie istniejących toohello plik dziennika zostanie zapisany błąd. |
| **Aktualizacja** |Jeśli urządzenie już istnieje z hello określony **identyfikator**, istniejące informacje zostały zastąpione hello podane dane wejściowe bez względu toohello **ETag** wartość. <br/>Jeśli urządzenie hello nie istnieje, toohello plik dziennika zostanie zapisany błąd. |
| **updateIfMatchETag** |Jeśli urządzenie już istnieje z hello określony **identyfikator**, istniejące informacje zostały zastąpione hello podane dane wejściowe tylko wtedy, gdy istnieje **ETag** zgodne. <br/>Jeśli urządzenie hello nie istnieje, toohello plik dziennika zostanie zapisany błąd. <br/>W przypadku **ETag** niezgodności, jest zapisywany błąd toohello pliku dziennika. |
| **createOrUpdateIfMatchETag** |Jeśli urządzenie nie istnieje z hello określony **identyfikator**, nowo jest zarejestrowany. <br/>Jeśli urządzenie hello już istnieje, istniejące informacje zostały zastąpione hello podane dane wejściowe tylko wtedy, gdy istnieje **ETag** zgodne. <br/>W przypadku **ETag** niezgodności, jest zapisywany błąd toohello pliku dziennika. <br> Hello użytkownika można opcjonalnie określić dwie danych wraz z danymi, hello urządzenia. Witaj dwie etag, jeśli jest określony, są przetwarzane niezależnie z urządzenia hello etag. W przypadku niezgodności z etag Witaj dwie istniejących toohello plik dziennika zostanie zapisany błąd. |
| **usuwanie** |Jeśli urządzenie już istnieje z hello określony **identyfikator**, jest usuwany bez względu toohello **ETag** wartość. <br/>Jeśli urządzenie hello nie istnieje, toohello plik dziennika zostanie zapisany błąd. |
| **deleteIfMatchETag** |Jeśli urządzenie już istnieje z hello określony **identyfikator**, jest usuwany, tylko wtedy, gdy istnieje **ETag** zgodne. Jeśli urządzenie hello nie istnieje, toohello plik dziennika zostanie zapisany błąd. <br/>Jeśli element etag toohello plik dziennika zostanie zapisany błąd. |

> [!NOTE]
> Jeśli dane serializacji hello nie jawnie definiować **parametrem importMode** flagi dla urządzeń, domyślne zbyt**createOrUpdate** podczas hello operację importowania.

## <a name="import-devices-example--bulk-device-provisioning"></a>Importuj przykładowe urządzeń — zbiorcze, inicjowanie obsługi administracyjnej urządzeń

Witaj poniższy przykład kodu C# ilustruje sposób toogenerate wiele tożsamości urządzenia który:

* Zawierają klucze uwierzytelniania.
* Zapis tego urządzenia informacji tooa blokowych obiektów blob.
* Importuj hello urządzeń w rejestrze tożsamości hello.

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

## <a name="import-devices-example--bulk-deletion"></a>Przykład urządzeń importu — zbiorczego usuwania

Hello poniższy przykład kodu pokazuje sposób toodelete hello urządzeń, które można dodać za pomocą hello powyższego przykładu kodu:

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

## <a name="get-hello-container-sas-uri"></a>Pobierz kontener hello identyfikatora URI połączenia SAS

Witaj poniższy przykład kodu pokazuje sposób toogenerate [identyfikatora URI połączenia SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) o odczytu, zapisu i usuwania uprawnień do kontenera obiektów blob:

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

## <a name="next-steps"></a>Następne kroki

W tym artykule przedstawiono sposób tooperform zbiorcze operacje rejestru tożsamości hello w Centrum IoT. Wykonaj te toolearn łącza więcej informacji na temat zarządzania Centrum IoT Azure:

* [Metryki Centrum IoT][lnk-metrics]
* [Operacje monitorowania][lnk-monitor]

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Przewodnik dewelopera Centrum IoT][lnk-devguide]
* [Symuluje urządzenia IoT krawędzi][lnk-iotedge]

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
