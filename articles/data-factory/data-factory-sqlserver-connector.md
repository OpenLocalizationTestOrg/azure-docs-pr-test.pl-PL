---
title: aaaMove tooand danych z programu SQL Server | Dokumentacja firmy Microsoft
description: "Więcej informacji dotyczących sposobu toomove danych do/z programu SQL Server bazy danych to znaczy lokalnej lub w maszynie Wirtualnej platformy Azure przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="ef225-103">Przenieś tooand danych z programu SQL Server — lokalnie lub na IaaS (Azure VM) przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="ef225-103">Move data tooand from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="ef225-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ef225-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="ef225-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="ef225-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="ef225-106">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="ef225-106">Supported scenarios</span></span>
<span data-ttu-id="ef225-107">Dane należy skopiować **z bazy danych programu SQL Server** toohello po magazynów danych:</span><span class="sxs-lookup"><span data-stu-id="ef225-107">You can copy data **from a SQL Server database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="ef225-108">Można skopiować danych z powitania po magazyny danych **bazy danych programu SQL Server tooa**:</span><span class="sxs-lookup"><span data-stu-id="ef225-108">You can copy data from hello following data stores **tooa SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="ef225-109">Obsługiwane wersje programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="ef225-109">Supported SQL Server versions</span></span>
<span data-ttu-id="ef225-110">Ta obsługa łącznika programu SQL Server kopiowania danych z / toohello po wersji wystąpienia obsługiwana lokalnie lub w IaaS platformy Azure przy użyciu zarówno uwierzytelnianie SQL i uwierzytelnianie systemu Windows: SQL Server 2016, programu SQL Server 2014, programu SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="ef225-110">This SQL Server connector support copying data from/toohello following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="ef225-111">Włączenie łączności</span><span class="sxs-lookup"><span data-stu-id="ef225-111">Enabling connectivity</span></span>
<span data-ttu-id="ef225-112">są tego samego hello Hello pojęcia i kroki niezbędne do łączenia z programu SQL Server obsługiwana lokalnie lub w usłudze Azure IaaS (infrastruktury jako — usługa), maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ef225-112">hello concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are hello same.</span></span> <span data-ttu-id="ef225-113">W obu przypadkach należy toouse brama zarządzania danymi dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="ef225-113">In both cases, you need toouse Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="ef225-114">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) toolearn artykuł o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello.</span><span class="sxs-lookup"><span data-stu-id="ef225-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="ef225-115">Konfigurowanie wystąpienia bramy jest jako warunek wstępny dla łączenia z programem SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ef225-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="ef225-116">Podczas instalowania bramy na powitania sam lokalnymi wystąpienia maszyny Wirtualnej maszynie lub w chmurze hello programu SQL Server w celu zapewnienia lepszej wydajności, zaleca się, zainstaluj je na oddzielnych komputerach.</span><span class="sxs-lookup"><span data-stu-id="ef225-116">While you can install gateway on hello same on-premises machine or cloud VM instance as hello SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="ef225-117">Taki hello bramy i serwera SQL na oddzielnych komputerach zmniejsza rywalizacji.</span><span class="sxs-lookup"><span data-stu-id="ef225-117">Having hello gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ef225-118">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="ef225-118">Getting started</span></span>
<span data-ttu-id="ef225-119">Można utworzyć potok z działaniem kopiowania przenoszenia danych z lokalną bazą danych programu SQL Server przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="ef225-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="ef225-120">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="ef225-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="ef225-121">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="ef225-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="ef225-122">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="ef225-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ef225-123">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="ef225-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ef225-124">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="ef225-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="ef225-125">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="ef225-125">Create a **data factory**.</span></span> <span data-ttu-id="ef225-126">Fabryka danych może zawierać co najmniej jeden potoków.</span><span class="sxs-lookup"><span data-stu-id="ef225-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="ef225-127">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ef225-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="ef225-128">Na przykład jeśli dane są kopiowane z tooan bazy danych programu SQL Server magazynu obiektów blob platformy Azure, utworzysz dwa toolink połączonej usługi bazy danych programu SQL Server i fabryki danych tooyour konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="ef225-128">For example, if you are copying data from a SQL Server database tooan Azure blob storage, you create two linked services toolink your SQL Server database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="ef225-129">Dla właściwości połączonej usługi, które są określone tooSQL bazy danych serwera, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="ef225-129">For linked service properties that are specific tooSQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="ef225-130">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="ef225-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="ef225-131">W przykładzie hello wymienionych w ostatnim kroku hello utworzeniu tabeli SQL hello toospecify zestawu danych w bazie danych programu SQL Server zawiera hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="ef225-131">In hello example mentioned in hello last step, you create a dataset toospecify hello SQL table in your SQL Server database that contains hello input data.</span></span> <span data-ttu-id="ef225-132">Utwórz innego kontenera obiektów blob hello toospecify zestawu danych i folderu hello, która przechowuje dane hello skopiowanych z hello bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ef225-132">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello SQL Server database.</span></span> <span data-ttu-id="ef225-133">Dla właściwości zestawu danych, które są określone tooSQL bazy danych serwera, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="ef225-133">For dataset properties that are specific tooSQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="ef225-134">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="ef225-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="ef225-135">W przykładzie hello wspomniano wcześniej używa SqlSource jako źródło i BlobSink jako zbiorniku dla aktywności kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="ef225-135">In hello example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="ef225-136">Podobnie są kopiowane z magazynu obiektów Blob Azure tooSQL bazy danych serwera, należy użyć BlobSource i SqlSink w przypadku działania kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="ef225-136">Similarly, if you are copying from Azure Blob Storage tooSQL Server Database, you use BlobSource and SqlSink in hello copy activity.</span></span> <span data-ttu-id="ef225-137">Dla właściwości działania kopiowania, które są określone tooSQL bazy danych serwera, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="ef225-137">For copy activity properties that are specific tooSQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="ef225-138">Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="ef225-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="ef225-139">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="ef225-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="ef225-140">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="ef225-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="ef225-141">Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z lokalną bazą danych programu SQL Server, zobacz [przykłady JSON](#json-examples-for-copying-data-from-and-to-sql-server) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="ef225-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="ef225-142">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooSQL serwera:</span><span class="sxs-lookup"><span data-stu-id="ef225-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="ef225-143">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="ef225-143">Linked service properties</span></span>
<span data-ttu-id="ef225-144">Tworzenie połączonej usługi typu **OnPremisesSqlServer** toolink fabrykę danych tooa bazy danych programu SQL Server lokalne.</span><span class="sxs-lookup"><span data-stu-id="ef225-144">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="ef225-145">Hello w poniższej tabeli przedstawiono opis dla usługi programu SQL Server połączone określonych lokalnych tooon elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="ef225-145">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="ef225-146">Witaj w poniższej tabeli przedstawiono opis dla określonych tooSQL elementów JSON usługi Serwer połączony.</span><span class="sxs-lookup"><span data-stu-id="ef225-146">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="ef225-147">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ef225-147">Property</span></span> | <span data-ttu-id="ef225-148">Opis</span><span class="sxs-lookup"><span data-stu-id="ef225-148">Description</span></span> | <span data-ttu-id="ef225-149">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ef225-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ef225-150">type</span><span class="sxs-lookup"><span data-stu-id="ef225-150">type</span></span> |<span data-ttu-id="ef225-151">powinien mieć ustawioną właściwość type Hello: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="ef225-151">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="ef225-152">Tak</span><span class="sxs-lookup"><span data-stu-id="ef225-152">Yes</span></span> |
| <span data-ttu-id="ef225-153">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="ef225-153">connectionString</span></span> |<span data-ttu-id="ef225-154">Określ informacje connectionString potrzebne tooconnect toohello lokalnej bazy danych SQL Server przy użyciu uwierzytelniania SQL lub uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="ef225-154">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="ef225-155">Tak</span><span class="sxs-lookup"><span data-stu-id="ef225-155">Yes</span></span> |
| <span data-ttu-id="ef225-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ef225-156">gatewayName</span></span> |<span data-ttu-id="ef225-157">Nazwa bramy hello hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ef225-157">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="ef225-158">Tak</span><span class="sxs-lookup"><span data-stu-id="ef225-158">Yes</span></span> |
| <span data-ttu-id="ef225-159">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="ef225-159">username</span></span> |<span data-ttu-id="ef225-160">Określ nazwę użytkownika, jeśli używasz uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="ef225-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="ef225-161">Przykład: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="ef225-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="ef225-162">Nie</span><span class="sxs-lookup"><span data-stu-id="ef225-162">No</span></span> |
| <span data-ttu-id="ef225-163">hasło</span><span class="sxs-lookup"><span data-stu-id="ef225-163">password</span></span> |<span data-ttu-id="ef225-164">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ef225-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="ef225-165">Nie</span><span class="sxs-lookup"><span data-stu-id="ef225-165">No</span></span> |

<span data-ttu-id="ef225-166">Można szyfrować poświadczeń przy użyciu hello **AzureRmDataFactoryEncryptValue nowy** polecenia cmdlet i używać ich w parametrach połączenia hello, jak pokazano w hello poniższy przykład (**EncryptedCredential** właściwość):</span><span class="sxs-lookup"><span data-stu-id="ef225-166">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="ef225-167">Przykłady</span><span class="sxs-lookup"><span data-stu-id="ef225-167">Samples</span></span>
<span data-ttu-id="ef225-168">**JSON dla przy użyciu uwierzytelniania programu SQL**</span><span class="sxs-lookup"><span data-stu-id="ef225-168">**JSON for using SQL Authentication**</span></span>

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
<span data-ttu-id="ef225-169">**JSON dla przy użyciu uwierzytelniania systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="ef225-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="ef225-170">Brama zarządzania danymi zostanie personifikacji hello określony tooconnect toohello lokalnego programu SQL Server bazy danych kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ef225-170">Data Management Gateway will impersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> 

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

## <a name="dataset-properties"></a><span data-ttu-id="ef225-171">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="ef225-171">Dataset properties</span></span>
<span data-ttu-id="ef225-172">W próbkach hello użyto zestawu danych typu **SqlServerTable** toorepresent tabeli w bazie danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ef225-172">In hello samples, you have used a dataset of type **SqlServerTable** toorepresent a table in a SQL Server database.</span></span>  

<span data-ttu-id="ef225-173">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ef225-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ef225-174">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów zestawu danych (SQL Server, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="ef225-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ef225-175">sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello.</span><span class="sxs-lookup"><span data-stu-id="ef225-175">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="ef225-176">Witaj **typeProperties** sekcja dla zestawu danych hello typu **SqlServerTable** ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="ef225-176">hello **typeProperties** section for hello dataset of type **SqlServerTable** has hello following properties:</span></span>

| <span data-ttu-id="ef225-177">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ef225-177">Property</span></span> | <span data-ttu-id="ef225-178">Opis</span><span class="sxs-lookup"><span data-stu-id="ef225-178">Description</span></span> | <span data-ttu-id="ef225-179">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ef225-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ef225-180">tableName</span><span class="sxs-lookup"><span data-stu-id="ef225-180">tableName</span></span> |<span data-ttu-id="ef225-181">Nazwa hello tabeli lub widoku w wystąpieniu bazy danych SQL Server hello, która jest połączona usługa odnosi się do.</span><span class="sxs-lookup"><span data-stu-id="ef225-181">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="ef225-182">Tak</span><span class="sxs-lookup"><span data-stu-id="ef225-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="ef225-183">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="ef225-183">Copy activity properties</span></span>
<span data-ttu-id="ef225-184">Chcesz przenieść dane z bazy danych programu SQL Server, należy ustawić typ źródła hello w przypadku działania kopiowania hello zbyt**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="ef225-184">If you are moving data from a SQL Server database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="ef225-185">Podobnie jeśli przenosisz bazę danych programu SQL Server tooa danych ustawisz typ ujścia hello w przypadku działania kopiowania hello zbyt**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="ef225-185">Similarly, if you are moving data tooa SQL Server database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="ef225-186">Ta sekcja zawiera listę obsługiwanych przez SqlSource i SqlSink właściwości.</span><span class="sxs-lookup"><span data-stu-id="ef225-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="ef225-187">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ef225-187">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ef225-188">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="ef225-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="ef225-189">Witaj działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.</span><span class="sxs-lookup"><span data-stu-id="ef225-189">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="ef225-190">Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="ef225-190">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="ef225-191">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="ef225-191">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="ef225-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="ef225-192">SqlSource</span></span>
<span data-ttu-id="ef225-193">Gdy źródło w działaniu kopiowania jest typu **SqlSource**, dostępne są następujące właściwości hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="ef225-193">When source in a copy activity is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="ef225-194">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ef225-194">Property</span></span> | <span data-ttu-id="ef225-195">Opis</span><span class="sxs-lookup"><span data-stu-id="ef225-195">Description</span></span> | <span data-ttu-id="ef225-196">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="ef225-196">Allowed values</span></span> | <span data-ttu-id="ef225-197">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ef225-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ef225-198">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="ef225-198">sqlReaderQuery</span></span> |<span data-ttu-id="ef225-199">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="ef225-199">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ef225-200">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="ef225-200">SQL query string.</span></span> <span data-ttu-id="ef225-201">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="ef225-201">For example: select * from MyTable.</span></span> <span data-ttu-id="ef225-202">Może odwoływać się wiele tabel z bazy danych hello odwołuje się hello wejściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="ef225-202">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="ef225-203">Jeśli nie zostanie określony, hello instrukcji SQL, która jest wykonywana: Wybierz z MyTable.</span><span class="sxs-lookup"><span data-stu-id="ef225-203">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="ef225-204">Nie</span><span class="sxs-lookup"><span data-stu-id="ef225-204">No</span></span> |
| <span data-ttu-id="ef225-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ef225-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="ef225-206">Nazwa hello przechowywane procedury, która odczytuje dane z hello tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="ef225-206">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="ef225-207">Nazwa hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="ef225-207">Name of hello stored procedure.</span></span> <span data-ttu-id="ef225-208">Witaj ostatniej instrukcji SQL musi być instrukcji SELECT w procedurze hello przechowywane.</span><span class="sxs-lookup"><span data-stu-id="ef225-208">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="ef225-209">Nie</span><span class="sxs-lookup"><span data-stu-id="ef225-209">No</span></span> |
| <span data-ttu-id="ef225-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ef225-210">storedProcedureParameters</span></span> |<span data-ttu-id="ef225-211">Parametry hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="ef225-211">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="ef225-212">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="ef225-212">Name/value pairs.</span></span> <span data-ttu-id="ef225-213">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="ef225-213">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="ef225-214">Nie</span><span class="sxs-lookup"><span data-stu-id="ef225-214">No</span></span> |

<span data-ttu-id="ef225-215">Jeśli hello **sqlReaderQuery** określono hello SqlSource, hello odbywa się działanie kopii tego zapytania hello bazy danych SQL Server źródła tooget hello danych.</span><span class="sxs-lookup"><span data-stu-id="ef225-215">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="ef225-216">Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="ef225-216">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="ef225-217">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello są używane toobuild toorun zapytania select, przed hello bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ef225-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="ef225-218">Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="ef225-218">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="ef225-219">Jeśli używasz **sqlReaderStoredProcedureName**, należy nadal toospecify wartość dla hello **tableName** właściwości w elemencie dataset hello JSON.</span><span class="sxs-lookup"><span data-stu-id="ef225-219">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="ef225-220">Nie ma żadnych operacji sprawdzania poprawności, jednak wykonywać na tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="ef225-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="ef225-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="ef225-221">SqlSink</span></span>
<span data-ttu-id="ef225-222">**SqlSink** obsługuje hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="ef225-222">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="ef225-223">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ef225-223">Property</span></span> | <span data-ttu-id="ef225-224">Opis</span><span class="sxs-lookup"><span data-stu-id="ef225-224">Description</span></span> | <span data-ttu-id="ef225-225">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="ef225-225">Allowed values</span></span> | <span data-ttu-id="ef225-226">Wymagane</span><span class="sxs-lookup"><span data-stu-id="ef225-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ef225-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ef225-227">writeBatchTimeout</span></span> |<span data-ttu-id="ef225-228">Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu.</span><span class="sxs-lookup"><span data-stu-id="ef225-228">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="ef225-229">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="ef225-229">timespan</span></span><br/><br/> <span data-ttu-id="ef225-230">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="ef225-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="ef225-231">Nie</span><span class="sxs-lookup"><span data-stu-id="ef225-231">No</span></span> |
| <span data-ttu-id="ef225-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ef225-232">writeBatchSize</span></span> |<span data-ttu-id="ef225-233">Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="ef225-233">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="ef225-234">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="ef225-234">Integer (number of rows)</span></span> |<span data-ttu-id="ef225-235">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="ef225-235">No (default: 10000)</span></span> |
| <span data-ttu-id="ef225-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="ef225-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="ef225-237">Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="ef225-237">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="ef225-238">Aby uzyskać więcej informacji, zobacz [powtarzalne kopiowania](#repeatable-copy) sekcji.</span><span class="sxs-lookup"><span data-stu-id="ef225-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="ef225-239">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="ef225-239">A query statement.</span></span> |<span data-ttu-id="ef225-240">Nie</span><span class="sxs-lookup"><span data-stu-id="ef225-240">No</span></span> |
| <span data-ttu-id="ef225-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="ef225-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="ef225-242">Określ nazwę kolumny toofill działanie kopiowania identyfikatorem wycinek automatycznie generowane, która jest używana tooclean zapasowych określonych wycinek czas ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="ef225-242">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="ef225-243">Aby uzyskać więcej informacji, zobacz [powtarzalne kopiowania](#repeatable-copy) sekcji.</span><span class="sxs-lookup"><span data-stu-id="ef225-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="ef225-244">Nazwa kolumny kolumnę o typie danych binary(32).</span><span class="sxs-lookup"><span data-stu-id="ef225-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="ef225-245">Nie</span><span class="sxs-lookup"><span data-stu-id="ef225-245">No</span></span> |
| <span data-ttu-id="ef225-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ef225-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="ef225-247">Nazwa hello procedury składowanej danych upserts (aktualizacje/INSERT) do tabeli docelowej hello.</span><span class="sxs-lookup"><span data-stu-id="ef225-247">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="ef225-248">Nazwa hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="ef225-248">Name of hello stored procedure.</span></span> |<span data-ttu-id="ef225-249">Nie</span><span class="sxs-lookup"><span data-stu-id="ef225-249">No</span></span> |
| <span data-ttu-id="ef225-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ef225-250">storedProcedureParameters</span></span> |<span data-ttu-id="ef225-251">Parametry hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="ef225-251">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="ef225-252">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="ef225-252">Name/value pairs.</span></span> <span data-ttu-id="ef225-253">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="ef225-253">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="ef225-254">Nie</span><span class="sxs-lookup"><span data-stu-id="ef225-254">No</span></span> |
| <span data-ttu-id="ef225-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="ef225-255">sqlWriterTableType</span></span> |<span data-ttu-id="ef225-256">Określ toobe nazwy typu tabeli używany w procedurze hello przechowywane.</span><span class="sxs-lookup"><span data-stu-id="ef225-256">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="ef225-257">Działanie kopiowania udostępnia dane hello przenoszone w tabeli tymczasowej o tym typie tabeli.</span><span class="sxs-lookup"><span data-stu-id="ef225-257">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="ef225-258">Procedura składowana kod następnie można scalać dane hello kopiowane z istniejącymi danymi.</span><span class="sxs-lookup"><span data-stu-id="ef225-258">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="ef225-259">Nazwa typu tabeli.</span><span class="sxs-lookup"><span data-stu-id="ef225-259">A table type name.</span></span> |<span data-ttu-id="ef225-260">Nie</span><span class="sxs-lookup"><span data-stu-id="ef225-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a><span data-ttu-id="ef225-261">Przykłady JSON do kopiowania danych z tooSQL serwera</span><span class="sxs-lookup"><span data-stu-id="ef225-261">JSON examples for copying data from and tooSQL Server</span></span>
<span data-ttu-id="ef225-262">Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ef225-262">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ef225-263">Witaj, jak następujące przykłady Pokaż toocopy tooand danych z programu SQL Server i magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="ef225-263">hello following samples show how toocopy data tooand from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="ef225-264">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła tooany z wychwytywanie hello wyrażony w [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="ef225-264">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a><span data-ttu-id="ef225-265">Przykład: Kopiowanie danych z programu SQL Server tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="ef225-265">Example: Copy data from SQL Server tooAzure Blob</span></span>
<span data-ttu-id="ef225-266">następujące przykładowe pokazuje Hello:</span><span class="sxs-lookup"><span data-stu-id="ef225-266">hello following sample shows:</span></span>

1. <span data-ttu-id="ef225-267">Połączonej usługi typu [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ef225-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="ef225-268">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ef225-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ef225-269">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ef225-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="ef225-270">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ef225-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ef225-271">Witaj [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [SqlSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ef225-271">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ef225-272">Przykładowe Hello kopiuje dane szeregów czasowych, z programu SQL Server tooan tabeli obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="ef225-272">hello sample copies time-series data from a SQL Server table tooan Azure blob every hour.</span></span> <span data-ttu-id="ef225-273">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="ef225-273">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="ef225-274">Pierwszym krokiem konfiguracji bramy zarządzania danymi hello.</span><span class="sxs-lookup"><span data-stu-id="ef225-274">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="ef225-275">Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ef225-275">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="ef225-276">**Usługi SQL Server połączone**</span><span class="sxs-lookup"><span data-stu-id="ef225-276">**SQL Server linked service**</span></span>
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
<span data-ttu-id="ef225-277">**Azure Blob połączoną usługą magazynu**</span><span class="sxs-lookup"><span data-stu-id="ef225-277">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="ef225-278">**Wejściowy zestaw danych programu SQL Server**</span><span class="sxs-lookup"><span data-stu-id="ef225-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="ef225-279">przykład Witaj przyjęto założenie, utworzono tabelę "MyTable" w programie SQL Server i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="ef225-279">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="ef225-280">Umożliwia wysyłanie zapytań przez wiele tabel w ramach tej samej bazy danych za pomocą jednego zestawu danych, ale pojedynczej tabeli muszą być używane do hello dataset tableName typeProperty powitalne.</span><span class="sxs-lookup"><span data-stu-id="ef225-280">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="ef225-281">Ustawienie "external": "prawda" informuje usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="ef225-281">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="ef225-282">**Azure Blob wyjściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="ef225-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="ef225-283">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="ef225-283">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ef225-284">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="ef225-284">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ef225-285">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="ef225-285">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="ef225-286">**W potoku z działanie kopiowania**</span><span class="sxs-lookup"><span data-stu-id="ef225-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="ef225-287">potok Hello zawiera działanie kopiowania który jest skonfigurowany toouse te zestawy danych wejściowych i wyjściowych i toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="ef225-287">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ef225-288">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**SqlSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ef225-288">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="ef225-289">Zapytanie SQL Hello określone dla hello **SqlReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="ef225-289">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
<span data-ttu-id="ef225-290">W tym przykładzie **sqlReaderQuery** dla hello SqlSource został określony.</span><span class="sxs-lookup"><span data-stu-id="ef225-290">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="ef225-291">Działanie kopiowania Hello jest uruchamiana to zapytanie dla hello danych hello tooget źródła danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ef225-291">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="ef225-292">Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="ef225-292">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="ef225-293">Hello sqlReaderQuery można odwoływać się wiele tabel w bazie danych hello odwołuje się hello wejściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="ef225-293">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="ef225-294">Nie jest tabelą hello ograniczone tooonly ustawione jako hello typeProperty tableName zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="ef225-294">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="ef225-295">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello są używane toobuild toorun zapytania select, przed hello bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ef225-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="ef225-296">Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="ef225-296">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="ef225-297">Zobacz hello [źródła Sql](#sqlsource) sekcji i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) hello listę obsługiwanych przez SqlSource i BlobSink właściwości.</span><span class="sxs-lookup"><span data-stu-id="ef225-297">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-toosql-server"></a><span data-ttu-id="ef225-298">Przykład: Kopiowanie danych z obiektu Blob Azure tooSQL serwera</span><span class="sxs-lookup"><span data-stu-id="ef225-298">Example: Copy data from Azure Blob tooSQL Server</span></span>
<span data-ttu-id="ef225-299">następujące przykładowe pokazuje Hello:</span><span class="sxs-lookup"><span data-stu-id="ef225-299">hello following sample shows:</span></span>

1. <span data-ttu-id="ef225-300">Witaj połączonej usługi typu [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ef225-300">hello linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="ef225-301">Witaj połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ef225-301">hello linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ef225-302">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ef225-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="ef225-303">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ef225-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ef225-304">Witaj [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="ef225-304">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="ef225-305">Przykładowe Hello kopiuje dane szeregów czasowych, z tabeli programu SQL Server tooa obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="ef225-305">hello sample copies time-series data from an Azure blob tooa SQL Server table every hour.</span></span> <span data-ttu-id="ef225-306">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="ef225-306">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="ef225-307">**Usługi SQL Server połączone**</span><span class="sxs-lookup"><span data-stu-id="ef225-307">**SQL Server linked service**</span></span>

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
<span data-ttu-id="ef225-308">**Azure Blob połączoną usługą magazynu**</span><span class="sxs-lookup"><span data-stu-id="ef225-308">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="ef225-309">**Azure wejściowego zestawu danych obiektów Blob**</span><span class="sxs-lookup"><span data-stu-id="ef225-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="ef225-310">Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="ef225-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ef225-311">Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="ef225-311">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ef225-312">Ścieżka folderu Hello korzysta rok, miesiąc i dzień część czas rozpoczęcia hello, a nazwa pliku hello część hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="ef225-312">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="ef225-313">"external": "prawda" ustawienie informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="ef225-313">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="ef225-314">**Zestaw danych wyjściowych programu SQL Server**</span><span class="sxs-lookup"><span data-stu-id="ef225-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="ef225-315">przykład Witaj kopiuje tabeli tooa danych o nazwie "MyTable" w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ef225-315">hello sample copies data tooa table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="ef225-316">Utwórz tabelę hello w programie SQL Server z hello taką samą liczbę kolumn, zgodnie z oczekiwaniami toocontain pliku Blob CSV hello.</span><span class="sxs-lookup"><span data-stu-id="ef225-316">Create hello table in SQL Server with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="ef225-317">Dodawaniu nowych wierszy tabeli toohello co godzinę.</span><span class="sxs-lookup"><span data-stu-id="ef225-317">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="ef225-318">**W potoku z działanie kopiowania**</span><span class="sxs-lookup"><span data-stu-id="ef225-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="ef225-319">potok Hello zawiera działanie kopiowania który jest skonfigurowany toouse te zestawy danych wejściowych i wyjściowych i toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="ef225-319">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ef225-320">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i **zbiornika** typu ustawiono zbyt**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="ef225-320">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="ef225-321">Rozwiązywanie problemów z połączeniem</span><span class="sxs-lookup"><span data-stu-id="ef225-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="ef225-322">Konfigurowanie połączeń zdalnych tooaccept programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ef225-322">Configure your SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="ef225-323">Uruchom **programu SQL Server Management Studio**, kliknij prawym przyciskiem myszy **serwera**i kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="ef225-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="ef225-324">Wybierz **połączeń** z listy hello i wyboru **Zezwalaj na połączenia zdalne toohello serwera**.</span><span class="sxs-lookup"><span data-stu-id="ef225-324">Select **Connections** from hello list and check **Allow remote connections toohello server**.</span></span>

    ![Włącz połączenia zdalne](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="ef225-326">Zobacz [konfigurowania dostępu zdalnego hello opcji konfiguracji serwera](https://msdn.microsoft.com/library/ms191464.aspx) szczegółowy opis kroków.</span><span class="sxs-lookup"><span data-stu-id="ef225-326">See [Configure hello remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="ef225-327">Uruchom **programu SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="ef225-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="ef225-328">Rozwiń węzeł **konfigurację sieci programu SQL Server** dla hello wystąpienia możesz chcieć, a następnie wybierz **protokoły dla elementu MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="ef225-328">Expand **SQL Server Network Configuration** for hello instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="ef225-329">Protokoły w prawym okienku hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="ef225-329">You should see protocols in hello right-pane.</span></span> <span data-ttu-id="ef225-330">Włącz protokół TCP/IP, klikając prawym przyciskiem myszy **TCP/IP** i klikając **włączyć**.</span><span class="sxs-lookup"><span data-stu-id="ef225-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Włącz protokół TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="ef225-332">Zobacz [włączyć lub wyłączyć protokół sieciowy serwera](https://msdn.microsoft.com/library/ms191294.aspx) szczegółowe informacje i alternatywny sposób włączania protokołu TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="ef225-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="ef225-333">W tym samym oknie Witaj, kliknij dwukrotnie **TCP/IP** toolaunch **właściwości protokołu TCP/IP** okna.</span><span class="sxs-lookup"><span data-stu-id="ef225-333">In hello same window, double-click **TCP/IP** toolaunch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="ef225-334">Przełącz toohello **adresów IP** kartę. Przewiń w dół toosee **IPWszystkie** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ef225-334">Switch toohello **IP Addresses** tab. Scroll down toosee **IPAll** section.</span></span> <span data-ttu-id="ef225-335">Zanotuj hello ** TCP Port ** (domyślnie jest **1433**).</span><span class="sxs-lookup"><span data-stu-id="ef225-335">Note down hello **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="ef225-336">Utwórz **regułę zapory systemu Windows hello** na ruch przychodzący tooallow maszyny hello za pośrednictwem tego portu.</span><span class="sxs-lookup"><span data-stu-id="ef225-336">Create a **rule for hello Windows Firewall** on hello machine tooallow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="ef225-337">**Sprawdź połączenie**: tooconnect toohello SQL Server przy użyciu w pełni kwalifikowana nazwa, użyj programu SQL Server Management Studio z innego komputera.</span><span class="sxs-lookup"><span data-stu-id="ef225-337">**Verify connection**: tooconnect toohello SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="ef225-338">Na przykład: "<machine>.<domain>. Corp.<company>.com, 1433. "</span><span class="sxs-lookup"><span data-stu-id="ef225-338">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="ef225-339">Zobacz [przenoszenie danych między lokalnych źródeł i w chmurze hello z brama zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md) Aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="ef225-339">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="ef225-340">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="ef225-340">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="ef225-341">Kolumny tożsamości w hello docelowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="ef225-341">Identity columns in hello target database</span></span>
<span data-ttu-id="ef225-342">Ta sekcja zawiera przykład, w którym kopiuje dane z tabeli źródłowej z nie tożsamości tooa docelowej tabeli z kolumny tożsamości.</span><span class="sxs-lookup"><span data-stu-id="ef225-342">This section provides an example that copies data from a source table with no identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="ef225-343">**Tabela źródłowa:**</span><span class="sxs-lookup"><span data-stu-id="ef225-343">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="ef225-344">**Tabela docelowa:**</span><span class="sxs-lookup"><span data-stu-id="ef225-344">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="ef225-345">Należy zauważyć, że tabela docelowa hello ma kolumny tożsamości.</span><span class="sxs-lookup"><span data-stu-id="ef225-345">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="ef225-346">**Źródło zestawu danych JSON definicji**</span><span class="sxs-lookup"><span data-stu-id="ef225-346">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="ef225-347">**Docelowy zestaw danych JSON definicji**</span><span class="sxs-lookup"><span data-stu-id="ef225-347">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="ef225-348">Należy zauważyć, że jako tabela źródłowa i docelowa mają różne schemat (element docelowy ma dodatkową kolumnę z tożsamością).</span><span class="sxs-lookup"><span data-stu-id="ef225-348">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="ef225-349">W tym scenariuszu należy toospecify **struktury** właściwości w definicji zestawu danych docelowego hello, która nie zawiera kolumny tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="ef225-349">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="ef225-350">Wywołaj procedurę składowaną z zbiornika SQL</span><span class="sxs-lookup"><span data-stu-id="ef225-350">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="ef225-351">Zobacz [wywołaj procedurę składowaną dla obiekt sink SQL w przypadku działania kopiowania](data-factory-invoke-stored-procedure-from-copy-activity.md) artykule przykład wywoływania procedury składowanej z obiektu sink SQL w działaniu kopiowania potoku.</span><span class="sxs-lookup"><span data-stu-id="ef225-351">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="ef225-352">Mapowanie typu dla programu SQL server</span><span class="sxs-lookup"><span data-stu-id="ef225-352">Type mapping for SQL server</span></span>
<span data-ttu-id="ef225-353">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, hello działanie kopiowania przeprowadza automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="ef225-353">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="ef225-354">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="ef225-354">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="ef225-355">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="ef225-355">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="ef225-356">Podczas przenoszenia danych za & z programu SQL server hello następujące mapowania są używane z too.NET typu SQL i odwrotnie.</span><span class="sxs-lookup"><span data-stu-id="ef225-356">When moving data too& from SQL server, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="ef225-357">Mapowanie Hello jest taki sam jak hello mapowanie typu danych serwera SQL dla ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="ef225-357">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="ef225-358">Typ aparatu bazy danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="ef225-358">SQL Server Database Engine type</span></span> | <span data-ttu-id="ef225-359">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="ef225-359">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="ef225-360">bigint</span><span class="sxs-lookup"><span data-stu-id="ef225-360">bigint</span></span> |<span data-ttu-id="ef225-361">Int64</span><span class="sxs-lookup"><span data-stu-id="ef225-361">Int64</span></span> |
| <span data-ttu-id="ef225-362">Binarne</span><span class="sxs-lookup"><span data-stu-id="ef225-362">binary</span></span> |<span data-ttu-id="ef225-363">Byte]</span><span class="sxs-lookup"><span data-stu-id="ef225-363">Byte[]</span></span> |
| <span data-ttu-id="ef225-364">bitowe</span><span class="sxs-lookup"><span data-stu-id="ef225-364">bit</span></span> |<span data-ttu-id="ef225-365">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="ef225-365">Boolean</span></span> |
| <span data-ttu-id="ef225-366">char</span><span class="sxs-lookup"><span data-stu-id="ef225-366">char</span></span> |<span data-ttu-id="ef225-367">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="ef225-367">String, Char[]</span></span> |
| <span data-ttu-id="ef225-368">Data</span><span class="sxs-lookup"><span data-stu-id="ef225-368">date</span></span> |<span data-ttu-id="ef225-369">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="ef225-369">DateTime</span></span> |
| <span data-ttu-id="ef225-370">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="ef225-370">Datetime</span></span> |<span data-ttu-id="ef225-371">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="ef225-371">DateTime</span></span> |
| <span data-ttu-id="ef225-372">datetime2</span><span class="sxs-lookup"><span data-stu-id="ef225-372">datetime2</span></span> |<span data-ttu-id="ef225-373">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="ef225-373">DateTime</span></span> |
| <span data-ttu-id="ef225-374">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="ef225-374">Datetimeoffset</span></span> |<span data-ttu-id="ef225-375">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="ef225-375">DateTimeOffset</span></span> |
| <span data-ttu-id="ef225-376">Decimal</span><span class="sxs-lookup"><span data-stu-id="ef225-376">Decimal</span></span> |<span data-ttu-id="ef225-377">Decimal</span><span class="sxs-lookup"><span data-stu-id="ef225-377">Decimal</span></span> |
| <span data-ttu-id="ef225-378">Atrybut FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="ef225-378">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="ef225-379">Byte]</span><span class="sxs-lookup"><span data-stu-id="ef225-379">Byte[]</span></span> |
| <span data-ttu-id="ef225-380">Float</span><span class="sxs-lookup"><span data-stu-id="ef225-380">Float</span></span> |<span data-ttu-id="ef225-381">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="ef225-381">Double</span></span> |
| <span data-ttu-id="ef225-382">Obraz</span><span class="sxs-lookup"><span data-stu-id="ef225-382">image</span></span> |<span data-ttu-id="ef225-383">Byte]</span><span class="sxs-lookup"><span data-stu-id="ef225-383">Byte[]</span></span> |
| <span data-ttu-id="ef225-384">int</span><span class="sxs-lookup"><span data-stu-id="ef225-384">int</span></span> |<span data-ttu-id="ef225-385">Int32</span><span class="sxs-lookup"><span data-stu-id="ef225-385">Int32</span></span> |
| <span data-ttu-id="ef225-386">oszczędność pieniędzy</span><span class="sxs-lookup"><span data-stu-id="ef225-386">money</span></span> |<span data-ttu-id="ef225-387">Decimal</span><span class="sxs-lookup"><span data-stu-id="ef225-387">Decimal</span></span> |
| <span data-ttu-id="ef225-388">nchar</span><span class="sxs-lookup"><span data-stu-id="ef225-388">nchar</span></span> |<span data-ttu-id="ef225-389">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="ef225-389">String, Char[]</span></span> |
| <span data-ttu-id="ef225-390">ntext</span><span class="sxs-lookup"><span data-stu-id="ef225-390">ntext</span></span> |<span data-ttu-id="ef225-391">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="ef225-391">String, Char[]</span></span> |
| <span data-ttu-id="ef225-392">numeryczne</span><span class="sxs-lookup"><span data-stu-id="ef225-392">numeric</span></span> |<span data-ttu-id="ef225-393">Decimal</span><span class="sxs-lookup"><span data-stu-id="ef225-393">Decimal</span></span> |
| <span data-ttu-id="ef225-394">nvarchar</span><span class="sxs-lookup"><span data-stu-id="ef225-394">nvarchar</span></span> |<span data-ttu-id="ef225-395">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="ef225-395">String, Char[]</span></span> |
| <span data-ttu-id="ef225-396">rzeczywiste</span><span class="sxs-lookup"><span data-stu-id="ef225-396">real</span></span> |<span data-ttu-id="ef225-397">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="ef225-397">Single</span></span> |
| <span data-ttu-id="ef225-398">ROWVERSION</span><span class="sxs-lookup"><span data-stu-id="ef225-398">rowversion</span></span> |<span data-ttu-id="ef225-399">Byte]</span><span class="sxs-lookup"><span data-stu-id="ef225-399">Byte[]</span></span> |
| <span data-ttu-id="ef225-400">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="ef225-400">smalldatetime</span></span> |<span data-ttu-id="ef225-401">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="ef225-401">DateTime</span></span> |
| <span data-ttu-id="ef225-402">smallint</span><span class="sxs-lookup"><span data-stu-id="ef225-402">smallint</span></span> |<span data-ttu-id="ef225-403">Int16</span><span class="sxs-lookup"><span data-stu-id="ef225-403">Int16</span></span> |
| <span data-ttu-id="ef225-404">smallmoney</span><span class="sxs-lookup"><span data-stu-id="ef225-404">smallmoney</span></span> |<span data-ttu-id="ef225-405">Decimal</span><span class="sxs-lookup"><span data-stu-id="ef225-405">Decimal</span></span> |
| <span data-ttu-id="ef225-406">sql_variant</span><span class="sxs-lookup"><span data-stu-id="ef225-406">sql_variant</span></span> |<span data-ttu-id="ef225-407">Obiekt *</span><span class="sxs-lookup"><span data-stu-id="ef225-407">Object *</span></span> |
| <span data-ttu-id="ef225-408">Tekst</span><span class="sxs-lookup"><span data-stu-id="ef225-408">text</span></span> |<span data-ttu-id="ef225-409">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="ef225-409">String, Char[]</span></span> |
| <span data-ttu-id="ef225-410">time</span><span class="sxs-lookup"><span data-stu-id="ef225-410">time</span></span> |<span data-ttu-id="ef225-411">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="ef225-411">TimeSpan</span></span> |
| <span data-ttu-id="ef225-412">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="ef225-412">timestamp</span></span> |<span data-ttu-id="ef225-413">Byte]</span><span class="sxs-lookup"><span data-stu-id="ef225-413">Byte[]</span></span> |
| <span data-ttu-id="ef225-414">tinyint</span><span class="sxs-lookup"><span data-stu-id="ef225-414">tinyint</span></span> |<span data-ttu-id="ef225-415">Bajtów</span><span class="sxs-lookup"><span data-stu-id="ef225-415">Byte</span></span> |
| <span data-ttu-id="ef225-416">Unikatowy identyfikator</span><span class="sxs-lookup"><span data-stu-id="ef225-416">uniqueidentifier</span></span> |<span data-ttu-id="ef225-417">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="ef225-417">Guid</span></span> |
| <span data-ttu-id="ef225-418">varbinary</span><span class="sxs-lookup"><span data-stu-id="ef225-418">varbinary</span></span> |<span data-ttu-id="ef225-419">Byte]</span><span class="sxs-lookup"><span data-stu-id="ef225-419">Byte[]</span></span> |
| <span data-ttu-id="ef225-420">varchar</span><span class="sxs-lookup"><span data-stu-id="ef225-420">varchar</span></span> |<span data-ttu-id="ef225-421">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="ef225-421">String, Char[]</span></span> |
| <span data-ttu-id="ef225-422">xml</span><span class="sxs-lookup"><span data-stu-id="ef225-422">xml</span></span> |<span data-ttu-id="ef225-423">XML</span><span class="sxs-lookup"><span data-stu-id="ef225-423">Xml</span></span> |

## <a name="mapping-source-toosink-columns"></a><span data-ttu-id="ef225-424">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="ef225-424">Mapping source toosink columns</span></span>
<span data-ttu-id="ef225-425">toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ef225-425">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="ef225-426">Kopiuj powtarzalne</span><span class="sxs-lookup"><span data-stu-id="ef225-426">Repeatable copy</span></span>
<span data-ttu-id="ef225-427">Podczas kopiowania danych tooSQL bazy danych serwera, działanie kopiowania hello dołącza tabeli ujścia toohello danych domyślnie.</span><span class="sxs-lookup"><span data-stu-id="ef225-427">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="ef225-428">Zamiast tego zobacz tooperform UPSERT [tooSqlSink powtarzalne zapisu](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ef225-428">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="ef225-429">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="ef225-429">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="ef225-430">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="ef225-430">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="ef225-431">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="ef225-431">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="ef225-432">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="ef225-432">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="ef225-433">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="ef225-433">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ef225-434">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="ef225-434">Performance and Tuning</span></span>
<span data-ttu-id="ef225-435">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="ef225-435">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
