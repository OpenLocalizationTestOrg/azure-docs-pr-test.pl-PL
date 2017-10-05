---
title: "Kopiowanie danych do/z systemem plików przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skopiować dane do i z lokalnego systemu plików przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 52305e54f539de6aba2ba9cc856a09e04d608ded
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="9f6a0-103">Kopiowanie danych do i z lokalnego systemu plików przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="9f6a0-103">Copy data to and from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="9f6a0-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure można skopiować danych z lokalnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-104">This article explains how to use the Copy Activity in Azure Data Factory to copy data to/from an on-premises file system.</span></span> <span data-ttu-id="9f6a0-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="9f6a0-106">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="9f6a0-106">Supported scenarios</span></span>
<span data-ttu-id="9f6a0-107">Dane należy skopiować **z lokalnego systemu plików** do następujących danych przechowuje:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-107">You can copy data **from an on-premises file system** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="9f6a0-108">Możesz skopiować dane z następujących baz danych **lokalnego systemu plików**:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-108">You can copy data from the following data stores **to an on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="9f6a0-109">Aktywność kopiowania nie powoduje usunięcia pliku źródłowego, po pomyślnym jest kopiowany do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="9f6a0-110">Jeśli musisz usunąć pliku źródłowego po pomyślnym kopii tworzenia działań niestandardowych do usuwania pliku i użyć działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="9f6a0-111">Włączenie łączności</span><span class="sxs-lookup"><span data-stu-id="9f6a0-111">Enabling connectivity</span></span>
<span data-ttu-id="9f6a0-112">Fabryka danych obsługuje połączenia z lokalnego systemu plików za pośrednictwem i **brama zarządzania danymi**.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-112">Data Factory supports connecting to and from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="9f6a0-113">Brama zarządzania danymi należy zainstalować w środowisku lokalnym dla usługi fabryka danych do nawiązania połączenia wszelkich obsługiwanych na lokalnym magazynem danych, w tym systemie plików.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-113">You must install the Data Management Gateway in your on-premises environment for the Data Factory service to connect to any supported on-premises data store including file system.</span></span> <span data-ttu-id="9f6a0-114">Aby dowiedzieć się więcej o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy, zobacz [przenoszenie danych między lokalnych źródeł i w chmurze z brama zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-114">To learn about Data Management Gateway and for step-by-step instructions on setting up the gateway, see [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="9f6a0-115">Oprócz brama zarządzania danymi inne pliki binarne muszą być zainstalowane do komunikowania się do i z lokalnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-115">Apart from Data Management Gateway, no other binary files need to be installed to communicate to and from an on-premises file system.</span></span> <span data-ttu-id="9f6a0-116">Należy zainstalować i używać bramy zarządzania danymi, nawet jeśli systemu plików jest w maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-116">You must install and use the Data Management Gateway even if the file system is in Azure IaaS VM.</span></span> <span data-ttu-id="9f6a0-117">Aby uzyskać szczegółowe informacje dotyczące bramy, zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-117">For detailed information about the gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="9f6a0-118">Aby używać udziału plików systemu Linux, zainstaluj [Samba](https://www.samba.org/) na serwerze Linux i instalacja bramy zarządzania danymi w systemie Windows server.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-118">To use a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="9f6a0-119">Instalowanie bramy zarządzania danymi na serwerze z systemem Linux nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9f6a0-120">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="9f6a0-120">Getting started</span></span>
<span data-ttu-id="9f6a0-121">Można utworzyć potok z działaniem kopiowania przenoszenia danych w systemie plików przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="9f6a0-122">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="9f6a0-123">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="9f6a0-124">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="9f6a0-125">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="9f6a0-126">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="9f6a0-127">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-127">Create a **data factory**.</span></span> <span data-ttu-id="9f6a0-128">Fabryka danych może zawierać co najmniej jeden potoków.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="9f6a0-129">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-129">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="9f6a0-130">Jeśli kopiujesz danych z magazynu obiektów blob platformy Azure do lokalnego systemu plików, na przykład utworzyć dwa połączone usługi, aby połączyć lokalnego systemu plików z kontem magazynu platformy Azure z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-130">For example, if you are copying data from an Azure blob storage to an on-premises file system, you create two linked services to link your on-premises file system and Azure storage account to your data factory.</span></span> <span data-ttu-id="9f6a0-131">Dla właściwości połączonej usługi, które są specyficzne dla lokalnego systemu plików, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-131">For linked service properties that are specific to an on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="9f6a0-132">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-132">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="9f6a0-133">W tym przykładzie wymienionych w ostatnim kroku tworzenia zestawu danych, aby określić folder, który zawiera dane wejściowe i kontener obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-133">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="9f6a0-134">I Utwórz innego elementu dataset, aby określić folder i nazwę pliku (opcjonalnie) w systemie plików.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-134">And, you create another dataset to specify the folder and file name (optional) in your file system.</span></span> <span data-ttu-id="9f6a0-135">Dla właściwości zestawu danych, które są specyficzne dla lokalnego systemu plików, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-135">For dataset properties that are specific to on-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="9f6a0-136">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="9f6a0-137">W przykładzie wspomniano wcześniej używasz BlobSource jako źródło i FileSystemSink jako zbiorniku dla działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-137">In the example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for the copy activity.</span></span> <span data-ttu-id="9f6a0-138">Podobnie lokalnego systemu plików są kopiowane do magazynu obiektów Blob Azure, należy użyć FileSystemSource i BlobSink w przypadku działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-138">Similarly, if you are copying from on-premises file system to Azure Blob Storage, you use FileSystemSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="9f6a0-139">Właściwości działania kopiowania, które są specyficzne dla lokalnego systemu plików, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-139">For copy activity properties that are specific to on-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="9f6a0-140">Aby uzyskać szczegółowe informacje dotyczące sposobu używania magazynu danych jako źródło lub zbiorniku kliknij łącze w poprzedniej sekcji dla magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-140">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="9f6a0-141">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-141">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="9f6a0-142">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="9f6a0-143">Dla przykładów z definicji JSON dla jednostek fabryki danych, które są używane do kopiowania danych do/z systemem plików, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-file-system) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-143">For samples with JSON definitions for Data Factory entities that are used to copy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="9f6a0-144">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do systemu plików:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-144">The following sections provide details about JSON properties that are used to define Data Factory entities specific to file system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="9f6a0-145">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="9f6a0-145">Linked service properties</span></span>
<span data-ttu-id="9f6a0-146">System plików lokalnych można połączyć z fabryki danych Azure z **na lokalnym serwerze plików** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-146">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="9f6a0-147">Poniższa tabela zawiera opisy elementy JSON, które są specyficzne dla usługi z lokalnym serwerem plików połączonych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-147">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="9f6a0-148">Właściwość</span><span class="sxs-lookup"><span data-stu-id="9f6a0-148">Property</span></span> | <span data-ttu-id="9f6a0-149">Opis</span><span class="sxs-lookup"><span data-stu-id="9f6a0-149">Description</span></span> | <span data-ttu-id="9f6a0-150">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9f6a0-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f6a0-151">type</span><span class="sxs-lookup"><span data-stu-id="9f6a0-151">type</span></span> |<span data-ttu-id="9f6a0-152">Upewnij się, że właściwość type ma ustawioną **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-152">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="9f6a0-153">Tak</span><span class="sxs-lookup"><span data-stu-id="9f6a0-153">Yes</span></span> |
| <span data-ttu-id="9f6a0-154">Host</span><span class="sxs-lookup"><span data-stu-id="9f6a0-154">host</span></span> |<span data-ttu-id="9f6a0-155">Określa ścieżkę katalogu głównego folderu, który chcesz skopiować.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-155">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="9f6a0-156">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-156">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="9f6a0-157">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="9f6a0-158">Tak</span><span class="sxs-lookup"><span data-stu-id="9f6a0-158">Yes</span></span> |
| <span data-ttu-id="9f6a0-159">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="9f6a0-159">userid</span></span> |<span data-ttu-id="9f6a0-160">Określ identyfikator użytkownika, który ma dostęp do serwera.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-160">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="9f6a0-161">Nie (Jeśli wybierzesz encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="9f6a0-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="9f6a0-162">hasło</span><span class="sxs-lookup"><span data-stu-id="9f6a0-162">password</span></span> |<span data-ttu-id="9f6a0-163">Określ hasło dla użytkownika (nazwa użytkownika).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-163">Specify the password for the user (userid).</span></span> |<span data-ttu-id="9f6a0-164">Nie (Jeśli wybierzesz encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="9f6a0-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="9f6a0-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="9f6a0-165">encryptedCredential</span></span> |<span data-ttu-id="9f6a0-166">Określ zaszyfrowane poświadczenia, które można uzyskać, uruchamiając polecenie cmdlet New-AzureRmDataFactoryEncryptValue.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-166">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="9f6a0-167">Nie (Jeśli wybierzesz określić identyfikator użytkownika i hasło w postaci zwykłego tekstu)</span><span class="sxs-lookup"><span data-stu-id="9f6a0-167">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="9f6a0-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="9f6a0-168">gatewayName</span></span> |<span data-ttu-id="9f6a0-169">Nazwa bramy, która fabryka danych ma używać do łączenia z serwerem plików lokalnych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-169">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="9f6a0-170">Tak</span><span class="sxs-lookup"><span data-stu-id="9f6a0-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="9f6a0-171">Przykładowe połączonej usługi i definicji zestawu danych</span><span class="sxs-lookup"><span data-stu-id="9f6a0-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="9f6a0-172">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="9f6a0-172">Scenario</span></span> | <span data-ttu-id="9f6a0-173">Host w definicji usługi połączonej</span><span class="sxs-lookup"><span data-stu-id="9f6a0-173">Host in linked service definition</span></span> | <span data-ttu-id="9f6a0-174">folderPath w definicji zestawu danych</span><span class="sxs-lookup"><span data-stu-id="9f6a0-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f6a0-175">Folder lokalny na komputerze bramy zarządzania danymi:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="9f6a0-176">Przykłady: D:\\ \* lub D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="9f6a0-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="9f6a0-177">D:\\ \\ (dla danych zarządzania bramy 2.0 i nowsze wersje)</span><span class="sxs-lookup"><span data-stu-id="9f6a0-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="9f6a0-178">localhost (dla starszych niż 2.0 bramy zarządzania danych)</span><span class="sxs-lookup"><span data-stu-id="9f6a0-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="9f6a0-179">. \\ \\ lub folderu\\\\podfolder (dla danych zarządzania bramy 2.0 i nowsze wersje)</span><span class="sxs-lookup"><span data-stu-id="9f6a0-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="9f6a0-180">D:\\ \\ lub D:\\\\folderu\\\\podfolder (dla wersji bramy poniżej 2.0)</span><span class="sxs-lookup"><span data-stu-id="9f6a0-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="9f6a0-181">Zdalny folder udostępniony:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="9f6a0-182">Przykłady: \\ \\MójSerwer\\udostępnianie\\ \* lub \\ \\MójSerwer\\udostępnianie\\folderu\\podfolderu\\*</span><span class="sxs-lookup"><span data-stu-id="9f6a0-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="9f6a0-183">\\\\\\\\MójSerwer\\\\udziału</span><span class="sxs-lookup"><span data-stu-id="9f6a0-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="9f6a0-184">. \\ \\ lub folderu\\\\podfolderu</span><span class="sxs-lookup"><span data-stu-id="9f6a0-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="9f6a0-185">Przykład: Przy użyciu nazwy użytkownika i hasła w postaci zwykłego tekstu</span><span class="sxs-lookup"><span data-stu-id="9f6a0-185">Example: Using username and password in plain text</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="9f6a0-186">Przykład: Użycie encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="9f6a0-186">Example: Using encryptedcredential</span></span>

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="9f6a0-187">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="9f6a0-187">Dataset properties</span></span>
<span data-ttu-id="9f6a0-188">Aby uzyskać pełną listę sekcje i właściwości, które są dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="9f6a0-189">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="9f6a0-190">Sekcja typeProperties jest różne dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-190">The typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="9f6a0-191">Zawiera informacje, takie jak lokalizacja i formatu danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-191">It provides information such as the location and format of the data in the data store.</span></span> <span data-ttu-id="9f6a0-192">TypeProperties sekcja dla zestawu danych typu **FileShare** ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-192">The typeProperties section for the dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="9f6a0-193">Właściwość</span><span class="sxs-lookup"><span data-stu-id="9f6a0-193">Property</span></span> | <span data-ttu-id="9f6a0-194">Opis</span><span class="sxs-lookup"><span data-stu-id="9f6a0-194">Description</span></span> | <span data-ttu-id="9f6a0-195">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9f6a0-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f6a0-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="9f6a0-196">folderPath</span></span> |<span data-ttu-id="9f6a0-197">Określa podrzędną do folderu.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-197">Specifies the subpath to the folder.</span></span> <span data-ttu-id="9f6a0-198">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-198">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="9f6a0-199">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="9f6a0-200">Możesz łączyć tej właściwości z **partitionBy** do folderu ścieżki oparte na wycinku rozpoczęcia/zakończenia daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-200">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="9f6a0-201">Tak</span><span class="sxs-lookup"><span data-stu-id="9f6a0-201">Yes</span></span> |
| <span data-ttu-id="9f6a0-202">fileName</span><span class="sxs-lookup"><span data-stu-id="9f6a0-202">fileName</span></span> |<span data-ttu-id="9f6a0-203">Określ nazwę pliku w **folderPath** aby tabela do odwoływania się do określonego pliku w folderze.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-203">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="9f6a0-204">Jeśli nie określono żadnej wartości dla tej właściwości, tabela wskazuje wszystkie pliki w folderze.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-204">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="9f6a0-205">Gdy **fileName** dla wyjściowego zestawu danych nie został określony i **preserveHierarchy** nie została określona w zbiornika działania nazwę wygenerowanego pliku znajduje się w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="9f6a0-206">`Data.<Guid>.txt`(Przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="9f6a0-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="9f6a0-207">Nie</span><span class="sxs-lookup"><span data-stu-id="9f6a0-207">No</span></span> |
| <span data-ttu-id="9f6a0-208">obiektu fileFilter</span><span class="sxs-lookup"><span data-stu-id="9f6a0-208">fileFilter</span></span> |<span data-ttu-id="9f6a0-209">Określ filtr służący do wybierania podzbioru pliki w ścieżce folderu, a nie wszystkie pliki.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-209">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="9f6a0-210">Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="9f6a0-211">Przykład 1: "obiektu"fileFilter: "* .log"</span><span class="sxs-lookup"><span data-stu-id="9f6a0-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="9f6a0-212">Przykład 2: "obiektu"fileFilter: 2014 - 1-?. txt"</span><span class="sxs-lookup"><span data-stu-id="9f6a0-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="9f6a0-213">Należy pamiętać, że tego obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="9f6a0-214">Nie</span><span class="sxs-lookup"><span data-stu-id="9f6a0-214">No</span></span> |
| <span data-ttu-id="9f6a0-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="9f6a0-215">partitionedBy</span></span> |<span data-ttu-id="9f6a0-216">PartitionedBy służy do określenia dynamiczne folderPath/fileName danych szeregu czasowego.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-216">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="9f6a0-217">Przykładem jest folderPath sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="9f6a0-218">Nie</span><span class="sxs-lookup"><span data-stu-id="9f6a0-218">No</span></span> |
| <span data-ttu-id="9f6a0-219">Format</span><span class="sxs-lookup"><span data-stu-id="9f6a0-219">format</span></span> | <span data-ttu-id="9f6a0-220">Obsługiwane są następujące typy format: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-220">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="9f6a0-221">Ustaw **typu** właściwości w formacie do jednej z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-221">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="9f6a0-222">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="9f6a0-223">Jeśli chcesz **skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcji format w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-223">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="9f6a0-224">Nie</span><span class="sxs-lookup"><span data-stu-id="9f6a0-224">No</span></span> |
| <span data-ttu-id="9f6a0-225">Kompresja</span><span class="sxs-lookup"><span data-stu-id="9f6a0-225">compression</span></span> | <span data-ttu-id="9f6a0-226">Określ typ i poziom kompresji danych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-226">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="9f6a0-227">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="9f6a0-228">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="9f6a0-229">zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="9f6a0-230">Nie</span><span class="sxs-lookup"><span data-stu-id="9f6a0-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="9f6a0-231">Nie można użyć nazwy pliku i obiektu fileFilter jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="9f6a0-232">Za pomocą właściwości partitionedBy</span><span class="sxs-lookup"><span data-stu-id="9f6a0-232">Using partitionedBy property</span></span>
<span data-ttu-id="9f6a0-233">Jak wspomniano w poprzedniej sekcji, można określić folderPath dynamiczne i nazwę pliku dla czasu danych serii za pomocą **partitionedBy** właściwość [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-233">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="9f6a0-234">Aby poznać więcej informacji na temat zestawów danych szeregu czasowego, planowanie i wycinków, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md), [planowania i wykonywania](data-factory-scheduling-and-execution.md), i [tworzenie potoków](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-234">To understand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="9f6a0-235">Przykład 1:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="9f6a0-236">W tym przykładzie {wycinka} zostanie zastąpiony wartością zmiennej systemowej fabryki danych SliceStart w formacie (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-236">In this example, {Slice} is replaced with the value of the Data Factory system variable SliceStart in the format (YYYYMMDDHH).</span></span> <span data-ttu-id="9f6a0-237">SliceStart odnosi się uruchomienie wycinka.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-237">SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="9f6a0-238">Element folderPath jest różne dla każdego wycinka.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-238">The folderPath is different for each slice.</span></span> <span data-ttu-id="9f6a0-239">Na przykład: wikidatagateway/wikisampledataout/2014100103 lub wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="9f6a0-240">Przykład 2:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-240">Sample 2:</span></span>

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

<span data-ttu-id="9f6a0-241">W tym przykładzie rok, miesiąc, dzień i czas SliceStart są wyodrębniane do oddzielnych zmiennych, korzystających z właściwości folderPath i nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that the folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="9f6a0-242">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="9f6a0-242">Copy activity properties</span></span>
<span data-ttu-id="9f6a0-243">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-243">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9f6a0-244">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe zestawy danych i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="9f6a0-245">Właściwości dostępne w **typeProperties** sekcji działania zależne od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-245">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span>

<span data-ttu-id="9f6a0-246">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-246">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="9f6a0-247">Jeśli przenosisz danych z lokalnego systemu plików w przypadku działania kopiowania, aby ustawić typ źródła **FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-247">If you are moving data from an on-premises file system, you set the source type in the copy activity to **FileSystemSource**.</span></span> <span data-ttu-id="9f6a0-248">Podobnie jeśli przenosisz dane do lokalnego systemu plików, należy ustawić typ ujścia w działanie kopiowania do **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-248">Similarly, if you are moving data to an on-premises file system, you set the sink type in the copy activity to **FileSystemSink**.</span></span> <span data-ttu-id="9f6a0-249">Ta sekcja zawiera listę obsługiwanych przez FileSystemSource i FileSystemSink właściwości.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="9f6a0-250">**FileSystemSource** obsługuje następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-250">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="9f6a0-251">Właściwość</span><span class="sxs-lookup"><span data-stu-id="9f6a0-251">Property</span></span> | <span data-ttu-id="9f6a0-252">Opis</span><span class="sxs-lookup"><span data-stu-id="9f6a0-252">Description</span></span> | <span data-ttu-id="9f6a0-253">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="9f6a0-253">Allowed values</span></span> | <span data-ttu-id="9f6a0-254">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9f6a0-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9f6a0-255">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="9f6a0-255">recursive</span></span> |<span data-ttu-id="9f6a0-256">Wskazuje, czy dane są odczytywane rekursywnie z podfoldery lub tylko określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-256">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="9f6a0-257">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="9f6a0-257">True, False (default)</span></span> |<span data-ttu-id="9f6a0-258">Nie</span><span class="sxs-lookup"><span data-stu-id="9f6a0-258">No</span></span> |

<span data-ttu-id="9f6a0-259">**FileSystemSink** obsługuje następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-259">**FileSystemSink** supports the following properties:</span></span>

| <span data-ttu-id="9f6a0-260">Właściwość</span><span class="sxs-lookup"><span data-stu-id="9f6a0-260">Property</span></span> | <span data-ttu-id="9f6a0-261">Opis</span><span class="sxs-lookup"><span data-stu-id="9f6a0-261">Description</span></span> | <span data-ttu-id="9f6a0-262">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="9f6a0-262">Allowed values</span></span> | <span data-ttu-id="9f6a0-263">Wymagane</span><span class="sxs-lookup"><span data-stu-id="9f6a0-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9f6a0-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="9f6a0-264">copyBehavior</span></span> |<span data-ttu-id="9f6a0-265">Określa zachowanie kopiowania, gdy źródłem jest BlobSource lub systemu plików.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-265">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="9f6a0-266">**PreserveHierarchy:** zachowuje hierarchię plików w folderze docelowym.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-266">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="9f6a0-267">Względna ścieżka pliku źródłowego do folderu źródłowego jest taka sama jak ścieżka względna docelowego pliku do folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-267">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="9f6a0-268">**FlattenHierarchy:** wszystkie pliki z folderu źródłowego są tworzone w pierwszy poziom folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-268">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="9f6a0-269">Pliki docelowe są tworzone z automatycznie generowaną nazwą.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-269">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="9f6a0-270">**MergeFiles:** scala wszystkie pliki z folderu źródłowego do jednego pliku.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-270">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="9f6a0-271">Jeśli określono nazwę pliku nazwy/obiektów blob, nazwa scalony plik jest określona nazwa.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-271">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="9f6a0-272">W przeciwnym razie jest nazwa pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="9f6a0-273">Nie</span><span class="sxs-lookup"><span data-stu-id="9f6a0-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="9f6a0-274">Przykłady cyklicznego i copyBehavior</span><span class="sxs-lookup"><span data-stu-id="9f6a0-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="9f6a0-275">W tej sekcji opisano efekty operacji kopiowania dla różnych kombinacji wartości dla właściwości cyklicznego i copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-275">This section describes the resulting behavior of the Copy operation for different combinations of values for the recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="9f6a0-276">wartości cykliczne</span><span class="sxs-lookup"><span data-stu-id="9f6a0-276">recursive value</span></span> | <span data-ttu-id="9f6a0-277">wartość copyBehavior</span><span class="sxs-lookup"><span data-stu-id="9f6a0-277">copyBehavior value</span></span> | <span data-ttu-id="9f6a0-278">Efekty</span><span class="sxs-lookup"><span data-stu-id="9f6a0-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f6a0-279">Wartość true</span><span class="sxs-lookup"><span data-stu-id="9f6a0-279">true</span></span> |<span data-ttu-id="9f6a0-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="9f6a0-280">preserveHierarchy</span></span> |<span data-ttu-id="9f6a0-281">Dla folderu źródłowego Folder1 o następującej strukturze</span><span class="sxs-lookup"><span data-stu-id="9f6a0-281">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="9f6a0-282">Folder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-282">Folder1</span></span><br/><span data-ttu-id="9f6a0-283">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9f6a0-284">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="9f6a0-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9f6a0-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9f6a0-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="9f6a0-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9f6a0-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9f6a0-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9f6a0-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9f6a0-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="9f6a0-289">folder docelowy Folder1 jest tworzony z tej samej struktury jako źródło:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-289">the target folder Folder1 is created with the same structure as the source:</span></span><br/><br/><span data-ttu-id="9f6a0-290">Folder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-290">Folder1</span></span><br/><span data-ttu-id="9f6a0-291">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9f6a0-292">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="9f6a0-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9f6a0-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9f6a0-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="9f6a0-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9f6a0-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9f6a0-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9f6a0-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9f6a0-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="9f6a0-297">Wartość true</span><span class="sxs-lookup"><span data-stu-id="9f6a0-297">true</span></span> |<span data-ttu-id="9f6a0-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="9f6a0-298">flattenHierarchy</span></span> |<span data-ttu-id="9f6a0-299">Dla folderu źródłowego Folder1 o następującej strukturze</span><span class="sxs-lookup"><span data-stu-id="9f6a0-299">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="9f6a0-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-300">Folder1</span></span><br/><span data-ttu-id="9f6a0-301">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9f6a0-302">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="9f6a0-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9f6a0-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9f6a0-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="9f6a0-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9f6a0-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9f6a0-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9f6a0-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9f6a0-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="9f6a0-307">element docelowy Folder1, utworzono o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="9f6a0-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-308">Folder1</span></span><br/><span data-ttu-id="9f6a0-309">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="9f6a0-310">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2</span><span class="sxs-lookup"><span data-stu-id="9f6a0-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="9f6a0-311">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik3</span><span class="sxs-lookup"><span data-stu-id="9f6a0-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="9f6a0-312">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File4</span><span class="sxs-lookup"><span data-stu-id="9f6a0-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="9f6a0-313">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File5</span><span class="sxs-lookup"><span data-stu-id="9f6a0-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="9f6a0-314">Wartość true</span><span class="sxs-lookup"><span data-stu-id="9f6a0-314">true</span></span> |<span data-ttu-id="9f6a0-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="9f6a0-315">mergeFiles</span></span> |<span data-ttu-id="9f6a0-316">Dla folderu źródłowego Folder1 o następującej strukturze</span><span class="sxs-lookup"><span data-stu-id="9f6a0-316">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="9f6a0-317">Folder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-317">Folder1</span></span><br/><span data-ttu-id="9f6a0-318">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9f6a0-319">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="9f6a0-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9f6a0-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9f6a0-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="9f6a0-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9f6a0-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9f6a0-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9f6a0-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9f6a0-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="9f6a0-324">element docelowy Folder1, utworzono o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-324">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="9f6a0-325">Folder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-325">Folder1</span></span><br/><span data-ttu-id="9f6a0-326">&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 + plik3 + File4 + pliku 5 zawartości są scalane w jeden plik o nazwie pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="9f6a0-327">wartość false</span><span class="sxs-lookup"><span data-stu-id="9f6a0-327">false</span></span> |<span data-ttu-id="9f6a0-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="9f6a0-328">preserveHierarchy</span></span> |<span data-ttu-id="9f6a0-329">Dla folderu źródłowego Folder1 o następującej strukturze</span><span class="sxs-lookup"><span data-stu-id="9f6a0-329">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="9f6a0-330">Folder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-330">Folder1</span></span><br/><span data-ttu-id="9f6a0-331">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9f6a0-332">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="9f6a0-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9f6a0-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9f6a0-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="9f6a0-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9f6a0-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9f6a0-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9f6a0-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9f6a0-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="9f6a0-337">folder docelowy Folder1 jest tworzony o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-337">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="9f6a0-338">Folder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-338">Folder1</span></span><br/><span data-ttu-id="9f6a0-339">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9f6a0-340">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="9f6a0-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="9f6a0-341">Subfolder1 plik3, File4 i File5 nie zostaje pobrana.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="9f6a0-342">wartość false</span><span class="sxs-lookup"><span data-stu-id="9f6a0-342">false</span></span> |<span data-ttu-id="9f6a0-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="9f6a0-343">flattenHierarchy</span></span> |<span data-ttu-id="9f6a0-344">Dla folderu źródłowego Folder1 o następującej strukturze</span><span class="sxs-lookup"><span data-stu-id="9f6a0-344">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="9f6a0-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-345">Folder1</span></span><br/><span data-ttu-id="9f6a0-346">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9f6a0-347">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="9f6a0-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9f6a0-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9f6a0-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="9f6a0-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9f6a0-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9f6a0-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9f6a0-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9f6a0-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="9f6a0-352">folder docelowy Folder1 jest tworzony o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-352">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="9f6a0-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-353">Folder1</span></span><br/><span data-ttu-id="9f6a0-354">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="9f6a0-355">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2</span><span class="sxs-lookup"><span data-stu-id="9f6a0-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="9f6a0-356">Subfolder1 plik3, File4 i File5 nie zostaje pobrana.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="9f6a0-357">wartość false</span><span class="sxs-lookup"><span data-stu-id="9f6a0-357">false</span></span> |<span data-ttu-id="9f6a0-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="9f6a0-358">mergeFiles</span></span> |<span data-ttu-id="9f6a0-359">Dla folderu źródłowego Folder1 o następującej strukturze</span><span class="sxs-lookup"><span data-stu-id="9f6a0-359">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="9f6a0-360">Folder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-360">Folder1</span></span><br/><span data-ttu-id="9f6a0-361">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="9f6a0-362">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="9f6a0-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="9f6a0-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="9f6a0-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="9f6a0-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="9f6a0-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="9f6a0-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="9f6a0-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="9f6a0-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="9f6a0-367">folder docelowy Folder1 jest tworzony o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-367">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="9f6a0-368">Folder1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-368">Folder1</span></span><br/><span data-ttu-id="9f6a0-369">&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 zawartości są scalane w jeden plik o nazwie pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="9f6a0-370">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="9f6a0-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="9f6a0-371">Subfolder1 plik3, File4 i File5 nie zostaje pobrana.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="9f6a0-372">Obsługiwane formaty plików i kompresji</span><span class="sxs-lookup"><span data-stu-id="9f6a0-372">Supported file and compression formats</span></span>
<span data-ttu-id="9f6a0-373">Zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md) artykuł na temat szczegółów.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-file-system"></a><span data-ttu-id="9f6a0-374">Przykłady JSON kopiowania danych do i z systemu plików</span><span class="sxs-lookup"><span data-stu-id="9f6a0-374">JSON examples for copying data to and from file system</span></span>
<span data-ttu-id="9f6a0-375">Poniższe przykłady zapewniają definicje JSON, których można utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-375">The following examples provide sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="9f6a0-376">Przedstawiają sposób kopiowania danych do i z lokalnego systemu plików i magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-376">They show how to copy data to and from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="9f6a0-377">Można jednak skopiować dane *bezpośrednio* z dowolnego źródła do dowolnego wychwytywanie na liście [obsługiwanych źródeł i wychwytywanie](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-377">However, you can copy data *directly* from any of the sources to any of the sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-to-azure-blob-storage"></a><span data-ttu-id="9f6a0-378">Przykład: Kopiowanie danych z lokalnego systemu plików do magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9f6a0-378">Example: Copy data from an on-premises file system to Azure Blob storage</span></span>
<span data-ttu-id="9f6a0-379">W tym przykładzie pokazano, jak można skopiować danych z lokalnego systemu plików do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-379">This sample shows how to copy data from an on-premises file system to Azure Blob storage.</span></span> <span data-ttu-id="9f6a0-380">Przykład zawiera następujące jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-380">The sample has the following Data Factory entities:</span></span>

* <span data-ttu-id="9f6a0-381">Połączonej usługi typu [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="9f6a0-382">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="9f6a0-383">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="9f6a0-384">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="9f6a0-385">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [FileSystemSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="9f6a0-386">Poniższy przykład kopiuje dane szeregów czasowych z lokalnego systemu plików do magazynu obiektów Blob Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-386">The following sample copies time-series data from an on-premises file system to Azure Blob storage every hour.</span></span> <span data-ttu-id="9f6a0-387">Właściwości JSON, które są używane w te przykłady są opisane w sekcjach po próbek.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-387">The JSON properties that are used in these samples are described in the sections after the samples.</span></span>

<span data-ttu-id="9f6a0-388">Pierwszym krokiem skonfigurować bramę zarządzania danymi zgodnie z instrukcjami wyświetlanymi w [przenoszenie danych między lokalnych źródeł i w chmurze z brama zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-388">As a first step, set up Data Management Gateway as per the instructions in [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="9f6a0-389">**Serwer plików lokalnych połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="9f6a0-389">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="9f6a0-390">Firma Microsoft zaleca używanie **encryptedCredential** właściwości zamiast **userid** i **hasło** właściwości.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-390">We recommend using the **encryptedCredential** property instead the **userid** and **password** properties.</span></span> <span data-ttu-id="9f6a0-391">Zobacz [serwera plików połączona usługa](#linked-service-properties) szczegółowe informacje o tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="9f6a0-392">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="9f6a0-392">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="9f6a0-393">**Lokalnego pliku zestawu danych wejściowych systemu:**</span><span class="sxs-lookup"><span data-stu-id="9f6a0-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="9f6a0-394">Dane są pobierane z nowego pliku co godzinę.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="9f6a0-395">Właściwości folderPath i nazwa pliku są określane na podstawie czasu rozpoczęcia wycinka.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-395">The folderPath and fileName properties are determined based on the start time of the slice.</span></span>  

<span data-ttu-id="9f6a0-396">Ustawienie `"external": "true"` fabryki danych informuje, czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-396">Setting `"external": "true"` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
      ]
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

<span data-ttu-id="9f6a0-397">**Magazyn obiektów Blob Azure wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="9f6a0-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="9f6a0-398">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-398">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="9f6a0-399">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-399">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="9f6a0-400">Ścieżka folderu używa rok, miesiąc, dzień i godzinę części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-400">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="9f6a0-401">**Działanie kopiowania w potoku z systemu plików źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="9f6a0-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="9f6a0-402">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-402">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="9f6a0-403">W definicji JSON potoku **źródła** ustawiono typ **FileSystemSource**, i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-403">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
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

### <a name="example-copy-data-from-azure-sql-database-to-an-on-premises-file-system"></a><span data-ttu-id="9f6a0-404">Przykład: Kopiowanie danych z bazy danych SQL Azure do lokalnego systemu plików</span><span class="sxs-lookup"><span data-stu-id="9f6a0-404">Example: Copy data from Azure SQL Database to an on-premises file system</span></span>
<span data-ttu-id="9f6a0-405">Poniższy przykład przedstawia:</span><span class="sxs-lookup"><span data-stu-id="9f6a0-405">The following sample shows:</span></span>

* <span data-ttu-id="9f6a0-406">Połączonej usługi typu [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="9f6a0-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="9f6a0-407">Połączonej usługi typu [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="9f6a0-408">Zestaw danych wejściowych typu [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="9f6a0-409">Wyjściowy zestaw danych typu [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="9f6a0-410">Potok z działania kopiowania, która używa [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) i [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="9f6a0-411">Przykład kopiuje dane szeregów czasowych z tabeli Azure SQL do lokalnego systemu plików co godzinę.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-411">The sample copies time-series data from an Azure SQL table to an on-premises file system every hour.</span></span> <span data-ttu-id="9f6a0-412">Właściwości JSON, które są używane w te przykłady zostały opisane w sekcjach po próbek.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-412">The JSON properties that are used in these samples are described in sections after the samples.</span></span>

<span data-ttu-id="9f6a0-413">**Baza danych SQL Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="9f6a0-413">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

<span data-ttu-id="9f6a0-414">**Serwer plików lokalnych połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="9f6a0-414">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="9f6a0-415">Firma Microsoft zaleca używanie **encryptedCredential** zamiast za pomocą właściwości **userid** i **hasło** właściwości.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-415">We recommend using the **encryptedCredential** property instead of using the **userid** and **password** properties.</span></span> <span data-ttu-id="9f6a0-416">Zobacz [System plików połączona usługa](#linked-service-properties) szczegółowe informacje o tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="9f6a0-417">**Azure SQL wejściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="9f6a0-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="9f6a0-418">Przykładzie założono, że po utworzeniu tabeli "MyTable" w języku SQL Azure i zawiera kolumnę o nazwie "timestampcolumn", szeregów czasowych danych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-418">The sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="9f6a0-419">Ustawienie ``“external”: ”true”`` fabryki danych informuje, czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-419">Setting ``“external”: ”true”`` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="9f6a0-420">**Lokalnego pliku systemu wyjściowego zestawu danych:**</span><span class="sxs-lookup"><span data-stu-id="9f6a0-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="9f6a0-421">Dane zostaną skopiowane do nowego pliku co godzinę.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-421">Data is copied to a new file every hour.</span></span> <span data-ttu-id="9f6a0-422">FolderPath i nazwę pliku dla obiekt blob są określane na podstawie czasu rozpoczęcia wycinka.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-422">The folderPath and fileName for the blob are determined based on the start time of the slice.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
      ]
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

<span data-ttu-id="9f6a0-423">**Działanie kopiowania w potoku z SQL źródłowy i odbiorczy systemu plików:**</span><span class="sxs-lookup"><span data-stu-id="9f6a0-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="9f6a0-424">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-424">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="9f6a0-425">W definicji JSON potoku **źródła** ustawiono typ **SqlSource**i **zbiornika** ustawiono typ **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-425">In the pipeline JSON definition, the **source** type is set to **SqlSource**, and the **sink** type is set to **FileSystemSink**.</span></span> <span data-ttu-id="9f6a0-426">Zapytanie SQL, który jest określony dla **SqlReaderQuery** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-426">The SQL query that is specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


<span data-ttu-id="9f6a0-427">Można również mapować kolumn z zestawu źródła danych do kolumn z zestawu danych zbiornika w definicji działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="9f6a0-427">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="9f6a0-428">Aby uzyskać więcej informacji, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="9f6a0-429">Wydajności i dostosowywanie</span><span class="sxs-lookup"><span data-stu-id="9f6a0-429">Performance and tuning</span></span>
 <span data-ttu-id="9f6a0-430">Aby dowiedzieć się więcej na temat kluczowych czynników, które mają wpływ na wydajność przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby, zobacz [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="9f6a0-430">To learn about key factors that impact the performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
