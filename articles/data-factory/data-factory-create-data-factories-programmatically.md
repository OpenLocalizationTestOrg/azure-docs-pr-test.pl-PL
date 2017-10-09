---
title: "potoki danych aaaCreate przy użyciu zestawu Azure .NET SDK | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprogrammatically tworzenia, monitorowania i zarządzania fabryki danych Azure przy użyciu zestawu SDK fabryki danych."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="62892-103">Tworzenie, monitorowanie i zarządzanie przy użyciu zestawu SDK .NET usługi Azure Data Factory fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="62892-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="62892-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="62892-104">Overview</span></span>
<span data-ttu-id="62892-105">Tworzenie, monitorowanie i zarządzanie fabryki danych Azure, programowo przy użyciu zestawu .NET SDK fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="62892-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="62892-106">Ten artykuł zawiera wskazówki, które możesz wykonać toocreate przykładowej aplikacji konsoli .NET, które tworzy i monitoruje fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="62892-106">This article contains a walkthrough that you can follow toocreate a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="62892-107">W tym artykule nie opisano wszystkich hello interfejs API .NET fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="62892-107">This article does not cover all hello Data Factory .NET API.</span></span> <span data-ttu-id="62892-108">Zobacz [dokumentacja interfejsu API platformy .NET fabryki danych](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) dla pełna dokumentacja interfejsu API platformy .NET dla fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="62892-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="62892-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="62892-109">Prerequisites</span></span>
* <span data-ttu-id="62892-110">Program Visual Studio w wersji 2012, 2013 lub 2015.</span><span class="sxs-lookup"><span data-stu-id="62892-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="62892-111">Pobierz i zainstaluj [zestawu Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="62892-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="62892-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62892-112">Azure PowerShell.</span></span> <span data-ttu-id="62892-113">Postępuj zgodnie z instrukcjami wyświetlanymi w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykuł tooinstall programu Azure PowerShell na komputerze.</span><span class="sxs-lookup"><span data-stu-id="62892-113">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="62892-114">Korzystając z programu Azure PowerShell toocreate aplikację usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62892-114">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="62892-115">Tworzenie aplikacji w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62892-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="62892-116">Tworzenie aplikacji usługi Azure Active Directory, tworzenie nazwy głównej usługi dla aplikacji hello i przypisać je toohello **współautora fabryki danych** roli.</span><span class="sxs-lookup"><span data-stu-id="62892-116">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="62892-117">Uruchom program **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="62892-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="62892-118">Uruchom następujące polecenie hello, a następnie wprowadź hello nazwy użytkownika i hasła, użyj toosign w toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="62892-118">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="62892-119">Uruchom następujące polecenie tooview hello wszystkie subskrypcje powitania dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="62892-119">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="62892-120">Uruchom następujące polecenie tooselect hello subskrypcję, która ma toowork z hello.</span><span class="sxs-lookup"><span data-stu-id="62892-120">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="62892-121">Zastąp  **&lt;NameOfAzureSubscription** &gt; o nazwie hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="62892-121">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="62892-122">Należy zanotować **SubscriptionId** i **TenantId** z hello dane wyjściowe tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="62892-122">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="62892-123">Tworzenie grupy zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** , uruchamiając następujące polecenie w środowiska PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="62892-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="62892-124">Jeśli hello grupy zasobów już istnieje, określić czy tooupdate go (Y) lub zachować go jako (N).</span><span class="sxs-lookup"><span data-stu-id="62892-124">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="62892-125">Jeśli używasz innej grupie zasobów, należy toouse hello Nazwa grupy zasobów, zamiast ADFTutorialResourceGroup w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="62892-125">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="62892-126">Utwórz aplikację usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62892-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="62892-127">Jeśli zostanie wyświetlony następujący błąd hello, określ inny adres URL, a następnie ponownie uruchom polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="62892-127">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="62892-128">Utwórz hello nazwy głównej usługi AD.</span><span class="sxs-lookup"><span data-stu-id="62892-128">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="62892-129">Dodaj toohello główna usługi **współautora fabryki danych** roli.</span><span class="sxs-lookup"><span data-stu-id="62892-129">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="62892-130">Pobierz identyfikator aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="62892-130">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="62892-131">Zanotuj identyfikator aplikacji hello (identyfikator aplikacji applicationID) z hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="62892-131">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="62892-132">Po wykonaniu tych kroków powinny być dostępne cztery następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="62892-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="62892-133">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="62892-133">Tenant ID</span></span>
* <span data-ttu-id="62892-134">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="62892-134">Subscription ID</span></span>
* <span data-ttu-id="62892-135">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="62892-135">Application ID</span></span>
* <span data-ttu-id="62892-136">Hasło (określone w poleceniu pierwszy hello)</span><span class="sxs-lookup"><span data-stu-id="62892-136">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="62892-137">Przewodnik</span><span class="sxs-lookup"><span data-stu-id="62892-137">Walkthrough</span></span>
<span data-ttu-id="62892-138">W przewodniku hello tworzenie fabryki danych z potok, który zawiera działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="62892-138">In hello walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="62892-139">Witaj działanie kopiowania kopiuje dane z folderu w folderze tooanother magazynu obiektów blob platformy Azure w hello sam magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="62892-139">hello copy activity copies data from a folder in your Azure blob storage tooanother folder in hello same blob storage.</span></span> 

<span data-ttu-id="62892-140">Witaj działanie kopiowania wykonuje hello przenoszenia danych w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="62892-140">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="62892-141">działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="62892-141">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="62892-142">Zobacz [działań przepływu danych](data-factory-data-movement-activities.md) artykułu szczegółowe informacje o hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="62892-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

1. <span data-ttu-id="62892-143">Za pomocą programu Visual Studio 2012/2013/2015 utwórz aplikację konsolową .NET C#.</span><span class="sxs-lookup"><span data-stu-id="62892-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="62892-144">Uruchom program **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="62892-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="62892-145">Kliknij przycisk **pliku**, punktu zbyt**nowy**i kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="62892-145">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="62892-146">Rozwiń węzeł **Szablony** i wybierz opcję **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="62892-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="62892-147">W tym przewodniku stosowany jest język C#, ale można użyć dowolnego języka platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="62892-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="62892-148">Wybierz **aplikacji konsoli** z hello listy typów projektu na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="62892-148">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="62892-149">Wprowadź **DataFactoryAPITestApp** dla hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="62892-149">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="62892-150">Wybierz **C:\ADFGetStarted** dla hello lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="62892-150">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="62892-151">Kliknij przycisk **OK** toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="62892-151">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="62892-152">Kliknij przycisk **narzędzia**, punktu zbyt**Menedżera pakietów NuGet**i kliknij przycisk **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="62892-152">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="62892-153">W hello **Konsola Menedżera pakietów**, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="62892-153">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="62892-154">Uruchom hello następujące polecenia tooinstall fabryki danych pakietu:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="62892-154">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="62892-155">Uruchom hello następującego pakietu usługi Azure Active Directory tooinstall polecenia (należy użyć interfejsu API usługi Active Directory w kodzie hello):`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="62892-155">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="62892-156">Zamień zawartość hello **App.config** plik w projekcie hello z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="62892-156">Replace hello contents of **App.config** file in hello project with hello following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="62892-157">W pliku App.Config hello, zaktualizuj wartości  **&lt;identyfikator aplikacji&gt;**,  **&lt;hasło&gt;**,  **&lt; Identyfikator subskrypcji&gt;**, i  **&lt;Identyfikatorem dzierżawy&gt;**  z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="62892-157">In hello App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="62892-158">Dodaj następujące hello **przy użyciu** toohello instrukcje **Program.cs** plik w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="62892-158">Add hello following **using** statements toohello **Program.cs** file in hello project.</span></span>

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. <span data-ttu-id="62892-159">Dodaj hello następującego kodu, który tworzy wystąpienie **DataPipelineManagementClient** toohello klasy **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="62892-159">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="62892-160">Ten obiekt toocreate są używane fabryki danych, połączonej usługi, wejściowych i wyjściowych zestawów danych i potoku.</span><span class="sxs-lookup"><span data-stu-id="62892-160">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="62892-161">Można również użyć tego obiektu wycinków toomonitor zestawu danych w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="62892-161">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="62892-162">Zastąp wartość hello **resourceGroupName** o nazwie hello grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="62892-162">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span> <span data-ttu-id="62892-163">Można utworzyć grupy zasobów przy użyciu hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="62892-163">You can create a resource group using hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="62892-164">Zaktualizuj nazwę hello danych fabryki (dataFactoryName) toobe unikatowy.</span><span class="sxs-lookup"><span data-stu-id="62892-164">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="62892-165">Nazwa fabryki danych hello musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="62892-165">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="62892-166">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="62892-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="62892-167">Dodaj następującego kodu, który tworzy hello **fabryki danych** toohello **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="62892-167">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. <span data-ttu-id="62892-168">Dodaj następującego kodu, który tworzy hello **połączonej usługi magazynu Azure** toohello **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="62892-168">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="62892-169">Zastąp wartości **storageaccountname** i **accountkey** nazwą konta usługi Azure Storage oraz jego kluczem.</span><span class="sxs-lookup"><span data-stu-id="62892-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. <span data-ttu-id="62892-170">Dodaj hello następującego kodu, który tworzy **zestawów danych wejściowych i wyjściowych** toohello **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="62892-170">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    <span data-ttu-id="62892-171">Witaj **FolderPath** dla hello blob danych wejściowych jest ustawiony za**adftutorial /** gdzie **adftutorial** jest nazwą hello hello kontenera w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="62892-171">hello **FolderPath** for hello input blob is set too**adftutorial/** where **adftutorial** is hello name of hello container in your blob storage.</span></span> <span data-ttu-id="62892-172">Ten kontener nie istnieje w magazynie obiektów blob platformy Azure, utworzyć kontener o tej nazwie: **adftutorial** i przekazać kontener toohello pliku tekstowego.</span><span class="sxs-lookup"><span data-stu-id="62892-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file toohello container.</span></span>

    <span data-ttu-id="62892-173">Hello FolderPath dla hello output ustawiono obiektu blob: **adftutorial/apifactoryoutput / {Slice}** gdzie **wycinka** jest hello na podstawie dynamicznie obliczona wartość **SliceStart**(uruchomienie Data i godzina każdy wycinek).</span><span class="sxs-lookup"><span data-stu-id="62892-173">hello FolderPath for hello output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on hello value of **SliceStart** (start date-time of each slice.)</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. <span data-ttu-id="62892-174">Dodaj hello poniższy kod, który **tworzy i włącza potoku** toohello **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="62892-174">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="62892-175">Ten potok zawiera działanie **CopyActivity**, które pobiera element **BlobSource** jako źródło i **BlobSink** jako ujście.</span><span class="sxs-lookup"><span data-stu-id="62892-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="62892-176">Witaj działanie kopiowania wykonuje hello przenoszenia danych w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="62892-176">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="62892-177">działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="62892-177">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="62892-178">Zobacz [działań przepływu danych](data-factory-data-movement-activities.md) artykułu szczegółowe informacje o hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="62892-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. <span data-ttu-id="62892-179">Dodaj hello następującego kodu toohello **Main** metody tooget hello stan wycinek danych hello wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="62892-179">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="62892-180">Istnieje tylko jeden wycinek oczekiwany w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="62892-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. <span data-ttu-id="62892-181">**(opcjonalnie)**  Dodaj hello poniższy kod tooget Uruchom szczegóły toohello wycinek danych **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="62892-181">**(optional)** Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="62892-182">Dodaj następujące metody pomocnika używany przez hello hello **Main** toohello metody **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="62892-182">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span> <span data-ttu-id="62892-183">Ta metoda powoduje okno dialogowe umożliwiające podaj **nazwy użytkownika** i **hasło** Użyj toolog w portalu tooAzure.</span><span class="sxs-lookup"><span data-stu-id="62892-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use toolog in tooAzure portal.</span></span>

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. <span data-ttu-id="62892-184">W Eksploratorze rozwiązań hello, rozwiń projekt hello: **DataFactoryAPITestApp**, kliknij prawym przyciskiem myszy **odwołania**i kliknij przycisk **Dodaj odwołanie**.</span><span class="sxs-lookup"><span data-stu-id="62892-184">In hello Solution Explorer, expand hello project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="62892-185">Zaznacz pole wyboru dla `System.Configuration` zestawu i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="62892-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="62892-186">Tworzenie aplikacji konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="62892-186">Build hello console application.</span></span> <span data-ttu-id="62892-187">Kliknij przycisk **kompilacji** w hello menu i kliknij przycisk **Kompiluj rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="62892-187">Click **Build** on hello menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="62892-188">Upewnij się, że istnieje co najmniej jeden plik w kontenerze adftutorial hello w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="62892-188">Confirm that there is at least one file in hello adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="62892-189">W przeciwnym razie utwórz Emp.txt plik w programie Notatnik z powitania po zawartości i przekaż go toohello adftutorial kontenera.</span><span class="sxs-lookup"><span data-stu-id="62892-189">If not, create Emp.txt file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="62892-190">Uruchom przykładowe hello klikając **debugowania** -> **Rozpocznij debugowanie** menu hello.</span><span class="sxs-lookup"><span data-stu-id="62892-190">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="62892-191">Po wyświetleniu hello **pierwsze uruchomienie szczegóły wycinka danych**, zaczekaj kilka minut, a następnie naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="62892-191">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="62892-192">Użyj hello tooverify portalu Azure w tej fabryce danych hello **APITutorialFactory** jest tworzony z następującego artefakty hello:</span><span class="sxs-lookup"><span data-stu-id="62892-192">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
    * <span data-ttu-id="62892-193">Połączona usługa: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="62892-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="62892-194">Zestaw danych: **DatasetBlobSource** i **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="62892-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="62892-195">Potok: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="62892-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="62892-196">Sprawdź, czy plik wyjściowy jest utworzony w hello **apifactoryoutput** folderu w hello **adftutorial** kontenera.</span><span class="sxs-lookup"><span data-stu-id="62892-196">Verify that an output file is created in hello **apifactoryoutput** folder in hello **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="62892-197">Pobierz listę wycinków danych nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="62892-197">Get a list of failed data slices</span></span> 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a><span data-ttu-id="62892-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62892-198">Next steps</span></span>
<span data-ttu-id="62892-199">Zobacz poniższy przykład do utworzenia potoku przy użyciu zestawu .NET SDK, który kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure hello:</span><span class="sxs-lookup"><span data-stu-id="62892-199">See hello following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage tooan Azure SQL database:</span></span> 

- [<span data-ttu-id="62892-200">Tworzenie potoku toocopy danych z magazynu obiektów Blob tooSQL bazy danych</span><span class="sxs-lookup"><span data-stu-id="62892-200">Create a pipeline toocopy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
