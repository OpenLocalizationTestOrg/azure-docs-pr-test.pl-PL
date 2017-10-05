---
title: "C#: rozpoczynanie pracy z usługą Azure SQL Database | Microsoft Docs"
description: "Wypróbuj usługę SQL Database SQL do tworzenia aplikacji w językach SQL i C#, a także utwórz bazę danych Azure SQL w języku C# przy użyciu biblioteki SQL Database Library for .NET."
keywords: "Spróbuj sql, sql c#"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: cfff2299-a474-4054-8d99-759af1ae5188
ms.service: sql-database
ms.custom: develop apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: csharp
ms.workload: data-management
ms.date: 10/04/2016
ms.author: sstein
ms.openlocfilehash: c8a2703da1ee3687f8d134e768dd8d31dc4f316b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-c-to-create-a-sql-database-with-the-sql-database-library-for-net"></a>Używanie języka C# do tworzenia bazy danych SQL z zastosowaniem biblioteki SQL Database Library for .NET

Dowiedz się, jak używać języka C# do tworzenia bazy danych Azure SQL z zastosowaniem [Biblioteki zarządzania usługą Microsoft Azure SQL dla programu .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql). W tym artykule opisano sposób tworzenia jednej bazy danych SQL w języku C#. Aby tworzyć pule elastyczne, zobacz temat [Tworzenie puli elastycznej](sql-database-elastic-pool-manage-csharp.md).

Biblioteka zarządzania usługą Azure SQL Database dla programu .NET dostarcza interfejs API oparty na usłudze [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), który opakowuje [interfejs API REST usługi SQL Database oparty na usłudze Resource Manager](https://docs.microsoft.com/rest/api/sql/).

> [!NOTE]
> Wiele nowych funkcji usługi SQL Database jest obsługiwanych tylko w przypadku zastosowania [modelu wdrażania przy użyciu usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). Dlatego należy zawsze używać najnowszej **Biblioteki zarządzania usługą SQL Database platformy Azure dla programu .NET ([dokumentacja](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [Pakiet NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**. Starsze [biblioteki oparte na modelu wdrożenia klasycznego](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) są obsługiwane tylko w trybie zgodności z poprzednimi wersjami, w związku z czym zalecane jest użycie nowszych bibliotek opartych na modelu wdrożenia przy użyciu usługi Resource Manager.
> 
> 

Do wykonania kroków opisanych w tym artykule potrzebne są:

* Subskrypcja platformy Azure. Jeśli potrzebujesz subskrypcji platformy Azure, po prostu kliknij pozycję **BEZPŁATNE KONTO** u góry tej strony, a następnie wróć do artykułu.
* Program Visual Studio. Aby uzyskać bezpłatną kopię programu Visual Studio, zobacz stronę [Visual Studio — pliki do pobrania](https://www.visualstudio.com/downloads/download-visual-studio-vs).

> [!NOTE]
> W tym artykule opisano proces tworzenia nowej, pustej bazy danych SQL. Modyfikacja metody *CreateOrUpdateDatabase(...)* w następującym przykładzie pozwala skopiować bazy danych i skalować je, utworzyć bazę danych w puli itp.  
> 

## <a name="create-a-console-app-and-install-the-required-libraries"></a>Tworzenie aplikacji konsoli i instalowanie wymaganych bibliotek
1. Uruchom program Visual Studio.
2. Kliknij pozycję **Plik** > **Nowy** > **Projekt**.
3. Utwórz **aplikację konsolową** w języku C# i nadaj jej następującą nazwę: *SqlDbConsoleApp*

Aby utworzyć bazę danych SQL w języku C#, załaduj wymagane biblioteki zarządzania (przy użyciu [konsoli menedżera pakietów](http://docs.nuget.org/Consume/Package-Manager-Console)):

1. Kliknij pozycję **Narzędzia** > **Menedżer pakietów NuGet** > **Konsola menedżera pakietów**.
2. Wpisz polecenie `Install-Package Microsoft.Azure.Management.Sql -Pre`, aby zainstalować najnowszą [Bibliotekę zarządzania usługą SQL platformy Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).
3. Wpisz polecenie `Install-Package Microsoft.Azure.Management.ResourceManager -Pre`, aby zainstalować [Bibliotekę usługi Microsoft Azure Resource Manager](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).
4. Wpisz polecenie `Install-Package Microsoft.Azure.Common.Authentication -Pre`, aby zainstalować [Wspólną bibliotekę uwierzytelniania platformy Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication). 

> [!NOTE]
> W przykładach podanych w tym artykule używane są synchroniczne formy poszczególnych żądań interfejsu API, które blokują działanie programu do momentu ukończenia wywołania REST na podległej usłudze. Dostępne są również metody asynchroniczne.
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a>Tworzenie serwera programu SQL Database, reguły zapory i bazy danych SQL — przykład w języku C#
W poniższym przykładzie tworzone są: grupa zasobów, serwer, reguła zapory i baza danych SQL. Zobacz [Tworzenie usługi podmiotu używanej do uzyskiwania dostępu do zasobów](#create-a-service-principal-to-access-resources), aby uzyskać zmienne `_subscriptionId, _tenantId, _applicationId, and _applicationSecret`.

Zastąp zawartość pliku **Program.cs** poniższym kodem i zaktualizuj elementy `{variables}` wartościami aplikacji (bez znaków `{}`).

    using Microsoft.Azure;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.Azure.Management.Sql;
    using Microsoft.Azure.Management.Sql.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System;

    namespace SqlDbConsoleApp
    {
    class Program
       {
        // For details about these four (4) values, see
        // https://azure.microsoft.com/documentation/articles/resource-group-authenticate-service-principal/
        static string _subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _tenantId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationSecret = "{your-password}";

        // Create management clients for the Azure resources your app needs to work with.
        // This app works with Resource Groups, and Azure SQL Database.
        static ResourceManagementClient _resourceMgmtClient;
        static SqlManagementClient _sqlMgmtClient;

        // Authentication token
        static AuthenticationResult _token;

        // Azure resource variables
        static string _resourceGroupName = "{resource-group-name}";
        static string _resourceGrouplocation = "{Azure-region}";

        static string _serverlocation = _resourceGrouplocation;
        static string _serverName = "{server-name}";
        static string _serverAdmin = "{server-admin-login}";
        static string _serverAdminPassword = "{server-admin-password}";

        static string _firewallRuleName = "{firewall-rule-name}";
        static string _startIpAddress = "{0.0.0.0}";
        static string _endIpAddress = "{255.255.255.255}";

        static string _databaseName = "{dbfromcsarticle}";
        static string _databaseEdition = DatabaseEditions.Basic;
        static string _databasePerfLevel = ""; // "S0", "S1", and so on here for other tiers


        static void Main(string[] args)
        {
            // Authenticate:
            _token = GetToken(_tenantId, _applicationId, _applicationSecret);
            Console.WriteLine("Token acquired. Expires on:" + _token.ExpiresOn);

            // Instantiate management clients:
            _resourceMgmtClient = new ResourceManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken));
            _sqlMgmtClient = new SqlManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken)) { SubscriptionId = _subscriptionId };

            Console.WriteLine("Resource group...");
            ResourceGroup rg = CreateOrUpdateResourceGroup(_resourceMgmtClient, _subscriptionId, _resourceGroupName, _resourceGrouplocation);
            Console.WriteLine("Resource group: " + rg.Id);


            Console.WriteLine("Server...");
            Server sgr = CreateOrUpdateServer(_sqlMgmtClient, _resourceGroupName, _serverlocation, _serverName, _serverAdmin, _serverAdminPassword);
            Console.WriteLine("Server: " + sgr.Id);

            Console.WriteLine("Server firewall...");
            FirewallRule fwr = CreateOrUpdateFirewallRule(_sqlMgmtClient, _resourceGroupName, _serverName, _firewallRuleName, _startIpAddress, _endIpAddress);
            Console.WriteLine("Server firewall: " + fwr.Id);

            Console.WriteLine("Database...");
            Database dbr = CreateOrUpdateDatabase(_sqlMgmtClient, _resourceGroupName, _serverName, _databaseName, _databaseEdition, _databasePerfLevel);
            Console.WriteLine("Database: " + dbr.Id);


            Console.WriteLine("Press any key to continue...");
            Console.ReadKey();
        }

        static ResourceGroup CreateOrUpdateResourceGroup(ResourceManagementClient resourceMgmtClient, string subscriptionId, string resourceGroupName, string resourceGroupLocation)
        {
            ResourceGroup resourceGroupParameters = new ResourceGroup()
            {
                Location = resourceGroupLocation,
            };
            resourceMgmtClient.SubscriptionId = subscriptionId;
            ResourceGroup resourceGroupResult = resourceMgmtClient.ResourceGroups.CreateOrUpdate(resourceGroupName, resourceGroupParameters);
            return resourceGroupResult;
        }

        static Server CreateOrUpdateServer(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverLocation, string serverName, string serverAdmin, string serverAdminPassword)
        {
            Server serverParameters = new Server()
            {
                Location = serverLocation,
                AdministratorLogin = serverAdmin,
                AdministratorLoginPassword = serverAdminPassword,
                Version = "12.0"
            };
            Server serverResult = sqlMgmtClient.Servers.CreateOrUpdate(resourceGroupName, serverName, serverParameters);
            return serverResult;
        }

        static FirewallRule CreateOrUpdateFirewallRule(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string firewallRuleName, string startIpAddress, string endIpAddress)
        {
            FirewallRule firewallParameters = new FirewallRule()
            {
                StartIpAddress = startIpAddress,
                EndIpAddress = endIpAddress
            };
            FirewallRule firewallResult = sqlMgmtClient.FirewallRules.CreateOrUpdate(resourceGroupName, serverName, firewallRuleName, firewallParameters);
            return firewallResult;
        }

        static Database CreateOrUpdateDatabase(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string databaseName, string databaseEdition, string databasePerfLevel)
        {
            // Retrieve the server that will host this database
            Server currentServer = sqlMgmtClient.Servers.Get(resourceGroupName, serverName);

            // Create a database: configure create or update parameters and properties explicitly
            Database newDatabaseParameters = new Database()
            {
                Location = currentServer.Location,
                CreateMode = CreateMode.Default,
                Edition = databaseEdition,
                RequestedServiceObjectiveName = databasePerfLevel

            };
            Database dbResponse = sqlMgmtClient.Databases.CreateOrUpdate(resourceGroupName, serverName, databaseName, newDatabaseParameters);
            return dbResponse;
        }



        private static AuthenticationResult GetToken(string tenantId, string applicationId, string applicationSecret)
        {
            AuthenticationContext authContext = new AuthenticationContext("https://login.windows.net/" + tenantId);
            _token = authContext.AcquireToken("https://management.core.windows.net/", new ClientCredential(applicationId, applicationSecret));
            return _token;
        }
      }
    }





## <a name="create-a-service-principal-to-access-resources"></a>Tworzenie usługi podmiotu używanej do uzyskiwania dostępu do zasobów
Poniższy skrypt środowiska PowerShell tworzy aplikację usługi Active Directory (AD) oraz jednostkę usługi wymaganą do uwierzytelnienia aplikacji w języku C#. Skrypt generuje wartości wyjściowe potrzebne w poprzednim przykładzie w języku C#. Aby uzyskać szczegółowe informacje, zobacz [Tworzenie usługi podmiotu używanej do uzyskiwania dostępu do zasobów przy użyciu programu Azure PowerShell](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    # Sign in to Azure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set to the subscription you want to work with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is the display name for your app, must be unique in your directory.
    # $uri does not need to be a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for the app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # To avoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun the following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output the values we need for our C# application to successfully authenticate

    Write-Output "Copy these values into the C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a>Następne kroki
Po wypróbowaniu usługi SQL Database i skonfigurowaniu bazy danych przy użyciu języka C# możesz przystąpić do czytania następujących artykułów:

* [Nawiązywanie połączenia z usługą SQL Database za pomocą programu SQL Server Management Studio i wykonywanie przykładowego zapytania T-SQL](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a>Dodatkowe zasoby
* [SQL Database](https://azure.microsoft.com/documentation/services/sql-database/)
* [Klasa bazy danych](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

<!--Image references-->
[1]: ./media/sql-database-get-started-csharp/aad.png
[2]: ./media/sql-database-get-started-csharp/permissions.png
[3]: ./media/sql-database-get-started-csharp/getdomain.png
[4]: ./media/sql-database-get-started-csharp/aad2.png
[5]: ./media/sql-database-get-started-csharp/aad-applications.png
[6]: ./media/sql-database-get-started-csharp/add.png
[7]: ./media/sql-database-get-started-csharp/add-application.png
[8]: ./media/sql-database-get-started-csharp/add-application2.png
[9]: ./media/sql-database-get-started-csharp/clientid.png
