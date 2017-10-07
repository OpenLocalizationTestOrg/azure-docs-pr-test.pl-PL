---
title: "aaaMove danych z lokalnego systemu plików HDFS | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toomove danych z lokalnego systemu plików HDFS przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="a6ef1-103">Przenoszenia danych z lokalnego systemu plików HDFS przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="a6ef1-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="a6ef1-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalnego systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises HDFS.</span></span> <span data-ttu-id="a6ef1-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="a6ef1-106">Można skopiować danych z magazynu danych zbiornika tooany obsługiwany system plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-106">You can copy data from HDFS tooany supported sink data store.</span></span> <span data-ttu-id="a6ef1-107">Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a6ef1-108">Fabryka danych aktualnie obsługuje tylko przenoszenia danych z lokalnego systemu plików HDFS tooother następującą liczbę magazynów danych, ale nie przenoszenia danych z innych danych tooan magazyny lokalny system plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-108">Data factory currently supports only moving data from an on-premises HDFS tooother data stores, but not for moving data from other data stores tooan on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="a6ef1-109">Aktywność kopiowania nie powoduje usunięcia pliku źródłowego hello po pomyślnie skopiowane toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="a6ef1-110">Jeśli potrzebujesz pliku źródłowego hello toodelete po pomyślnym kopiowania, Utwórz plik hello toodelete działań niestandardowych i użyj hello działania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="a6ef1-111">Włączenie łączności</span><span class="sxs-lookup"><span data-stu-id="a6ef1-111">Enabling connectivity</span></span>
<span data-ttu-id="a6ef1-112">Usługi fabryka danych obsługuje łączenia HDFS tooon lokalnych przy użyciu hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-112">Data Factory service supports connecting tooon-premises HDFS using hello Data Management Gateway.</span></span> <span data-ttu-id="a6ef1-113">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) toolearn artykuł o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="a6ef1-114">Użyj hello bramy tooconnect tooHDFS nawet wtedy, gdy jest ona hostowana w maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-114">Use hello gateway tooconnect tooHDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="a6ef1-115">Marka hello się zbyt dostęp brama zarządzania danymi**wszystkie** hello [nazwa węzła serwera]: [nazwa węzła portu] i [serwery węzła danych]: [port węzeł danych] hello klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-115">Make sure hello Data Management Gateway can access too**ALL** hello [name node server]:[name node port] and [data node servers]:[data node port] of hello Hadoop cluster.</span></span> <span data-ttu-id="a6ef1-116">Domyślne [nazwa węzła port] jest 50070, a domyślna [port węzeł danych] jest 50075.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="a6ef1-117">Podczas instalowania bramy na powitania sam lokalnymi maszyny lub hello Azure VM hello systemu plików HDFS, zalecamy zainstalowanie bramy hello na oddzielnych maszyny/Azure IaaS maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-117">While you can install gateway on hello same on-premises machine or hello Azure VM as hello HDFS, we recommend that you install hello gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="a6ef1-118">Wystąpienia bramy na osobnym komputerze ogranicza rywalizację zasobów, poprawia wydajność.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="a6ef1-119">Po zainstalowaniu bramy hello na osobnym komputerze hello maszyny powinny być stanie tooaccess hello maszyny z hello systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-119">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a6ef1-120">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="a6ef1-120">Getting started</span></span>
<span data-ttu-id="a6ef1-121">Można utworzyć potok z działania kopiowania, który przenosi dane ze źródła systemu plików HDFS przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="a6ef1-122">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="a6ef1-123">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="a6ef1-124">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a6ef1-125">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="a6ef1-126">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="a6ef1-127">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="a6ef1-128">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="a6ef1-129">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="a6ef1-130">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="a6ef1-131">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="a6ef1-132">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z magazynu danych systemu plików HDFS, zobacz [przykład JSON: kopiowanie danych z lokalnego systemu plików HDFS tooAzure obiektu Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="a6ef1-133">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooHDFS:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooHDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a6ef1-134">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="a6ef1-134">Linked service properties</span></span>
<span data-ttu-id="a6ef1-135">Połączona usługa łączy fabryki danych tooa magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-135">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="a6ef1-136">Tworzenie połączonej usługi typu **Hdfs** toolink lokalnego systemu plików HDFS tooyour usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-136">You create a linked service of type **Hdfs** toolink an on-premises HDFS tooyour data factory.</span></span> <span data-ttu-id="a6ef1-137">Hello w poniższej tabeli przedstawiono opis usługi określonego tooHDFS połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-137">hello following table provides description for JSON elements specific tooHDFS linked service.</span></span>

| <span data-ttu-id="a6ef1-138">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a6ef1-138">Property</span></span> | <span data-ttu-id="a6ef1-139">Opis</span><span class="sxs-lookup"><span data-stu-id="a6ef1-139">Description</span></span> | <span data-ttu-id="a6ef1-140">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a6ef1-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6ef1-141">type</span><span class="sxs-lookup"><span data-stu-id="a6ef1-141">type</span></span> |<span data-ttu-id="a6ef1-142">musi mieć ustawioną właściwość type Hello: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="a6ef1-142">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="a6ef1-143">Tak</span><span class="sxs-lookup"><span data-stu-id="a6ef1-143">Yes</span></span> |
| <span data-ttu-id="a6ef1-144">Url</span><span class="sxs-lookup"><span data-stu-id="a6ef1-144">Url</span></span> |<span data-ttu-id="a6ef1-145">Adres URL toohello systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="a6ef1-145">URL toohello HDFS</span></span> |<span data-ttu-id="a6ef1-146">Tak</span><span class="sxs-lookup"><span data-stu-id="a6ef1-146">Yes</span></span> |
| <span data-ttu-id="a6ef1-147">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="a6ef1-147">authenticationType</span></span> |<span data-ttu-id="a6ef1-148">Anonimowe lub Windows.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="a6ef1-149">toouse **uwierzytelnianie Kerberos** łącznika systemu plików HDFS, można znaleźć zbyt[w tej sekcji](#use-kerberos-authentication-for-hdfs-connector) tooset się w lokalnym środowisku odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-149">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="a6ef1-150">Tak</span><span class="sxs-lookup"><span data-stu-id="a6ef1-150">Yes</span></span> |
| <span data-ttu-id="a6ef1-151">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="a6ef1-151">userName</span></span> |<span data-ttu-id="a6ef1-152">Uwierzytelnianie nazwy użytkownika dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-152">Username for Windows authentication.</span></span> |<span data-ttu-id="a6ef1-153">Tak (w przypadku uwierzytelniania systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="a6ef1-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="a6ef1-154">hasło</span><span class="sxs-lookup"><span data-stu-id="a6ef1-154">password</span></span> |<span data-ttu-id="a6ef1-155">Hasło dla uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-155">Password for Windows authentication.</span></span> |<span data-ttu-id="a6ef1-156">Tak (w przypadku uwierzytelniania systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="a6ef1-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="a6ef1-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a6ef1-157">gatewayName</span></span> |<span data-ttu-id="a6ef1-158">Nazwa bramy hello hello usługi fabryka danych należy używać toohello tooconnect systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-158">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="a6ef1-159">Tak</span><span class="sxs-lookup"><span data-stu-id="a6ef1-159">Yes</span></span> |
| <span data-ttu-id="a6ef1-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="a6ef1-160">encryptedCredential</span></span> |<span data-ttu-id="a6ef1-161">[Nowy AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) hello poświadczeń dostępu do danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="a6ef1-162">Nie</span><span class="sxs-lookup"><span data-stu-id="a6ef1-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="a6ef1-163">Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="a6ef1-163">Using Anonymous authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a><span data-ttu-id="a6ef1-164">Przy użyciu uwierzytelniania systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a6ef1-164">Using Windows authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a><span data-ttu-id="a6ef1-165">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="a6ef1-165">Dataset properties</span></span>
<span data-ttu-id="a6ef1-166">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a6ef1-167">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="a6ef1-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a6ef1-168">Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="a6ef1-169">Witaj typeProperties sekcja dla zestawu danych typu **FileShare** (w tym system plików HDFS w zestawie danych) ma następujące właściwości hello</span><span class="sxs-lookup"><span data-stu-id="a6ef1-169">hello typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has hello following properties</span></span>

| <span data-ttu-id="a6ef1-170">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a6ef1-170">Property</span></span> | <span data-ttu-id="a6ef1-171">Opis</span><span class="sxs-lookup"><span data-stu-id="a6ef1-171">Description</span></span> | <span data-ttu-id="a6ef1-172">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a6ef1-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6ef1-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="a6ef1-173">folderPath</span></span> |<span data-ttu-id="a6ef1-174">Ścieżka folderu toohello.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-174">Path toohello folder.</span></span> <span data-ttu-id="a6ef1-175">Przykład:`myfolder`</span><span class="sxs-lookup"><span data-stu-id="a6ef1-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="a6ef1-176">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-176">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="a6ef1-177">Na przykład: folder\subfolder, określ folder\\\\podfolderów i dla d:\samplefolder, określ d:\\\\folder_przykładowy.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="a6ef1-178">Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-178">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="a6ef1-179">Tak</span><span class="sxs-lookup"><span data-stu-id="a6ef1-179">Yes</span></span> |
| <span data-ttu-id="a6ef1-180">fileName</span><span class="sxs-lookup"><span data-stu-id="a6ef1-180">fileName</span></span> |<span data-ttu-id="a6ef1-181">Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-181">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="a6ef1-182">Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-182">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="a6ef1-183">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-183">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="a6ef1-184">Dane. <Guid>.txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="a6ef1-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="a6ef1-185">Nie</span><span class="sxs-lookup"><span data-stu-id="a6ef1-185">No</span></span> |
| <span data-ttu-id="a6ef1-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="a6ef1-186">partitionedBy</span></span> |<span data-ttu-id="a6ef1-187">partitionedBy mogą być używane toospecify folderPath dynamicznych, nazwę pliku dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-187">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="a6ef1-188">Przykład: folderPath sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="a6ef1-189">Nie</span><span class="sxs-lookup"><span data-stu-id="a6ef1-189">No</span></span> |
| <span data-ttu-id="a6ef1-190">Format</span><span class="sxs-lookup"><span data-stu-id="a6ef1-190">format</span></span> | <span data-ttu-id="a6ef1-191">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-191">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="a6ef1-192">Zestaw hello **typu** właściwości w formacie tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-192">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="a6ef1-193">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="a6ef1-194">Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-194">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="a6ef1-195">Nie</span><span class="sxs-lookup"><span data-stu-id="a6ef1-195">No</span></span> |
| <span data-ttu-id="a6ef1-196">Kompresja</span><span class="sxs-lookup"><span data-stu-id="a6ef1-196">compression</span></span> | <span data-ttu-id="a6ef1-197">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-197">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="a6ef1-198">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="a6ef1-199">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="a6ef1-200">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="a6ef1-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="a6ef1-201">Nie</span><span class="sxs-lookup"><span data-stu-id="a6ef1-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="a6ef1-202">Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="a6ef1-203">Za pomocą właściwości partionedBy</span><span class="sxs-lookup"><span data-stu-id="a6ef1-203">Using partionedBy property</span></span>
<span data-ttu-id="a6ef1-204">Jak wspomniano w poprzedniej sekcji hello, można określić folderPath dynamiczne i nazwę pliku dla danych serii czasu z hello **partitionedBy** właściwość [funkcje fabryki danych i zmienne systemu hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="a6ef1-204">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="a6ef1-205">toolearn więcej informacji na temat zestawów danych serii czasu, planowanie i wycinków, zobacz [tworzenie zestawów danych](data-factory-create-datasets.md), [planowanie i wykonanie](data-factory-scheduling-and-execution.md), i [tworzenie potoków](data-factory-create-pipelines.md) artykułów.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-205">toolearn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="a6ef1-206">Przykład 1:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="a6ef1-207">W tym przykładzie {wycinka} zostanie zastąpiony hello wartość zmiennej fabryki danych systemu SliceStart w formacie hello (YYYYMMDDHH) określona.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-207">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="a6ef1-208">Witaj SliceStart odwołuje się czas toostart hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-208">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="a6ef1-209">Witaj folderPath jest różne dla każdego wycinka.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-209">hello folderPath is different for each slice.</span></span> <span data-ttu-id="a6ef1-210">Na przykład: wikidatagateway/wikisampledataout/2014100103 lub wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="a6ef1-211">Przykład 2:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-211">Sample 2:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="a6ef1-212">W tym przykładzie rok, miesiąc, dzień i czas SliceStart są wyodrębniane do oddzielnych zmiennych, które są używane przez właściwości folderPath i nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="a6ef1-213">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="a6ef1-213">Copy activity properties</span></span>
<span data-ttu-id="a6ef1-214">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-214">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a6ef1-215">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="a6ef1-216">Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-216">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="a6ef1-217">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-217">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="a6ef1-218">Dla działania kopiowania, gdy źródłem jest typu **FileSystemSource** hello następujące właściwości są dostępne w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-218">For Copy Activity, when source is of type **FileSystemSource** hello following properties are available in typeProperties section:</span></span>

<span data-ttu-id="a6ef1-219">**FileSystemSource** obsługuje hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-219">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="a6ef1-220">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a6ef1-220">Property</span></span> | <span data-ttu-id="a6ef1-221">Opis</span><span class="sxs-lookup"><span data-stu-id="a6ef1-221">Description</span></span> | <span data-ttu-id="a6ef1-222">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="a6ef1-222">Allowed values</span></span> | <span data-ttu-id="a6ef1-223">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a6ef1-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a6ef1-224">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="a6ef1-224">recursive</span></span> |<span data-ttu-id="a6ef1-225">Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-225">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="a6ef1-226">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="a6ef1-226">True, False (default)</span></span> |<span data-ttu-id="a6ef1-227">Nie</span><span class="sxs-lookup"><span data-stu-id="a6ef1-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="a6ef1-228">Obsługiwane formaty plików i kompresji</span><span class="sxs-lookup"><span data-stu-id="a6ef1-228">Supported file and compression formats</span></span>
<span data-ttu-id="a6ef1-229">Zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md) artykuł na temat szczegółów.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a><span data-ttu-id="a6ef1-230">Przykład JSON: kopiowanie danych z lokalnego systemu plików HDFS tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="a6ef1-230">JSON example: Copy data from on-premises HDFS tooAzure Blob</span></span>
<span data-ttu-id="a6ef1-231">W tym przykładzie pokazano sposób toocopy danych z lokalnego systemu plików HDFS tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-231">This sample shows how toocopy data from an on-premises HDFS tooAzure Blob Storage.</span></span> <span data-ttu-id="a6ef1-232">Jednak dane mogą być kopiowane **bezpośrednio** tooany wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-232">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="a6ef1-233">przykład Witaj definicje JSON powitania po jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-233">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="a6ef1-234">Można użyć tych toocreate definicje danych toocopy potoku z systemu plików HDFS tooAzure magazynu obiektów Blob za pomocą [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a6ef1-234">You can use these definitions toocreate a pipeline toocopy data from HDFS tooAzure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="a6ef1-235">Połączonej usługi typu [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a6ef1-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="a6ef1-236">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a6ef1-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a6ef1-237">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a6ef1-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="a6ef1-238">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a6ef1-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a6ef1-239">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [FileSystemSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a6ef1-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a6ef1-240">przykład Witaj kopiuje dane z lokalnego systemu plików HDFS tooan obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-240">hello sample copies data from an on-premises HDFS tooan Azure blob every hour.</span></span> <span data-ttu-id="a6ef1-241">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-241">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="a6ef1-242">Pierwszym krokiem należy skonfigurować bramę zarządzania danymi hello.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-242">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="a6ef1-243">Witaj instrukcjami hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-243">hello instructions in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="a6ef1-244">**System plików HDFS połączonej usługi:** w tym przykładzie używa hello uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-244">**HDFS linked service:** This example uses hello Windows authentication.</span></span> <span data-ttu-id="a6ef1-245">Zobacz [HDFS połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="a6ef1-246">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="a6ef1-246">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="a6ef1-247">**System plików HDFS wejściowy zestaw danych:** ten zestaw danych odwołuje się folderu systemu plików HDFS toohello DataTransfer/UnitTest /.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-247">**HDFS input dataset:** This dataset refers toohello HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="a6ef1-248">potok Hello kopiuje wszystkie pliki hello do tego miejsca docelowego toohello folderu.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-248">hello pipeline copies all hello files in this folder toohello destination.</span></span>

<span data-ttu-id="a6ef1-249">Ustawienie "external": "prawda" informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-249">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

<span data-ttu-id="a6ef1-250">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="a6ef1-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="a6ef1-251">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="a6ef1-251">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a6ef1-252">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-252">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="a6ef1-253">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-253">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="a6ef1-254">**Działanie kopiowania w potoku z systemu plików źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="a6ef1-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="a6ef1-255">potok Hello zawiera działanie kopiowania który jest skonfigurowany toouse te zestawy danych wejściowych i wyjściowych i toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-255">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="a6ef1-256">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**FileSystemSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-256">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="a6ef1-257">Zapytanie SQL Hello określone dla hello **zapytania** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-257">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="a6ef1-258">Uwierzytelnianie Kerberos dla łącznika systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="a6ef1-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="a6ef1-259">Istnieją dwie opcje tooset środowiska lokalne powitania tak toouse uwierzytelniania Kerberos w systemie plików HDFS łącznika.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-259">There are two options tooset up hello on-premises environment so as toouse Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="a6ef1-260">Możesz wybrać hello, co najlepiej pasuje do sprawę.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-260">You can choose hello one better fits your case.</span></span>
* <span data-ttu-id="a6ef1-261">Opcja 1: [maszyna bramy sprzężenia obszaru Kerberos](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="a6ef1-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="a6ef1-262">Opcja 2: [włączyć wzajemnego zaufania między domeną systemu Windows i protokół Kerberos](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="a6ef1-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="a6ef1-263"><a name="kerberos-join-realm"></a>Opcja 1: Dołącz maszynę bramy obszaru Kerberos</span><span class="sxs-lookup"><span data-stu-id="a6ef1-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="a6ef1-264">Wymaganie:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-264">Requirement:</span></span>

* <span data-ttu-id="a6ef1-265">Maszyna bramy Hello musi protokół Kerberos hello toojoin i nie można dołączyć do dowolnej domeny systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-265">hello gateway machine needs toojoin hello Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="a6ef1-266">Jak tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-266">How tooconfigure:</span></span>

<span data-ttu-id="a6ef1-267">**Na komputerze bramy:**</span><span class="sxs-lookup"><span data-stu-id="a6ef1-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="a6ef1-268">Uruchom hello **Ksetup** tooconfigure narzędzie hello Centrum dystrybucji KLUCZY Kerberos serwera i obszar.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-268">Run hello **Ksetup** utility tooconfigure hello Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="a6ef1-269">Hello maszyny musi być skonfigurowany jako członek grupy roboczej, ponieważ obszaru Kerberos różni się od domeny systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-269">hello machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="a6ef1-270">Można to osiągnąć przez ustawienie hello protokół Kerberos i dodanie serwera Centrum dystrybucji KLUCZY w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-270">This can be achieved by setting hello Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="a6ef1-271">Zastąp *REALM.COM* z własnych odpowiednich obszaru zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="a6ef1-272">**Uruchom ponownie** maszyny powitania po wykonaniu tych poleceń 2.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-272">**Restart** hello machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="a6ef1-273">Sprawdź konfigurację hello z **Ksetup** polecenia.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-273">Verify hello configuration with **Ksetup** command.</span></span> <span data-ttu-id="a6ef1-274">dane wyjściowe Hello powinien być podobny do:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-274">hello output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="a6ef1-275">**W fabryce danych Azure:**</span><span class="sxs-lookup"><span data-stu-id="a6ef1-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="a6ef1-276">Skonfigurować za pomocą łącznika systemu plików HDFS hello **uwierzytelniania systemu Windows** wraz z protokołu Kerberos główną nazwę i hasło tooconnect toohello HDFS źródła danych.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-276">Configure hello HDFS connector using **Windows authentication** together with your Kerberos principal name and password tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="a6ef1-277">Sprawdź [właściwości powiązanych z systemu plików HDFS](#linked-service-properties) sekcji Szczegóły konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="a6ef1-278"><a name="kerberos-mutual-trust"></a>Opcja 2: Włączanie wzajemnego zaufania między domeną systemu Windows i protokół Kerberos</span><span class="sxs-lookup"><span data-stu-id="a6ef1-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="a6ef1-279">Wymaganie:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-279">Requirement:</span></span>
*   <span data-ttu-id="a6ef1-280">Maszyna bramy Hello musi zostać dołączony do domeny systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-280">hello gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="a6ef1-281">Potrzebne ustawienia uprawnień tooupdate hello kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-281">You need permission tooupdate hello domain controller's settings.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="a6ef1-282">Jak tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-282">How tooconfigure:</span></span>

> [!NOTE]
> <span data-ttu-id="a6ef1-283">Zastąp REALM.COM i AD.COM w hello samouczka z własnych odpowiednich obszaru i kontroler domeny, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-283">Replace REALM.COM and AD.COM in hello following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="a6ef1-284">**Na serwerze Centrum dystrybucji KLUCZY:**</span><span class="sxs-lookup"><span data-stu-id="a6ef1-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="a6ef1-285">Edytuje konfigurację Centrum dystrybucji KLUCZY hello w **krb5.conf** toolet pliku Centrum dystrybucji KLUCZY zaufania domeny systemu Windows, odwoływanie toohello następującego szablonu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-285">Edit hello KDC configuration in **krb5.conf** file toolet KDC trust Windows Domain referring toohello following configuration template.</span></span> <span data-ttu-id="a6ef1-286">Domyślnie program hello konfiguracji znajduje się pod adresem **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-286">By default, hello configuration is located at **/etc/krb5.conf**.</span></span>

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  <span data-ttu-id="a6ef1-287">**Uruchom ponownie** hello po konfiguracji Usługa Centrum dystrybucji KLUCZY.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-287">**Restart** hello KDC service after configuration.</span></span>

2.  <span data-ttu-id="a6ef1-288">Przygotowanie podmiot zabezpieczeń o nazwie  **krbtgt/REALM.COM@AD.COM**  w Centrum dystrybucji KLUCZY serwera z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with hello following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="a6ef1-289">W **hadoop.security.auth_to_local** konfigurację usługi systemu plików HDFS plików, dodawanie `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="a6ef1-290">**Na kontrolerze domeny:**</span><span class="sxs-lookup"><span data-stu-id="a6ef1-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="a6ef1-291">Uruchom następujące hello **Ksetup** tooadd wpis obszaru polecenia:</span><span class="sxs-lookup"><span data-stu-id="a6ef1-291">Run hello following **Ksetup** commands tooadd a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="a6ef1-292">Ustanowienie relacji zaufania z domeny systemu Windows tooKerberos obszaru.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-292">Establish trust from Windows Domain tooKerberos Realm.</span></span> <span data-ttu-id="a6ef1-293">[hasło] jest hello hasła dla podmiotu hello  **krbtgt/REALM.COM@AD.COM** .</span><span class="sxs-lookup"><span data-stu-id="a6ef1-293">[password] is hello password for hello principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="a6ef1-294">Wybierz algorytm szyfrowania używany w protokole Kerberos.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="a6ef1-295">Przejdź tooServer Manager > Zarządzanie zasadami grupy > domeny > Obiekty zasad grupy > domyślny lub zasad domeny Active i edycji.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-295">Go tooServer Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="a6ef1-296">W hello **Edytor zarządzania zasadami grupy** oknie podręcznym, przejdź tooComputer konfiguracji > zasady > Ustawienia systemu Windows > Ustawienia zabezpieczeń > Zasady lokalne > Opcje zabezpieczeń i skonfigurować **sieci zabezpieczenia: Konfigurowanie typów szyfrowania dozwolone dla protokołu Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-296">In hello **Group Policy Management Editor** popup window, go tooComputer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="a6ef1-297">Algorytm szyfrowania wybierz hello ma toouse przy połączeniu tooKDC.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-297">Select hello encryption algorithm you want toouse when connect tooKDC.</span></span> <span data-ttu-id="a6ef1-298">Zazwyczaj można po prostu wybierz wszystkie opcje hello.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-298">Commonly, you can simply select all hello options.</span></span>

        ![Typy szyfrowania konfiguracji dla protokołu Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="a6ef1-300">Użyj **Ksetup** polecenia toospecify hello szyfrowania algorytmu toobe używane na powitania określonego obszaru.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-300">Use **Ksetup** command toospecify hello encryption algorithm toobe used on hello specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="a6ef1-301">Utwórz główną w kolejności toouse głównej protokołu Kerberos w domenie systemu Windows hello mapowanie między hello konta domeny i protokołu Kerberos.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-301">Create hello mapping between hello domain account and Kerberos principal, in order toouse Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="a6ef1-302">Uruchamianie narzędzi administracyjnych hello > **użytkownicy usługi Active Directory i komputery**.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-302">Start hello Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="a6ef1-303">Skonfiguruj zaawansowane funkcje, klikając **widoku** > **zaawansowanych funkcji**.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="a6ef1-304">Zlokalizuj hello konta toowhich toocreate mapowania, a następnie kliknij prawym przyciskiem myszy tooview **mapowania nazw** > kliknij **nazwy protokołu Kerberos** kartę.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-304">Locate hello account toowhich you want toocreate mappings, and right-click tooview **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="a6ef1-305">Dodaj podmiot zabezpieczeń z hello obszaru.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-305">Add a principal from hello realm.</span></span>

        ![Mapowania tożsamości zabezpieczeń](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="a6ef1-307">**Na komputerze bramy:**</span><span class="sxs-lookup"><span data-stu-id="a6ef1-307">**On gateway machine:**</span></span>

* <span data-ttu-id="a6ef1-308">Uruchom następujące hello **Ksetup** polecenia tooadd wpis obszaru.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-308">Run hello following **Ksetup** commands tooadd a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="a6ef1-309">**W fabryce danych Azure:**</span><span class="sxs-lookup"><span data-stu-id="a6ef1-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="a6ef1-310">Skonfigurować za pomocą łącznika systemu plików HDFS hello **uwierzytelniania systemu Windows** wraz z Twojego konta domeny albo źródło danych systemu plików HDFS toohello tooconnect główna protokołu Kerberos.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-310">Configure hello HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="a6ef1-311">Sprawdź [właściwości powiązanych z systemu plików HDFS](#linked-service-properties) sekcji Szczegóły konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="a6ef1-312">toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a6ef1-312">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="a6ef1-313">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="a6ef1-313">Performance and Tuning</span></span>
<span data-ttu-id="a6ef1-314">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="a6ef1-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
