---
title: Przenoszenie danych do i z programu SQL Server | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat sposobu przenoszenia danych z bazy danych programu SQL Server działa lokalnie lub w maszynie Wirtualnej platformy Azure przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: 9cd2077d897631457925cda5ef5e6df3c0c33177
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="3a1a2-103">Przenoszenie danych do i z lokalnej instalacji programu SQL Server lub na IaaS (Azure VM) przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="3a1a2-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="3a1a2-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przeniesienia danych z lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="3a1a2-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="3a1a2-106">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="3a1a2-106">Supported scenarios</span></span>
<span data-ttu-id="3a1a2-107">Dane należy skopiować **z bazy danych programu SQL Server** do następujących danych przechowuje:</span><span class="sxs-lookup"><span data-stu-id="3a1a2-107">You can copy data **from a SQL Server database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="3a1a2-108">Możesz skopiować dane z następujących baz danych **bazą danych programu SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="3a1a2-108">You can copy data from the following data stores **to a SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="3a1a2-109">Obsługiwane wersje programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="3a1a2-109">Supported SQL Server versions</span></span>
<span data-ttu-id="3a1a2-110">Ta obsługa łącznika programu SQL Server kopiowanie danych z i do następujących wersji wystąpienia obsługiwana lokalnie lub w IaaS platformy Azure przy użyciu zarówno uwierzytelnianie SQL i uwierzytelnianie systemu Windows: SQL Server 2016, programu SQL Server 2014, programu SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="3a1a2-110">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="3a1a2-111">Włączenie łączności</span><span class="sxs-lookup"><span data-stu-id="3a1a2-111">Enabling connectivity</span></span>
<span data-ttu-id="3a1a2-112">Koncepcje i kroki niezbędne do łączenia z programu SQL Server obsługiwana lokalnie lub na maszynach wirtualnych Azure IaaS (infrastruktury jako — usługa) są takie same.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-112">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span></span> <span data-ttu-id="3a1a2-113">W obu przypadkach należy użyć bramy zarządzania danymi dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-113">In both cases, you need to use Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="3a1a2-114">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby dowiedzieć się więcej na temat bramy zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="3a1a2-115">Konfigurowanie wystąpienia bramy jest jako warunek wstępny dla łączenia z programem SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="3a1a2-116">Gdy możesz zainstalować bramę na tym samym komputerze lokalnym lub wystąpienie maszyny Wirtualnej w chmurze, co program SQL Server w celu zapewnienia lepszej wydajności, zaleca się zainstalować je na oddzielnych komputerach.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-116">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="3a1a2-117">Taki bramy i serwera SQL na oddzielnych komputerach zmniejsza rywalizacji.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-117">Having the gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="3a1a2-118">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="3a1a2-118">Getting started</span></span>
<span data-ttu-id="3a1a2-119">Można utworzyć potok z działaniem kopiowania przenoszenia danych z lokalną bazą danych programu SQL Server przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="3a1a2-120">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="3a1a2-121">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="3a1a2-122">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3a1a2-123">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="3a1a2-124">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="3a1a2-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="3a1a2-125">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-125">Create a **data factory**.</span></span> <span data-ttu-id="3a1a2-126">Fabryka danych może zawierać co najmniej jeden potoków.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="3a1a2-127">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="3a1a2-128">Na przykład jeśli kopiujesz dane z bazy danych programu SQL Server do magazynu obiektów blob platformy Azure, Utwórz dwa połączone usługi, aby połączyć bazy danych programu SQL Server z kontem magazynu platformy Azure z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-128">For example, if you are copying data from a SQL Server database to an Azure blob storage, you create two linked services to link your SQL Server database and Azure storage account to your data factory.</span></span> <span data-ttu-id="3a1a2-129">Dla właściwości połączonej usługi, które są specyficzne dla bazy danych programu SQL Server, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-129">For linked service properties that are specific to SQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="3a1a2-130">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="3a1a2-131">W tym przykładzie wymienionych w ostatnim kroku tworzenia zestawu danych, aby określić tabeli SQL w bazie danych programu SQL Server, zawierający dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-131">In the example mentioned in the last step, you create a dataset to specify the SQL table in your SQL Server database that contains the input data.</span></span> <span data-ttu-id="3a1a2-132">I Utwórz innego elementu dataset, aby określić folder, w którym przechowywane są dane skopiowane z bazy danych programu SQL Server i kontener obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-132">And, you create another dataset to specify the blob container and the folder that holds the data copied from the SQL Server database.</span></span> <span data-ttu-id="3a1a2-133">Dla właściwości zestawu danych, które są specyficzne dla bazy danych programu SQL Server, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-133">For dataset properties that are specific to SQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="3a1a2-134">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="3a1a2-135">W przykładzie wspomniano wcześniej używasz SqlSource jako źródło i BlobSink jako zbiorniku dla działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-135">In the example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="3a1a2-136">Podobnie są kopiowane z magazynu obiektów Blob Azure do bazy danych programu SQL Server, należy użyć BlobSource i SqlSink w przypadku działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-136">Similarly, if you are copying from Azure Blob Storage to SQL Server Database, you use BlobSource and SqlSink in the copy activity.</span></span> <span data-ttu-id="3a1a2-137">Właściwości działania kopiowania specyficzne dla bazy danych programu SQL Server, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-137">For copy activity properties that are specific to SQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="3a1a2-138">Aby uzyskać szczegółowe informacje dotyczące sposobu używania magazynu danych jako źródło lub zbiorniku kliknij łącze w poprzedniej sekcji dla magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="3a1a2-139">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="3a1a2-140">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="3a1a2-141">Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane do kopiowania danych do/z lokalną bazą danych programu SQL Server, zobacz [przykłady JSON](#json-examples-for-copying-data-from-and-to-sql-server) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="3a1a2-142">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do programu SQL Server:</span><span class="sxs-lookup"><span data-stu-id="3a1a2-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="3a1a2-143">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="3a1a2-143">Linked service properties</span></span>
<span data-ttu-id="3a1a2-144">Tworzenie połączonej usługi typu **OnPremisesSqlServer** do połączenia z lokalną bazą danych programu SQL Server z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-144">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="3a1a2-145">Poniższa tabela zawiera opis specyficzne dla lokalnej usługi SQL Server połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-145">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="3a1a2-146">Poniższa tabela zawiera opis specyficzne dla usługi SQL Server połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-146">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="3a1a2-147">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3a1a2-147">Property</span></span> | <span data-ttu-id="3a1a2-148">Opis</span><span class="sxs-lookup"><span data-stu-id="3a1a2-148">Description</span></span> | <span data-ttu-id="3a1a2-149">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3a1a2-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a1a2-150">type</span><span class="sxs-lookup"><span data-stu-id="3a1a2-150">type</span></span> |<span data-ttu-id="3a1a2-151">Powinien mieć ustawioną właściwość type: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-151">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="3a1a2-152">Tak</span><span class="sxs-lookup"><span data-stu-id="3a1a2-152">Yes</span></span> |
| <span data-ttu-id="3a1a2-153">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="3a1a2-153">connectionString</span></span> |<span data-ttu-id="3a1a2-154">Określ connectionString informacje wymagane do połączenia z lokalną bazą danych programu SQL Server, przy użyciu uwierzytelniania SQL lub uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-154">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="3a1a2-155">Tak</span><span class="sxs-lookup"><span data-stu-id="3a1a2-155">Yes</span></span> |
| <span data-ttu-id="3a1a2-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3a1a2-156">gatewayName</span></span> |<span data-ttu-id="3a1a2-157">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-157">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="3a1a2-158">Tak</span><span class="sxs-lookup"><span data-stu-id="3a1a2-158">Yes</span></span> |
| <span data-ttu-id="3a1a2-159">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="3a1a2-159">username</span></span> |<span data-ttu-id="3a1a2-160">Określ nazwę użytkownika, jeśli używasz uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="3a1a2-161">Przykład: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="3a1a2-162">Nie</span><span class="sxs-lookup"><span data-stu-id="3a1a2-162">No</span></span> |
| <span data-ttu-id="3a1a2-163">hasło</span><span class="sxs-lookup"><span data-stu-id="3a1a2-163">password</span></span> |<span data-ttu-id="3a1a2-164">Określ hasło dla konta użytkownika, określone nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="3a1a2-165">Nie</span><span class="sxs-lookup"><span data-stu-id="3a1a2-165">No</span></span> |

<span data-ttu-id="3a1a2-166">Można szyfrować poświadczeń przy użyciu **AzureRmDataFactoryEncryptValue nowy** polecenia cmdlet i używać ich w parametrach połączenia, jak pokazano w poniższym przykładzie (**EncryptedCredential** właściwość):</span><span class="sxs-lookup"><span data-stu-id="3a1a2-166">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="3a1a2-167">Przykłady</span><span class="sxs-lookup"><span data-stu-id="3a1a2-167">Samples</span></span>
<span data-ttu-id="3a1a2-168">**JSON dla przy użyciu uwierzytelniania programu SQL**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-168">**JSON for using SQL Authentication**</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
<span data-ttu-id="3a1a2-169">**JSON dla przy użyciu uwierzytelniania systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="3a1a2-170">Brama zarządzania danymi zostanie spersonifikować określone konto użytkownika nawiązać połączenia z lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-170">Data Management Gateway will impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="3a1a2-171">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="3a1a2-171">Dataset properties</span></span>
<span data-ttu-id="3a1a2-172">W przykładach, użyto zestawu danych typu **SqlServerTable** do reprezentowania tabeli w bazie danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-172">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span></span>  

<span data-ttu-id="3a1a2-173">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3a1a2-174">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów zestawu danych (SQL Server, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="3a1a2-175">Sekcja typeProperties jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-175">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="3a1a2-176">**TypeProperties** sekcja dla zestawu danych typu **SqlServerTable** ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="3a1a2-176">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span></span>

| <span data-ttu-id="3a1a2-177">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3a1a2-177">Property</span></span> | <span data-ttu-id="3a1a2-178">Opis</span><span class="sxs-lookup"><span data-stu-id="3a1a2-178">Description</span></span> | <span data-ttu-id="3a1a2-179">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3a1a2-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a1a2-180">tableName</span><span class="sxs-lookup"><span data-stu-id="3a1a2-180">tableName</span></span> |<span data-ttu-id="3a1a2-181">Nazwa tabeli lub widoku w wystąpieniu bazy danych serwera SQL, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-181">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="3a1a2-182">Tak</span><span class="sxs-lookup"><span data-stu-id="3a1a2-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="3a1a2-183">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="3a1a2-183">Copy activity properties</span></span>
<span data-ttu-id="3a1a2-184">Jeśli przenosisz dane z bazy danych programu SQL Server, w przypadku działania kopiowania, aby ustawić typ źródła **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-184">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="3a1a2-185">Podobnie jeśli przenosisz dane do bazy danych programu SQL Server, należy ustawić typ ujścia w działanie kopiowania do **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-185">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="3a1a2-186">Ta sekcja zawiera listę obsługiwanych przez SqlSource i SqlSink właściwości.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="3a1a2-187">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-187">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3a1a2-188">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="3a1a2-189">Działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-189">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="3a1a2-190">Właściwości, które są dostępne w sekcji typeProperties działania różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-190">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="3a1a2-191">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-191">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="3a1a2-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="3a1a2-192">SqlSource</span></span>
<span data-ttu-id="3a1a2-193">Gdy źródło w działaniu kopiowania jest typu **SqlSource**, są dostępne w następujących właściwości **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="3a1a2-193">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="3a1a2-194">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3a1a2-194">Property</span></span> | <span data-ttu-id="3a1a2-195">Opis</span><span class="sxs-lookup"><span data-stu-id="3a1a2-195">Description</span></span> | <span data-ttu-id="3a1a2-196">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="3a1a2-196">Allowed values</span></span> | <span data-ttu-id="3a1a2-197">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3a1a2-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3a1a2-198">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="3a1a2-198">sqlReaderQuery</span></span> |<span data-ttu-id="3a1a2-199">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-199">Use the custom query to read data.</span></span> |<span data-ttu-id="3a1a2-200">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-200">SQL query string.</span></span> <span data-ttu-id="3a1a2-201">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-201">For example: select * from MyTable.</span></span> <span data-ttu-id="3a1a2-202">Może odwoływać się wiele tabel z bazy danych odwołuje się zestaw danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-202">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="3a1a2-203">Jeśli nie zostanie określony, która zostanie wykonana instrukcja SQL: Wybierz z MyTable.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-203">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="3a1a2-204">Nie</span><span class="sxs-lookup"><span data-stu-id="3a1a2-204">No</span></span> |
| <span data-ttu-id="3a1a2-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="3a1a2-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="3a1a2-206">Nazwa procedury przechowywanej, która odczytuje dane z tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-206">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="3a1a2-207">Nazwa procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-207">Name of the stored procedure.</span></span> <span data-ttu-id="3a1a2-208">Ostatniej instrukcji SQL musi być instrukcji SELECT w procedurze składowanej.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-208">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="3a1a2-209">Nie</span><span class="sxs-lookup"><span data-stu-id="3a1a2-209">No</span></span> |
| <span data-ttu-id="3a1a2-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="3a1a2-210">storedProcedureParameters</span></span> |<span data-ttu-id="3a1a2-211">Parametry dla procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-211">Parameters for the stored procedure.</span></span> |<span data-ttu-id="3a1a2-212">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-212">Name/value pairs.</span></span> <span data-ttu-id="3a1a2-213">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, nazwy i wielkość liter w wyrazie parametry procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-213">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="3a1a2-214">Nie</span><span class="sxs-lookup"><span data-stu-id="3a1a2-214">No</span></span> |

<span data-ttu-id="3a1a2-215">Jeśli **sqlReaderQuery** określono dla SqlSource, odbywa się działanie kopii tego zapytania względem źródła danych programu SQL Server można pobrać danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-215">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="3a1a2-216">Można również określić procedury składowanej, podając **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli jest to procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-216">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="3a1a2-217">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName kolumny zdefiniowane w sekcji struktury są używane do tworzenia zapytania select w celu uruchomienia bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="3a1a2-218">Jeśli definicji zestawu danych nie ma on struktury, wszystkie kolumny są wybierane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-218">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="3a1a2-219">Jeśli używasz **sqlReaderStoredProcedureName**, należy określić wartość dla **tableName** właściwość w zestawie danych JSON.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-219">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="3a1a2-220">Nie ma żadnych operacji sprawdzania poprawności, jednak wykonywać na tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="3a1a2-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="3a1a2-221">SqlSink</span></span>
<span data-ttu-id="3a1a2-222">**SqlSink** obsługuje następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="3a1a2-222">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="3a1a2-223">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3a1a2-223">Property</span></span> | <span data-ttu-id="3a1a2-224">Opis</span><span class="sxs-lookup"><span data-stu-id="3a1a2-224">Description</span></span> | <span data-ttu-id="3a1a2-225">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="3a1a2-225">Allowed values</span></span> | <span data-ttu-id="3a1a2-226">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3a1a2-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3a1a2-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="3a1a2-227">writeBatchTimeout</span></span> |<span data-ttu-id="3a1a2-228">Czas na ukończenie zanim upłynie limit czasu operacji wstawiania wsadowego oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-228">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="3a1a2-229">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="3a1a2-229">timespan</span></span><br/><br/> <span data-ttu-id="3a1a2-230">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="3a1a2-231">Nie</span><span class="sxs-lookup"><span data-stu-id="3a1a2-231">No</span></span> |
| <span data-ttu-id="3a1a2-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="3a1a2-232">writeBatchSize</span></span> |<span data-ttu-id="3a1a2-233">Wstawia dane do tabeli SQL, gdy writeBatchSize osiągnie rozmiar buforu.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-233">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="3a1a2-234">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="3a1a2-234">Integer (number of rows)</span></span> |<span data-ttu-id="3a1a2-235">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="3a1a2-235">No (default: 10000)</span></span> |
| <span data-ttu-id="3a1a2-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="3a1a2-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="3a1a2-237">Określ kwerendę dla działania kopiowania do wykonania w taki sposób, że dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-237">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="3a1a2-238">Aby uzyskać więcej informacji, zobacz [powtarzalne kopiowania](#repeatable-copy) sekcji.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="3a1a2-239">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-239">A query statement.</span></span> |<span data-ttu-id="3a1a2-240">Nie</span><span class="sxs-lookup"><span data-stu-id="3a1a2-240">No</span></span> |
| <span data-ttu-id="3a1a2-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="3a1a2-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="3a1a2-242">Określ nazwę kolumny dla aktywności kopiowania wypełnić automatycznie generowane wycinek identyfikator, który służy do oczyszczania danych określonego wycinek czas ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-242">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="3a1a2-243">Aby uzyskać więcej informacji, zobacz [powtarzalne kopiowania](#repeatable-copy) sekcji.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="3a1a2-244">Nazwa kolumny kolumnę o typie danych binary(32).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="3a1a2-245">Nie</span><span class="sxs-lookup"><span data-stu-id="3a1a2-245">No</span></span> |
| <span data-ttu-id="3a1a2-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="3a1a2-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="3a1a2-247">Nazwa procedury składowanej danych upserts (aktualizacje/INSERT) do tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-247">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="3a1a2-248">Nazwa procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-248">Name of the stored procedure.</span></span> |<span data-ttu-id="3a1a2-249">Nie</span><span class="sxs-lookup"><span data-stu-id="3a1a2-249">No</span></span> |
| <span data-ttu-id="3a1a2-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="3a1a2-250">storedProcedureParameters</span></span> |<span data-ttu-id="3a1a2-251">Parametry dla procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-251">Parameters for the stored procedure.</span></span> |<span data-ttu-id="3a1a2-252">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-252">Name/value pairs.</span></span> <span data-ttu-id="3a1a2-253">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, nazwy i wielkość liter w wyrazie parametry procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-253">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="3a1a2-254">Nie</span><span class="sxs-lookup"><span data-stu-id="3a1a2-254">No</span></span> |
| <span data-ttu-id="3a1a2-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="3a1a2-255">sqlWriterTableType</span></span> |<span data-ttu-id="3a1a2-256">Należy określić nazwę typu tabeli do użycia w procedurze składowanej.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-256">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="3a1a2-257">Działanie kopiowania udostępnia dane jest przenoszony w tabeli tymczasowej o tym typie tabeli.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-257">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="3a1a2-258">Kod procedury składowanej można następnie scalić dane są kopiowane z istniejącymi danymi.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-258">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="3a1a2-259">Nazwa typu tabeli.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-259">A table type name.</span></span> |<span data-ttu-id="3a1a2-260">Nie</span><span class="sxs-lookup"><span data-stu-id="3a1a2-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-to-sql-server"></a><span data-ttu-id="3a1a2-261">Przykłady JSON do kopiowania danych do programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="3a1a2-261">JSON examples for copying data from and to SQL Server</span></span>
<span data-ttu-id="3a1a2-262">Poniższe przykłady zapewniają definicje JSON, których można utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-262">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="3a1a2-263">Poniższe przykłady pokazują, jak skopiować dane do i z programu SQL Server i magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-263">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="3a1a2-264">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-264">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-to-azure-blob"></a><span data-ttu-id="3a1a2-265">Przykład: Kopiowanie danych z programu SQL Server do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3a1a2-265">Example: Copy data from SQL Server to Azure Blob</span></span>
<span data-ttu-id="3a1a2-266">Poniższy przykład przedstawia:</span><span class="sxs-lookup"><span data-stu-id="3a1a2-266">The following sample shows:</span></span>

1. <span data-ttu-id="3a1a2-267">Połączonej usługi typu [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="3a1a2-268">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3a1a2-269">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="3a1a2-270">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="3a1a2-271">[Potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [SqlSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-271">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="3a1a2-272">Przykład kopiuje dane szeregów czasowych z tabeli programu SQL Server do obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-272">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span></span> <span data-ttu-id="3a1a2-273">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-273">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="3a1a2-274">Pierwszym krokiem konfiguracji bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-274">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="3a1a2-275">Instrukcje znajdują się w [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-275">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="3a1a2-276">**Usługi SQL Server połączone**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-276">**SQL Server linked service**</span></span>
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="3a1a2-277">**Azure Blob połączoną usługą magazynu**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-277">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="3a1a2-278">**Wejściowy zestaw danych programu SQL Server**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="3a1a2-279">Przykładzie przyjęto założenie, utworzono tabelę "MyTable" w programie SQL Server i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-279">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="3a1a2-280">Kwerendy można na wiele tabel w ramach tej samej bazy danych za pomocą jednego zestawu danych, ale pojedynczej tabeli muszą być używane do typeProperty tableName zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-280">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="3a1a2-281">Ustawienie "external": "prawda" informuje usługi fabryka danych czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-281">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="3a1a2-282">**Azure Blob wyjściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="3a1a2-283">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-283">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3a1a2-284">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-284">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="3a1a2-285">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-285">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="3a1a2-286">**W potoku z działanie kopiowania**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="3a1a2-287">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania tych zestawów danych wejściowych i wyjściowych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-287">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="3a1a2-288">W definicji JSON potoku **źródła** ustawiono typ **SqlSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-288">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="3a1a2-289">Określony dla zapytania SQL **SqlReaderQuery** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-289">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```
<span data-ttu-id="3a1a2-290">W tym przykładzie **sqlReaderQuery** dla SqlSource został określony.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-290">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="3a1a2-291">Działanie kopiowania uruchamia to zapytanie względem źródła danych programu SQL Server można pobrać danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-291">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="3a1a2-292">Można również określić procedury składowanej, podając **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli jest to procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-292">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="3a1a2-293">SqlReaderQuery można odwoływać się wiele tabel w bazie danych odwołuje się zestaw danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-293">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="3a1a2-294">Nie jest ograniczona do tabeli, ustawić jako typeProperty tableName zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-294">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="3a1a2-295">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName kolumny zdefiniowane w sekcji struktury są używane do tworzenia zapytania select w celu uruchomienia bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="3a1a2-296">Jeśli definicji zestawu danych nie ma on struktury, wszystkie kolumny są wybierane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-296">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="3a1a2-297">Zobacz [źródła Sql](#sqlsource) sekcji i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) listę obsługiwanych przez SqlSource i BlobSink właściwości.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-297">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-to-sql-server"></a><span data-ttu-id="3a1a2-298">Przykład: Kopiowanie danych z obiektu Blob Azure do programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="3a1a2-298">Example: Copy data from Azure Blob to SQL Server</span></span>
<span data-ttu-id="3a1a2-299">Poniższy przykład przedstawia:</span><span class="sxs-lookup"><span data-stu-id="3a1a2-299">The following sample shows:</span></span>

1. <span data-ttu-id="3a1a2-300">Połączonej usługi typu [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-300">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="3a1a2-301">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-301">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3a1a2-302">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="3a1a2-303">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="3a1a2-304">[Potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-304">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="3a1a2-305">Kopie próbki szeregów czasowych dane z usługi Azure blob do programu SQL Server tabeli co godzinę.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-305">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span></span> <span data-ttu-id="3a1a2-306">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-306">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="3a1a2-307">**Usługi SQL Server połączone**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-307">**SQL Server linked service**</span></span>

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="3a1a2-308">**Azure Blob połączoną usługą magazynu**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-308">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="3a1a2-309">**Azure wejściowego zestawu danych obiektów Blob**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="3a1a2-310">Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3a1a2-311">Nazwa i ścieżka pliku folder dla obiektu blob dynamicznie są oceniane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-311">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="3a1a2-312">Ścieżka folderu korzysta rok, miesiąc i dzień część czas rozpoczęcia, a nazwa pliku godzina część czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-312">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="3a1a2-313">"external": ustawienie "prawda" usługi fabryka danych informuje, czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-313">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="3a1a2-314">**Zestaw danych wyjściowych programu SQL Server**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="3a1a2-315">Przykład kopiuje dane do tabeli o nazwie "MyTable" w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-315">The sample copies data to a table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="3a1a2-316">Tworzenie tabeli w programie SQL Server z taką samą liczbę kolumn, zgodnie z oczekiwaniami pliku Blob CSV zawiera.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-316">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="3a1a2-317">Nowe wiersze są dodawane do tabeli co godzinę.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-317">New rows are added to the table every hour.</span></span>

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="3a1a2-318">**W potoku z działanie kopiowania**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="3a1a2-319">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania tych zestawów danych wejściowych i wyjściowych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-319">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="3a1a2-320">W definicji JSON potoku **źródła** ustawiono typ **BlobSource** i **zbiornika** ustawiono typ **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-320">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="3a1a2-321">Rozwiązywanie problemów z połączeniem</span><span class="sxs-lookup"><span data-stu-id="3a1a2-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="3a1a2-322">Skonfiguruj program SQL Server na akceptowanie połączeń zdalnych.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-322">Configure your SQL Server to accept remote connections.</span></span> <span data-ttu-id="3a1a2-323">Uruchom **programu SQL Server Management Studio**, kliknij prawym przyciskiem myszy **serwera**i kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="3a1a2-324">Wybierz **połączeń** z listy i wyboru **zezwolenie na zdalne połączenia z serwerem**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-324">Select **Connections** from the list and check **Allow remote connections to the server**.</span></span>

    ![Włącz połączenia zdalne](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="3a1a2-326">Zobacz [konfigurowania dostępu zdalnego opcji konfiguracji serwera](https://msdn.microsoft.com/library/ms191464.aspx) szczegółowy opis kroków.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-326">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="3a1a2-327">Uruchom **programu SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="3a1a2-328">Rozwiń węzeł **konfigurację sieci programu SQL Server** dla tego wystąpienia, a następnie wybierz **protokoły dla elementu MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-328">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="3a1a2-329">Powinny pojawić się protokołów w prawym okienku.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-329">You should see protocols in the right-pane.</span></span> <span data-ttu-id="3a1a2-330">Włącz protokół TCP/IP, klikając prawym przyciskiem myszy **TCP/IP** i klikając **włączyć**.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Włącz protokół TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="3a1a2-332">Zobacz [włączyć lub wyłączyć protokół sieciowy serwera](https://msdn.microsoft.com/library/ms191294.aspx) szczegółowe informacje i alternatywny sposób włączania protokołu TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="3a1a2-333">W tym samym oknie, kliknij dwukrotnie **TCP/IP** można uruchomić **właściwości protokołu TCP/IP** okna.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-333">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="3a1a2-334">Przełącz się do **adresów IP** kartę.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-334">Switch to the **IP Addresses** tab.</span></span> <span data-ttu-id="3a1a2-335">Przewiń w dół, aby znaleźć **IPWszystkie** sekcji.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-335">Scroll down to see **IPAll** section.</span></span> <span data-ttu-id="3a1a2-336">Należy zanotować ** TCP Port ** (domyślnie jest **1433**).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-336">Note down the **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="3a1a2-337">Utwórz **reguły zapory systemu Windows** na maszynie, aby zezwolić na ruch przychodzący za pośrednictwem tego portu.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-337">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="3a1a2-338">**Sprawdź połączenie**: Aby połączyć się z serwerem SQL przy użyciu w pełni kwalifikowanej nazwy, użyj programu SQL Server Management Studio z innego komputera.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-338">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="3a1a2-339">Na przykład: "<machine>.<domain>. Corp.<company>.com, 1433. "</span><span class="sxs-lookup"><span data-stu-id="3a1a2-339">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="3a1a2-340">Zobacz [przenoszenie danych między lokalnych źródeł i w chmurze z brama zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md) Aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-340">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="3a1a2-341">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-341">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="3a1a2-342">Kolumny tożsamości w docelowej bazie danych</span><span class="sxs-lookup"><span data-stu-id="3a1a2-342">Identity columns in the target database</span></span>
<span data-ttu-id="3a1a2-343">Ta sekcja zawiera przykład, w którym kopiuje dane z tabeli źródłowej z żadnej kolumny tożsamości do tabeli docelowej z kolumny tożsamości.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-343">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="3a1a2-344">**Tabela źródłowa:**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-344">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="3a1a2-345">**Tabela docelowa:**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-345">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="3a1a2-346">Zwróć uwagę, że tabela docelowa ma kolumny tożsamości.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-346">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="3a1a2-347">**Źródło zestawu danych JSON definicji**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-347">**Source dataset JSON definition**</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="3a1a2-348">**Docelowy zestaw danych JSON definicji**</span><span class="sxs-lookup"><span data-stu-id="3a1a2-348">**Destination dataset JSON definition**</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

<span data-ttu-id="3a1a2-349">Należy zauważyć, że jako tabela źródłowa i docelowa mają różne schemat (element docelowy ma dodatkową kolumnę z tożsamością).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-349">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="3a1a2-350">W tym scenariuszu, należy określić **struktury** właściwości w definicji zestawu danych docelowego, który nie zawiera kolumny tożsamości.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-350">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="3a1a2-351">Wywołaj procedurę składowaną z zbiornika SQL</span><span class="sxs-lookup"><span data-stu-id="3a1a2-351">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="3a1a2-352">Zobacz [wywołaj procedurę składowaną dla obiekt sink SQL w przypadku działania kopiowania](data-factory-invoke-stored-procedure-from-copy-activity.md) artykule przykład wywoływania procedury składowanej z obiektu sink SQL w działaniu kopiowania potoku.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-352">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="3a1a2-353">Mapowanie typu dla programu SQL server</span><span class="sxs-lookup"><span data-stu-id="3a1a2-353">Type mapping for SQL server</span></span>
<span data-ttu-id="3a1a2-354">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, wykonuje działanie kopiowania automatyczne konwersje z typów źródła do zbiornika typów o następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="3a1a2-354">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="3a1a2-355">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="3a1a2-355">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="3a1a2-356">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="3a1a2-356">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="3a1a2-357">Podczas przenoszenia danych do i z programu SQL server, następujące mapowania są używane z typu SQL typ architektury .NET i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-357">When moving data to & from SQL server, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="3a1a2-358">Mapowanie jest taka sama jak mapowanie typu danych serwera SQL dla ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-358">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="3a1a2-359">Typ aparatu bazy danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="3a1a2-359">SQL Server Database Engine type</span></span> | <span data-ttu-id="3a1a2-360">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="3a1a2-360">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="3a1a2-361">bigint</span><span class="sxs-lookup"><span data-stu-id="3a1a2-361">bigint</span></span> |<span data-ttu-id="3a1a2-362">Int64</span><span class="sxs-lookup"><span data-stu-id="3a1a2-362">Int64</span></span> |
| <span data-ttu-id="3a1a2-363">Binarne</span><span class="sxs-lookup"><span data-stu-id="3a1a2-363">binary</span></span> |<span data-ttu-id="3a1a2-364">Byte]</span><span class="sxs-lookup"><span data-stu-id="3a1a2-364">Byte[]</span></span> |
| <span data-ttu-id="3a1a2-365">bitowe</span><span class="sxs-lookup"><span data-stu-id="3a1a2-365">bit</span></span> |<span data-ttu-id="3a1a2-366">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="3a1a2-366">Boolean</span></span> |
| <span data-ttu-id="3a1a2-367">char</span><span class="sxs-lookup"><span data-stu-id="3a1a2-367">char</span></span> |<span data-ttu-id="3a1a2-368">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="3a1a2-368">String, Char[]</span></span> |
| <span data-ttu-id="3a1a2-369">Data</span><span class="sxs-lookup"><span data-stu-id="3a1a2-369">date</span></span> |<span data-ttu-id="3a1a2-370">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="3a1a2-370">DateTime</span></span> |
| <span data-ttu-id="3a1a2-371">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="3a1a2-371">Datetime</span></span> |<span data-ttu-id="3a1a2-372">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="3a1a2-372">DateTime</span></span> |
| <span data-ttu-id="3a1a2-373">datetime2</span><span class="sxs-lookup"><span data-stu-id="3a1a2-373">datetime2</span></span> |<span data-ttu-id="3a1a2-374">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="3a1a2-374">DateTime</span></span> |
| <span data-ttu-id="3a1a2-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="3a1a2-375">Datetimeoffset</span></span> |<span data-ttu-id="3a1a2-376">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="3a1a2-376">DateTimeOffset</span></span> |
| <span data-ttu-id="3a1a2-377">Decimal</span><span class="sxs-lookup"><span data-stu-id="3a1a2-377">Decimal</span></span> |<span data-ttu-id="3a1a2-378">Decimal</span><span class="sxs-lookup"><span data-stu-id="3a1a2-378">Decimal</span></span> |
| <span data-ttu-id="3a1a2-379">Atrybut FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="3a1a2-379">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="3a1a2-380">Byte]</span><span class="sxs-lookup"><span data-stu-id="3a1a2-380">Byte[]</span></span> |
| <span data-ttu-id="3a1a2-381">Float</span><span class="sxs-lookup"><span data-stu-id="3a1a2-381">Float</span></span> |<span data-ttu-id="3a1a2-382">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="3a1a2-382">Double</span></span> |
| <span data-ttu-id="3a1a2-383">Obraz</span><span class="sxs-lookup"><span data-stu-id="3a1a2-383">image</span></span> |<span data-ttu-id="3a1a2-384">Byte]</span><span class="sxs-lookup"><span data-stu-id="3a1a2-384">Byte[]</span></span> |
| <span data-ttu-id="3a1a2-385">int</span><span class="sxs-lookup"><span data-stu-id="3a1a2-385">int</span></span> |<span data-ttu-id="3a1a2-386">Int32</span><span class="sxs-lookup"><span data-stu-id="3a1a2-386">Int32</span></span> |
| <span data-ttu-id="3a1a2-387">oszczędność pieniędzy</span><span class="sxs-lookup"><span data-stu-id="3a1a2-387">money</span></span> |<span data-ttu-id="3a1a2-388">Decimal</span><span class="sxs-lookup"><span data-stu-id="3a1a2-388">Decimal</span></span> |
| <span data-ttu-id="3a1a2-389">nchar</span><span class="sxs-lookup"><span data-stu-id="3a1a2-389">nchar</span></span> |<span data-ttu-id="3a1a2-390">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="3a1a2-390">String, Char[]</span></span> |
| <span data-ttu-id="3a1a2-391">ntext</span><span class="sxs-lookup"><span data-stu-id="3a1a2-391">ntext</span></span> |<span data-ttu-id="3a1a2-392">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="3a1a2-392">String, Char[]</span></span> |
| <span data-ttu-id="3a1a2-393">numeryczne</span><span class="sxs-lookup"><span data-stu-id="3a1a2-393">numeric</span></span> |<span data-ttu-id="3a1a2-394">Decimal</span><span class="sxs-lookup"><span data-stu-id="3a1a2-394">Decimal</span></span> |
| <span data-ttu-id="3a1a2-395">nvarchar</span><span class="sxs-lookup"><span data-stu-id="3a1a2-395">nvarchar</span></span> |<span data-ttu-id="3a1a2-396">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="3a1a2-396">String, Char[]</span></span> |
| <span data-ttu-id="3a1a2-397">rzeczywiste</span><span class="sxs-lookup"><span data-stu-id="3a1a2-397">real</span></span> |<span data-ttu-id="3a1a2-398">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="3a1a2-398">Single</span></span> |
| <span data-ttu-id="3a1a2-399">ROWVERSION</span><span class="sxs-lookup"><span data-stu-id="3a1a2-399">rowversion</span></span> |<span data-ttu-id="3a1a2-400">Byte]</span><span class="sxs-lookup"><span data-stu-id="3a1a2-400">Byte[]</span></span> |
| <span data-ttu-id="3a1a2-401">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="3a1a2-401">smalldatetime</span></span> |<span data-ttu-id="3a1a2-402">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="3a1a2-402">DateTime</span></span> |
| <span data-ttu-id="3a1a2-403">smallint</span><span class="sxs-lookup"><span data-stu-id="3a1a2-403">smallint</span></span> |<span data-ttu-id="3a1a2-404">Int16</span><span class="sxs-lookup"><span data-stu-id="3a1a2-404">Int16</span></span> |
| <span data-ttu-id="3a1a2-405">smallmoney</span><span class="sxs-lookup"><span data-stu-id="3a1a2-405">smallmoney</span></span> |<span data-ttu-id="3a1a2-406">Decimal</span><span class="sxs-lookup"><span data-stu-id="3a1a2-406">Decimal</span></span> |
| <span data-ttu-id="3a1a2-407">sql_variant</span><span class="sxs-lookup"><span data-stu-id="3a1a2-407">sql_variant</span></span> |<span data-ttu-id="3a1a2-408">Obiekt *</span><span class="sxs-lookup"><span data-stu-id="3a1a2-408">Object *</span></span> |
| <span data-ttu-id="3a1a2-409">Tekst</span><span class="sxs-lookup"><span data-stu-id="3a1a2-409">text</span></span> |<span data-ttu-id="3a1a2-410">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="3a1a2-410">String, Char[]</span></span> |
| <span data-ttu-id="3a1a2-411">time</span><span class="sxs-lookup"><span data-stu-id="3a1a2-411">time</span></span> |<span data-ttu-id="3a1a2-412">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="3a1a2-412">TimeSpan</span></span> |
| <span data-ttu-id="3a1a2-413">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="3a1a2-413">timestamp</span></span> |<span data-ttu-id="3a1a2-414">Byte]</span><span class="sxs-lookup"><span data-stu-id="3a1a2-414">Byte[]</span></span> |
| <span data-ttu-id="3a1a2-415">tinyint</span><span class="sxs-lookup"><span data-stu-id="3a1a2-415">tinyint</span></span> |<span data-ttu-id="3a1a2-416">Bajtów</span><span class="sxs-lookup"><span data-stu-id="3a1a2-416">Byte</span></span> |
| <span data-ttu-id="3a1a2-417">Unikatowy identyfikator</span><span class="sxs-lookup"><span data-stu-id="3a1a2-417">uniqueidentifier</span></span> |<span data-ttu-id="3a1a2-418">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="3a1a2-418">Guid</span></span> |
| <span data-ttu-id="3a1a2-419">varbinary</span><span class="sxs-lookup"><span data-stu-id="3a1a2-419">varbinary</span></span> |<span data-ttu-id="3a1a2-420">Byte]</span><span class="sxs-lookup"><span data-stu-id="3a1a2-420">Byte[]</span></span> |
| <span data-ttu-id="3a1a2-421">varchar</span><span class="sxs-lookup"><span data-stu-id="3a1a2-421">varchar</span></span> |<span data-ttu-id="3a1a2-422">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="3a1a2-422">String, Char[]</span></span> |
| <span data-ttu-id="3a1a2-423">xml</span><span class="sxs-lookup"><span data-stu-id="3a1a2-423">xml</span></span> |<span data-ttu-id="3a1a2-424">XML</span><span class="sxs-lookup"><span data-stu-id="3a1a2-424">Xml</span></span> |

## <a name="mapping-source-to-sink-columns"></a><span data-ttu-id="3a1a2-425">Źródło mapowania na obiekt sink kolumn</span><span class="sxs-lookup"><span data-stu-id="3a1a2-425">Mapping source to sink columns</span></span>
<span data-ttu-id="3a1a2-426">Aby mapować kolumn z zestawu źródła danych do kolumn z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-426">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="3a1a2-427">Kopiuj powtarzalne</span><span class="sxs-lookup"><span data-stu-id="3a1a2-427">Repeatable copy</span></span>
<span data-ttu-id="3a1a2-428">Podczas kopiowania danych do bazy danych serwera SQL, działanie kopiowania dołącza dane do tabeli ujścia domyślnie.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-428">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="3a1a2-429">Aby zamiast tego przeprowadzić UPSERT, zobacz [Repeatable zapisu SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artykułu.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-429">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="3a1a2-430">Podczas kopiowania danych z danych relacyjnych przechowuje, należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-430">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="3a1a2-431">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-431">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="3a1a2-432">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-432">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="3a1a2-433">Podczas wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że te same dane jest do odczytu niezależnie od tego, ile razy wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-433">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="3a1a2-434">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="3a1a2-434">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="3a1a2-435">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="3a1a2-435">Performance and Tuning</span></span>
<span data-ttu-id="3a1a2-436">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="3a1a2-436">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
