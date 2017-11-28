---
title: "C#: rozpoczynanie pracy z usługą Azure SQL Database | Microsoft Docs"
description: "Wypróbuj usługę SQL Database umożliwiający projektowanie aplikacji SQL i C# i utworzyć bazę danych SQL Azure z C# za pomocą hello SQL Database Library for .NET."
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
ms.openlocfilehash: e880ebabd53546bea37a13186b0f1a13db35b684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a><span data-ttu-id="900bf-104">Za pomocą C# toocreate bazy danych SQL hello SQL Database Library for .NET</span><span class="sxs-lookup"><span data-stu-id="900bf-104">Use C# toocreate a SQL database with hello SQL Database Library for .NET</span></span>

<span data-ttu-id="900bf-105">Dowiedz się, jak toocreate toouse C# Azure SQL bazy danych z hello [Biblioteka zarządzania SQL Microsoft Azure dla platformy .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span><span class="sxs-lookup"><span data-stu-id="900bf-105">Learn how toouse C# toocreate an Azure SQL database with hello [Microsoft Azure SQL Management Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span> <span data-ttu-id="900bf-106">W tym artykule opisano, jak toocreate pojedynczej bazy danych SQL i C#.</span><span class="sxs-lookup"><span data-stu-id="900bf-106">This article describes how toocreate a single database with SQL and C#.</span></span> <span data-ttu-id="900bf-107">toocreate pule elastyczne, zobacz [tworzenia puli elastycznej](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="900bf-107">toocreate elastic pools, see [Create an elastic pool](sql-database-elastic-pool-manage-csharp.md).</span></span>

<span data-ttu-id="900bf-108">udostępnia Hello Biblioteka zarządzania bazy danych SQL Azure dla platformy .NET [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)— na podstawie interfejsu API, który opakowuje hello [na podstawie Menedżera zasobów SQL bazy danych interfejsu API REST](https://docs.microsoft.com/rest/api/sql/).</span><span class="sxs-lookup"><span data-stu-id="900bf-108">hello Azure SQL Database Management Library for .NET provides an [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-based API that wraps hello [Resource Manager-based SQL Database REST API](https://docs.microsoft.com/rest/api/sql/).</span></span>

> [!NOTE]
> <span data-ttu-id="900bf-109">Wiele nowych funkcji bazy danych SQL są obsługiwane tylko, gdy używasz hello [modelu wdrażania usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), więc hello zawsze należy używać najnowszej **Biblioteka zarządzania bazy danych SQL Azure dla platformy .NET ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [pakietu NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**.</span><span class="sxs-lookup"><span data-stu-id="900bf-109">Many new features of SQL Database are only supported when you are using hello [Azure Resource Manager deployment model](../azure-resource-manager/resource-group-overview.md), so you should always use hello latest **Azure SQL Database Management Library for .NET ([docs](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet Package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**.</span></span> <span data-ttu-id="900bf-110">Witaj starsze [klasycznego modelu wdrażania na podstawie biblioteki](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) są obsługiwane dla zgodności z poprzednimi wersjami, dlatego zalecane jest użycie hello nowszej Menedżera zasobów na podstawie biblioteki.</span><span class="sxs-lookup"><span data-stu-id="900bf-110">hello older [classic deployment model based libraries](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) are supported for backward compatibility only, so we recommend you use hello newer Resource Manager based libraries.</span></span>
> 
> 

<span data-ttu-id="900bf-111">toocomplete hello kroki opisane w tym artykule, potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="900bf-111">toocomplete hello steps in this article, you need hello following:</span></span>

* <span data-ttu-id="900bf-112">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="900bf-112">An Azure subscription.</span></span> <span data-ttu-id="900bf-113">Jeśli potrzebujesz subskrypcji platformy Azure po prostu kliknij **bezpłatne konto** u góry hello tej strony, a następnie wróć toofinish w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="900bf-113">If you need an Azure subscription simply click **FREE ACCOUNT** at hello top of this page, and then come back toofinish this article.</span></span>
* <span data-ttu-id="900bf-114">Program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="900bf-114">Visual Studio.</span></span> <span data-ttu-id="900bf-115">Aby uzyskać bezpłatną kopię programu Visual Studio, zobacz hello [programu Visual Studio pobiera](https://www.visualstudio.com/downloads/download-visual-studio-vs) strony.</span><span class="sxs-lookup"><span data-stu-id="900bf-115">For a free copy of Visual Studio, see hello [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) page.</span></span>

> [!NOTE]
> <span data-ttu-id="900bf-116">W tym artykule opisano proces tworzenia nowej, pustej bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="900bf-116">This article creates a new, blank SQL database.</span></span> <span data-ttu-id="900bf-117">Modyfikowanie hello *CreateOrUpdateDatabase(...)*  metody w hello następujące przykładowe toocopy bazy danych, skalowania bazy danych, Utwórz bazę danych w puli, itp.</span><span class="sxs-lookup"><span data-stu-id="900bf-117">Modify hello *CreateOrUpdateDatabase(...)* method in hello following sample toocopy databases, scale databases, create a database in a pool, etc.</span></span>  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a><span data-ttu-id="900bf-118">Utwórz aplikację konsoli i zainstaluj hello wymaganych bibliotek</span><span class="sxs-lookup"><span data-stu-id="900bf-118">Create a console app and install hello required libraries</span></span>
1. <span data-ttu-id="900bf-119">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="900bf-119">Start Visual Studio.</span></span>
2. <span data-ttu-id="900bf-120">Kliknij pozycję **Plik** > **Nowy** > **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="900bf-120">Click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="900bf-121">Utwórz **aplikację konsolową** w języku C# i nadaj jej następującą nazwę: *SqlDbConsoleApp*</span><span class="sxs-lookup"><span data-stu-id="900bf-121">Create a C# **Console Application** and name it: *SqlDbConsoleApp*</span></span>

<span data-ttu-id="900bf-122">toocreate bazy danych SQL w języku C#, obciążenia hello wymagane biblioteki zarządzania (przy użyciu hello [konsoli Menedżera pakietów](http://docs.nuget.org/Consume/Package-Manager-Console)):</span><span class="sxs-lookup"><span data-stu-id="900bf-122">toocreate a SQL database with C#, load hello required management libraries (using hello [package manager console](http://docs.nuget.org/Consume/Package-Manager-Console)):</span></span>

1. <span data-ttu-id="900bf-123">Kliknij pozycję **Narzędzia** > **Menedżer pakietów NuGet** > **Konsola menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="900bf-123">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="900bf-124">Typ `Install-Package Microsoft.Azure.Management.Sql -Pre` najnowszych hello tooinstall [Biblioteka zarządzania Microsoft Azure SQL](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span><span class="sxs-lookup"><span data-stu-id="900bf-124">Type `Install-Package Microsoft.Azure.Management.Sql -Pre` tooinstall hello latest [Microsoft Azure SQL Management Library](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).</span></span>
3. <span data-ttu-id="900bf-125">Typ `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [Biblioteka programu Microsoft Azure Resource Manager](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).</span><span class="sxs-lookup"><span data-stu-id="900bf-125">Type `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [Microsoft Azure Resource Manager Library](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).</span></span>
4. <span data-ttu-id="900bf-126">Typ `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [wspólnej biblioteki uwierzytelniania firmy Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication).</span><span class="sxs-lookup"><span data-stu-id="900bf-126">Type `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [Microsoft Azure Common Authentication Library](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication).</span></span> 

> [!NOTE]
> <span data-ttu-id="900bf-127">Hello przykłady w tym artykule używane są synchroniczne formy poszczególnych żądań interfejsu API i blok do momentu ukończenia wywołania REST hello na powitania źródłowa usługa.</span><span class="sxs-lookup"><span data-stu-id="900bf-127">hello examples in this article use a synchronous form of each API request and block until completion of hello REST call on hello underlying service.</span></span> <span data-ttu-id="900bf-128">Dostępne są również metody asynchroniczne.</span><span class="sxs-lookup"><span data-stu-id="900bf-128">There are async methods available.</span></span>
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a><span data-ttu-id="900bf-129">Tworzenie serwera programu SQL Database, reguły zapory i bazy danych SQL — przykład w języku C#</span><span class="sxs-lookup"><span data-stu-id="900bf-129">Create a SQL Database server, firewall rule, and SQL database - C# example</span></span>
<span data-ttu-id="900bf-130">następujące przykładowe Hello tworzy grupę zasobów, serwer regułę zapory i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="900bf-130">hello following sample creates a resource group, server, firewall rule, and a SQL database.</span></span> <span data-ttu-id="900bf-131">Zobacz, [utworzyć tooaccess główna usługi zasobów](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` zmiennych.</span><span class="sxs-lookup"><span data-stu-id="900bf-131">See, [Create a service principal tooaccess resources](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variables.</span></span>

<span data-ttu-id="900bf-132">Zamień zawartość hello **Program.cs** z następujących hello i hello aktualizacji `{variables}` własnymi wartościami aplikacji (nie dołączaj hello `{}`).</span><span class="sxs-lookup"><span data-stu-id="900bf-132">Replace hello contents of **Program.cs** with hello following, and update hello `{variables}` with your app values (do not include hello `{}`).</span></span>

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

        // Create management clients for hello Azure resources your app needs toowork with.
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


            Console.WriteLine("Press any key toocontinue...");
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
            // Retrieve hello server that will host this database
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





## <a name="create-a-service-principal-tooaccess-resources"></a><span data-ttu-id="900bf-133">Utwórz zasoby tooaccess głównej usługi</span><span class="sxs-lookup"><span data-stu-id="900bf-133">Create a service principal tooaccess resources</span></span>
<span data-ttu-id="900bf-134">Witaj następujący skrypt programu PowerShell tworzy hello aplikacji usługi Active Directory (AD) i usługi hello główna, że potrzebujemy tooauthenticate aplikacji C#.</span><span class="sxs-lookup"><span data-stu-id="900bf-134">hello following PowerShell script creates hello Active Directory (AD) application and hello service principal that we need tooauthenticate our C# app.</span></span> <span data-ttu-id="900bf-135">Witaj skrypt generuje wartości, które firma Microsoft wymagane dla hello poprzedzających C# przykładowe.</span><span class="sxs-lookup"><span data-stu-id="900bf-135">hello script outputs values we need for hello preceding C# sample.</span></span> <span data-ttu-id="900bf-136">Aby uzyskać szczegółowe informacje, zobacz [toocreate programu Azure PowerShell Użyj nazwy głównej usługi zasobów tooaccess](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="900bf-136">For detailed information, see [Use Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a><span data-ttu-id="900bf-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="900bf-137">Next steps</span></span>
<span data-ttu-id="900bf-138">Teraz, po wypróbowaniu usługi SQL Database i konfigurowania bazy danych w języku C#, możesz przystąpić do hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="900bf-138">Now that you've tried SQL Database and set up a database with C#, you're ready for hello following articles:</span></span>

* [<span data-ttu-id="900bf-139">Uzyskuj tooSQL bazy danych programu SQL Server Management Studio i wykonywanie przykładowego zapytania T-SQL</span><span class="sxs-lookup"><span data-stu-id="900bf-139">Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query</span></span>](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a><span data-ttu-id="900bf-140">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="900bf-140">Additional Resources</span></span>
* [<span data-ttu-id="900bf-141">SQL Database</span><span class="sxs-lookup"><span data-stu-id="900bf-141">SQL Database</span></span>](https://azure.microsoft.com/documentation/services/sql-database/)
* [<span data-ttu-id="900bf-142">Klasa bazy danych</span><span class="sxs-lookup"><span data-stu-id="900bf-142">Database Class</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

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
