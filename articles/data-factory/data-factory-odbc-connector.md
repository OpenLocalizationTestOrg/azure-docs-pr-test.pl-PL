---
title: aaaMove danych z baz danych ODBC | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat sposobu toomove danych ze źródła danych ODBC są przechowywane przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="f917a-103">Przenieś magazyny danych ODBC z danych przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="f917a-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="f917a-104">W tym artykule opisano, jak przechowywać toouse hello działanie kopiowania danych toomove fabryki danych Azure z lokalnymi danymi ODBC.</span><span class="sxs-lookup"><span data-stu-id="f917a-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises ODBC data store.</span></span> <span data-ttu-id="f917a-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="f917a-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="f917a-106">Można skopiować danych z magazynu ODBC danych magazynu tooany obsługiwane ujścia danych.</span><span class="sxs-lookup"><span data-stu-id="f917a-106">You can copy data from an ODBC data store tooany supported sink data store.</span></span> <span data-ttu-id="f917a-107">Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="f917a-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="f917a-108">Fabryka danych aktualnie obsługuje tylko przeniesienie tooother magazyny danych magazynu danych ze źródła danych ODBC, ale nie do przenoszenia danych z magazynu magazynów danych ODBC tooan innych danych.</span><span class="sxs-lookup"><span data-stu-id="f917a-108">Data factory currently supports only moving data from an ODBC data store tooother data stores, but not for moving data from other data stores tooan ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="f917a-109">Włączenie łączności</span><span class="sxs-lookup"><span data-stu-id="f917a-109">Enabling connectivity</span></span>
<span data-ttu-id="f917a-110">Usługi fabryka danych obsługuje połączenia lokalnego tooon ODBC — źródła przy użyciu hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="f917a-110">Data Factory service supports connecting tooon-premises ODBC sources using hello Data Management Gateway.</span></span> <span data-ttu-id="f917a-111">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) toolearn artykuł o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello.</span><span class="sxs-lookup"><span data-stu-id="f917a-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="f917a-112">Użyj magazynu danych ODBC tooan hello bramy tooconnect, nawet jeśli jest obsługiwany w maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="f917a-112">Use hello gateway tooconnect tooan ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="f917a-113">Możesz zainstalować bramę hello na powitania lokalnego tego samego komputera lub maszyny Wirtualnej platformy Azure jako magazynu danych ODBC hello hello.</span><span class="sxs-lookup"><span data-stu-id="f917a-113">You can install hello gateway on hello same on-premises machine or hello Azure VM as hello ODBC data store.</span></span> <span data-ttu-id="f917a-114">Jednak zaleca się instalowania bramy hello na oddzielnych maszyny/Azure IaaS maszyny Wirtualnej rywalizacji tooavoid i w celu zapewnienia lepszej wydajności.</span><span class="sxs-lookup"><span data-stu-id="f917a-114">However, we recommend that you install hello gateway on a separate machine/Azure IaaS VM tooavoid resource contention and for better performance.</span></span> <span data-ttu-id="f917a-115">Po zainstalowaniu bramy hello na osobnym komputerze hello maszyny powinny być możliwe tooaccess hello maszyny z magazynem danych ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="f917a-115">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello ODBC data store.</span></span>

<span data-ttu-id="f917a-116">Oprócz hello brama zarządzania danymi należy również sterownika ODBC hello tooinstall hello magazynu danych na komputerze bramy hello.</span><span class="sxs-lookup"><span data-stu-id="f917a-116">Apart from hello Data Management Gateway, you also need tooinstall hello ODBC driver for hello data store on hello gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="f917a-117">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="f917a-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f917a-118">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="f917a-118">Getting started</span></span>
<span data-ttu-id="f917a-119">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu danych ODBC, za pomocą różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="f917a-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="f917a-120">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="f917a-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="f917a-121">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="f917a-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="f917a-122">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="f917a-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f917a-123">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="f917a-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="f917a-124">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="f917a-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="f917a-125">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="f917a-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="f917a-126">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="f917a-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="f917a-127">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="f917a-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="f917a-128">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="f917a-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="f917a-129">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="f917a-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="f917a-130">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z magazynu danych ODBC, zobacz [przykład JSON: tooAzure obiektu Blob magazynu kopii danych ze źródła danych ODBC](#json-example-copy-data-from-odbc-data-store-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="f917a-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an ODBC data store, see [JSON example: Copy data from ODBC data store tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="f917a-131">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są magazynu danych określonego tooODBC jednostek fabryki danych używanych toodefine:</span><span class="sxs-lookup"><span data-stu-id="f917a-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f917a-132">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="f917a-132">Linked service properties</span></span>
<span data-ttu-id="f917a-133">Hello w poniższej tabeli przedstawiono opis usługi określonego tooODBC połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="f917a-133">hello following table provides description for JSON elements specific tooODBC linked service.</span></span>

| <span data-ttu-id="f917a-134">Właściwość</span><span class="sxs-lookup"><span data-stu-id="f917a-134">Property</span></span> | <span data-ttu-id="f917a-135">Opis</span><span class="sxs-lookup"><span data-stu-id="f917a-135">Description</span></span> | <span data-ttu-id="f917a-136">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f917a-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f917a-137">type</span><span class="sxs-lookup"><span data-stu-id="f917a-137">type</span></span> |<span data-ttu-id="f917a-138">musi mieć ustawioną właściwość type Hello: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="f917a-138">hello type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="f917a-139">Tak</span><span class="sxs-lookup"><span data-stu-id="f917a-139">Yes</span></span> |
| <span data-ttu-id="f917a-140">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="f917a-140">connectionString</span></span> |<span data-ttu-id="f917a-141">poświadczenie zaszyfrowana Hello poświadczeń innych niż dostępu część hello ciąg połączenia i opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="f917a-141">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="f917a-142">Przykłady w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="f917a-142">See examples in hello following sections.</span></span> |<span data-ttu-id="f917a-143">Tak</span><span class="sxs-lookup"><span data-stu-id="f917a-143">Yes</span></span> |
| <span data-ttu-id="f917a-144">poświadczenia</span><span class="sxs-lookup"><span data-stu-id="f917a-144">credential</span></span> |<span data-ttu-id="f917a-145">Hello dostępu do poświadczeń część hello parametrów połączenia określonego w formacie wartość właściwości sterownika.</span><span class="sxs-lookup"><span data-stu-id="f917a-145">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="f917a-146">Przykład: "Uid =<user ID>; Pwd =<password>; RefreshToken =<secret refresh token>; ".</span><span class="sxs-lookup"><span data-stu-id="f917a-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="f917a-147">Nie</span><span class="sxs-lookup"><span data-stu-id="f917a-147">No</span></span> |
| <span data-ttu-id="f917a-148">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="f917a-148">authenticationType</span></span> |<span data-ttu-id="f917a-149">Typ uwierzytelniania używany Magazyn danych ODBC toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="f917a-149">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="f917a-150">Możliwe wartości to: anonimowych, jak i podstawowych.</span><span class="sxs-lookup"><span data-stu-id="f917a-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="f917a-151">Tak</span><span class="sxs-lookup"><span data-stu-id="f917a-151">Yes</span></span> |
| <span data-ttu-id="f917a-152">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="f917a-152">username</span></span> |<span data-ttu-id="f917a-153">Określ nazwę użytkownika, jeśli używasz uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f917a-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="f917a-154">Nie</span><span class="sxs-lookup"><span data-stu-id="f917a-154">No</span></span> |
| <span data-ttu-id="f917a-155">hasło</span><span class="sxs-lookup"><span data-stu-id="f917a-155">password</span></span> |<span data-ttu-id="f917a-156">Określ hasło dla konta użytkownika hello określone dla hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f917a-156">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="f917a-157">Nie</span><span class="sxs-lookup"><span data-stu-id="f917a-157">No</span></span> |
| <span data-ttu-id="f917a-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f917a-158">gatewayName</span></span> |<span data-ttu-id="f917a-159">Nazwa bramy hello hello usługi fabryka danych należy używać magazynu danych ODBC toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="f917a-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="f917a-160">Tak</span><span class="sxs-lookup"><span data-stu-id="f917a-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="f917a-161">Przy użyciu uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="f917a-161">Using Basic authentication</span></span>

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
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="f917a-162">Przy użyciu poświadczeń zaszyfrowanych przy użyciu uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="f917a-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="f917a-163">Można szyfrować poświadczeń hello przy użyciu hello [AzureRMDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/mt603802.aspx) polecenia cmdlet (w wersji 1.0 programu Azure PowerShell) lub [AzureDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 lub starszej wersji hello Program Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="f917a-163">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="f917a-164">Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="f917a-164">Using Anonymous authentication</span></span>

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


## <a name="dataset-properties"></a><span data-ttu-id="f917a-165">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="f917a-165">Dataset properties</span></span>
<span data-ttu-id="f917a-166">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="f917a-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f917a-167">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="f917a-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="f917a-168">Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="f917a-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="f917a-169">Witaj typeProperties sekcja dla zestawu danych typu **RelationalTable** (w tym zestawie danych ODBC) ma następujące właściwości hello</span><span class="sxs-lookup"><span data-stu-id="f917a-169">hello typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has hello following properties</span></span>

| <span data-ttu-id="f917a-170">Właściwość</span><span class="sxs-lookup"><span data-stu-id="f917a-170">Property</span></span> | <span data-ttu-id="f917a-171">Opis</span><span class="sxs-lookup"><span data-stu-id="f917a-171">Description</span></span> | <span data-ttu-id="f917a-172">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f917a-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f917a-173">tableName</span><span class="sxs-lookup"><span data-stu-id="f917a-173">tableName</span></span> |<span data-ttu-id="f917a-174">Nazwa tabeli hello w magazynie danych ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="f917a-174">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="f917a-175">Tak</span><span class="sxs-lookup"><span data-stu-id="f917a-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="f917a-176">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="f917a-176">Copy activity properties</span></span>
<span data-ttu-id="f917a-177">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="f917a-177">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f917a-178">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="f917a-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="f917a-179">Właściwości dostępne w hello **typeProperties** sekcji aktywności hello na powitania drugiej zależą od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="f917a-179">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="f917a-180">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="f917a-180">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="f917a-181">W przypadku działania kopiowania, gdy źródłem jest typu **RelationalSource** (która obejmuje ODBC), hello następujące właściwości są dostępne w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="f917a-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="f917a-182">Właściwość</span><span class="sxs-lookup"><span data-stu-id="f917a-182">Property</span></span> | <span data-ttu-id="f917a-183">Opis</span><span class="sxs-lookup"><span data-stu-id="f917a-183">Description</span></span> | <span data-ttu-id="f917a-184">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="f917a-184">Allowed values</span></span> | <span data-ttu-id="f917a-185">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f917a-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f917a-186">query</span><span class="sxs-lookup"><span data-stu-id="f917a-186">query</span></span> |<span data-ttu-id="f917a-187">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="f917a-187">Use hello custom query tooread data.</span></span> |<span data-ttu-id="f917a-188">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="f917a-188">SQL query string.</span></span> <span data-ttu-id="f917a-189">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="f917a-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="f917a-190">Tak</span><span class="sxs-lookup"><span data-stu-id="f917a-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a><span data-ttu-id="f917a-191">Przykład JSON: tooAzure obiektu Blob magazynu kopii danych ze źródła danych ODBC</span><span class="sxs-lookup"><span data-stu-id="f917a-191">JSON example: Copy data from ODBC data store tooAzure Blob</span></span>
<span data-ttu-id="f917a-192">W poniższym przykładzie przedstawiono definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f917a-192">This example provides JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f917a-193">Pokazuje, jak dane toocopy z ODBC źródła tooan magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f917a-193">It shows how toocopy data from an ODBC source tooan Azure Blob Storage.</span></span> <span data-ttu-id="f917a-194">Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="f917a-194">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="f917a-195">przykład Witaj ma hello następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="f917a-195">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="f917a-196">Połączonej usługi typu [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f917a-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="f917a-197">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f917a-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f917a-198">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f917a-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="f917a-199">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f917a-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f917a-200">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f917a-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f917a-201">przykład Witaj kopiuje dane z wyniku kwerendy w obiekcie blob tooa magazynu danych ODBC, co godzinę.</span><span class="sxs-lookup"><span data-stu-id="f917a-201">hello sample copies data from a query result in an ODBC data store tooa blob every hour.</span></span> <span data-ttu-id="f917a-202">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="f917a-202">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="f917a-203">Pierwszym krokiem należy skonfigurować bramę zarządzania danymi hello.</span><span class="sxs-lookup"><span data-stu-id="f917a-203">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="f917a-204">Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="f917a-204">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="f917a-205">**ODBC połączona usługa** w tym przykładzie używa hello uwierzytelnianie podstawowe.</span><span class="sxs-lookup"><span data-stu-id="f917a-205">**ODBC linked service** This example uses hello Basic authentication.</span></span> <span data-ttu-id="f917a-206">Zobacz [ODBC połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.</span><span class="sxs-lookup"><span data-stu-id="f917a-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="f917a-207">**Połączona usługa Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="f917a-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="f917a-208">**Wejściowy zestaw danych ODBC**</span><span class="sxs-lookup"><span data-stu-id="f917a-208">**ODBC input dataset**</span></span>

<span data-ttu-id="f917a-209">przykład Witaj przyjęto założenie, utworzono tabelę "MyTable" w bazie danych ODBC i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="f917a-209">hello sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="f917a-210">Ustawienie "external": "prawda" informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="f917a-210">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="f917a-211">**Azure Blob wyjściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="f917a-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="f917a-212">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="f917a-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f917a-213">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="f917a-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="f917a-214">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="f917a-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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


<span data-ttu-id="f917a-215">**Działanie kopiowania w potoku ze źródłem ODBC (RelationalSource) i ujście obiektów Blob (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="f917a-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="f917a-216">potok Hello zawiera działanie kopiowania który jest skonfigurowany toouse te zestawy danych wejściowych i wyjściowych i toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="f917a-216">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="f917a-217">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f917a-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="f917a-218">Zapytanie SQL Hello określone dla hello **zapytania** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="f917a-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="f917a-219">Mapowanie typu dla ODBC</span><span class="sxs-lookup"><span data-stu-id="f917a-219">Type mapping for ODBC</span></span>
<span data-ttu-id="f917a-220">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z powitania po rozwinięcie:</span><span class="sxs-lookup"><span data-stu-id="f917a-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="f917a-221">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="f917a-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="f917a-222">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="f917a-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="f917a-223">Podczas przenoszenia danych z baz danych ODBC, typy danych ODBC są typami too.NET zamapowane, jak wspomniano w hello [mapowanie typu danych ODBC](https://msdn.microsoft.com/library/cc668763.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="f917a-223">When moving data from ODBC data stores, ODBC data types are mapped too.NET types as mentioned in hello [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="f917a-224">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="f917a-224">Map source toosink columns</span></span>
<span data-ttu-id="f917a-225">toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f917a-225">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="f917a-226">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="f917a-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="f917a-227">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="f917a-227">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="f917a-228">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="f917a-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="f917a-229">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="f917a-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="f917a-230">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="f917a-230">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="f917a-231">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="f917a-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="f917a-232">GE historyk magazynu</span><span class="sxs-lookup"><span data-stu-id="f917a-232">GE Historian store</span></span>
<span data-ttu-id="f917a-233">Utwórz ODBC połączone usługi toolink [historyk Proficy GE (teraz GE historyk)](http://www.geautomation.com/products/proficy-historian) fabryki danych Azure tooan magazynu danych, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f917a-233">You create an ODBC linked service toolink a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store tooan Azure data factory as shown in hello following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="f917a-234">Instalowanie bramy zarządzania danymi na maszynie lokalnej i zarejestruj bramę hello hello Portal.</span><span class="sxs-lookup"><span data-stu-id="f917a-234">Install Data Management Gateway on an on-premises machine and register hello gateway with hello portal.</span></span> <span data-ttu-id="f917a-235">bramy Hello zainstalowanej na komputerze lokalnym używa sterownika ODBC hello GE historyk tooconnect toohello historyk GE magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="f917a-235">hello gateway installed on your on-premises computer uses hello ODBC driver for GE Historian tooconnect toohello GE Historian data store.</span></span> <span data-ttu-id="f917a-236">W związku z tym należy zainstalować sterownik hello, jeśli nie jest już zainstalowany na komputerze bramy hello.</span><span class="sxs-lookup"><span data-stu-id="f917a-236">Therefore, install hello driver if it is not already installed on hello gateway machine.</span></span> <span data-ttu-id="f917a-237">Zobacz [włączenie łączności](#enabling-connectivity) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="f917a-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="f917a-238">Przed użyciem hello historyk GE przechowywania w rozwiązaniu fabryki danych, należy sprawdzić, czy brama hello łączy toohello magazynu danych przy użyciu instrukcji w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="f917a-238">Before you use hello GE Historian store in a Data Factory solution, verify whether hello gateway can connect toohello data store using instructions in hello next section.</span></span>

<span data-ttu-id="f917a-239">Przeczytaj artykuł powitania od początku hello szczegółowe omówienie używania danych ODBC są przechowywane jako źródło danych magazynów w operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="f917a-239">Read hello article from hello beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="f917a-240">Rozwiązywanie problemów z połączeniem</span><span class="sxs-lookup"><span data-stu-id="f917a-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="f917a-241">problemy z połączeniem tootroubleshoot, użyj hello **diagnostyki** karcie **Menedżera konfiguracji bramy zarządzania danymi**.</span><span class="sxs-lookup"><span data-stu-id="f917a-241">tootroubleshoot connection issues, use hello **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="f917a-242">Uruchom **Menedżera konfiguracji bramy zarządzania danymi**.</span><span class="sxs-lookup"><span data-stu-id="f917a-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="f917a-243">Możesz uruchomić "C:\Program Files\Microsoft danych zarządzania Gateway\1.0\Shared\ConfigManager.exe" bezpośrednio (lub) wyszukiwania dla **bramy** toofind łącze zbyt**brama zarządzania danymi firmy Microsoft** Aplikacja, jak pokazano w powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="f917a-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** toofind a link too**Microsoft Data Management Gateway** application as shown in hello following image.</span></span>

    ![Brama wyszukiwania](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="f917a-245">Przełącz toohello **diagnostyki** kartę.</span><span class="sxs-lookup"><span data-stu-id="f917a-245">Switch toohello **Diagnostics** tab.</span></span>

    ![Diagnostyki bramy](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="f917a-247">Wybierz hello **typu** danych magazynu (połączonej usługi).</span><span class="sxs-lookup"><span data-stu-id="f917a-247">Select hello **type** of data store (linked service).</span></span>
4. <span data-ttu-id="f917a-248">Określ **uwierzytelniania** , a następnie wprowadź **poświadczenia** (lub) wprowadź **ciąg połączenia** to magazyn danych toohello tooconnect używane.</span><span class="sxs-lookup"><span data-stu-id="f917a-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used tooconnect toohello data store.</span></span>
5. <span data-ttu-id="f917a-249">Kliknij przycisk **połączenie testowe** magazynu danych toohello tootest hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="f917a-249">Click **Test connection** tootest hello connection toohello data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f917a-250">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="f917a-250">Performance and Tuning</span></span>
<span data-ttu-id="f917a-251">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="f917a-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
