<span data-ttu-id="5f635-101">Witaj [Biblioteka Microsoft Azure Configuration Manager dla platformy .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) zawiera klasę do analizowania parametrów połączenia w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5f635-101">hello [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span></span> <span data-ttu-id="5f635-102">Witaj [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) klasy analizuje ustawienia konfiguracji niezależnie od tego, czy aplikacja kliencka hello jest uruchomiona na pulpicie hello na urządzeniu przenośnym w maszynie wirtualnej platformy Azure lub usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="5f635-102">hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether hello client application is running on hello desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span></span>

<span data-ttu-id="5f635-103">tooreference hello pakietu CloudConfigurationManager, Dodaj następujące hello `using` dyrektywy:</span><span class="sxs-lookup"><span data-stu-id="5f635-103">tooreference hello CloudConfigurationManager package, add hello following `using` directive:</span></span>

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

<span data-ttu-id="5f635-104">Oto przykład pokazujący, jak tooretrieve, parametrów połączenia, z pliku konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="5f635-104">Here's an example that shows how tooretrieve a connection string from a configuration file:</span></span>

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

<span data-ttu-id="5f635-105">Przy użyciu hello Azure Configuration Manager jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="5f635-105">Using hello Azure Configuration Manager is optional.</span></span> <span data-ttu-id="5f635-106">Można również użyć interfejsu API, takich jak hello .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) klasy.</span><span class="sxs-lookup"><span data-stu-id="5f635-106">You can also use an API like hello .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span></span>

