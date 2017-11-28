---
title: Przenoszenie danych z baz danych ODBC | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat sposobu przenoszenia danych z baz danych ODBC przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 269d9802ca4a6a16dbf9021929fe21104cb431f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="8d461-103">Przenieś magazyny danych ODBC z danych przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="8d461-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="8d461-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przenoszenia danych z lokalnego magazynu danych ODBC.</span><span class="sxs-lookup"><span data-stu-id="8d461-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises ODBC data store.</span></span> <span data-ttu-id="8d461-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="8d461-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="8d461-106">Wszystkie obsługiwanych ujścia magazynu danych można skopiować danych z magazynu danych ODBC.</span><span class="sxs-lookup"><span data-stu-id="8d461-106">You can copy data from an ODBC data store to any supported sink data store.</span></span> <span data-ttu-id="8d461-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="8d461-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="8d461-108">Fabryka danych aktualnie obsługuje tylko dane przenoszenie, z magazynu danych ODBC do innych magazynów danych, ale nie do przenoszenia danych z innych magazynów danych z magazynem danych ODBC.</span><span class="sxs-lookup"><span data-stu-id="8d461-108">Data factory currently supports only moving data from an ODBC data store to other data stores, but not for moving data from other data stores to an ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="8d461-109">Włączenie łączności</span><span class="sxs-lookup"><span data-stu-id="8d461-109">Enabling connectivity</span></span>
<span data-ttu-id="8d461-110">Usługi fabryka danych obsługuje połączenia ze źródłami ODBC lokalnymi przy użyciu bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="8d461-110">Data Factory service supports connecting to on-premises ODBC sources using the Data Management Gateway.</span></span> <span data-ttu-id="8d461-111">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby dowiedzieć się więcej na temat bramy zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy.</span><span class="sxs-lookup"><span data-stu-id="8d461-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="8d461-112">Użyj bramy w celu połączenia z magazynem danych ODBC, nawet jeśli jest obsługiwany w maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="8d461-112">Use the gateway to connect to an ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="8d461-113">Bramę można zainstalować na tym samym komputerze lokalnym lub maszynie Wirtualnej platformy Azure do przechowywania danych ODBC.</span><span class="sxs-lookup"><span data-stu-id="8d461-113">You can install the gateway on the same on-premises machine or the Azure VM as the ODBC data store.</span></span> <span data-ttu-id="8d461-114">Jednak zaleca się zainstalowanie bramy na oddzielnym komputerze/Azure IaaS maszyny Wirtualnej, aby uniknąć rywalizacji i lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="8d461-114">However, we recommend that you install the gateway on a separate machine/Azure IaaS VM to avoid resource contention and for better performance.</span></span> <span data-ttu-id="8d461-115">Po zainstalowaniu bramy na osobnym komputerze maszynie powinno być możliwe dostęp do komputera z magazynem danych ODBC.</span><span class="sxs-lookup"><span data-stu-id="8d461-115">When you install the gateway on a separate machine, the machine should be able to access the machine with the ODBC data store.</span></span>

<span data-ttu-id="8d461-116">Oprócz brama zarządzania danymi należy również zainstalować sterownika ODBC dla magazynu danych na komputerze bramy.</span><span class="sxs-lookup"><span data-stu-id="8d461-116">Apart from the Data Management Gateway, you also need to install the ODBC driver for the data store on the gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="8d461-117">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="8d461-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8d461-118">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="8d461-118">Getting started</span></span>
<span data-ttu-id="8d461-119">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu danych ODBC, za pomocą różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="8d461-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="8d461-120">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="8d461-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="8d461-121">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="8d461-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="8d461-122">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="8d461-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="8d461-123">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="8d461-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="8d461-124">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="8d461-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="8d461-125">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="8d461-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="8d461-126">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="8d461-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="8d461-127">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="8d461-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="8d461-128">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="8d461-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="8d461-129">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="8d461-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="8d461-130">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane do kopiowania danych z magazynu danych ODBC, zobacz [przykład JSON: magazynu kopii danych ze źródła danych ODBC do obiektów Blob platformy Azure](#json-example-copy-data-from-odbc-data-store-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="8d461-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an ODBC data store, see [JSON example: Copy data from ODBC data store to Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="8d461-131">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do magazynu danych ODBC:</span><span class="sxs-lookup"><span data-stu-id="8d461-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to ODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="8d461-132">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="8d461-132">Linked service properties</span></span>
<span data-ttu-id="8d461-133">Poniższa tabela zawiera opis specyficzne dla ODBC elementy JSON połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="8d461-133">The following table provides description for JSON elements specific to ODBC linked service.</span></span>

| <span data-ttu-id="8d461-134">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8d461-134">Property</span></span> | <span data-ttu-id="8d461-135">Opis</span><span class="sxs-lookup"><span data-stu-id="8d461-135">Description</span></span> | <span data-ttu-id="8d461-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8d461-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d461-137">type</span><span class="sxs-lookup"><span data-stu-id="8d461-137">type</span></span> |<span data-ttu-id="8d461-138">Właściwość type musi mieć ustawioną: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="8d461-138">The type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="8d461-139">Tak</span><span class="sxs-lookup"><span data-stu-id="8d461-139">Yes</span></span> |
| <span data-ttu-id="8d461-140">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="8d461-140">connectionString</span></span> |<span data-ttu-id="8d461-141">Poświadczenie dostępu z systemem innym niż część ciąg połączenia i opcjonalnie zaszyfrowane poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="8d461-141">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="8d461-142">Przykłady w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="8d461-142">See examples in the following sections.</span></span> |<span data-ttu-id="8d461-143">Tak</span><span class="sxs-lookup"><span data-stu-id="8d461-143">Yes</span></span> |
| <span data-ttu-id="8d461-144">poświadczenia</span><span class="sxs-lookup"><span data-stu-id="8d461-144">credential</span></span> |<span data-ttu-id="8d461-145">Dostęp do poświadczeń część ciągu połączenia określonego w formacie wartości właściwości sterownika.</span><span class="sxs-lookup"><span data-stu-id="8d461-145">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="8d461-146">Przykład: "Uid =<user ID>; Pwd =<password>; RefreshToken =<secret refresh token>; ".</span><span class="sxs-lookup"><span data-stu-id="8d461-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="8d461-147">Nie</span><span class="sxs-lookup"><span data-stu-id="8d461-147">No</span></span> |
| <span data-ttu-id="8d461-148">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="8d461-148">authenticationType</span></span> |<span data-ttu-id="8d461-149">Typ uwierzytelniania używany do łączenia się z magazynem danych ODBC.</span><span class="sxs-lookup"><span data-stu-id="8d461-149">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="8d461-150">Możliwe wartości to: anonimowych, jak i podstawowych.</span><span class="sxs-lookup"><span data-stu-id="8d461-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="8d461-151">Tak</span><span class="sxs-lookup"><span data-stu-id="8d461-151">Yes</span></span> |
| <span data-ttu-id="8d461-152">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="8d461-152">username</span></span> |<span data-ttu-id="8d461-153">Określ nazwę użytkownika, jeśli używasz uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="8d461-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="8d461-154">Nie</span><span class="sxs-lookup"><span data-stu-id="8d461-154">No</span></span> |
| <span data-ttu-id="8d461-155">hasło</span><span class="sxs-lookup"><span data-stu-id="8d461-155">password</span></span> |<span data-ttu-id="8d461-156">Określ hasło dla konta użytkownika, określone nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8d461-156">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="8d461-157">Nie</span><span class="sxs-lookup"><span data-stu-id="8d461-157">No</span></span> |
| <span data-ttu-id="8d461-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8d461-158">gatewayName</span></span> |<span data-ttu-id="8d461-159">Nazwa bramy, która powinna być używana przez usługi fabryka danych do połączenia z magazynem danych ODBC.</span><span class="sxs-lookup"><span data-stu-id="8d461-159">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="8d461-160">Tak</span><span class="sxs-lookup"><span data-stu-id="8d461-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="8d461-161">Przy użyciu uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="8d461-161">Using Basic authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="8d461-162">Przy użyciu poświadczeń zaszyfrowanych przy użyciu uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="8d461-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="8d461-163">Można szyfrować poświadczeń przy użyciu [AzureRMDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/mt603802.aspx) polecenia cmdlet (w wersji 1.0 programu Azure PowerShell) lub [AzureDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 lub starszej wersji programu Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="8d461-163">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="8d461-164">Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="8d461-164">Using Anonymous authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a><span data-ttu-id="8d461-165">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="8d461-165">Dataset properties</span></span>
<span data-ttu-id="8d461-166">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="8d461-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8d461-167">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="8d461-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="8d461-168">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="8d461-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="8d461-169">TypeProperties sekcja dla zestawu danych typu **RelationalTable** (w tym zestawie danych ODBC) ma następujące właściwości</span><span class="sxs-lookup"><span data-stu-id="8d461-169">The typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has the following properties</span></span>

| <span data-ttu-id="8d461-170">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8d461-170">Property</span></span> | <span data-ttu-id="8d461-171">Opis</span><span class="sxs-lookup"><span data-stu-id="8d461-171">Description</span></span> | <span data-ttu-id="8d461-172">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8d461-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d461-173">tableName</span><span class="sxs-lookup"><span data-stu-id="8d461-173">tableName</span></span> |<span data-ttu-id="8d461-174">Nazwa tabeli w magazynie danych ODBC.</span><span class="sxs-lookup"><span data-stu-id="8d461-174">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="8d461-175">Tak</span><span class="sxs-lookup"><span data-stu-id="8d461-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="8d461-176">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="8d461-176">Copy activity properties</span></span>
<span data-ttu-id="8d461-177">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="8d461-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8d461-178">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="8d461-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="8d461-179">Właściwości dostępne w **typeProperties** sekcji działania z drugiej strony zależą od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="8d461-179">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="8d461-180">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="8d461-180">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="8d461-181">W przypadku działania kopiowania, gdy źródłem jest typu **RelationalSource** (która obejmuje ODBC), w sekcji typeProperties dostępne są następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="8d461-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="8d461-182">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8d461-182">Property</span></span> | <span data-ttu-id="8d461-183">Opis</span><span class="sxs-lookup"><span data-stu-id="8d461-183">Description</span></span> | <span data-ttu-id="8d461-184">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="8d461-184">Allowed values</span></span> | <span data-ttu-id="8d461-185">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8d461-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8d461-186">query</span><span class="sxs-lookup"><span data-stu-id="8d461-186">query</span></span> |<span data-ttu-id="8d461-187">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="8d461-187">Use the custom query to read data.</span></span> |<span data-ttu-id="8d461-188">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="8d461-188">SQL query string.</span></span> <span data-ttu-id="8d461-189">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="8d461-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="8d461-190">Tak</span><span class="sxs-lookup"><span data-stu-id="8d461-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-to-azure-blob"></a><span data-ttu-id="8d461-191">Przykład JSON: magazynu kopii danych ze źródła danych ODBC do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8d461-191">JSON example: Copy data from ODBC data store to Azure Blob</span></span>
<span data-ttu-id="8d461-192">W poniższym przykładzie przedstawiono definicje JSON, których można utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8d461-192">This example provides JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8d461-193">Widoczny jest sposób kopiowania danych ze źródła danych ODBC do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="8d461-193">It shows how to copy data from an ODBC source to an Azure Blob Storage.</span></span> <span data-ttu-id="8d461-194">Jednak można skopiować danych do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="8d461-194">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="8d461-195">Przykład zawiera następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="8d461-195">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="8d461-196">Połączonej usługi typu [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8d461-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="8d461-197">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8d461-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8d461-198">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8d461-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="8d461-199">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8d461-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="8d461-200">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8d461-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="8d461-201">Przykład kopiuje dane z wyniku kwerendy w magazynie danych ODBC do obiektu blob co godzinę.</span><span class="sxs-lookup"><span data-stu-id="8d461-201">The sample copies data from a query result in an ODBC data store to a blob every hour.</span></span> <span data-ttu-id="8d461-202">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="8d461-202">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="8d461-203">Pierwszym krokiem należy skonfigurować bramę zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="8d461-203">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="8d461-204">Instrukcje znajdują się w [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="8d461-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="8d461-205">**ODBC połączona usługa** w tym przykładzie użyto uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="8d461-205">**ODBC linked service** This example uses the Basic authentication.</span></span> <span data-ttu-id="8d461-206">Zobacz [ODBC połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.</span><span class="sxs-lookup"><span data-stu-id="8d461-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="8d461-207">**Połączona usługa Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="8d461-207">**Azure Storage linked service**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
    }
}
```

<span data-ttu-id="8d461-208">**Wejściowy zestaw danych ODBC**</span><span class="sxs-lookup"><span data-stu-id="8d461-208">**ODBC input dataset**</span></span>

<span data-ttu-id="8d461-209">Przykładzie przyjęto założenie, utworzono tabelę "MyTable" w bazie danych ODBC i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="8d461-209">The sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="8d461-210">Ustawienie "external": "prawda" informuje usługi fabryka danych czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="8d461-210">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="8d461-211">**Azure Blob wyjściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="8d461-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="8d461-212">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="8d461-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8d461-213">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="8d461-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="8d461-214">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="8d461-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


<span data-ttu-id="8d461-215">**Działanie kopiowania w potoku ze źródłem ODBC (RelationalSource) i ujście obiektów Blob (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="8d461-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="8d461-216">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania tych zestawów danych wejściowych i wyjściowych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="8d461-216">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="8d461-217">W definicji JSON potoku **źródła** ustawiono typ **RelationalSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="8d461-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="8d461-218">Określony dla zapytania SQL **zapytania** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="8d461-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="8d461-219">Mapowanie typu dla ODBC</span><span class="sxs-lookup"><span data-stu-id="8d461-219">Type mapping for ODBC</span></span>
<span data-ttu-id="8d461-220">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, automatyczne konwersje z typów źródła do zbiornika typy z następujących rozwinięcie wykonuje działania kopiowania:</span><span class="sxs-lookup"><span data-stu-id="8d461-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="8d461-221">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="8d461-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="8d461-222">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="8d461-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="8d461-223">Podczas przenoszenia danych z baz danych ODBC, typy danych ODBC są mapowane do typów .NET, jak wspomniano w [mapowanie typu danych ODBC](https://msdn.microsoft.com/library/cc668763.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="8d461-223">When moving data from ODBC data stores, ODBC data types are mapped to .NET types as mentioned in the [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="8d461-224">Obiekt sink kolumn mapy źródła</span><span class="sxs-lookup"><span data-stu-id="8d461-224">Map source to sink columns</span></span>
<span data-ttu-id="8d461-225">Aby uzyskać informacje dotyczące mapowania kolumn w zestawie źródła danych do kolumn w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="8d461-225">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="8d461-226">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="8d461-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="8d461-227">Podczas kopiowania danych z danych relacyjnych przechowuje, należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="8d461-227">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="8d461-228">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="8d461-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="8d461-229">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="8d461-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="8d461-230">Podczas wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że te same dane jest do odczytu niezależnie od tego, ile razy wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="8d461-230">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="8d461-231">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="8d461-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="8d461-232">GE historyk magazynu</span><span class="sxs-lookup"><span data-stu-id="8d461-232">GE Historian store</span></span>
<span data-ttu-id="8d461-233">Tworzenie usługi ODBC połączone, aby połączyć [historyk Proficy GE (teraz GE historyk)](http://www.geautomation.com/products/proficy-historian) magazynu danych do fabryki danych Azure, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="8d461-233">You create an ODBC linked service to link a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of the GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="8d461-234">Instalowanie bramy zarządzania danymi na maszynie lokalnej i zarejestruj bramę przy użyciu portalu.</span><span class="sxs-lookup"><span data-stu-id="8d461-234">Install Data Management Gateway on an on-premises machine and register the gateway with the portal.</span></span> <span data-ttu-id="8d461-235">Przy użyciu sterownika ODBC dla historyk GE brama zainstalowanej na komputerze lokalnym do nawiązania połączenia z magazynem danych historyk GE.</span><span class="sxs-lookup"><span data-stu-id="8d461-235">The gateway installed on your on-premises computer uses the ODBC driver for GE Historian to connect to the GE Historian data store.</span></span> <span data-ttu-id="8d461-236">W związku z tym należy zainstalować sterownik, jeśli nie jest już zainstalowany na komputerze bramy.</span><span class="sxs-lookup"><span data-stu-id="8d461-236">Therefore, install the driver if it is not already installed on the gateway machine.</span></span> <span data-ttu-id="8d461-237">Zobacz [włączenie łączności](#enabling-connectivity) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="8d461-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="8d461-238">Przed użyciem magazynu historyk GE w rozwiązaniu fabryki danych, należy sprawdzić, czy brama łączy się magazynu danych przy użyciu instrukcji w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="8d461-238">Before you use the GE Historian store in a Data Factory solution, verify whether the gateway can connect to the data store using instructions in the next section.</span></span>

<span data-ttu-id="8d461-239">Przeczytaj artykuł od samego początku, aby uzyskać szczegółowy przegląd przy użyciu danych ODBC są przechowywane jako źródło danych magazynów w operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="8d461-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="8d461-240">Rozwiązywanie problemów z połączeniem</span><span class="sxs-lookup"><span data-stu-id="8d461-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="8d461-241">Aby rozwiązać problemy z połączeniem, użyj **diagnostyki** karcie **Menedżera konfiguracji bramy zarządzania danymi**.</span><span class="sxs-lookup"><span data-stu-id="8d461-241">To troubleshoot connection issues, use the **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="8d461-242">Uruchom **Menedżera konfiguracji bramy zarządzania danymi**.</span><span class="sxs-lookup"><span data-stu-id="8d461-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="8d461-243">Możesz uruchomić "C:\Program Files\Microsoft danych zarządzania Gateway\1.0\Shared\ConfigManager.exe" bezpośrednio (lub) wyszukiwania dla **bramy** można znaleźć link do **brama zarządzania danymi firmy Microsoft** aplikacji, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="8d461-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** to find a link to **Microsoft Data Management Gateway** application as shown in the following image.</span></span>

    ![Brama wyszukiwania](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="8d461-245">Przełącz się do **diagnostyki** kartę.</span><span class="sxs-lookup"><span data-stu-id="8d461-245">Switch to the **Diagnostics** tab.</span></span>

    ![Diagnostyki bramy](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="8d461-247">Wybierz **typu** danych magazynu (połączonej usługi).</span><span class="sxs-lookup"><span data-stu-id="8d461-247">Select the **type** of data store (linked service).</span></span>
4. <span data-ttu-id="8d461-248">Określ **uwierzytelniania** , a następnie wprowadź **poświadczenia** (lub) wprowadź **ciąg połączenia** używany do nawiązania połączenia z magazynem danych.</span><span class="sxs-lookup"><span data-stu-id="8d461-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used to connect to the data store.</span></span>
5. <span data-ttu-id="8d461-249">Kliknij przycisk **połączenie testowe** do testowania połączenia z magazynem danych.</span><span class="sxs-lookup"><span data-stu-id="8d461-249">Click **Test connection** to test the connection to the data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8d461-250">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="8d461-250">Performance and Tuning</span></span>
<span data-ttu-id="8d461-251">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="8d461-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
