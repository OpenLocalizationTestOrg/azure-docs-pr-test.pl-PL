---
title: "Kopiowanie danych do/z programem Oracle przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skopiować dane z bazy danych Oracle bazy danych lokalnych przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: bb6af719fe6f1a30c5933ce4342a4c0c072f3ff4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="3e661-103">Kopiowanie danych z bazy danych Oracle lokalnymi przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="3e661-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="3e661-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przeniesienia danych z lokalną bazą danych Oracle.</span><span class="sxs-lookup"><span data-stu-id="3e661-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="3e661-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3e661-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="3e661-106">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="3e661-106">Supported scenarios</span></span>
<span data-ttu-id="3e661-107">Dane należy skopiować **z bazy danych Oracle** do następujących danych przechowuje:</span><span class="sxs-lookup"><span data-stu-id="3e661-107">You can copy data **from an Oracle database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="3e661-108">Możesz skopiować dane z następujących baz danych **z bazą danych Oracle**:</span><span class="sxs-lookup"><span data-stu-id="3e661-108">You can copy data from the following data stores **to an Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="3e661-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3e661-109">Prerequisites</span></span>
<span data-ttu-id="3e661-110">Fabryka danych obsługuje łączenie z lokalnych źródeł Oracle przy użyciu bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="3e661-110">Data Factory supports connecting to on-premises Oracle sources using the Data Management Gateway.</span></span> <span data-ttu-id="3e661-111">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby dowiedzieć się więcej na temat bramy zarządzania danymi i [przenoszenia danych z lokalnymi do chmury](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku dotyczące konfigurowania bramy potoku danych Przenoszenie danych.</span><span class="sxs-lookup"><span data-stu-id="3e661-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="3e661-112">Wymagana jest brama, nawet jeśli programu Oracle znajduje się w maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="3e661-112">Gateway is required even if the Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="3e661-113">Można zainstalować bramę na tej samej maszyny Wirtualnej IaaS do przechowywania danych lub w innej maszyny Wirtualnej, tak długo, jak bramy można połączyć z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="3e661-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="3e661-114">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="3e661-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="3e661-115">Obsługiwane wersje i instalacji</span><span class="sxs-lookup"><span data-stu-id="3e661-115">Supported versions and installation</span></span>
<span data-ttu-id="3e661-116">Ten łącznik Oracle obsługuje dwie wersje sterowników:</span><span class="sxs-lookup"><span data-stu-id="3e661-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="3e661-117">**Sterownik firmy Microsoft dla programu Oracle (zalecane)**: począwszy od brama zarządzania danymi w wersji 2.7, sterownik Oracle jest instalowany automatycznie wraz z bramą, dzięki czemu nie trzeba dodatkowo obsługi sterowników do firmy Microsoft Ustanów łączność z programem Oracle, i może również wystąpić lepszą wydajność kopiowania za pomocą tego sterownika.</span><span class="sxs-lookup"><span data-stu-id="3e661-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with the gateway, so you don't need to additionally handle the driver in order to establish connectivity to Oracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="3e661-118">Poniżej wersji Oracle bazy danych są obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="3e661-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="3e661-119">R1 Oracle 12c (12.1)</span><span class="sxs-lookup"><span data-stu-id="3e661-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="3e661-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="3e661-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="3e661-121">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="3e661-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="3e661-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="3e661-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="3e661-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="3e661-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e661-124">Sterownik firmy Microsoft dla programu Oracle aktualnie obsługuje tylko kopiowanie danych z programem Oracle, ale bez zapisywania do bazy danych Oracle.</span><span class="sxs-lookup"><span data-stu-id="3e661-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing to Oracle.</span></span> <span data-ttu-id="3e661-125">I należy pamiętać, że możliwości połączenia testów na karcie diagnostyki bramy zarządzania danych nie obsługuje tego sterownika.</span><span class="sxs-lookup"><span data-stu-id="3e661-125">And note the test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="3e661-126">Alternatywnie służy Kreator kopiowania Aby zweryfikować połączenie.</span><span class="sxs-lookup"><span data-stu-id="3e661-126">Alternatively, you can use the copy wizard to validate the connectivity.</span></span>
>

- <span data-ttu-id="3e661-127">**Dostawca danych programu Oracle dla platformy .NET:** można również użyć dostawcy danych programu Oracle można skopiować danych z i do programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="3e661-127">**Oracle Data Provider for .NET:** you can also choose to use Oracle Data Provider to copy data from/to Oracle.</span></span> <span data-ttu-id="3e661-128">Ten składnik jest uwzględniona w [Oracle danych dostęp do składników dla systemu Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3e661-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="3e661-129">Na komputerze, na którym zainstalowano bramę, należy zainstalować odpowiednią wersję (32/64-bitowe).</span><span class="sxs-lookup"><span data-stu-id="3e661-129">Install the appropriate version (32/64 bit) on the machine where the gateway is installed.</span></span> <span data-ttu-id="3e661-130">[Dostawca danych programu Oracle .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) możesz uzyskać dostępu do bazy danych Oracle 10 GB/s w wersji 2 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="3e661-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access to Oracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="3e661-131">Jeśli zostanie wybrana opcja "Instalacja XCopy", wykonaj czynności opisane w pliku readme.htm.</span><span class="sxs-lookup"><span data-stu-id="3e661-131">If you choose “XCopy Installation”, follow steps in the readme.htm.</span></span> <span data-ttu-id="3e661-132">Firma Microsoft zaleca się wybranie Instalatora przy użyciu interfejsu użytkownika (z systemem innym niż — XCopy jeden).</span><span class="sxs-lookup"><span data-stu-id="3e661-132">We recommend you choose the installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="3e661-133">Po zainstalowaniu dostawcy, **ponowne uruchomienie** usługa hosta bramy zarządzania danymi na tym komputerze za pomocą usługi w aplecie (lub) Menedżera konfiguracji bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="3e661-133">After installing the provider, **restart** the Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="3e661-134">Użycie Kreatora kopiowania do tworzenia potoku kopiowania, typ sterownika będzie ustalona automatycznie.</span><span class="sxs-lookup"><span data-stu-id="3e661-134">If you use copy wizard to author the copy pipeline, the driver type will be auto-determined.</span></span> <span data-ttu-id="3e661-135">Sterownik Microsoft zostanie użyty domyślnie, chyba że używana wersja bramy jest niższa niż 2.7 lub wybierz Oracle jako obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="3e661-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="3e661-136">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="3e661-136">Getting started</span></span>
<span data-ttu-id="3e661-137">Można utworzyć potok z działaniem kopiowania przenoszenia danych z lokalną bazą danych Oracle przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="3e661-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="3e661-138">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="3e661-138">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="3e661-139">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="3e661-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="3e661-140">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="3e661-140">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3e661-141">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3e661-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="3e661-142">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="3e661-142">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="3e661-143">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="3e661-143">Create a **data factory**.</span></span> <span data-ttu-id="3e661-144">Fabryka danych może zawierać co najmniej jeden potoków.</span><span class="sxs-lookup"><span data-stu-id="3e661-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="3e661-145">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="3e661-145">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="3e661-146">Na przykład jeśli kopiujesz dane z bazy danych Oralce do magazynu obiektów blob platformy Azure, Utwórz dwa połączone usługi, aby połączyć z bazą danych Oracle z kontem magazynu platformy Azure z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="3e661-146">For example, if you are copying data from an Oralce database to an Azure blob storage, you create two linked services to link your Oracle database and Azure storage account to your data factory.</span></span> <span data-ttu-id="3e661-147">Dla właściwości połączonej usługi, które są specyficzne dla Oracle, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="3e661-147">For linked service properties that are specific to Oracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="3e661-148">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3e661-148">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="3e661-149">W tym przykładzie wymienionych w ostatnim kroku tworzenia zestawu danych, aby określić tabeli w bazie danych programu Oracle, który zawiera dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="3e661-149">In the example mentioned in the last step, you create a dataset to specify the table in your Oracle database that contains the input data.</span></span> <span data-ttu-id="3e661-150">I Utwórz innego elementu dataset, aby określić folder, w którym przechowywane są dane skopiowane z bazą danych Oracle i kontener obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="3e661-150">And, you create another dataset to specify the blob container and the folder that holds the data copied from the Oracle database.</span></span> <span data-ttu-id="3e661-151">Dla właściwości zestawu danych, które są specyficzne dla Oracle, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="3e661-151">For dataset properties that are specific to Oracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="3e661-152">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="3e661-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="3e661-153">W przykładzie wspomniano wcześniej używasz OracleSource jako źródło i BlobSink jako zbiorniku dla działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3e661-153">In the example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="3e661-154">Podobnie są kopiowane z magazynu obiektów Blob Azure do bazy danych Oracle, należy użyć BlobSource i OracleSink w przypadku działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3e661-154">Similarly, if you are copying from Azure Blob Storage to Oracle Database, you use BlobSource and OracleSink in the copy activity.</span></span> <span data-ttu-id="3e661-155">Dla właściwości działania kopiowania, które są specyficzne dla baz danych programu Oracle, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="3e661-155">For copy activity properties that are specific to Oracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="3e661-156">Aby uzyskać szczegółowe informacje dotyczące sposobu używania magazynu danych jako źródło lub zbiorniku kliknij łącze w poprzedniej sekcji dla magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="3e661-156">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="3e661-157">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="3e661-157">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="3e661-158">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="3e661-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="3e661-159">Dla przykładów z definicji JSON dla jednostek fabryki danych, które są używane do kopiowania danych do/z lokalną bazą danych Oracle, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-oracle-database) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="3e661-159">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="3e661-160">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="3e661-160">The following sections provide details about JSON properties that are used to define Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="3e661-161">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="3e661-161">Linked service properties</span></span>
<span data-ttu-id="3e661-162">Poniższa tabela zawiera opis specyficzne dla usługi Oracle połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="3e661-162">The following table provides description for JSON elements specific to Oracle linked service.</span></span>

| <span data-ttu-id="3e661-163">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3e661-163">Property</span></span> | <span data-ttu-id="3e661-164">Opis</span><span class="sxs-lookup"><span data-stu-id="3e661-164">Description</span></span> | <span data-ttu-id="3e661-165">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3e661-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e661-166">type</span><span class="sxs-lookup"><span data-stu-id="3e661-166">type</span></span> |<span data-ttu-id="3e661-167">Właściwość type musi mieć ustawioną: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="3e661-167">The type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="3e661-168">Tak</span><span class="sxs-lookup"><span data-stu-id="3e661-168">Yes</span></span> |
| <span data-ttu-id="3e661-169">driverType</span><span class="sxs-lookup"><span data-stu-id="3e661-169">driverType</span></span> | <span data-ttu-id="3e661-170">Określ sterowniku można skopiować danych z/do bazy danych programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="3e661-170">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="3e661-171">Dozwolone wartości to **Microsoft** lub **ODP** (ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="3e661-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="3e661-172">Zobacz [obsługiwanych wersji i instalacji](#supported-versions-and-installation) sekcji Szczegóły sterownika.</span><span class="sxs-lookup"><span data-stu-id="3e661-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="3e661-173">Nie</span><span class="sxs-lookup"><span data-stu-id="3e661-173">No</span></span> |
| <span data-ttu-id="3e661-174">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="3e661-174">connectionString</span></span> | <span data-ttu-id="3e661-175">Podaj informacje wymagane do połączenia z wystąpieniem bazy danych programu Oracle dla właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="3e661-175">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="3e661-176">Tak</span><span class="sxs-lookup"><span data-stu-id="3e661-176">Yes</span></span> |
| <span data-ttu-id="3e661-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3e661-177">gatewayName</span></span> | <span data-ttu-id="3e661-178">Nazwa bramy, czy jest używany do łączenia się z serwerem Oracle lokalnej</span><span class="sxs-lookup"><span data-stu-id="3e661-178">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="3e661-179">Tak</span><span class="sxs-lookup"><span data-stu-id="3e661-179">Yes</span></span> |

<span data-ttu-id="3e661-180">**Przykład: za pomocą sterownika Microsoft:**</span><span class="sxs-lookup"><span data-stu-id="3e661-180">**Example: using Microsoft driver:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="3e661-181">**Przykład: za pomocą sterownika ODP**</span><span class="sxs-lookup"><span data-stu-id="3e661-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="3e661-182">Zapoznaj się [tej lokacji](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) dozwolone formaty.</span><span class="sxs-lookup"><span data-stu-id="3e661-182">Refer to [this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for the allowed formats.</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="3e661-183">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="3e661-183">Dataset properties</span></span>
<span data-ttu-id="3e661-184">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="3e661-184">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3e661-185">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Oracle, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="3e661-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="3e661-186">Sekcja typeProperties jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="3e661-186">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="3e661-187">Sekcja typeProperties dla zestawu danych typu OracleTable ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="3e661-187">The typeProperties section for the dataset of type OracleTable has the following properties:</span></span>

| <span data-ttu-id="3e661-188">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3e661-188">Property</span></span> | <span data-ttu-id="3e661-189">Opis</span><span class="sxs-lookup"><span data-stu-id="3e661-189">Description</span></span> | <span data-ttu-id="3e661-190">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3e661-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e661-191">tableName</span><span class="sxs-lookup"><span data-stu-id="3e661-191">tableName</span></span> |<span data-ttu-id="3e661-192">Nazwa tabeli w bazie danych programu Oracle, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="3e661-192">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="3e661-193">Nie (Jeśli **oracleReaderQuery** z **OracleSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="3e661-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="3e661-194">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="3e661-194">Copy activity properties</span></span>
<span data-ttu-id="3e661-195">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="3e661-195">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3e661-196">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="3e661-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="3e661-197">Działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.</span><span class="sxs-lookup"><span data-stu-id="3e661-197">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="3e661-198">Właściwości, które są dostępne w sekcji typeProperties działania różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="3e661-198">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="3e661-199">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="3e661-199">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="3e661-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="3e661-200">OracleSource</span></span>
<span data-ttu-id="3e661-201">W przypadku działania kopiowania, gdy źródłem jest typu **OracleSource** następujące właściwości są dostępne w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="3e661-201">In Copy activity, when the source is of type **OracleSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="3e661-202">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3e661-202">Property</span></span> | <span data-ttu-id="3e661-203">Opis</span><span class="sxs-lookup"><span data-stu-id="3e661-203">Description</span></span> | <span data-ttu-id="3e661-204">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="3e661-204">Allowed values</span></span> | <span data-ttu-id="3e661-205">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3e661-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3e661-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="3e661-206">oracleReaderQuery</span></span> |<span data-ttu-id="3e661-207">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="3e661-207">Use the custom query to read data.</span></span> |<span data-ttu-id="3e661-208">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="3e661-208">SQL query string.</span></span> <span data-ttu-id="3e661-209">Na przykład: Wybierz * z MyTable</span><span class="sxs-lookup"><span data-stu-id="3e661-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="3e661-210">Jeśli nie zostanie określony, która zostanie wykonana instrukcja SQL: Wybierz * z MyTable</span><span class="sxs-lookup"><span data-stu-id="3e661-210">If not specified, the SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="3e661-211">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="3e661-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="3e661-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="3e661-212">OracleSink</span></span>
<span data-ttu-id="3e661-213">**OracleSink** obsługuje następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="3e661-213">**OracleSink** supports the following properties:</span></span>

| <span data-ttu-id="3e661-214">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3e661-214">Property</span></span> | <span data-ttu-id="3e661-215">Opis</span><span class="sxs-lookup"><span data-stu-id="3e661-215">Description</span></span> | <span data-ttu-id="3e661-216">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="3e661-216">Allowed values</span></span> | <span data-ttu-id="3e661-217">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3e661-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3e661-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="3e661-218">writeBatchTimeout</span></span> |<span data-ttu-id="3e661-219">Czas na ukończenie zanim upłynie limit czasu operacji wstawiania wsadowego oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="3e661-219">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="3e661-220">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="3e661-220">timespan</span></span><br/><br/> <span data-ttu-id="3e661-221">Przykład: 00:30:00 (30 minut).</span><span class="sxs-lookup"><span data-stu-id="3e661-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="3e661-222">Nie</span><span class="sxs-lookup"><span data-stu-id="3e661-222">No</span></span> |
| <span data-ttu-id="3e661-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="3e661-223">writeBatchSize</span></span> |<span data-ttu-id="3e661-224">Wstawia dane do tabeli SQL, gdy writeBatchSize osiągnie rozmiar buforu.</span><span class="sxs-lookup"><span data-stu-id="3e661-224">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="3e661-225">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="3e661-225">Integer (number of rows)</span></span> |<span data-ttu-id="3e661-226">Nie (domyślne: 100)</span><span class="sxs-lookup"><span data-stu-id="3e661-226">No (default: 100)</span></span> |
| <span data-ttu-id="3e661-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="3e661-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="3e661-228">Określ kwerendę dla działania kopiowania do wykonania w taki sposób, że dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="3e661-228">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="3e661-229">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="3e661-229">A query statement.</span></span> |<span data-ttu-id="3e661-230">Nie</span><span class="sxs-lookup"><span data-stu-id="3e661-230">No</span></span> |
| <span data-ttu-id="3e661-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="3e661-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="3e661-232">Określ nazwę kolumny dla aktywności kopiowania wypełnić automatycznie generowane wycinek identyfikator, który służy do oczyszczania danych określonego wycinek czas ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="3e661-232">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="3e661-233">Nazwa kolumny kolumnę o typie danych binary(32).</span><span class="sxs-lookup"><span data-stu-id="3e661-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="3e661-234">Nie</span><span class="sxs-lookup"><span data-stu-id="3e661-234">No</span></span> |

## <a name="json-examples-for-copying-data-to-and-from-oracle-database"></a><span data-ttu-id="3e661-235">Przykłady JSON kopiowania danych do i z bazą danych Oracle</span><span class="sxs-lookup"><span data-stu-id="3e661-235">JSON examples for copying data to and from Oracle database</span></span>
<span data-ttu-id="3e661-236">W poniższym przykładzie przedstawiono przykładowe definicje JSON, które można użyć, aby utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3e661-236">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="3e661-237">Przedstawiają sposób kopiowania danych z/do bazy danych programu Oracle z magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3e661-237">They show how to copy data from/to an Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="3e661-238">Jednak można skopiować danych do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="3e661-238">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-to-azure-blob"></a><span data-ttu-id="3e661-239">Przykład: Kopiowanie danych z programu Oracle do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3e661-239">Example: Copy data from Oracle to Azure Blob</span></span>

<span data-ttu-id="3e661-240">Przykład zawiera następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="3e661-240">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="3e661-241">Połączonej usługi typu [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3e661-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="3e661-242">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3e661-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3e661-243">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3e661-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="3e661-244">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3e661-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="3e661-245">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) jako źródło i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) jako obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="3e661-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="3e661-246">Przykład kopiuje dane z tabeli w bazie danych programu Oracle lokalnego do obiektu blob co godzinę.</span><span class="sxs-lookup"><span data-stu-id="3e661-246">The sample copies data from a table in an on-premises Oracle database to a blob hourly.</span></span> <span data-ttu-id="3e661-247">Aby uzyskać więcej informacji na różne właściwości używane w przykładowej dokumentacji w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="3e661-247">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="3e661-248">**Oracle połączone usługi:**</span><span class="sxs-lookup"><span data-stu-id="3e661-248">**Oracle linked service:**</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="3e661-249">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="3e661-249">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="3e661-250">**Wejściowy zestaw danych Oracle:**</span><span class="sxs-lookup"><span data-stu-id="3e661-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="3e661-251">Przykład przyjęto założenie, utworzono tabelę "MyTable" w oprogramowaniu Oracle i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="3e661-251">The sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="3e661-252">Ustawienie "external": "prawda" informuje usługi fabryka danych czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="3e661-252">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
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

<span data-ttu-id="3e661-253">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="3e661-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="3e661-254">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="3e661-254">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3e661-255">Nazwa i ścieżka pliku folder dla obiektu blob dynamicznie są oceniane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="3e661-255">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="3e661-256">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="3e661-256">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="3e661-257">**W potoku z działania kopiowania:**</span><span class="sxs-lookup"><span data-stu-id="3e661-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="3e661-258">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="3e661-258">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="3e661-259">W definicji JSON potoku **źródła** ustawiono typ **OracleSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="3e661-259">In the pipeline JSON definition, the **source** type is set to **OracleSource** and **sink** type is set to **BlobSink**.</span></span>  <span data-ttu-id="3e661-260">Zapytanie SQL określony za pomocą **oracleReaderQuery** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="3e661-260">The SQL query specified with **oracleReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-to-oracle"></a><span data-ttu-id="3e661-261">Przykład: Kopiowanie danych z obiektu Blob Azure do programu Oracle</span><span class="sxs-lookup"><span data-stu-id="3e661-261">Example: Copy data from Azure Blob to Oracle</span></span>
<span data-ttu-id="3e661-262">W tym przykładzie pokazano, jak skopiować dane z magazynu obiektów Blob platformy Azure z bazą danych Oracle lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="3e661-262">This sample shows how to copy data from an Azure Blob Storage to an on-premises Oracle database.</span></span> <span data-ttu-id="3e661-263">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="3e661-263">However, data can be copied **directly** from any of the sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="3e661-264">Przykład zawiera następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="3e661-264">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="3e661-265">Połączonej usługi typu [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3e661-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="3e661-266">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3e661-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3e661-267">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3e661-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="3e661-268">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3e661-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="3e661-269">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) jako źródło [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) jako obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="3e661-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="3e661-270">Przykład kopiuje dane z obiektu blob do tabeli w bazie danych programu Oracle lokalnymi co godzinę.</span><span class="sxs-lookup"><span data-stu-id="3e661-270">The sample copies data from a blob to a table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="3e661-271">Aby uzyskać więcej informacji na różne właściwości używane w przykładowej dokumentacji w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="3e661-271">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="3e661-272">**Oracle połączone usługi:**</span><span class="sxs-lookup"><span data-stu-id="3e661-272">**Oracle linked service:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="3e661-273">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="3e661-273">**Azure Blob storage linked service:**</span></span>
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="3e661-274">**Azure wejściowego zestawu danych obiektów Blob**</span><span class="sxs-lookup"><span data-stu-id="3e661-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="3e661-275">Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="3e661-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3e661-276">Nazwa i ścieżka pliku folder dla obiektu blob dynamicznie są oceniane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="3e661-276">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="3e661-277">Ścieżka folderu korzysta rok, miesiąc i dzień część czas rozpoczęcia, a nazwa pliku godzina część czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="3e661-277">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="3e661-278">"external": ustawienie "prawda" usługi fabryka danych informuje, że w tej tabeli zewnętrznej dla fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="3e661-278">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
            "frequency": "Day",
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

<span data-ttu-id="3e661-279">**Oracle wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="3e661-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="3e661-280">Przykładzie przyjęto założenie, że w Oracle utworzono tabelę "MyTable".</span><span class="sxs-lookup"><span data-stu-id="3e661-280">The sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="3e661-281">Tworzenie tabeli w oprogramowaniu Oracle z taką samą liczbę kolumn zgodnie z oczekiwaniami pliku Blob CSV zawiera.</span><span class="sxs-lookup"><span data-stu-id="3e661-281">Create the table in Oracle with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="3e661-282">Nowe wiersze są dodawane do tabeli co godzinę.</span><span class="sxs-lookup"><span data-stu-id="3e661-282">New rows are added to the table every hour.</span></span>

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

<span data-ttu-id="3e661-283">**W potoku z działania kopiowania:**</span><span class="sxs-lookup"><span data-stu-id="3e661-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="3e661-284">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="3e661-284">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="3e661-285">W definicji JSON potoku **źródła** ustawiono typ **BlobSource** i **zbiornika** ustawiono typ **OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="3e661-285">In the pipeline JSON definition, the **source** type is set to **BlobSource** and the **sink** type is set to **OracleSink**.</span></span>  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a><span data-ttu-id="3e661-286">Wskazówki dotyczące rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="3e661-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="3e661-287">Problem 1: Dostawca danych programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="3e661-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="3e661-288">Zobacz następujące tematy **komunikat o błędzie**:</span><span class="sxs-lookup"><span data-stu-id="3e661-288">You see the following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable to find the requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="3e661-289">**Możliwe przyczyny:**</span><span class="sxs-lookup"><span data-stu-id="3e661-289">**Possible causes:**</span></span>

1. <span data-ttu-id="3e661-290">.NET Framework Data Provider for Oracle nie został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="3e661-290">The .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="3e661-291">.NET Framework Data Provider for Oracle została zainstalowana w .NET Framework 2.0 i nie znajduje się w folderze programu .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="3e661-291">The .NET Framework Data Provider for Oracle was installed to .NET Framework 2.0 and is not found in the .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="3e661-292">**Rozdzielczość/obejście problemu:**</span><span class="sxs-lookup"><span data-stu-id="3e661-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="3e661-293">Jeśli nie zainstalowano dostawcy .NET dla Oracle, [go zainstalować](http://www.oracle.com/technetwork/topics/dotnet/downloads/) i ponów próbę wykonania tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="3e661-293">If you haven't installed the .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry the scenario.</span></span>
2. <span data-ttu-id="3e661-294">Jeśli zostanie wyświetlony komunikat o błędzie nawet po zainstalowaniu dostawcy, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="3e661-294">If you get the error message even after installing the provider, do the following steps:</span></span>
   1. <span data-ttu-id="3e661-295">Otwórz konfiguracji komputera programu .NET 2.0 z folderu: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="3e661-295">Open machine config of .NET 2.0 from the folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="3e661-296">Wyszukaj **dostawca danych programu Oracle dla platformy .NET**, i można znaleźć wpisu, jak pokazano w poniższym przykładzie w obszarze **system.dane** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Dostawca danych programu oracle dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="3e661-296">Search for **Oracle Data Provider for .NET**, and you should be able to find an entry as shown in the following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="3e661-297">”</span><span class="sxs-lookup"><span data-stu-id="3e661-297">”</span></span>
3. <span data-ttu-id="3e661-298">Skopiuj ten wpis w pliku machine.config w następującym folderze v4.0: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, a następnie zmień tę wersję 4.xxx.x.x.</span><span class="sxs-lookup"><span data-stu-id="3e661-298">Copy this entry to the machine.config file in the following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change the version to 4.xxx.x.x.</span></span>
4. <span data-ttu-id="3e661-299">Zainstaluj "\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll < ścieżka instalacji ODP.NET >" w globalnej pamięci podręcznej zestawów (GAC), uruchamiając `gacutil /i [provider path]`. ## porady dotyczące rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="3e661-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into the global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="3e661-300">Problem 2: formatowanie daty/godziny</span><span class="sxs-lookup"><span data-stu-id="3e661-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="3e661-301">Zobacz następujące tematy **komunikat o błędzie**:</span><span class="sxs-lookup"><span data-stu-id="3e661-301">You see the following **error message**:</span></span>

    Message=Operation failed in Oracle Database with the following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="3e661-302">**Rozdzielczość/obejście problemu:**</span><span class="sxs-lookup"><span data-stu-id="3e661-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="3e661-303">Może być konieczne dostosowanie ciągu zapytania w Twojej aktywności kopiowania oparte na konfiguracji daty w bazie danych programu Oracle, jak pokazano w poniższym przykładzie (funkcja to_date):</span><span class="sxs-lookup"><span data-stu-id="3e661-303">You may need to adjust the query string in your copy activity based on how dates are configured in your Oracle database, as shown in the following sample (using the to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="3e661-304">Mapowanie typu dla Oracle</span><span class="sxs-lookup"><span data-stu-id="3e661-304">Type mapping for Oracle</span></span>
<span data-ttu-id="3e661-305">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu działanie kopiowania przeprowadza automatyczne konwersje z typów źródła do zbiornika typów o następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="3e661-305">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="3e661-306">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="3e661-306">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="3e661-307">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="3e661-307">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="3e661-308">Podczas przenoszenia danych z bazy danych Oracle, następujące mapowania są używane z typem danych Oracle typ architektury .NET i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="3e661-308">When moving data from Oracle, the following mappings are used from Oracle data type to .NET type and vice versa.</span></span>

| <span data-ttu-id="3e661-309">Typ danych Oracle</span><span class="sxs-lookup"><span data-stu-id="3e661-309">Oracle data type</span></span> | <span data-ttu-id="3e661-310">Typ danych .NET framework</span><span class="sxs-lookup"><span data-stu-id="3e661-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="3e661-311">BPLIK</span><span class="sxs-lookup"><span data-stu-id="3e661-311">BFILE</span></span> |<span data-ttu-id="3e661-312">Byte]</span><span class="sxs-lookup"><span data-stu-id="3e661-312">Byte[]</span></span> |
| <span data-ttu-id="3e661-313">OBIEKT BLOB</span><span class="sxs-lookup"><span data-stu-id="3e661-313">BLOB</span></span> |<span data-ttu-id="3e661-314">Byte]</span><span class="sxs-lookup"><span data-stu-id="3e661-314">Byte[]</span></span> |
| <span data-ttu-id="3e661-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="3e661-315">CHAR</span></span> |<span data-ttu-id="3e661-316">Ciąg</span><span class="sxs-lookup"><span data-stu-id="3e661-316">String</span></span> |
| <span data-ttu-id="3e661-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="3e661-317">CLOB</span></span> |<span data-ttu-id="3e661-318">Ciąg</span><span class="sxs-lookup"><span data-stu-id="3e661-318">String</span></span> |
| <span data-ttu-id="3e661-319">DATA</span><span class="sxs-lookup"><span data-stu-id="3e661-319">DATE</span></span> |<span data-ttu-id="3e661-320">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="3e661-320">DateTime</span></span> |
| <span data-ttu-id="3e661-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="3e661-321">FLOAT</span></span> |<span data-ttu-id="3e661-322">Decimal, ciąg (jeśli precyzja > 28)</span><span class="sxs-lookup"><span data-stu-id="3e661-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="3e661-323">LICZBA CAŁKOWITA</span><span class="sxs-lookup"><span data-stu-id="3e661-323">INTEGER</span></span> |<span data-ttu-id="3e661-324">Decimal, ciąg (jeśli precyzja > 28)</span><span class="sxs-lookup"><span data-stu-id="3e661-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="3e661-325">INTERWAŁ ROK, MIESIĄC</span><span class="sxs-lookup"><span data-stu-id="3e661-325">INTERVAL YEAR TO MONTH</span></span> |<span data-ttu-id="3e661-326">Int32</span><span class="sxs-lookup"><span data-stu-id="3e661-326">Int32</span></span> |
| <span data-ttu-id="3e661-327">INTERWAŁ DZIEŃ NA SEKUNDĘ</span><span class="sxs-lookup"><span data-stu-id="3e661-327">INTERVAL DAY TO SECOND</span></span> |<span data-ttu-id="3e661-328">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="3e661-328">TimeSpan</span></span> |
| <span data-ttu-id="3e661-329">DŁUGA</span><span class="sxs-lookup"><span data-stu-id="3e661-329">LONG</span></span> |<span data-ttu-id="3e661-330">Ciąg</span><span class="sxs-lookup"><span data-stu-id="3e661-330">String</span></span> |
| <span data-ttu-id="3e661-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="3e661-331">LONG RAW</span></span> |<span data-ttu-id="3e661-332">Byte]</span><span class="sxs-lookup"><span data-stu-id="3e661-332">Byte[]</span></span> |
| <span data-ttu-id="3e661-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="3e661-333">NCHAR</span></span> |<span data-ttu-id="3e661-334">Ciąg</span><span class="sxs-lookup"><span data-stu-id="3e661-334">String</span></span> |
| <span data-ttu-id="3e661-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="3e661-335">NCLOB</span></span> |<span data-ttu-id="3e661-336">Ciąg</span><span class="sxs-lookup"><span data-stu-id="3e661-336">String</span></span> |
| <span data-ttu-id="3e661-337">NUMER</span><span class="sxs-lookup"><span data-stu-id="3e661-337">NUMBER</span></span> |<span data-ttu-id="3e661-338">Decimal, ciąg (jeśli precyzja > 28)</span><span class="sxs-lookup"><span data-stu-id="3e661-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="3e661-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="3e661-339">NVARCHAR2</span></span> |<span data-ttu-id="3e661-340">Ciąg</span><span class="sxs-lookup"><span data-stu-id="3e661-340">String</span></span> |
| <span data-ttu-id="3e661-341">NIEPRZETWORZONE</span><span class="sxs-lookup"><span data-stu-id="3e661-341">RAW</span></span> |<span data-ttu-id="3e661-342">Byte]</span><span class="sxs-lookup"><span data-stu-id="3e661-342">Byte[]</span></span> |
| <span data-ttu-id="3e661-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="3e661-343">ROWID</span></span> |<span data-ttu-id="3e661-344">Ciąg</span><span class="sxs-lookup"><span data-stu-id="3e661-344">String</span></span> |
| <span data-ttu-id="3e661-345">ZNACZNIK CZASU</span><span class="sxs-lookup"><span data-stu-id="3e661-345">TIMESTAMP</span></span> |<span data-ttu-id="3e661-346">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="3e661-346">DateTime</span></span> |
| <span data-ttu-id="3e661-347">SYGNATURA CZASOWA Z LOKALNEJ STREFIE CZASOWEJ</span><span class="sxs-lookup"><span data-stu-id="3e661-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="3e661-348">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="3e661-348">DateTime</span></span> |
| <span data-ttu-id="3e661-349">SYGNATURA CZASOWA ZE STREFĄ CZASOWĄ</span><span class="sxs-lookup"><span data-stu-id="3e661-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="3e661-350">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="3e661-350">DateTime</span></span> |
| <span data-ttu-id="3e661-351">LICZBA CAŁKOWITA BEZ ZNAKU</span><span class="sxs-lookup"><span data-stu-id="3e661-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="3e661-352">Numer</span><span class="sxs-lookup"><span data-stu-id="3e661-352">Number</span></span> |
| <span data-ttu-id="3e661-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="3e661-353">VARCHAR2</span></span> |<span data-ttu-id="3e661-354">Ciąg</span><span class="sxs-lookup"><span data-stu-id="3e661-354">String</span></span> |
| <span data-ttu-id="3e661-355">XML</span><span class="sxs-lookup"><span data-stu-id="3e661-355">XML</span></span> |<span data-ttu-id="3e661-356">Ciąg</span><span class="sxs-lookup"><span data-stu-id="3e661-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="3e661-357">Typ danych **INTERWAŁ rok na miesiąc** i **na dzień INTERWAŁU drugie** nie są obsługiwane, gdy za pomocą sterownika Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3e661-357">Data type **INTERVAL YEAR TO MONTH** and **INTERVAL DAY TO SECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="3e661-358">Obiekt sink kolumn mapy źródła</span><span class="sxs-lookup"><span data-stu-id="3e661-358">Map source to sink columns</span></span>
<span data-ttu-id="3e661-359">Aby uzyskać informacje dotyczące mapowania kolumn w zestawie źródła danych do kolumn w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="3e661-359">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="3e661-360">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="3e661-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="3e661-361">Podczas kopiowania danych z danych relacyjnych przechowuje, należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="3e661-361">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="3e661-362">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="3e661-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="3e661-363">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="3e661-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="3e661-364">Podczas wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że te same dane jest do odczytu niezależnie od tego, ile razy wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="3e661-364">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="3e661-365">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="3e661-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="3e661-366">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="3e661-366">Performance and Tuning</span></span>
<span data-ttu-id="3e661-367">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="3e661-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
