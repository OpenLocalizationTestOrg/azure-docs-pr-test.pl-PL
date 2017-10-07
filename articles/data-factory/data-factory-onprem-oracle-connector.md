---
title: "aaaCopy danych do/z programem Oracle przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocopy danych z bazy danych Oracle, który jest lokalnie przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="01215-103">Kopiowanie danych z bazy danych Oracle lokalnymi przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="01215-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="01215-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z lokalną bazą danych Oracle.</span><span class="sxs-lookup"><span data-stu-id="01215-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="01215-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="01215-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="01215-106">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="01215-106">Supported scenarios</span></span>
<span data-ttu-id="01215-107">Dane należy skopiować **z bazy danych Oracle** toohello po magazynów danych:</span><span class="sxs-lookup"><span data-stu-id="01215-107">You can copy data **from an Oracle database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="01215-108">Można skopiować danych z powitania po magazyny danych **bazą danych Oracle tooan**:</span><span class="sxs-lookup"><span data-stu-id="01215-108">You can copy data from hello following data stores **tooan Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="01215-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="01215-109">Prerequisites</span></span>
<span data-ttu-id="01215-110">Fabryka danych obsługuje łączącego źródeł Oracle tooon lokalnych przy użyciu hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="01215-110">Data Factory supports connecting tooon-premises Oracle sources using hello Data Management Gateway.</span></span> <span data-ttu-id="01215-111">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) toolearn artykuł na temat bramy zarządzania danymi i [przenoszenia danych z lokalnego toocloud](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku dotyczące konfigurowania bramy hello potoku danych toomove danych.</span><span class="sxs-lookup"><span data-stu-id="01215-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article toolearn about Data Management Gateway and [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="01215-112">Wymagana jest brama, nawet jeśli hello Oracle znajduje się w maszynie Wirtualnej platformy Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="01215-112">Gateway is required even if hello Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="01215-113">Możesz zainstalować bramę hello na powitania sam maszyn wirtualnych IaaS jako dane hello przechowywania lub na innej maszynie Wirtualnej tak długo, jak bramy hello połączyć toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="01215-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="01215-114">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="01215-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="01215-115">Obsługiwane wersje i instalacji</span><span class="sxs-lookup"><span data-stu-id="01215-115">Supported versions and installation</span></span>
<span data-ttu-id="01215-116">Ten łącznik Oracle obsługuje dwie wersje sterowników:</span><span class="sxs-lookup"><span data-stu-id="01215-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="01215-117">**Sterownik firmy Microsoft dla programu Oracle (zalecane)**: począwszy od brama zarządzania danymi w wersji 2.7, sterownik firmy Microsoft dla programu Oracle jest instalowany automatycznie wraz z bramy hello, więc nie trzeba tooadditionally dojście hello sterowników w kolejności tooestablish tooOracle łączność, a także mogą wystąpić lepszą wydajność kopiowania za pomocą tego sterownika.</span><span class="sxs-lookup"><span data-stu-id="01215-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with hello gateway, so you don't need tooadditionally handle hello driver in order tooestablish connectivity tooOracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="01215-118">Poniżej wersji Oracle bazy danych są obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="01215-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="01215-119">R1 Oracle 12c (12.1)</span><span class="sxs-lookup"><span data-stu-id="01215-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="01215-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="01215-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="01215-121">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="01215-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="01215-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="01215-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="01215-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="01215-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="01215-124">Sterownik firmy Microsoft dla programu Oracle aktualnie obsługuje tylko kopiowanie danych z programem Oracle, ale bez zapisywania tooOracle.</span><span class="sxs-lookup"><span data-stu-id="01215-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing tooOracle.</span></span> <span data-ttu-id="01215-125">I możliwości połączenia Uwaga hello testów na karcie diagnostyki bramy zarządzania danych nie obsługuje tego sterownika.</span><span class="sxs-lookup"><span data-stu-id="01215-125">And note hello test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="01215-126">Alternatywnie można użyć hello kopiowania kreatora toovalidate hello łączności.</span><span class="sxs-lookup"><span data-stu-id="01215-126">Alternatively, you can use hello copy wizard toovalidate hello connectivity.</span></span>
>

- <span data-ttu-id="01215-127">**Dostawca danych programu Oracle dla platformy .NET:** można także toouse dostawca danych programu Oracle toocopy danych z / tooOracle.</span><span class="sxs-lookup"><span data-stu-id="01215-127">**Oracle Data Provider for .NET:** you can also choose toouse Oracle Data Provider toocopy data from/tooOracle.</span></span> <span data-ttu-id="01215-128">Ten składnik jest uwzględniona w [Oracle danych dostęp do składników dla systemu Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="01215-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="01215-129">Na maszynie hello, w której zainstalowano bramę hello, należy zainstalować odpowiednią wersję hello (32/64-bitowe).</span><span class="sxs-lookup"><span data-stu-id="01215-129">Install hello appropriate version (32/64 bit) on hello machine where hello gateway is installed.</span></span> <span data-ttu-id="01215-130">[Dostawca danych programu Oracle .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) mogą uzyskiwać dostęp do tooOracle Database 10 g wersji 2 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="01215-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access tooOracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="01215-131">Jeśli zostanie wybrana opcja "Instalacja XCopy", wykonaj kroki w pliku readme.htm hello.</span><span class="sxs-lookup"><span data-stu-id="01215-131">If you choose “XCopy Installation”, follow steps in hello readme.htm.</span></span> <span data-ttu-id="01215-132">Zaleca się wybrać hello Instalatora przy użyciu interfejsu użytkownika (z systemem innym niż — XCopy jeden).</span><span class="sxs-lookup"><span data-stu-id="01215-132">We recommend you choose hello installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="01215-133">Po zainstalowaniu dostawcy hello **ponowne uruchomienie** hello usługa hosta bramy zarządzania danymi na tym komputerze za pomocą usługi w aplecie (lub) Menedżera konfiguracji bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="01215-133">After installing hello provider, **restart** hello Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="01215-134">Użycie kopii Kreatora tooauthor hello kopiowania potoku hello sterownik typu będzie ustalona automatycznie.</span><span class="sxs-lookup"><span data-stu-id="01215-134">If you use copy wizard tooauthor hello copy pipeline, hello driver type will be auto-determined.</span></span> <span data-ttu-id="01215-135">Sterownik Microsoft zostanie użyty domyślnie, chyba że używana wersja bramy jest niższa niż 2.7 lub wybierz Oracle jako obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="01215-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="01215-136">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="01215-136">Getting started</span></span>
<span data-ttu-id="01215-137">Można utworzyć potok z działaniem kopiowania przenoszenia danych z lokalną bazą danych Oracle przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="01215-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="01215-138">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="01215-138">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="01215-139">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="01215-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="01215-140">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="01215-140">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="01215-141">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="01215-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="01215-142">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="01215-142">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="01215-143">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="01215-143">Create a **data factory**.</span></span> <span data-ttu-id="01215-144">Fabryka danych może zawierać co najmniej jeden potoków.</span><span class="sxs-lookup"><span data-stu-id="01215-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="01215-145">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="01215-145">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="01215-146">Na przykład jeśli dane są kopiowane z Oralce tooan bazy danych magazynu obiektów blob platformy Azure, utworzysz dwa toolink połączonej usługi bazy danych Oracle i fabryki danych tooyour konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="01215-146">For example, if you are copying data from an Oralce database tooan Azure blob storage, you create two linked services toolink your Oracle database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="01215-147">Dla właściwości połączonej usługi, które są określone tooOracle, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="01215-147">For linked service properties that are specific tooOracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="01215-148">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="01215-148">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="01215-149">W przykładzie hello wymienionych w ostatnim kroku hello utworzysz tabelę hello toospecify zestawu danych w bazie danych programu Oracle zawiera hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="01215-149">In hello example mentioned in hello last step, you create a dataset toospecify hello table in your Oracle database that contains hello input data.</span></span> <span data-ttu-id="01215-150">Utwórz innego kontenera obiektów blob hello toospecify zestawu danych i folderu hello, która przechowuje dane hello skopiowanych z hello baz danych programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="01215-150">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello Oracle database.</span></span> <span data-ttu-id="01215-151">Dla właściwości zestawu danych, które są określone tooOracle [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="01215-151">For dataset properties that are specific tooOracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="01215-152">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="01215-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="01215-153">W przykładzie hello wspomniano wcześniej używa OracleSource jako źródło i BlobSink jako zbiorniku dla aktywności kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="01215-153">In hello example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="01215-154">Podobnie są kopiowane z magazynu obiektów Blob Azure tooOracle bazy danych, należy użyć BlobSource i OracleSink w przypadku działania kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="01215-154">Similarly, if you are copying from Azure Blob Storage tooOracle Database, you use BlobSource and OracleSink in hello copy activity.</span></span> <span data-ttu-id="01215-155">Dla właściwości działania kopiowania, które są określone tooOracle bazy danych, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="01215-155">For copy activity properties that are specific tooOracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="01215-156">Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="01215-156">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="01215-157">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="01215-157">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="01215-158">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="01215-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="01215-159">Dla przykładów z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z lokalną bazą danych Oracle, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-oracle-database) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="01215-159">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="01215-160">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="01215-160">hello following sections provide details about JSON properties that are used toodefine Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="01215-161">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="01215-161">Linked service properties</span></span>
<span data-ttu-id="01215-162">Hello w poniższej tabeli przedstawiono opis usługi określonego tooOracle połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="01215-162">hello following table provides description for JSON elements specific tooOracle linked service.</span></span>

| <span data-ttu-id="01215-163">Właściwość</span><span class="sxs-lookup"><span data-stu-id="01215-163">Property</span></span> | <span data-ttu-id="01215-164">Opis</span><span class="sxs-lookup"><span data-stu-id="01215-164">Description</span></span> | <span data-ttu-id="01215-165">Wymagane</span><span class="sxs-lookup"><span data-stu-id="01215-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="01215-166">type</span><span class="sxs-lookup"><span data-stu-id="01215-166">type</span></span> |<span data-ttu-id="01215-167">musi mieć ustawioną właściwość type Hello: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="01215-167">hello type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="01215-168">Tak</span><span class="sxs-lookup"><span data-stu-id="01215-168">Yes</span></span> |
| <span data-ttu-id="01215-169">driverType</span><span class="sxs-lookup"><span data-stu-id="01215-169">driverType</span></span> | <span data-ttu-id="01215-170">Określ, które sterownik toouse toocopy dane z / tooOracle bazy danych.</span><span class="sxs-lookup"><span data-stu-id="01215-170">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="01215-171">Dozwolone wartości to **Microsoft** lub **ODP** (ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="01215-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="01215-172">Zobacz [obsługiwanych wersji i instalacji](#supported-versions-and-installation) sekcji Szczegóły sterownika.</span><span class="sxs-lookup"><span data-stu-id="01215-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="01215-173">Nie</span><span class="sxs-lookup"><span data-stu-id="01215-173">No</span></span> |
| <span data-ttu-id="01215-174">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="01215-174">connectionString</span></span> | <span data-ttu-id="01215-175">Określ informacje niezbędne wystąpienie bazy danych Oracle toohello tooconnect hello właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="01215-175">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="01215-176">Tak</span><span class="sxs-lookup"><span data-stu-id="01215-176">Yes</span></span> |
| <span data-ttu-id="01215-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="01215-177">gatewayName</span></span> | <span data-ttu-id="01215-178">Nazwa bramy hello, że jest używana tooconnect toohello lokalnego serwera Oracle</span><span class="sxs-lookup"><span data-stu-id="01215-178">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="01215-179">Tak</span><span class="sxs-lookup"><span data-stu-id="01215-179">Yes</span></span> |

<span data-ttu-id="01215-180">**Przykład: za pomocą sterownika Microsoft:**</span><span class="sxs-lookup"><span data-stu-id="01215-180">**Example: using Microsoft driver:**</span></span>
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

<span data-ttu-id="01215-181">**Przykład: za pomocą sterownika ODP**</span><span class="sxs-lookup"><span data-stu-id="01215-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="01215-182">Odwołuje się zbyt[tej lokacji](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) dla hello dozwolone formaty.</span><span class="sxs-lookup"><span data-stu-id="01215-182">Refer too[this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for hello allowed formats.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="01215-183">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="01215-183">Dataset properties</span></span>
<span data-ttu-id="01215-184">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="01215-184">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="01215-185">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Oracle, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="01215-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="01215-186">sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello.</span><span class="sxs-lookup"><span data-stu-id="01215-186">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="01215-187">Witaj typeProperties sekcja dla zestawu danych hello typu OracleTable ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="01215-187">hello typeProperties section for hello dataset of type OracleTable has hello following properties:</span></span>

| <span data-ttu-id="01215-188">Właściwość</span><span class="sxs-lookup"><span data-stu-id="01215-188">Property</span></span> | <span data-ttu-id="01215-189">Opis</span><span class="sxs-lookup"><span data-stu-id="01215-189">Description</span></span> | <span data-ttu-id="01215-190">Wymagane</span><span class="sxs-lookup"><span data-stu-id="01215-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="01215-191">tableName</span><span class="sxs-lookup"><span data-stu-id="01215-191">tableName</span></span> |<span data-ttu-id="01215-192">Oznacza nazwę tabeli hello na powitania hello połączonej usługi bazy danych programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="01215-192">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="01215-193">Nie (Jeśli **oracleReaderQuery** z **OracleSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="01215-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="01215-194">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="01215-194">Copy activity properties</span></span>
<span data-ttu-id="01215-195">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="01215-195">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="01215-196">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="01215-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="01215-197">Witaj działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.</span><span class="sxs-lookup"><span data-stu-id="01215-197">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="01215-198">Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="01215-198">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="01215-199">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="01215-199">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="01215-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="01215-200">OracleSource</span></span>
<span data-ttu-id="01215-201">W przypadku działania kopiowania, gdy źródłem hello jest typu **OracleSource** hello następujące właściwości są dostępne w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="01215-201">In Copy activity, when hello source is of type **OracleSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="01215-202">Właściwość</span><span class="sxs-lookup"><span data-stu-id="01215-202">Property</span></span> | <span data-ttu-id="01215-203">Opis</span><span class="sxs-lookup"><span data-stu-id="01215-203">Description</span></span> | <span data-ttu-id="01215-204">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="01215-204">Allowed values</span></span> | <span data-ttu-id="01215-205">Wymagane</span><span class="sxs-lookup"><span data-stu-id="01215-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="01215-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="01215-206">oracleReaderQuery</span></span> |<span data-ttu-id="01215-207">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="01215-207">Use hello custom query tooread data.</span></span> |<span data-ttu-id="01215-208">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="01215-208">SQL query string.</span></span> <span data-ttu-id="01215-209">Na przykład: Wybierz * z MyTable</span><span class="sxs-lookup"><span data-stu-id="01215-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="01215-210">Jeśli nie zostanie określony, hello instrukcji SQL, która jest wykonywana: Wybierz * z MyTable</span><span class="sxs-lookup"><span data-stu-id="01215-210">If not specified, hello SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="01215-211">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="01215-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="01215-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="01215-212">OracleSink</span></span>
<span data-ttu-id="01215-213">**OracleSink** obsługuje hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="01215-213">**OracleSink** supports hello following properties:</span></span>

| <span data-ttu-id="01215-214">Właściwość</span><span class="sxs-lookup"><span data-stu-id="01215-214">Property</span></span> | <span data-ttu-id="01215-215">Opis</span><span class="sxs-lookup"><span data-stu-id="01215-215">Description</span></span> | <span data-ttu-id="01215-216">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="01215-216">Allowed values</span></span> | <span data-ttu-id="01215-217">Wymagane</span><span class="sxs-lookup"><span data-stu-id="01215-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="01215-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="01215-218">writeBatchTimeout</span></span> |<span data-ttu-id="01215-219">Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu.</span><span class="sxs-lookup"><span data-stu-id="01215-219">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="01215-220">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="01215-220">timespan</span></span><br/><br/> <span data-ttu-id="01215-221">Przykład: 00:30:00 (30 minut).</span><span class="sxs-lookup"><span data-stu-id="01215-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="01215-222">Nie</span><span class="sxs-lookup"><span data-stu-id="01215-222">No</span></span> |
| <span data-ttu-id="01215-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="01215-223">writeBatchSize</span></span> |<span data-ttu-id="01215-224">Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="01215-224">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="01215-225">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="01215-225">Integer (number of rows)</span></span> |<span data-ttu-id="01215-226">Nie (domyślne: 100)</span><span class="sxs-lookup"><span data-stu-id="01215-226">No (default: 100)</span></span> |
| <span data-ttu-id="01215-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="01215-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="01215-228">Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="01215-228">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="01215-229">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="01215-229">A query statement.</span></span> |<span data-ttu-id="01215-230">Nie</span><span class="sxs-lookup"><span data-stu-id="01215-230">No</span></span> |
| <span data-ttu-id="01215-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="01215-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="01215-232">Określ nazwę kolumny toofill działanie kopiowania identyfikatorem wycinek automatycznie generowane, która jest używana tooclean zapasowych określonych wycinek czas ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="01215-232">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="01215-233">Nazwa kolumny kolumnę o typie danych binary(32).</span><span class="sxs-lookup"><span data-stu-id="01215-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="01215-234">Nie</span><span class="sxs-lookup"><span data-stu-id="01215-234">No</span></span> |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a><span data-ttu-id="01215-235">Przykłady JSON do kopiowania tooand danych z bazy danych Oracle</span><span class="sxs-lookup"><span data-stu-id="01215-235">JSON examples for copying data tooand from Oracle database</span></span>
<span data-ttu-id="01215-236">Witaj poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="01215-236">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="01215-237">Przedstawiają sposób toocopy danych z / tooan Oracle bazy danych do/z magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="01215-237">They show how toocopy data from/tooan Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="01215-238">Jednak dane mogą być tooany skopiowanych z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="01215-238">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a><span data-ttu-id="01215-239">Przykład: Kopiowanie danych z programu Oracle tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="01215-239">Example: Copy data from Oracle tooAzure Blob</span></span>

<span data-ttu-id="01215-240">przykład Witaj ma hello następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="01215-240">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="01215-241">Połączonej usługi typu [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="01215-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="01215-242">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="01215-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="01215-243">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="01215-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="01215-244">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="01215-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="01215-245">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) jako źródło i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) jako obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="01215-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="01215-246">przykład Witaj co godzinę kopiuje dane z tabeli w obiekcie blob tooa bazy danych Oracle lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="01215-246">hello sample copies data from a table in an on-premises Oracle database tooa blob hourly.</span></span> <span data-ttu-id="01215-247">Aby uzyskać więcej informacji na różne właściwości używane w przykładowym hello dokumentacji w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="01215-247">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="01215-248">**Oracle połączone usługi:**</span><span class="sxs-lookup"><span data-stu-id="01215-248">**Oracle linked service:**</span></span>

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

<span data-ttu-id="01215-249">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="01215-249">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="01215-250">**Wejściowy zestaw danych Oracle:**</span><span class="sxs-lookup"><span data-stu-id="01215-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="01215-251">przykład Witaj przyjęto założenie, utworzono tabelę "MyTable" w oprogramowaniu Oracle i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="01215-251">hello sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="01215-252">Ustawienie "external": "prawda" informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="01215-252">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="01215-253">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="01215-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="01215-254">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="01215-254">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="01215-255">Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="01215-255">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="01215-256">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="01215-256">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="01215-257">**W potoku z działania kopiowania:**</span><span class="sxs-lookup"><span data-stu-id="01215-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="01215-258">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="01215-258">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="01215-259">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**OracleSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="01215-259">In hello pipeline JSON definition, hello **source** type is set too**OracleSource** and **sink** type is set too**BlobSink**.</span></span>  <span data-ttu-id="01215-260">Zapytanie SQL Hello określony za pomocą **oracleReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="01215-260">hello SQL query specified with **oracleReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-toooracle"></a><span data-ttu-id="01215-261">Przykład: Kopiowanie danych z tooOracle obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="01215-261">Example: Copy data from Azure Blob tooOracle</span></span>
<span data-ttu-id="01215-262">W tym przykładzie pokazano sposób toocopy danych z magazynu obiektów Blob Azure tooan lokalnej bazy danych programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="01215-262">This sample shows how toocopy data from an Azure Blob Storage tooan on-premises Oracle database.</span></span> <span data-ttu-id="01215-263">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="01215-263">However, data can be copied **directly** from any of hello sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="01215-264">przykład Witaj ma hello następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="01215-264">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="01215-265">Połączonej usługi typu [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="01215-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="01215-266">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="01215-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="01215-267">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="01215-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="01215-268">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="01215-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="01215-269">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) jako źródło [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) jako obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="01215-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="01215-270">przykład Witaj kopiuje dane z tabeli tooa obiektów blob w lokalną bazą danych Oracle co godzinę.</span><span class="sxs-lookup"><span data-stu-id="01215-270">hello sample copies data from a blob tooa table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="01215-271">Aby uzyskać więcej informacji na różne właściwości używane w przykładowym hello dokumentacji w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="01215-271">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="01215-272">**Oracle połączone usługi:**</span><span class="sxs-lookup"><span data-stu-id="01215-272">**Oracle linked service:**</span></span>
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

<span data-ttu-id="01215-273">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="01215-273">**Azure Blob storage linked service:**</span></span>
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

<span data-ttu-id="01215-274">**Azure wejściowego zestawu danych obiektów Blob**</span><span class="sxs-lookup"><span data-stu-id="01215-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="01215-275">Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="01215-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="01215-276">Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="01215-276">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="01215-277">Ścieżka folderu Hello korzysta rok, miesiąc i dzień część czas rozpoczęcia hello, a nazwa pliku hello część hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="01215-277">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="01215-278">"external": ustawienie "prawda" hello usługi fabryka danych informuje, że ta tabela zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="01215-278">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="01215-279">**Oracle wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="01215-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="01215-280">przykład Witaj przyjęto założenie, że w Oracle utworzono tabelę "MyTable".</span><span class="sxs-lookup"><span data-stu-id="01215-280">hello sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="01215-281">Utwórz tabelę hello w oprogramowaniu Oracle z hello taką samą liczbę kolumn, zgodnie z oczekiwaniami toocontain pliku Blob CSV hello.</span><span class="sxs-lookup"><span data-stu-id="01215-281">Create hello table in Oracle with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="01215-282">Dodawaniu nowych wierszy tabeli toohello co godzinę.</span><span class="sxs-lookup"><span data-stu-id="01215-282">New rows are added toohello table every hour.</span></span>

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

<span data-ttu-id="01215-283">**W potoku z działania kopiowania:**</span><span class="sxs-lookup"><span data-stu-id="01215-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="01215-284">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="01215-284">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="01215-285">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i hello **zbiornika** typu ustawiono zbyt**OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="01215-285">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and hello **sink** type is set too**OracleSink**.</span></span>  

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


## <a name="troubleshooting-tips"></a><span data-ttu-id="01215-286">Wskazówki dotyczące rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="01215-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="01215-287">Problem 1: Dostawca danych programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="01215-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="01215-288">Zobacz następujące hello **komunikat o błędzie**:</span><span class="sxs-lookup"><span data-stu-id="01215-288">You see hello following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="01215-289">**Możliwe przyczyny:**</span><span class="sxs-lookup"><span data-stu-id="01215-289">**Possible causes:**</span></span>

1. <span data-ttu-id="01215-290">Witaj .NET Framework Data Provider for Oracle nie został zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="01215-290">hello .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="01215-291">.NET Framework Data Provider for Oracle Hello został zainstalowany too.NET Framework 2.0 i nie został znaleziony w folderach hello programu .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="01215-291">hello .NET Framework Data Provider for Oracle was installed too.NET Framework 2.0 and is not found in hello .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="01215-292">**Rozdzielczość/obejście problemu:**</span><span class="sxs-lookup"><span data-stu-id="01215-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="01215-293">Jeśli nie zainstalowano hello dostawcy .NET dla Oracle, [go zainstalować](http://www.oracle.com/technetwork/topics/dotnet/downloads/) i ponów próbę hello scenariusza.</span><span class="sxs-lookup"><span data-stu-id="01215-293">If you haven't installed hello .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry hello scenario.</span></span>
2. <span data-ttu-id="01215-294">Jeśli otrzymasz komunikat o błędzie hello nawet po zainstalowaniu dostawcy hello hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="01215-294">If you get hello error message even after installing hello provider, do hello following steps:</span></span>
   1. <span data-ttu-id="01215-295">Otwórz konfiguracji komputera programu .NET 2.0 z folderu hello: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="01215-295">Open machine config of .NET 2.0 from hello folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="01215-296">Wyszukaj **dostawca danych programu Oracle dla platformy .NET**, i powinno być możliwe toofind wpis pokazane na powitania po próbki w **system.dane** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Dostawca danych programu oracle dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="01215-296">Search for **Oracle Data Provider for .NET**, and you should be able toofind an entry as shown in hello following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="01215-297">”</span><span class="sxs-lookup"><span data-stu-id="01215-297">”</span></span>
3. <span data-ttu-id="01215-298">Skopiuj ten plik machine.config toohello wpis w hello następującego folderu v4.0: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config i too4.xxx.x.x wersji hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="01215-298">Copy this entry toohello machine.config file in hello following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change hello version too4.xxx.x.x.</span></span>
4. <span data-ttu-id="01215-299">Zainstaluj "\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll < ścieżka instalacji ODP.NET >" na powitania globalnej pamięci podręcznej zestawów (GAC), uruchamiając `gacutil /i [provider path]`. ## porady dotyczące rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="01215-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into hello global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="01215-300">Problem 2: formatowanie daty/godziny</span><span class="sxs-lookup"><span data-stu-id="01215-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="01215-301">Zobacz następujące hello **komunikat o błędzie**:</span><span class="sxs-lookup"><span data-stu-id="01215-301">You see hello following **error message**:</span></span>

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="01215-302">**Rozdzielczość/obejście problemu:**</span><span class="sxs-lookup"><span data-stu-id="01215-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="01215-303">Ciąg zapytania hello tooadjust może być konieczne w przypadku Twojego działania kopiowania oparte na konfiguracji daty w bazie danych programu Oracle, jak pokazano poniżej hello próbki (przy użyciu funkcji to_date hello):</span><span class="sxs-lookup"><span data-stu-id="01215-303">You may need tooadjust hello query string in your copy activity based on how dates are configured in your Oracle database, as shown in hello following sample (using hello to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="01215-304">Mapowanie typu dla Oracle</span><span class="sxs-lookup"><span data-stu-id="01215-304">Type mapping for Oracle</span></span>
<span data-ttu-id="01215-305">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu działanie kopiowania przeprowadza automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="01215-305">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="01215-306">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="01215-306">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="01215-307">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="01215-307">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="01215-308">Podczas przenoszenia danych z bazy danych Oracle, następujące mapowania hello są używane z too.NET typu danych Oracle i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="01215-308">When moving data from Oracle, hello following mappings are used from Oracle data type too.NET type and vice versa.</span></span>

| <span data-ttu-id="01215-309">Typ danych Oracle</span><span class="sxs-lookup"><span data-stu-id="01215-309">Oracle data type</span></span> | <span data-ttu-id="01215-310">Typ danych .NET framework</span><span class="sxs-lookup"><span data-stu-id="01215-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="01215-311">BPLIK</span><span class="sxs-lookup"><span data-stu-id="01215-311">BFILE</span></span> |<span data-ttu-id="01215-312">Byte]</span><span class="sxs-lookup"><span data-stu-id="01215-312">Byte[]</span></span> |
| <span data-ttu-id="01215-313">OBIEKT BLOB</span><span class="sxs-lookup"><span data-stu-id="01215-313">BLOB</span></span> |<span data-ttu-id="01215-314">Byte]</span><span class="sxs-lookup"><span data-stu-id="01215-314">Byte[]</span></span> |
| <span data-ttu-id="01215-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="01215-315">CHAR</span></span> |<span data-ttu-id="01215-316">Ciąg</span><span class="sxs-lookup"><span data-stu-id="01215-316">String</span></span> |
| <span data-ttu-id="01215-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="01215-317">CLOB</span></span> |<span data-ttu-id="01215-318">Ciąg</span><span class="sxs-lookup"><span data-stu-id="01215-318">String</span></span> |
| <span data-ttu-id="01215-319">DATA</span><span class="sxs-lookup"><span data-stu-id="01215-319">DATE</span></span> |<span data-ttu-id="01215-320">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="01215-320">DateTime</span></span> |
| <span data-ttu-id="01215-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="01215-321">FLOAT</span></span> |<span data-ttu-id="01215-322">Decimal, ciąg (jeśli precyzja > 28)</span><span class="sxs-lookup"><span data-stu-id="01215-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="01215-323">LICZBA CAŁKOWITA</span><span class="sxs-lookup"><span data-stu-id="01215-323">INTEGER</span></span> |<span data-ttu-id="01215-324">Decimal, ciąg (jeśli precyzja > 28)</span><span class="sxs-lookup"><span data-stu-id="01215-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="01215-325">INTERWAŁ tooMONTH roku</span><span class="sxs-lookup"><span data-stu-id="01215-325">INTERVAL YEAR tooMONTH</span></span> |<span data-ttu-id="01215-326">Int32</span><span class="sxs-lookup"><span data-stu-id="01215-326">Int32</span></span> |
| <span data-ttu-id="01215-327">INTERWAŁ tooSECOND dnia</span><span class="sxs-lookup"><span data-stu-id="01215-327">INTERVAL DAY tooSECOND</span></span> |<span data-ttu-id="01215-328">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="01215-328">TimeSpan</span></span> |
| <span data-ttu-id="01215-329">DŁUGA</span><span class="sxs-lookup"><span data-stu-id="01215-329">LONG</span></span> |<span data-ttu-id="01215-330">Ciąg</span><span class="sxs-lookup"><span data-stu-id="01215-330">String</span></span> |
| <span data-ttu-id="01215-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="01215-331">LONG RAW</span></span> |<span data-ttu-id="01215-332">Byte]</span><span class="sxs-lookup"><span data-stu-id="01215-332">Byte[]</span></span> |
| <span data-ttu-id="01215-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="01215-333">NCHAR</span></span> |<span data-ttu-id="01215-334">Ciąg</span><span class="sxs-lookup"><span data-stu-id="01215-334">String</span></span> |
| <span data-ttu-id="01215-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="01215-335">NCLOB</span></span> |<span data-ttu-id="01215-336">Ciąg</span><span class="sxs-lookup"><span data-stu-id="01215-336">String</span></span> |
| <span data-ttu-id="01215-337">NUMER</span><span class="sxs-lookup"><span data-stu-id="01215-337">NUMBER</span></span> |<span data-ttu-id="01215-338">Decimal, ciąg (jeśli precyzja > 28)</span><span class="sxs-lookup"><span data-stu-id="01215-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="01215-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="01215-339">NVARCHAR2</span></span> |<span data-ttu-id="01215-340">Ciąg</span><span class="sxs-lookup"><span data-stu-id="01215-340">String</span></span> |
| <span data-ttu-id="01215-341">NIEPRZETWORZONE</span><span class="sxs-lookup"><span data-stu-id="01215-341">RAW</span></span> |<span data-ttu-id="01215-342">Byte]</span><span class="sxs-lookup"><span data-stu-id="01215-342">Byte[]</span></span> |
| <span data-ttu-id="01215-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="01215-343">ROWID</span></span> |<span data-ttu-id="01215-344">Ciąg</span><span class="sxs-lookup"><span data-stu-id="01215-344">String</span></span> |
| <span data-ttu-id="01215-345">ZNACZNIK CZASU</span><span class="sxs-lookup"><span data-stu-id="01215-345">TIMESTAMP</span></span> |<span data-ttu-id="01215-346">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="01215-346">DateTime</span></span> |
| <span data-ttu-id="01215-347">SYGNATURA CZASOWA Z LOKALNEJ STREFIE CZASOWEJ</span><span class="sxs-lookup"><span data-stu-id="01215-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="01215-348">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="01215-348">DateTime</span></span> |
| <span data-ttu-id="01215-349">SYGNATURA CZASOWA ZE STREFĄ CZASOWĄ</span><span class="sxs-lookup"><span data-stu-id="01215-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="01215-350">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="01215-350">DateTime</span></span> |
| <span data-ttu-id="01215-351">LICZBA CAŁKOWITA BEZ ZNAKU</span><span class="sxs-lookup"><span data-stu-id="01215-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="01215-352">Liczba</span><span class="sxs-lookup"><span data-stu-id="01215-352">Number</span></span> |
| <span data-ttu-id="01215-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="01215-353">VARCHAR2</span></span> |<span data-ttu-id="01215-354">Ciąg</span><span class="sxs-lookup"><span data-stu-id="01215-354">String</span></span> |
| <span data-ttu-id="01215-355">XML</span><span class="sxs-lookup"><span data-stu-id="01215-355">XML</span></span> |<span data-ttu-id="01215-356">Ciąg</span><span class="sxs-lookup"><span data-stu-id="01215-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="01215-357">Typ danych **tooMONTH roku INTERWAŁ** i **tooSECOND dzień INTERWAŁ** nie są obsługiwane, gdy za pomocą sterownika Microsoft.</span><span class="sxs-lookup"><span data-stu-id="01215-357">Data type **INTERVAL YEAR tooMONTH** and **INTERVAL DAY tooSECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="01215-358">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="01215-358">Map source toosink columns</span></span>
<span data-ttu-id="01215-359">toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="01215-359">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="01215-360">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="01215-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="01215-361">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="01215-361">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="01215-362">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="01215-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="01215-363">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="01215-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="01215-364">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="01215-364">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="01215-365">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="01215-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="01215-366">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="01215-366">Performance and Tuning</span></span>
<span data-ttu-id="01215-367">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="01215-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
