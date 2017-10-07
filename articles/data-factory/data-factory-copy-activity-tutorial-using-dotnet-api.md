---
title: "Samouczek: tworzenie potoku za pomocą działania kopiowania przy użyciu interfejsu API .NET | Microsoft Docs"
description: "Ten samouczek zawiera instrukcje tworzenia potoku usługi Azure Data Factory za pomocą działania kopiowania przy użyciu interfejsu API .NET."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="f7727-103">Samouczek: tworzenie potoku za pomocą działania kopiowania przy użyciu interfejsu API .NET</span><span class="sxs-lookup"><span data-stu-id="f7727-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f7727-104">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f7727-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="f7727-105">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="f7727-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="f7727-106">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f7727-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="f7727-107">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f7727-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="f7727-108">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7727-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="f7727-109">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f7727-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="f7727-110">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="f7727-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="f7727-111">Interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="f7727-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="f7727-112">W tym artykule dowiesz się, jak toouse [interfejs API .NET](https://portal.azure.com) toocreate fabryki danych z potok, który kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f7727-112">In this article, you learn how toouse [.NET API](https://portal.azure.com) toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="f7727-113">Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem hello [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykuł przed wykonaniem tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="f7727-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="f7727-114">W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania).</span><span class="sxs-lookup"><span data-stu-id="f7727-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="f7727-115">działanie kopiowania Hello kopiuje dane z magazynu danych obsługiwanych ujścia magazynu tooa obsługiwane dane.</span><span class="sxs-lookup"><span data-stu-id="f7727-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="f7727-116">Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f7727-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f7727-117">działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="f7727-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="f7727-118">Aby uzyskać więcej informacji na temat hello działanie kopiowania, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f7727-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="f7727-119">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="f7727-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="f7727-120">I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań.</span><span class="sxs-lookup"><span data-stu-id="f7727-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="f7727-121">Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="f7727-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="f7727-122">Aby zapoznać się z pełną dokumentacją dotyczącą interfejsu API .NET usługi Data Factory, zobacz [dokumentację interfejsu API .NET usługi Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="f7727-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="f7727-123">Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego.</span><span class="sxs-lookup"><span data-stu-id="f7727-123">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="f7727-124">Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie danych tootransform potoku, przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="f7727-124">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7727-125">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f7727-125">Prerequisites</span></span>
* <span data-ttu-id="f7727-126">Przejdź przez [samouczek omówienie i wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget omówienie samouczek hello i pełne hello **wymagań wstępnych** czynności.</span><span class="sxs-lookup"><span data-stu-id="f7727-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget an overview of hello tutorial and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="f7727-127">Program Visual Studio w wersji 2012, 2013 lub 2015.</span><span class="sxs-lookup"><span data-stu-id="f7727-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="f7727-128">Pobierz i zainstaluj zestaw [SDK .NET Azure](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f7727-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="f7727-129">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f7727-129">Azure PowerShell.</span></span> <span data-ttu-id="f7727-130">Postępuj zgodnie z instrukcjami wyświetlanymi w [jak tooinstall i konfigurowanie programu Azure PowerShell](../powershell-install-configure.md) artykuł tooinstall programu Azure PowerShell na komputerze.</span><span class="sxs-lookup"><span data-stu-id="f7727-130">Follow instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="f7727-131">Korzystając z programu Azure PowerShell toocreate aplikację usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f7727-131">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="f7727-132">Tworzenie aplikacji w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7727-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="f7727-133">Tworzenie aplikacji usługi Azure Active Directory, tworzenie nazwy głównej usługi dla aplikacji hello i przypisać je toohello **współautora fabryki danych** roli.</span><span class="sxs-lookup"><span data-stu-id="f7727-133">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="f7727-134">Uruchom program **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f7727-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="f7727-135">Uruchom następujące polecenie hello, a następnie wprowadź hello nazwy użytkownika i hasła, użyj toosign w toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f7727-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="f7727-136">Uruchom następujące polecenie tooview hello wszystkie subskrypcje powitania dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="f7727-136">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="f7727-137">Uruchom następujące polecenie tooselect hello subskrypcję, która ma toowork z hello.</span><span class="sxs-lookup"><span data-stu-id="f7727-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="f7727-138">Zastąp  **&lt;NameOfAzureSubscription** &gt; o nazwie hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f7727-138">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="f7727-139">Należy zanotować **SubscriptionId** i **TenantId** z hello dane wyjściowe tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="f7727-139">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="f7727-140">Tworzenie grupy zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** , uruchamiając następujące polecenie w środowiska PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="f7727-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="f7727-141">Jeśli hello grupy zasobów już istnieje, określić czy tooupdate go (Y) lub zachować go jako (N).</span><span class="sxs-lookup"><span data-stu-id="f7727-141">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="f7727-142">Jeśli używasz innej grupie zasobów, należy toouse hello Nazwa grupy zasobów, zamiast ADFTutorialResourceGroup w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="f7727-142">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="f7727-143">Utwórz aplikację usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f7727-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="f7727-144">Jeśli zostanie wyświetlony następujący błąd hello, określ inny adres URL, a następnie ponownie uruchom polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="f7727-144">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="f7727-145">Utwórz hello nazwy głównej usługi AD.</span><span class="sxs-lookup"><span data-stu-id="f7727-145">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="f7727-146">Dodaj toohello główna usługi **współautora fabryki danych** roli.</span><span class="sxs-lookup"><span data-stu-id="f7727-146">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="f7727-147">Pobierz identyfikator aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="f7727-147">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="f7727-148">Zanotuj identyfikator aplikacji hello (identyfikator aplikacji applicationID) z hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="f7727-148">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="f7727-149">Po wykonaniu tych kroków powinny być dostępne cztery następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="f7727-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="f7727-150">Identyfikator dzierżawy</span><span class="sxs-lookup"><span data-stu-id="f7727-150">Tenant ID</span></span>
* <span data-ttu-id="f7727-151">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f7727-151">Subscription ID</span></span>
* <span data-ttu-id="f7727-152">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="f7727-152">Application ID</span></span>
* <span data-ttu-id="f7727-153">Hasło (określone w poleceniu pierwszy hello)</span><span class="sxs-lookup"><span data-stu-id="f7727-153">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="f7727-154">Przewodnik</span><span class="sxs-lookup"><span data-stu-id="f7727-154">Walkthrough</span></span>
1. <span data-ttu-id="f7727-155">Za pomocą programu Visual Studio 2012/2013/2015 utwórz aplikację konsolową .NET C#.</span><span class="sxs-lookup"><span data-stu-id="f7727-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="f7727-156">Uruchom program **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="f7727-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="f7727-157">Kliknij przycisk **pliku**, punktu zbyt**nowy**i kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="f7727-157">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="f7727-158">Rozwiń węzeł **Szablony** i wybierz opcję **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="f7727-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="f7727-159">W tym przewodniku stosowany jest język C#, ale można użyć dowolnego języka platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="f7727-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="f7727-160">Wybierz **aplikacji konsoli** z hello listy typów projektu na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="f7727-160">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="f7727-161">Wprowadź **DataFactoryAPITestApp** dla hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="f7727-161">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="f7727-162">Wybierz **C:\ADFGetStarted** dla hello lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="f7727-162">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="f7727-163">Kliknij przycisk **OK** toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="f7727-163">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="f7727-164">Kliknij przycisk **narzędzia**, punktu zbyt**Menedżera pakietów NuGet**i kliknij przycisk **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="f7727-164">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="f7727-165">W hello **Konsola Menedżera pakietów**, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f7727-165">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="f7727-166">Uruchom hello następujące polecenia tooinstall fabryki danych pakietu:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="f7727-166">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="f7727-167">Uruchom hello następującego pakietu usługi Azure Active Directory tooinstall polecenia (należy użyć interfejsu API usługi Active Directory w kodzie hello):`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="f7727-167">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="f7727-168">Dodaj następujące hello **appSetttings** toohello sekcji **App.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="f7727-168">Add hello following **appSetttings** section toohello **App.config** file.</span></span> <span data-ttu-id="f7727-169">Te ustawienia są używane przez metodę pomocniczą hello: **GetAuthorizationHeader**.</span><span class="sxs-lookup"><span data-stu-id="f7727-169">These settings are used by hello helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="f7727-170">Zastąp wartości **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** i **&lt;tenant ID&gt;** własnymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="f7727-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="f7727-171">Dodaj następujące hello **przy użyciu** instrukcje toohello pliku źródłowego (Program.cs) w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="f7727-171">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

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

6. <span data-ttu-id="f7727-172">Dodaj hello następującego kodu, który tworzy wystąpienie **DataPipelineManagementClient** toohello klasy **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="f7727-172">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="f7727-173">Ten obiekt toocreate są używane fabryki danych, połączonej usługi, wejściowych i wyjściowych zestawów danych i potoku.</span><span class="sxs-lookup"><span data-stu-id="f7727-173">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="f7727-174">Można również użyć tego obiektu wycinków toomonitor zestawu danych w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="f7727-174">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="f7727-175">Zastąp wartość hello **resourceGroupName** o nazwie hello grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f7727-175">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="f7727-176">Zaktualizuj nazwę hello danych fabryki (dataFactoryName) toobe unikatowy.</span><span class="sxs-lookup"><span data-stu-id="f7727-176">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="f7727-177">Nazwa fabryki danych hello musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="f7727-177">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="f7727-178">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="f7727-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="f7727-179">Dodaj następującego kodu, który tworzy hello **fabryki danych** toohello **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="f7727-179">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

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

    <span data-ttu-id="f7727-180">Fabryka danych może obejmować jeden lub wiele potoków.</span><span class="sxs-lookup"><span data-stu-id="f7727-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="f7727-181">Potok może obejmować jedno lub wiele działań.</span><span class="sxs-lookup"><span data-stu-id="f7727-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="f7727-182">Na przykład toocopy działanie kopiowania danych z magazynu danych docelowy tooa źródłowego i HDInsight Hive działania toorun tootransform skryptu Hive wejściowe dane wyjściowe tooproduct danych.</span><span class="sxs-lookup"><span data-stu-id="f7727-182">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="f7727-183">Zacznijmy od utworzenia hello fabryki danych w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="f7727-183">Let's start with creating hello data factory in this step.</span></span>
8. <span data-ttu-id="f7727-184">Dodaj następującego kodu, który tworzy hello **połączonej usługi magazynu Azure** toohello **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="f7727-184">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f7727-185">Zastąp wartości **storageaccountname** i **accountkey** nazwą konta usługi Azure Storage oraz jego kluczem.</span><span class="sxs-lookup"><span data-stu-id="f7727-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="f7727-186">Połączone usługi są tworzone w toolink fabryki danych dane są przechowywane i obliczeniowe fabryki danych toohello usług.</span><span class="sxs-lookup"><span data-stu-id="f7727-186">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="f7727-187">W tym samouczku nie przedstawiono korzystania z żadnych usług obliczeniowych, takich jak Azure HDInsight czy Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f7727-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="f7727-188">Zostają użyte dwa magazyny danych typu Azure Storage (źródło) i Azure SQL Database (lokalizacja docelowa).</span><span class="sxs-lookup"><span data-stu-id="f7727-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="f7727-189">W związku z tym tworzy się dwie połączone usługi o nazwie AzureStorageLinkedService i AzureSqlLinkedService typu: AzureStorage i AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="f7727-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="f7727-190">Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f7727-190">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="f7727-191">To konto magazynu jest hello jedną w którym utworzono kontener i hello dane przekazane jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f7727-191">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="f7727-192">Dodaj hello następującego kodu, który tworzy **Azure SQL połączona usługa** toohello **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="f7727-192">Add hello following code that creates an **Azure SQL linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f7727-193">Zastąp wartości **servername**, **databasename**, **username** oraz **password** nazwą serwera SQL Azure, nazwą bazy danych, nazwą użytkownika i hasłem.</span><span class="sxs-lookup"><span data-stu-id="f7727-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    <span data-ttu-id="f7727-194">AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="f7727-194">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="f7727-195">dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f7727-195">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="f7727-196">Utworzono hello pustych elementów tabeli w tej bazie danych jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f7727-196">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="f7727-197">Dodaj hello następującego kodu, który tworzy **zestawów danych wejściowych i wyjściowych** toohello **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="f7727-197">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
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

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
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
    
    <span data-ttu-id="f7727-198">W poprzednim kroku hello utworzono toolink połączone usługi konta magazynu Azure i fabryki danych tooyour bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="f7727-198">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="f7727-199">W tym kroku należy zdefiniować dwa zestawy danych o nazwie InputDataset i OutputDataset reprezentujące danych wejściowych i wyjściowych danych przechowywanych w magazynach danych hello odwołuje się AzureStorageLinkedService i AzureSqlLinkedService odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="f7727-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="f7727-200">Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f7727-200">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="f7727-201">I zestawu danych wejściowych obiektu blob hello (InputDataset) określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="f7727-201">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="f7727-202">Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="f7727-202">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="f7727-203">I hello danych wyjściowych SQL tabeli dataset (OututDataset) określa hello tabeli w hello bazy danych toowhich powitalne dane z magazynu obiektów blob hello są kopiowane.</span><span class="sxs-lookup"><span data-stu-id="f7727-203">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

    <span data-ttu-id="f7727-204">W tym kroku utworzysz zestaw danych o nazwie InputDataset, który wskazuje plik obiektu blob tooa (emp.txt) w folderze głównym hello kontenera obiektów blob (adftutorial) w hello reprezentowany przez hello AzureStorageLinkedService połączone usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="f7727-204">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="f7727-205">Brak określić wartość dla nazwy pliku hello (lub Pomiń je), danych z wszystkich obiektów blob w folderze wejściowych hello są skopiowanych toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="f7727-205">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="f7727-206">W tym samouczku należy określić wartość dla hello fileName.</span><span class="sxs-lookup"><span data-stu-id="f7727-206">In this tutorial, you specify a value for hello fileName.</span></span>    

    <span data-ttu-id="f7727-207">W tym kroku tworzony jest wyjściowy zestaw danych o nazwie **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f7727-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="f7727-208">Ten zestaw danych wskazuje tooa tabeli SQL w bazie danych Azure SQL hello reprezentowany przez **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f7727-208">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="f7727-209">Dodaj hello poniższy kod, który **tworzy i włącza potoku** toohello **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="f7727-209">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="f7727-210">W tym kroku opisano tworzenie potoku za pomocą **działania kopiowania**, w którym parametr **InputDataset** jest używany jako dane wejściowe, a parametr **OutputDataset** jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="f7727-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

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
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
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
                    }
                }
            }
        });
    ```

    <span data-ttu-id="f7727-211">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="f7727-211">Note hello following points:</span></span>
   
    - <span data-ttu-id="f7727-212">W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="f7727-212">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="f7727-213">Aby uzyskać więcej informacji o działaniu kopiowania hello, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f7727-213">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="f7727-214">W rozwiązaniach usługi Data Factory można również użyć [działań dotyczących przekształcania danych](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f7727-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="f7727-215">Dane wejściowe dla działania hello jest ustawiony za**InputDataset** i danych wyjściowych dla działania hello jest ustawiony za**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f7727-215">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="f7727-216">W hello **typeProperties** sekcji **BlobSource** jest określony jako typ źródła hello i **SqlSink** jest określony jako typ ujścia hello.</span><span class="sxs-lookup"><span data-stu-id="f7727-216">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="f7727-217">Aby uzyskać pełną listę obsługiwanych przez działanie kopiowania hello jako źródła i wychwytywanie magazyny danych, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f7727-217">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f7727-218">toolearn jak przechowywać toouse określonych danych obsługiwane jako źródło/ujście, kliknij łącze hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="f7727-218">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
   
    <span data-ttu-id="f7727-219">Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="f7727-219">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="f7727-220">W tym samouczku wyjściowy zestaw danych jest skonfigurowane tooproduce wycinek godzinę.</span><span class="sxs-lookup"><span data-stu-id="f7727-220">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="f7727-221">potok Hello ma czas rozpoczęcia i godzina zakończenia, będące w ciągu jednego dnia od siebie, który wynosi 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="f7727-221">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="f7727-222">W związku z tym 24 wycinków wyjściowy zestaw danych są produkowane przez hello potoku.</span><span class="sxs-lookup"><span data-stu-id="f7727-222">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span>
12. <span data-ttu-id="f7727-223">Dodaj hello następującego kodu toohello **Main** metody tooget hello stan wycinek danych hello wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="f7727-223">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="f7727-224">W tym przykładzie oczekiwany jest tylko wycinek.</span><span class="sxs-lookup"><span data-stu-id="f7727-224">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="f7727-225">Dodaj poniższe informacje tooget uruchomić kod dla toohello wycinek danych hello **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="f7727-225">Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

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
            }
        );

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

14. <span data-ttu-id="f7727-226">Dodaj następujące metody pomocnika używany przez hello hello **Main** toohello metody **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="f7727-226">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f7727-227">Podczas kopiowania i wklejania hello następującego kodu, upewnij się, że hello skopiowanych kod jest w hello sam poziom jako hello metody Main.</span><span class="sxs-lookup"><span data-stu-id="f7727-227">When you copy and paste hello following code, make sure that hello copied code is at hello same level as hello Main method.</span></span>

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

15. <span data-ttu-id="f7727-228">W Eksploratorze rozwiązań hello rozwiń hello projektu (DataFactoryAPITestApp), kliknij prawym przyciskiem myszy **odwołania**i kliknij przycisk **Dodaj odwołanie**.</span><span class="sxs-lookup"><span data-stu-id="f7727-228">In hello Solution Explorer, expand hello project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="f7727-229">Zaznacz pole wyboru zestawu **System.Configuration**.</span><span class="sxs-lookup"><span data-stu-id="f7727-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="f7727-230">i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7727-230">and click **OK**.</span></span>
16. <span data-ttu-id="f7727-231">Tworzenie aplikacji konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="f7727-231">Build hello console application.</span></span> <span data-ttu-id="f7727-232">Kliknij przycisk **kompilacji** w hello menu i kliknij przycisk **Kompiluj rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="f7727-232">Click **Build** on hello menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="f7727-233">Upewnij się, że istnieje co najmniej jeden plik w hello **adftutorial** kontenera w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f7727-233">Confirm that there is at least one file in hello **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="f7727-234">Jeśli nie, należy utworzyć **Emp.txt** pliku w Notatniku z powitania po zawartości i przekaż go toohello adftutorial kontenera.</span><span class="sxs-lookup"><span data-stu-id="f7727-234">If not, create **Emp.txt** file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="f7727-235">Uruchom przykładowe hello klikając **debugowania** -> **Rozpocznij debugowanie** menu hello.</span><span class="sxs-lookup"><span data-stu-id="f7727-235">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="f7727-236">Po wyświetleniu hello **pierwsze uruchomienie szczegóły wycinka danych**, zaczekaj kilka minut, a następnie naciśnij klawisz **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="f7727-236">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="f7727-237">Użyj hello tooverify portalu Azure w tej fabryce danych hello **APITutorialFactory** jest tworzony z następującego artefakty hello:</span><span class="sxs-lookup"><span data-stu-id="f7727-237">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
   * <span data-ttu-id="f7727-238">Połączona usługa: **LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="f7727-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="f7727-239">Zestaw danych: **InputDataset** i **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f7727-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="f7727-240">Potok: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="f7727-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="f7727-241">Sprawdź, czy hello dwa rekordy pracowników są tworzone w hello **pustych elementów** tabeli w hello określona baza danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="f7727-241">Verify that hello two employee records are created in hello **emp** table in hello specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7727-242">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7727-242">Next steps</span></span>
<span data-ttu-id="f7727-243">Aby zapoznać się z pełną dokumentacją dotyczącą interfejsu API .NET usługi Data Factory, zobacz [dokumentację interfejsu API .NET usługi Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="f7727-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="f7727-244">W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="f7727-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="f7727-245">Witaj Poniższa tabela zawiera listę magazynów danych obsługiwane jako źródeł i miejsc docelowych przez działanie kopiowania hello:</span><span class="sxs-lookup"><span data-stu-id="f7727-245">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="f7727-246">toolearn o jak magazyn danych toocopy z danych, kliknij łącze hello hello magazynu danych w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="f7727-246">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>

