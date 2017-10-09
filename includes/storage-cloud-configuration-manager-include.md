Witaj [Biblioteka Microsoft Azure Configuration Manager dla platformy .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) zawiera klasę do analizowania parametrów połączenia w pliku konfiguracji. Witaj [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) klasy analizuje ustawienia konfiguracji niezależnie od tego, czy aplikacja kliencka hello jest uruchomiona na pulpicie hello na urządzeniu przenośnym w maszynie wirtualnej platformy Azure lub usługi w chmurze Azure.

tooreference hello pakietu CloudConfigurationManager, Dodaj następujące hello `using` dyrektywy:

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

Oto przykład pokazujący, jak tooretrieve, parametrów połączenia, z pliku konfiguracji:

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

Przy użyciu hello Azure Configuration Manager jest opcjonalne. Można również użyć interfejsu API, takich jak hello .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) klasy.

