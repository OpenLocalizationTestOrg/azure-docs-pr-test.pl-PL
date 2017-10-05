---
title: "Przenoszenia danych z lokalnego systemu plików HDFS | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu przenoszenia danych z lokalnego systemu plików HDFS przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: 9a8f3156a62a1a7aa49377349e8a85454efeda50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="00493-103">Przenoszenia danych z lokalnego systemu plików HDFS przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="00493-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="00493-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przenoszenia danych z lokalnego systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="00493-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises HDFS.</span></span> <span data-ttu-id="00493-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="00493-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="00493-106">Można skopiować danych z systemu plików HDFS żadnych obsługiwanych ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="00493-106">You can copy data from HDFS to any supported sink data store.</span></span> <span data-ttu-id="00493-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="00493-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="00493-108">Fabryka danych aktualnie obsługuje tylko dane przenoszenie, z lokalnego systemu plików HDFS do innych magazynów danych, ale nie do przenoszenia danych z innych magazynów danych do lokalnego systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="00493-108">Data factory currently supports only moving data from an on-premises HDFS to other data stores, but not for moving data from other data stores to an on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="00493-109">Aktywność kopiowania nie powoduje usunięcia pliku źródłowego, po pomyślnym jest kopiowany do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="00493-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="00493-110">Jeśli musisz usunąć pliku źródłowego po pomyślnym kopii tworzenia działań niestandardowych do usuwania pliku i użyć działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="00493-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="00493-111">Włączenie łączności</span><span class="sxs-lookup"><span data-stu-id="00493-111">Enabling connectivity</span></span>
<span data-ttu-id="00493-112">Usługi fabryka danych obsługuje nawiązywania połączenia z lokalnym systemem plików HDFS przy użyciu bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="00493-112">Data Factory service supports connecting to on-premises HDFS using the Data Management Gateway.</span></span> <span data-ttu-id="00493-113">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby dowiedzieć się więcej na temat bramy zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy.</span><span class="sxs-lookup"><span data-stu-id="00493-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="00493-114">Użyj bramy do nawiązania połączenia systemu plików HDFS nawet wtedy, gdy jest ona hostowana w maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="00493-114">Use the gateway to connect to HDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="00493-115">Upewnij się, że dostęp brama zarządzania danymi do **wszystkie** [nazwa węzła serwera]: [nazwa węzła portu] i [serwery danych węzła]: [port węzeł danych] klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="00493-115">Make sure the Data Management Gateway can access to **ALL** the [name node server]:[name node port] and [data node servers]:[data node port] of the Hadoop cluster.</span></span> <span data-ttu-id="00493-116">Domyślne [nazwa węzła port] jest 50070, a domyślna [port węzeł danych] jest 50075.</span><span class="sxs-lookup"><span data-stu-id="00493-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="00493-117">Gdy bramy można zainstalować na tym samym komputerze lokalnym lub maszyny Wirtualnej platformy Azure jako system plików HDFS, zaleca się zainstalować bramę na oddzielnych maszyny/Azure IaaS maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="00493-117">While you can install gateway on the same on-premises machine or the Azure VM as the HDFS, we recommend that you install the gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="00493-118">Wystąpienia bramy na osobnym komputerze ogranicza rywalizację zasobów, poprawia wydajność.</span><span class="sxs-lookup"><span data-stu-id="00493-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="00493-119">Po zainstalowaniu bramy na osobnym komputerze maszynie powinno być możliwe dostęp do komputera z systemem plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="00493-119">When you install the gateway on a separate machine, the machine should be able to access the machine with the HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="00493-120">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="00493-120">Getting started</span></span>
<span data-ttu-id="00493-121">Można utworzyć potok z działania kopiowania, który przenosi dane ze źródła systemu plików HDFS przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="00493-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="00493-122">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="00493-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="00493-123">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="00493-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="00493-124">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="00493-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="00493-125">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="00493-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="00493-126">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="00493-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="00493-127">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="00493-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="00493-128">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="00493-128">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="00493-129">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="00493-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="00493-130">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="00493-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="00493-131">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="00493-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="00493-132">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane do kopiowania danych z magazynu danych systemu plików HDFS, zobacz [przykład JSON: kopiowanie danych z lokalnego systemu plików HDFS do obiektów Blob platformy Azure](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="00493-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS to Azure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="00493-133">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do systemu plików HDFS:</span><span class="sxs-lookup"><span data-stu-id="00493-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to HDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="00493-134">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="00493-134">Linked service properties</span></span>
<span data-ttu-id="00493-135">Połączona usługa łączy magazynu danych z fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="00493-135">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="00493-136">Tworzenie połączonej usługi typu **Hdfs** do połączenia z lokalnym systemem plików HDFS z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="00493-136">You create a linked service of type **Hdfs** to link an on-premises HDFS to your data factory.</span></span> <span data-ttu-id="00493-137">Poniższa tabela zawiera opis specyficzne dla systemu plików HDFS elementy JSON połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="00493-137">The following table provides description for JSON elements specific to HDFS linked service.</span></span>

| <span data-ttu-id="00493-138">Właściwość</span><span class="sxs-lookup"><span data-stu-id="00493-138">Property</span></span> | <span data-ttu-id="00493-139">Opis</span><span class="sxs-lookup"><span data-stu-id="00493-139">Description</span></span> | <span data-ttu-id="00493-140">Wymagane</span><span class="sxs-lookup"><span data-stu-id="00493-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00493-141">type</span><span class="sxs-lookup"><span data-stu-id="00493-141">type</span></span> |<span data-ttu-id="00493-142">Właściwość type musi mieć ustawioną: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="00493-142">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="00493-143">Tak</span><span class="sxs-lookup"><span data-stu-id="00493-143">Yes</span></span> |
| <span data-ttu-id="00493-144">Url</span><span class="sxs-lookup"><span data-stu-id="00493-144">Url</span></span> |<span data-ttu-id="00493-145">Adres URL do systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="00493-145">URL to the HDFS</span></span> |<span data-ttu-id="00493-146">Tak</span><span class="sxs-lookup"><span data-stu-id="00493-146">Yes</span></span> |
| <span data-ttu-id="00493-147">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="00493-147">authenticationType</span></span> |<span data-ttu-id="00493-148">Anonimowe lub Windows.</span><span class="sxs-lookup"><span data-stu-id="00493-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="00493-149">Umożliwia **uwierzytelnianie Kerberos** łącznika systemu plików HDFS, można znaleźć w temacie [w tej sekcji](#use-kerberos-authentication-for-hdfs-connector) do odpowiednio skonfigurowane w lokalnym środowisku.</span><span class="sxs-lookup"><span data-stu-id="00493-149">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="00493-150">Tak</span><span class="sxs-lookup"><span data-stu-id="00493-150">Yes</span></span> |
| <span data-ttu-id="00493-151">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="00493-151">userName</span></span> |<span data-ttu-id="00493-152">Uwierzytelnianie nazwy użytkownika dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="00493-152">Username for Windows authentication.</span></span> |<span data-ttu-id="00493-153">Tak (w przypadku uwierzytelniania systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="00493-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="00493-154">hasło</span><span class="sxs-lookup"><span data-stu-id="00493-154">password</span></span> |<span data-ttu-id="00493-155">Hasło dla uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="00493-155">Password for Windows authentication.</span></span> |<span data-ttu-id="00493-156">Tak (w przypadku uwierzytelniania systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="00493-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="00493-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="00493-157">gatewayName</span></span> |<span data-ttu-id="00493-158">Nazwa bramy, która powinna być używana do nawiązania połączenia systemu plików HDFS usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="00493-158">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="00493-159">Tak</span><span class="sxs-lookup"><span data-stu-id="00493-159">Yes</span></span> |
| <span data-ttu-id="00493-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="00493-160">encryptedCredential</span></span> |<span data-ttu-id="00493-161">[Nowy AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) poświadczeń dostępu do danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="00493-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="00493-162">Nie</span><span class="sxs-lookup"><span data-stu-id="00493-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="00493-163">Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="00493-163">Using Anonymous authentication</span></span>

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

### <a name="using-windows-authentication"></a><span data-ttu-id="00493-164">Przy użyciu uwierzytelniania systemu Windows</span><span class="sxs-lookup"><span data-stu-id="00493-164">Using Windows authentication</span></span>

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
## <a name="dataset-properties"></a><span data-ttu-id="00493-165">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="00493-165">Dataset properties</span></span>
<span data-ttu-id="00493-166">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="00493-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="00493-167">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="00493-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="00493-168">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="00493-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="00493-169">TypeProperties sekcja dla zestawu danych typu **FileShare** (w tym system plików HDFS w zestawie danych) ma następujące właściwości</span><span class="sxs-lookup"><span data-stu-id="00493-169">The typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has the following properties</span></span>

| <span data-ttu-id="00493-170">Właściwość</span><span class="sxs-lookup"><span data-stu-id="00493-170">Property</span></span> | <span data-ttu-id="00493-171">Opis</span><span class="sxs-lookup"><span data-stu-id="00493-171">Description</span></span> | <span data-ttu-id="00493-172">Wymagane</span><span class="sxs-lookup"><span data-stu-id="00493-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00493-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="00493-173">folderPath</span></span> |<span data-ttu-id="00493-174">Ścieżka do folderu.</span><span class="sxs-lookup"><span data-stu-id="00493-174">Path to the folder.</span></span> <span data-ttu-id="00493-175">Przykład:`myfolder`</span><span class="sxs-lookup"><span data-stu-id="00493-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="00493-176">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu.</span><span class="sxs-lookup"><span data-stu-id="00493-176">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="00493-177">Na przykład: folder\subfolder, określ folder\\\\podfolderów i dla d:\samplefolder, określ d:\\\\folder_przykładowy.</span><span class="sxs-lookup"><span data-stu-id="00493-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="00493-178">Możesz łączyć tej właściwości z **partitionBy** do folderu ścieżki oparte na wycinku rozpoczęcia/zakończenia daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="00493-178">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="00493-179">Tak</span><span class="sxs-lookup"><span data-stu-id="00493-179">Yes</span></span> |
| <span data-ttu-id="00493-180">fileName</span><span class="sxs-lookup"><span data-stu-id="00493-180">fileName</span></span> |<span data-ttu-id="00493-181">Określ nazwę pliku w **folderPath** aby tabela do odwoływania się do określonego pliku w folderze.</span><span class="sxs-lookup"><span data-stu-id="00493-181">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="00493-182">Jeśli nie określono żadnej wartości dla tej właściwości, tabela wskazuje wszystkie pliki w folderze.</span><span class="sxs-lookup"><span data-stu-id="00493-182">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="00493-183">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwę wygenerowanego pliku będzie poniżej tego formatu:</span><span class="sxs-lookup"><span data-stu-id="00493-183">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="00493-184">Dane. <Guid>.txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="00493-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="00493-185">Nie</span><span class="sxs-lookup"><span data-stu-id="00493-185">No</span></span> |
| <span data-ttu-id="00493-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="00493-186">partitionedBy</span></span> |<span data-ttu-id="00493-187">partitionedBy może służyć do określenia dynamiczne folderPath, nazwę pliku dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="00493-187">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="00493-188">Przykład: folderPath sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="00493-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="00493-189">Nie</span><span class="sxs-lookup"><span data-stu-id="00493-189">No</span></span> |
| <span data-ttu-id="00493-190">Format</span><span class="sxs-lookup"><span data-stu-id="00493-190">format</span></span> | <span data-ttu-id="00493-191">Obsługiwane są następujące typy format: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="00493-191">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="00493-192">Ustaw **typu** właściwości w formacie do jednej z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="00493-192">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="00493-193">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="00493-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="00493-194">Jeśli chcesz **skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcji format w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="00493-194">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="00493-195">Nie</span><span class="sxs-lookup"><span data-stu-id="00493-195">No</span></span> |
| <span data-ttu-id="00493-196">Kompresja</span><span class="sxs-lookup"><span data-stu-id="00493-196">compression</span></span> | <span data-ttu-id="00493-197">Określ typ i poziom kompresji danych.</span><span class="sxs-lookup"><span data-stu-id="00493-197">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="00493-198">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="00493-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="00493-199">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="00493-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="00493-200">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="00493-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="00493-201">Nie</span><span class="sxs-lookup"><span data-stu-id="00493-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="00493-202">Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.</span><span class="sxs-lookup"><span data-stu-id="00493-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="00493-203">Za pomocą właściwości partionedBy</span><span class="sxs-lookup"><span data-stu-id="00493-203">Using partionedBy property</span></span>
<span data-ttu-id="00493-204">Jak wspomniano w poprzedniej sekcji, można określić folderPath dynamiczne i nazwę pliku dla czasu danych serii za pomocą **partitionedBy** właściwość [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="00493-204">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="00493-205">Aby dowiedzieć się więcej na temat zestawów danych serii czasu, planowanie i wycinków, zobacz [tworzenie zestawów danych](data-factory-create-datasets.md), [planowanie i wykonanie](data-factory-scheduling-and-execution.md), i [tworzenie potoków](data-factory-create-pipelines.md) artykułów.</span><span class="sxs-lookup"><span data-stu-id="00493-205">To learn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="00493-206">Przykład 1:</span><span class="sxs-lookup"><span data-stu-id="00493-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="00493-207">W tym przykładzie {wycinka} zostanie zastąpiony wartością zmiennej systemowej SliceStart fabryki danych w formacie (YYYYMMDDHH) określona.</span><span class="sxs-lookup"><span data-stu-id="00493-207">In this example {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="00493-208">SliceStart odnosi się uruchomienie wycinka.</span><span class="sxs-lookup"><span data-stu-id="00493-208">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="00493-209">Element folderPath jest różne dla każdego wycinka.</span><span class="sxs-lookup"><span data-stu-id="00493-209">The folderPath is different for each slice.</span></span> <span data-ttu-id="00493-210">Na przykład: wikidatagateway/wikisampledataout/2014100103 lub wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="00493-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="00493-211">Przykład 2:</span><span class="sxs-lookup"><span data-stu-id="00493-211">Sample 2:</span></span>

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
<span data-ttu-id="00493-212">W tym przykładzie rok, miesiąc, dzień i czas SliceStart są wyodrębniane do oddzielnych zmiennych, które są używane przez właściwości folderPath i nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="00493-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="00493-213">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="00493-213">Copy activity properties</span></span>
<span data-ttu-id="00493-214">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="00493-214">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="00493-215">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="00493-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="00493-216">Właściwości, które są dostępne w sekcji typeProperties działania różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="00493-216">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="00493-217">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="00493-217">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="00493-218">Dla działania kopiowania, gdy źródłem jest typu **FileSystemSource** w sekcji typeProperties dostępne są następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="00493-218">For Copy Activity, when source is of type **FileSystemSource** the following properties are available in typeProperties section:</span></span>

<span data-ttu-id="00493-219">**FileSystemSource** obsługuje następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="00493-219">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="00493-220">Właściwość</span><span class="sxs-lookup"><span data-stu-id="00493-220">Property</span></span> | <span data-ttu-id="00493-221">Opis</span><span class="sxs-lookup"><span data-stu-id="00493-221">Description</span></span> | <span data-ttu-id="00493-222">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="00493-222">Allowed values</span></span> | <span data-ttu-id="00493-223">Wymagane</span><span class="sxs-lookup"><span data-stu-id="00493-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00493-224">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="00493-224">recursive</span></span> |<span data-ttu-id="00493-225">Wskazuje, czy dane są odczytywane rekursywnie z folderów sub lub tylko określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="00493-225">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="00493-226">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="00493-226">True, False (default)</span></span> |<span data-ttu-id="00493-227">Nie</span><span class="sxs-lookup"><span data-stu-id="00493-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="00493-228">Obsługiwane formaty plików i kompresji</span><span class="sxs-lookup"><span data-stu-id="00493-228">Supported file and compression formats</span></span>
<span data-ttu-id="00493-229">Zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md) artykuł na temat szczegółów.</span><span class="sxs-lookup"><span data-stu-id="00493-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-to-azure-blob"></a><span data-ttu-id="00493-230">Przykład JSON: kopiowanie danych z lokalnego systemu plików HDFS do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="00493-230">JSON example: Copy data from on-premises HDFS to Azure Blob</span></span>
<span data-ttu-id="00493-231">W tym przykładzie pokazano, jak można skopiować danych z lokalnego systemu plików HDFS do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="00493-231">This sample shows how to copy data from an on-premises HDFS to Azure Blob Storage.</span></span> <span data-ttu-id="00493-232">Jednak dane mogą być kopiowane **bezpośrednio** do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="00493-232">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="00493-233">Przykład zawiera definicje JSON dla następujących jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="00493-233">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="00493-234">Te definicje umożliwia tworzenie potoku można skopiować danych z systemu plików HDFS do magazynu obiektów Blob Azure przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="00493-234">You can use these definitions to create a pipeline to copy data from HDFS to Azure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="00493-235">Połączonej usługi typu [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="00493-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="00493-236">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="00493-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="00493-237">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="00493-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="00493-238">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="00493-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="00493-239">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [FileSystemSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="00493-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="00493-240">Przykład kopiuje dane z lokalnego systemu plików HDFS obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="00493-240">The sample copies data from an on-premises HDFS to an Azure blob every hour.</span></span> <span data-ttu-id="00493-241">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="00493-241">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="00493-242">Pierwszym krokiem należy skonfigurować bramę zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="00493-242">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="00493-243">Instrukcje w [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="00493-243">The instructions in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="00493-244">**System plików HDFS połączonej usługi:** w tym przykładzie używane uwierzytelnianie systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="00493-244">**HDFS linked service:** This example uses the Windows authentication.</span></span> <span data-ttu-id="00493-245">Zobacz [HDFS połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.</span><span class="sxs-lookup"><span data-stu-id="00493-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="00493-246">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="00493-246">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="00493-247">**System plików HDFS wejściowy zestaw danych:** ten zestaw danych odwołuje się do folderu systemu plików HDFS DataTransfer/UnitTest /.</span><span class="sxs-lookup"><span data-stu-id="00493-247">**HDFS input dataset:** This dataset refers to the HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="00493-248">Potok kopiuje wszystkie pliki w tym folderze, do miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="00493-248">The pipeline copies all the files in this folder to the destination.</span></span>

<span data-ttu-id="00493-249">Ustawienie "external": "prawda" informuje usługi fabryka danych czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="00493-249">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="00493-250">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="00493-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="00493-251">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="00493-251">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="00493-252">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="00493-252">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="00493-253">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="00493-253">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="00493-254">**Działanie kopiowania w potoku z systemu plików źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="00493-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="00493-255">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania tych zestawów danych wejściowych i wyjściowych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="00493-255">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="00493-256">W definicji JSON potoku **źródła** ustawiono typ **FileSystemSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="00493-256">In the pipeline JSON definition, the **source** type is set to **FileSystemSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="00493-257">Określony dla zapytania SQL **zapytania** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="00493-257">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="00493-258">Uwierzytelnianie Kerberos dla łącznika systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="00493-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="00493-259">Dostępne są dwie opcje do skonfigurowania środowiska lokalnego tak, aby korzystał z uwierzytelniania Kerberos w systemie plików HDFS łącznika.</span><span class="sxs-lookup"><span data-stu-id="00493-259">There are two options to set up the on-premises environment so as to use Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="00493-260">Możesz wybrać ten, który najlepiej pasuje do sprawę.</span><span class="sxs-lookup"><span data-stu-id="00493-260">You can choose the one better fits your case.</span></span>
* <span data-ttu-id="00493-261">Opcja 1: [maszyna bramy sprzężenia obszaru Kerberos](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="00493-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="00493-262">Opcja 2: [włączyć wzajemnego zaufania między domeną systemu Windows i protokół Kerberos](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="00493-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="00493-263"><a name="kerberos-join-realm"></a>Opcja 1: Dołącz maszynę bramy obszaru Kerberos</span><span class="sxs-lookup"><span data-stu-id="00493-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="00493-264">Wymaganie:</span><span class="sxs-lookup"><span data-stu-id="00493-264">Requirement:</span></span>

* <span data-ttu-id="00493-265">Maszyna bramy należy dołączyć obszaru Kerberos i nie można dołączyć do dowolnej domeny systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="00493-265">The gateway machine needs to join the Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="00493-266">Jak skonfigurować:</span><span class="sxs-lookup"><span data-stu-id="00493-266">How to configure:</span></span>

<span data-ttu-id="00493-267">**Na komputerze bramy:**</span><span class="sxs-lookup"><span data-stu-id="00493-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="00493-268">Uruchom **Ksetup** narzędzie, aby skonfigurować serwer Centrum dystrybucji KLUCZY protokołu Kerberos i obszar.</span><span class="sxs-lookup"><span data-stu-id="00493-268">Run the **Ksetup** utility to configure the Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="00493-269">Komputer musi być skonfigurowany jako członek grupy roboczej, ponieważ obszaru Kerberos różni się od domeny systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="00493-269">The machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="00493-270">Można to osiągnąć przez ustawienie obszaru Kerberos i dodanie serwera Centrum dystrybucji KLUCZY w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="00493-270">This can be achieved by setting the Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="00493-271">Zastąp *REALM.COM* z własnych odpowiednich obszaru zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="00493-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="00493-272">**Uruchom ponownie** komputer po wykonaniu tych poleceń 2.</span><span class="sxs-lookup"><span data-stu-id="00493-272">**Restart** the machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="00493-273">Sprawdź konfigurację z **Ksetup** polecenia.</span><span class="sxs-lookup"><span data-stu-id="00493-273">Verify the configuration with **Ksetup** command.</span></span> <span data-ttu-id="00493-274">Dane wyjściowe powinny być takie jak:</span><span class="sxs-lookup"><span data-stu-id="00493-274">The output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="00493-275">**W fabryce danych Azure:**</span><span class="sxs-lookup"><span data-stu-id="00493-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="00493-276">Skonfigurować za pomocą łącznika systemu plików HDFS **uwierzytelniania systemu Windows** wraz z nazwy głównej protokołu Kerberos i hasło, aby połączyć się ze źródłem danych systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="00493-276">Configure the HDFS connector using **Windows authentication** together with your Kerberos principal name and password to connect to the HDFS data source.</span></span> <span data-ttu-id="00493-277">Sprawdź [właściwości powiązanych z systemu plików HDFS](#linked-service-properties) sekcji Szczegóły konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="00493-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="00493-278"><a name="kerberos-mutual-trust"></a>Opcja 2: Włączanie wzajemnego zaufania między domeną systemu Windows i protokół Kerberos</span><span class="sxs-lookup"><span data-stu-id="00493-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="00493-279">Wymaganie:</span><span class="sxs-lookup"><span data-stu-id="00493-279">Requirement:</span></span>
*   <span data-ttu-id="00493-280">Maszyna bramy należy przyłączyć do domeny systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="00493-280">The gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="00493-281">Wymagane jest uprawnienie można zaktualizować ustawień kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="00493-281">You need permission to update the domain controller's settings.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="00493-282">Jak skonfigurować:</span><span class="sxs-lookup"><span data-stu-id="00493-282">How to configure:</span></span>

> [!NOTE]
> <span data-ttu-id="00493-283">Zamień REALM.COM i AD.COM w samouczku następujące własnych odpowiednich obszaru i kontroler domeny, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="00493-283">Replace REALM.COM and AD.COM in the following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="00493-284">**Na serwerze Centrum dystrybucji KLUCZY:**</span><span class="sxs-lookup"><span data-stu-id="00493-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="00493-285">Edytuje konfigurację Centrum dystrybucji KLUCZY w **krb5.conf** pliku, aby umożliwić Centrum dystrybucji KLUCZY zaufania domeny systemu Windows, które odnoszą się do następujących szablonu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="00493-285">Edit the KDC configuration in **krb5.conf** file to let KDC trust Windows Domain referring to the following configuration template.</span></span> <span data-ttu-id="00493-286">Domyślnie konfiguracji znajduje się w **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="00493-286">By default, the configuration is located at **/etc/krb5.conf**.</span></span>

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

  <span data-ttu-id="00493-287">**Uruchom ponownie** Usługa Centrum dystrybucji KLUCZY po konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="00493-287">**Restart** the KDC service after configuration.</span></span>

2.  <span data-ttu-id="00493-288">Przygotowanie podmiot zabezpieczeń o nazwie  **krbtgt/REALM.COM@AD.COM**  w Centrum dystrybucji KLUCZY serwera przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="00493-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with the following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="00493-289">W **hadoop.security.auth_to_local** konfigurację usługi systemu plików HDFS plików, dodawanie `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="00493-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="00493-290">**Na kontrolerze domeny:**</span><span class="sxs-lookup"><span data-stu-id="00493-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="00493-291">Uruchom następujące polecenie **Ksetup** polecenia, aby dodać wpis obszarów:</span><span class="sxs-lookup"><span data-stu-id="00493-291">Run the following **Ksetup** commands to add a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="00493-292">Ustanowienia zaufania z domeny systemu Windows do obszaru protokołu Kerberos.</span><span class="sxs-lookup"><span data-stu-id="00493-292">Establish trust from Windows Domain to Kerberos Realm.</span></span> <span data-ttu-id="00493-293">[hasło] jest hasłem dla podmiotu zabezpieczeń  **krbtgt/REALM.COM@AD.COM** .</span><span class="sxs-lookup"><span data-stu-id="00493-293">[password] is the password for the principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="00493-294">Wybierz algorytm szyfrowania używany w protokole Kerberos.</span><span class="sxs-lookup"><span data-stu-id="00493-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="00493-295">Przejdź do Menedżera serwera > Zarządzanie zasadami grupy > domeny > Obiekty zasad grupy > domyślny lub zasady domeny Active i edycji.</span><span class="sxs-lookup"><span data-stu-id="00493-295">Go to Server Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="00493-296">W **Edytor zarządzania zasadami grupy** okno podręczne, przejdź do pozycji Konfiguracja komputera > zasady > Ustawienia systemu Windows > Ustawienia zabezpieczeń > Zasady lokalne > Opcje zabezpieczeń i skonfigurować **sieci zabezpieczenia: Konfigurowanie typów szyfrowania dozwolone dla protokołu Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="00493-296">In the **Group Policy Management Editor** popup window, go to Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="00493-297">Wybierz algorytm szyfrowania, którego chcesz użyć, gdy nawiązać Centrum dystrybucji KLUCZY.</span><span class="sxs-lookup"><span data-stu-id="00493-297">Select the encryption algorithm you want to use when connect to KDC.</span></span> <span data-ttu-id="00493-298">Zazwyczaj można po prostu wybierz wszystkie opcje.</span><span class="sxs-lookup"><span data-stu-id="00493-298">Commonly, you can simply select all the options.</span></span>

        ![Typy szyfrowania konfiguracji dla protokołu Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="00493-300">Użyj **Ksetup** polecenie, aby określić algorytm szyfrowania, który ma być używany dla określonego obszaru.</span><span class="sxs-lookup"><span data-stu-id="00493-300">Use **Ksetup** command to specify the encryption algorithm to be used on the specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="00493-301">Utwórz mapowania między konto domeny i główna protokołu Kerberos, aby używały nazwy głównej protokołu Kerberos w domenie systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="00493-301">Create the mapping between the domain account and Kerberos principal, in order to use Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="00493-302">Uruchamianie narzędzi administracyjnych > **użytkownicy usługi Active Directory i komputery**.</span><span class="sxs-lookup"><span data-stu-id="00493-302">Start the Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="00493-303">Skonfiguruj zaawansowane funkcje, klikając **widoku** > **zaawansowanych funkcji**.</span><span class="sxs-lookup"><span data-stu-id="00493-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="00493-304">Zlokalizuj konto, do którego chcesz utworzyć mapowania i kliknij prawym przyciskiem myszy, aby wyświetlić **mapowania nazw** > kliknij **nazwy protokołu Kerberos** kartę.</span><span class="sxs-lookup"><span data-stu-id="00493-304">Locate the account to which you want to create mappings, and right-click to view **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="00493-305">Dodaj podmiot zabezpieczeń z obszaru.</span><span class="sxs-lookup"><span data-stu-id="00493-305">Add a principal from the realm.</span></span>

        ![Mapowania tożsamości zabezpieczeń](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="00493-307">**Na komputerze bramy:**</span><span class="sxs-lookup"><span data-stu-id="00493-307">**On gateway machine:**</span></span>

* <span data-ttu-id="00493-308">Uruchom następujące polecenie **Ksetup** polecenia, aby dodać wpis obszaru.</span><span class="sxs-lookup"><span data-stu-id="00493-308">Run the following **Ksetup** commands to add a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="00493-309">**W fabryce danych Azure:**</span><span class="sxs-lookup"><span data-stu-id="00493-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="00493-310">Skonfigurować za pomocą łącznika systemu plików HDFS **uwierzytelniania systemu Windows** wraz z Twojego konta domeny albo podmiot zabezpieczeń protokołu Kerberos do nawiązania połączenia ze źródłem danych systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="00493-310">Configure the HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal to connect to the HDFS data source.</span></span> <span data-ttu-id="00493-311">Sprawdź [właściwości powiązanych z systemu plików HDFS](#linked-service-properties) sekcji Szczegóły konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="00493-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="00493-312">Aby mapować kolumn z zestawu źródła danych do kolumn z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="00493-312">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="00493-313">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="00493-313">Performance and Tuning</span></span>
<span data-ttu-id="00493-314">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="00493-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
