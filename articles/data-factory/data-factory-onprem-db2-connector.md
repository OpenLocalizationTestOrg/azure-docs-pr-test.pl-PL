---
title: "aaaMove danych z bazy danych DB2 przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomove dane z bazy danych DB2 lokalnej bazy danych przy użyciu działania kopiowania fabryki danych Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="2d338-103">Przenieść dane z bazy danych DB2 za pomocą działania kopiowania fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="2d338-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="2d338-104">W tym artykule opisano używania działania kopiowania fabryki danych Azure toocopy danych z magazynu danych tooa lokalnej bazy danych DB2 bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2d338-104">This article describes how you can use Copy Activity in Azure Data Factory toocopy data from an on-premises DB2 database tooa data store.</span></span> <span data-ttu-id="2d338-105">Możesz skopiować magazynu tooany danych, który jest wymieniony jako obsługiwany zbiornika w hello [działań przepływu danych fabryki danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2d338-105">You can copy data tooany store that is listed as a supported sink in hello [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="2d338-106">W tym temacie opiera się na powitania artykułu fabryki danych, które zawiera omówienie przepływu danych za pomocą działania kopiowania i wyświetla kombinacje magazynu danych hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="2d338-106">This topic builds on hello Data Factory article, which presents an overview of data movement by using Copy Activity and lists hello supported data store combinations.</span></span> 

<span data-ttu-id="2d338-107">Fabryka danych aktualnie obsługuje tylko przenoszenia danych z tooa bazy danych DB2 [obsługiwanych ujścia magazynu danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2d338-107">Data Factory currently supports only moving data from a DB2 database tooa [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="2d338-108">Przenoszenie danych z innych danych przechowuje tooa bazy danych DB2 bazy danych nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="2d338-108">Moving data from other data stores tooa DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d338-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2d338-109">Prerequisites</span></span>
<span data-ttu-id="2d338-110">Fabryka danych obsługuje połączenia bazy danych DB2 lokalnie tooan przy użyciu hello [brama zarządzania danymi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="2d338-110">Data Factory supports connecting tooan on-premises DB2 database by using hello [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="2d338-111">Aby uzyskać instrukcje krok po kroku tooset zapasową hello bramy danych w potoku toomove danych, zobacz hello [przenoszenia danych z lokalnego toocloud](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2d338-111">For step-by-step instructions tooset up hello gateway data pipeline toomove your data, see hello [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="2d338-112">Wymagana jest brama, nawet jeśli hello bazy danych DB2 znajduje się na maszynie Wirtualnej Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="2d338-112">A gateway is required even if hello DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="2d338-113">Możesz zainstalować bramę hello na powitania tej samej IaaS maszyny Wirtualnej jako hello magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="2d338-113">You can install hello gateway on hello same IaaS VM as hello data store.</span></span> <span data-ttu-id="2d338-114">Jeśli brama hello można połączyć z usługą toohello bazy danych, możesz zainstalować hello bramę na innej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2d338-114">If hello gateway can connect toohello database, you can install hello gateway on a different VM.</span></span>

<span data-ttu-id="2d338-115">Brama zarządzania danymi Hello oferuje wbudowane sterownik bazy danych DB2, więc nie zostanie toomanually zainstalować sterownik toocopy danych z bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="2d338-115">hello data management gateway provides a built-in DB2 driver, so you don't need toomanually install a driver toocopy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="2d338-116">Aby uzyskać wskazówki dotyczące rozwiązywania problemów dotyczących połączenia i problemy bramy, zobacz hello [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2d338-116">For tips on troubleshooting connection and gateway issues, see hello [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="2d338-117">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="2d338-117">Supported versions</span></span>
<span data-ttu-id="2d338-118">Łącznik Hello DB2 fabryki danych obsługuje hello IBM DB2 platform i wersje Menedżera dostępu programu SQL Distributed relacyjnej bazy danych architektury DRDA () w wersji 9, 10 lub 11:</span><span class="sxs-lookup"><span data-stu-id="2d338-118">hello Data Factory DB2 connector supports hello following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="2d338-119">IBM DB2 w wersji 11.1 z/OS</span><span class="sxs-lookup"><span data-stu-id="2d338-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="2d338-120">IBM DB2 w wersji 10.1 z/OS</span><span class="sxs-lookup"><span data-stu-id="2d338-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="2d338-121">IBM DB2 (AS400) i wersji 7.2</span><span class="sxs-lookup"><span data-stu-id="2d338-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="2d338-122">IBM DB2 i (AS400) w wersji 7.1</span><span class="sxs-lookup"><span data-stu-id="2d338-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="2d338-123">IBM DB2 dla systemu Linux, UNIX i systemu Windows (LUW) w wersji 11</span><span class="sxs-lookup"><span data-stu-id="2d338-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="2d338-124">IBM DB2 dla LUW wersji 10.5</span><span class="sxs-lookup"><span data-stu-id="2d338-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="2d338-125">IBM DB2 dla LUW wersji 10.1</span><span class="sxs-lookup"><span data-stu-id="2d338-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="2d338-126">Jeśli zostanie wyświetlony komunikat o błędzie powitania "hello pakietu odpowiedniego tooan SQL instrukcji żądania wykonania nie został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="2d338-126">If you receive hello error message "hello package corresponding tooan SQL statement execution request was not found.</span></span> <span data-ttu-id="2d338-127">SQLSTATE 51002 SQLCODE =-805, = "hello przyczyna jest potrzebny pakiet nie został utworzony dla zwykłego użytkownika hello na powitania systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2d338-127">SQLSTATE=51002 SQLCODE=-805," hello reason is a necessary package is not created for hello normal user on hello OS.</span></span> <span data-ttu-id="2d338-128">tooresolve ten problem, wykonaj te instrukcje dla danego typu serwera bazy danych DB2:</span><span class="sxs-lookup"><span data-stu-id="2d338-128">tooresolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="2d338-129">Bazy danych DB2 dla i (AS400): umożliwia użytkownikowi zasilania utworzyć kolekcję hello na powitania zwykłego użytkownika przed uruchomieniem działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2d338-129">DB2 for i (AS400): Let a power user create hello collection for hello normal user before running Copy Activity.</span></span> <span data-ttu-id="2d338-130">toocreate hello kolekcji, użyj polecenia hello:`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="2d338-130">toocreate hello collection, use hello command: `create collection <username>`</span></span>
> - <span data-ttu-id="2d338-131">Bazy danych DB2 z/OS lub LUW: Użyj konta wysokiego poziomu uprawnień — użytkownik zaawansowany lub administrator urzędów pakietu i powiązania, BINDADD, uprawnienia EXECUTE tooPUBLIC — toorun hello raz kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2d338-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE tooPUBLIC permissions--toorun hello copy once.</span></span> <span data-ttu-id="2d338-132">Witaj potrzebny pakiet jest tworzony automatycznie podczas kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="2d338-132">hello necessary package is automatically created during hello copy.</span></span> <span data-ttu-id="2d338-133">Potem można przełączać wstecz toohello zwykłego użytkownika dla sekwencji kolejnych kopii.</span><span class="sxs-lookup"><span data-stu-id="2d338-133">Afterward, you can switch back toohello normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2d338-134">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="2d338-134">Getting started</span></span>
<span data-ttu-id="2d338-135">Można utworzyć potoku o toomove działania kopiowania danych z magazynu danych programu DB2 lokalnie przy użyciu różnych narzędzi i interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="2d338-135">You can create a pipeline with a copy activity toomove data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="2d338-136">Witaj Najprostszym sposobem toocreate potoku jest hello toouse kreatora kopiowania fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="2d338-136">hello easiest way toocreate a pipeline is toouse hello Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="2d338-137">Szybkie przewodnik dotyczący tworzenia za pomocą Kreatora kopiowania hello potoku, zobacz hello [samouczek: tworzenie potoku za pomocą Kreatora kopiowania hello](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2d338-137">For a quick walkthrough on creating a pipeline by using hello Copy Wizard, see hello [Tutorial: Create a pipeline by using hello Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="2d338-138">Można również użyć narzędzia toocreate potoku, w tym hello portalu Azure, programu Visual Studio, programu Azure PowerShell, usługi Azure Resource Manager szablonu, hello interfejs API .NET i hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="2d338-138">You can also use tools toocreate a pipeline, including hello Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, hello .NET API, and hello REST API.</span></span> <span data-ttu-id="2d338-139">Aby uzyskać instrukcje krok po kroku toocreate potoku z działaniem kopiowania, zobacz hello [samouczek działanie kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="2d338-139">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="2d338-140">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="2d338-140">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="2d338-141">Tworzenie fabryki danych tooyour magazynów danych wejściowych i wyjściowych toolink połączonych usług.</span><span class="sxs-lookup"><span data-stu-id="2d338-141">Create linked services toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="2d338-142">Tworzenie zestawów danych toorepresent w danych wejściowych i wyjściowych danych dla operacji kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="2d338-142">Create datasets toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="2d338-143">Utworzyć potok aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="2d338-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2d338-144">Używania hello kreatora kopiowania, definicje JSON hello fabryki danych połączone usługi, zestawy danych i jednostek potoku są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="2d338-144">When you use hello Copy Wizard, JSON definitions for hello Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="2d338-145">Użycie narzędzia lub interfejsów API (z wyjątkiem hello interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello hello jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="2d338-145">When you use tools or APIs (except hello .NET API), you define hello Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="2d338-146">Witaj [przykład JSON: kopiowanie danych z bazy danych DB2 tooAzure magazynu obiektów Blob](#json-example-copy-data-from-db2-to-azure-blob) zawiera definicje JSON hello hello jednostek fabryki danych, które są używane toocopy danych z magazynu danych programu DB2 lokalnie.</span><span class="sxs-lookup"><span data-stu-id="2d338-146">hello [JSON example: Copy data from DB2 tooAzure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows hello JSON definitions for hello Data Factory entities that are used toocopy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="2d338-147">Witaj następujące sekcje zawierają szczegółowe informacje o hello właściwości JSON, które są używane toodefine hello fabryki danych podmiotów, które są określone tooa bazy danych DB2 magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="2d338-147">hello following sections provide details about hello JSON properties that are used toodefine hello Data Factory entities that are specific tooa DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="2d338-148">Właściwości usługi połączone bazy danych DB2</span><span class="sxs-lookup"><span data-stu-id="2d338-148">DB2 linked service properties</span></span>
<span data-ttu-id="2d338-149">Witaj w poniższej tabeli wymieniono właściwości JSON hello, które są określone tooa bazy danych DB2 połączone usługi.</span><span class="sxs-lookup"><span data-stu-id="2d338-149">hello following table lists hello JSON properties that are specific tooa DB2 linked service.</span></span>

| <span data-ttu-id="2d338-150">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2d338-150">Property</span></span> | <span data-ttu-id="2d338-151">Opis</span><span class="sxs-lookup"><span data-stu-id="2d338-151">Description</span></span> | <span data-ttu-id="2d338-152">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2d338-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2d338-153">**Typ**</span><span class="sxs-lookup"><span data-stu-id="2d338-153">**type**</span></span> |<span data-ttu-id="2d338-154">Ta właściwość musi być ustawiona zbyt**OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="2d338-154">This property must be set too**OnPremisesDB2**.</span></span> |<span data-ttu-id="2d338-155">Tak</span><span class="sxs-lookup"><span data-stu-id="2d338-155">Yes</span></span> |
| <span data-ttu-id="2d338-156">**Serwer**</span><span class="sxs-lookup"><span data-stu-id="2d338-156">**server**</span></span> |<span data-ttu-id="2d338-157">Nazwa powitania serwera hello bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="2d338-157">hello name of hello DB2 server.</span></span> |<span data-ttu-id="2d338-158">Tak</span><span class="sxs-lookup"><span data-stu-id="2d338-158">Yes</span></span> |
| <span data-ttu-id="2d338-159">**bazy danych**</span><span class="sxs-lookup"><span data-stu-id="2d338-159">**database**</span></span> |<span data-ttu-id="2d338-160">Nazwa Hello hello bazy danych DB2 bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2d338-160">hello name of hello DB2 database.</span></span> |<span data-ttu-id="2d338-161">Tak</span><span class="sxs-lookup"><span data-stu-id="2d338-161">Yes</span></span> |
| <span data-ttu-id="2d338-162">**Schemat**</span><span class="sxs-lookup"><span data-stu-id="2d338-162">**schema**</span></span> |<span data-ttu-id="2d338-163">Nazwa Hello hello schematu w bazie danych hello bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="2d338-163">hello name of hello schema in hello DB2 database.</span></span> <span data-ttu-id="2d338-164">Ta właściwość jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="2d338-164">This property is case-sensitive.</span></span> |<span data-ttu-id="2d338-165">Nie</span><span class="sxs-lookup"><span data-stu-id="2d338-165">No</span></span> |
| <span data-ttu-id="2d338-166">**Typ authenticationType**</span><span class="sxs-lookup"><span data-stu-id="2d338-166">**authenticationType**</span></span> |<span data-ttu-id="2d338-167">Hello typ uwierzytelniania, który jest używany tooconnect toohello bazy danych DB2 w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="2d338-167">hello type of authentication that is used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="2d338-168">Witaj możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="2d338-168">hello possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="2d338-169">Tak</span><span class="sxs-lookup"><span data-stu-id="2d338-169">Yes</span></span> |
| <span data-ttu-id="2d338-170">**Nazwa użytkownika**</span><span class="sxs-lookup"><span data-stu-id="2d338-170">**username**</span></span> |<span data-ttu-id="2d338-171">Nazwa Hello hello konta użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="2d338-171">hello name for hello user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="2d338-172">Nie</span><span class="sxs-lookup"><span data-stu-id="2d338-172">No</span></span> |
| <span data-ttu-id="2d338-173">**hasło**</span><span class="sxs-lookup"><span data-stu-id="2d338-173">**password**</span></span> |<span data-ttu-id="2d338-174">Hello hasło dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="2d338-174">hello password for hello user account.</span></span> |<span data-ttu-id="2d338-175">Nie</span><span class="sxs-lookup"><span data-stu-id="2d338-175">No</span></span> |
| <span data-ttu-id="2d338-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="2d338-176">**gatewayName**</span></span> |<span data-ttu-id="2d338-177">Nazwa Hello hello bramy, która hello usługi fabryka danych należy używać tooconnect toohello lokalną bazą danych DB2.</span><span class="sxs-lookup"><span data-stu-id="2d338-177">hello name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="2d338-178">Tak</span><span class="sxs-lookup"><span data-stu-id="2d338-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="2d338-179">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="2d338-179">Dataset properties</span></span>
<span data-ttu-id="2d338-180">Listę hello sekcje i właściwości, które są dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2d338-180">For a list of hello sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2d338-181">Sekcje, takich jak **struktury**, **dostępności**i hello **zasad** dla zestawu danych JSON, są podobne dla wszystkich typów obiektów dataset (Azure SQL, magazynem Azure Blob, tabel Azure Magazyn i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="2d338-181">Sections, such as **structure**, **availability**, and hello **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="2d338-182">Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="2d338-182">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="2d338-183">Witaj **typeProperties** sekcja dla zestawu danych typu **RelationalTable**, które dotyczą hello bazy danych DB2 zestawu danych, hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="2d338-183">hello **typeProperties** section for a dataset of type **RelationalTable**, which includes hello DB2 dataset, has hello following property:</span></span>

| <span data-ttu-id="2d338-184">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2d338-184">Property</span></span> | <span data-ttu-id="2d338-185">Opis</span><span class="sxs-lookup"><span data-stu-id="2d338-185">Description</span></span> | <span data-ttu-id="2d338-186">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2d338-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2d338-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="2d338-187">**tableName**</span></span> |<span data-ttu-id="2d338-188">Nazwa Hello hello tabeli w wystąpieniu bazy danych hello DB2, który hello połączonej usługi odwołuje się do.</span><span class="sxs-lookup"><span data-stu-id="2d338-188">hello name of hello table in hello DB2 database instance that hello linked service refers to.</span></span> <span data-ttu-id="2d338-189">Ta właściwość jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="2d338-189">This property is case-sensitive.</span></span> |<span data-ttu-id="2d338-190">Nie (jeśli hello **zapytania** właściwości działania kopiowania typu **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="2d338-190">No (if hello **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="2d338-191">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="2d338-191">Copy Activity properties</span></span>
<span data-ttu-id="2d338-192">Listę hello sekcje i właściwości, które są dostępne do definiowania działania kopiowania, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2d338-192">For a list of hello sections and properties that are available for defining copy activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2d338-193">Kopiuj właściwości działania, takie jak **nazwa**, **opis**, **dane wejściowe** tabeli, **generuje** tabeli, i **zasad**, są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="2d338-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="2d338-194">Witaj właściwości, które są dostępne w hello **typeProperties** sekcji hello działanie dla każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="2d338-194">hello properties that are available in hello **typeProperties** section of hello activity for each activity type.</span></span> <span data-ttu-id="2d338-195">Dla działania kopiowania właściwości hello zależy od hello typy źródeł danych i sink.</span><span class="sxs-lookup"><span data-stu-id="2d338-195">For Copy Activity, hello properties vary depending on hello types of data sources and sinks.</span></span>

<span data-ttu-id="2d338-196">Dla działania kopiowania, gdy źródłem hello jest typu **RelationalSource** (która obejmuje bazy danych DB2), hello następujące właściwości są dostępne w hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="2d338-196">For Copy Activity, when hello source is of type **RelationalSource** (which includes DB2), hello following properties are available in hello **typeProperties** section:</span></span>

| <span data-ttu-id="2d338-197">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2d338-197">Property</span></span> | <span data-ttu-id="2d338-198">Opis</span><span class="sxs-lookup"><span data-stu-id="2d338-198">Description</span></span> | <span data-ttu-id="2d338-199">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="2d338-199">Allowed values</span></span> | <span data-ttu-id="2d338-200">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2d338-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2d338-201">**zapytania**</span><span class="sxs-lookup"><span data-stu-id="2d338-201">**query**</span></span> |<span data-ttu-id="2d338-202">Użyj hello zapytanie niestandardowe tooread hello danych.</span><span class="sxs-lookup"><span data-stu-id="2d338-202">Use hello custom query tooread hello data.</span></span> |<span data-ttu-id="2d338-203">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="2d338-203">SQL query string.</span></span> <span data-ttu-id="2d338-204">Na przykład: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="2d338-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="2d338-205">Nie (jeśli hello **tableName** określono właściwości zestawu danych)</span><span class="sxs-lookup"><span data-stu-id="2d338-205">No (if hello **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="2d338-206">Nazwy schematu i tabeli jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="2d338-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="2d338-207">W instrukcji zapytania hello, ujmij nazw właściwości, za pomocą "" (podwójne cudzysłowy).</span><span class="sxs-lookup"><span data-stu-id="2d338-207">In hello query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="2d338-208">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2d338-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a><span data-ttu-id="2d338-209">Przykład JSON: kopiowanie danych z bazy danych DB2 tooAzure magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="2d338-209">JSON example: Copy data from DB2 tooAzure Blob storage</span></span>
<span data-ttu-id="2d338-210">W poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu hello można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2d338-210">This example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2d338-211">przykład Witaj pokazuje, jak toocopy dane z bazy danych DB2 bazy danych magazynu tooBlob.</span><span class="sxs-lookup"><span data-stu-id="2d338-211">hello example shows you how toocopy data from a DB2 database tooBlob storage.</span></span> <span data-ttu-id="2d338-212">Jednak możesz skopiować dane zbyt[wszystkie obsługiwane dane przechowywane typ ujścia](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="2d338-212">However, data can be copied too[any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="2d338-213">przykład Witaj ma powitania po jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="2d338-213">hello sample has hello following Data Factory entities:</span></span>

- <span data-ttu-id="2d338-214">Bazy danych DB2 połączonej usługi typu [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="2d338-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="2d338-215">Połączonej usługi typu magazynu obiektów Blob platformy Azure [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="2d338-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="2d338-216">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="2d338-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="2d338-217">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="2d338-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="2d338-218">A [potoku](data-factory-create-pipelines.md) z działania kopiowania, który używa hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) właściwości</span><span class="sxs-lookup"><span data-stu-id="2d338-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="2d338-219">przykład Witaj co godzinę kopiuje dane z wyniku kwerendy w tooan bazy danych DB2 obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2d338-219">hello sample copies data from a query result in a DB2 database tooan Azure blob hourly.</span></span> <span data-ttu-id="2d338-220">Witaj JSON właściwości, które są używane w przykładowym hello są opisane w hello sekcjach hello jednostki definicje.</span><span class="sxs-lookup"><span data-stu-id="2d338-220">hello JSON properties that are used in hello sample are described in hello sections that follow hello entity definitions.</span></span>

<span data-ttu-id="2d338-221">Pierwszym krokiem Zainstaluj i skonfiguruj bramę danych.</span><span class="sxs-lookup"><span data-stu-id="2d338-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="2d338-222">Instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2d338-222">Instructions are in hello [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="2d338-223">**Bazy danych DB2 połączone usługi**</span><span class="sxs-lookup"><span data-stu-id="2d338-223">**DB2 linked service**</span></span>

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="2d338-224">**Azure Blob połączoną usługą magazynu**</span><span class="sxs-lookup"><span data-stu-id="2d338-224">**Azure Blob storage linked service**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="2d338-225">**Wejściowy zestaw danych DB2**</span><span class="sxs-lookup"><span data-stu-id="2d338-225">**DB2 input dataset**</span></span>

<span data-ttu-id="2d338-226">przykład Witaj przyjęto założenie, że utworzono tabelę w bazie danych DB2 o nazwie "MyTable", która zawiera kolumnę z etykietą "timestamp" hello czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="2d338-226">hello sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for hello time series data.</span></span>

<span data-ttu-id="2d338-227">Witaj **zewnętrznych** właściwość jest ustawiona zbyt "wartość true."</span><span class="sxs-lookup"><span data-stu-id="2d338-227">hello **external** property is set too"true."</span></span> <span data-ttu-id="2d338-228">Usługi fabryka danych hello to ustawienie informuje o tym, że ten zestaw danych jest zewnętrzne toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="2d338-228">This setting informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="2d338-229">Zwróć uwagę, że hello **typu** właściwość jest ustawiona zbyt**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="2d338-229">Notice that hello **type** property is set too**RelationalTable**.</span></span>


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
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

<span data-ttu-id="2d338-230">**Azure Blob wyjściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="2d338-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="2d338-231">Dane są zapisywane nowego obiektu blob tooa co godzinę przez ustawienie hello **częstotliwość** właściwości zbyt "Hour" i hello **interwał** too1 właściwości.</span><span class="sxs-lookup"><span data-stu-id="2d338-231">Data is written tooa new blob every hour by setting hello **frequency** property too"Hour" and hello **interval** property too1.</span></span> <span data-ttu-id="2d338-232">Witaj **folderPath** właściwości dla obiektu blob hello dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="2d338-232">hello **folderPath** property for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="2d338-233">Ścieżka folderu Hello używa hello rok, miesiąc, dzień i godzinę części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="2d338-233">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="2d338-234">**Potoku dla aktywności kopiowania hello**</span><span class="sxs-lookup"><span data-stu-id="2d338-234">**Pipeline for hello copy activity**</span></span>

<span data-ttu-id="2d338-235">potok Hello zawiera działanie kopiowania, który jest skonfigurowany toouse określony wejściowych i wyjściowych zestawów danych i która jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="2d338-235">hello pipeline contains a copy activity that is configured toouse specified input and output datasets and which is scheduled toorun every hour.</span></span> <span data-ttu-id="2d338-236">W definicji JSON dla potoku hello hello, hello **źródła** typu ustawiono zbyt**RelationalSource** i hello **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2d338-236">In hello JSON definition for hello pipeline, hello **source** type is set too**RelationalSource** and hello **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="2d338-237">Zapytanie SQL Hello określone dla hello **zapytania** właściwości wybiera hello danych z tabeli "Zamówienia" hello.</span><span class="sxs-lookup"><span data-stu-id="2d338-237">hello SQL query specified for hello **query** property selects hello data from hello "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a><span data-ttu-id="2d338-238">Mapowanie typu dla bazy danych DB2</span><span class="sxs-lookup"><span data-stu-id="2d338-238">Type mapping for DB2</span></span>
<span data-ttu-id="2d338-239">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, działanie kopiowania wykonuje automatyczne konwersje typu toosink typu źródłowego za pomocą następującego rozwinięcie hello:</span><span class="sxs-lookup"><span data-stu-id="2d338-239">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type toosink type by using hello following two-step approach:</span></span>

1. <span data-ttu-id="2d338-240">Konwertować z typu .NET tooa typu natywnego źródła</span><span class="sxs-lookup"><span data-stu-id="2d338-240">Convert from a native source type tooa .NET type</span></span>
2. <span data-ttu-id="2d338-241">Konwertować z typu natywnego zbiornika tooa typu .NET</span><span class="sxs-lookup"><span data-stu-id="2d338-241">Convert from a .NET type tooa native sink type</span></span>

<span data-ttu-id="2d338-242">Hello następujące mapowania są używane, gdy działanie kopiowania konwertuje hello dane z bazy danych DB2 .NET tooa typu:</span><span class="sxs-lookup"><span data-stu-id="2d338-242">hello following mappings are used when Copy Activity converts hello data from a DB2 type tooa .NET type:</span></span>

| <span data-ttu-id="2d338-243">Typ bazy danych DB2</span><span class="sxs-lookup"><span data-stu-id="2d338-243">DB2 database type</span></span> | <span data-ttu-id="2d338-244">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="2d338-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="2d338-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="2d338-245">SmallInt</span></span> |<span data-ttu-id="2d338-246">Int16</span><span class="sxs-lookup"><span data-stu-id="2d338-246">Int16</span></span> |
| <span data-ttu-id="2d338-247">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="2d338-247">Integer</span></span> |<span data-ttu-id="2d338-248">Int32</span><span class="sxs-lookup"><span data-stu-id="2d338-248">Int32</span></span> |
| <span data-ttu-id="2d338-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="2d338-249">BigInt</span></span> |<span data-ttu-id="2d338-250">Int64</span><span class="sxs-lookup"><span data-stu-id="2d338-250">Int64</span></span> |
| <span data-ttu-id="2d338-251">Real</span><span class="sxs-lookup"><span data-stu-id="2d338-251">Real</span></span> |<span data-ttu-id="2d338-252">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="2d338-252">Single</span></span> |
| <span data-ttu-id="2d338-253">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="2d338-253">Double</span></span> |<span data-ttu-id="2d338-254">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="2d338-254">Double</span></span> |
| <span data-ttu-id="2d338-255">Float</span><span class="sxs-lookup"><span data-stu-id="2d338-255">Float</span></span> |<span data-ttu-id="2d338-256">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="2d338-256">Double</span></span> |
| <span data-ttu-id="2d338-257">Decimal</span><span class="sxs-lookup"><span data-stu-id="2d338-257">Decimal</span></span> |<span data-ttu-id="2d338-258">Decimal</span><span class="sxs-lookup"><span data-stu-id="2d338-258">Decimal</span></span> |
| <span data-ttu-id="2d338-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="2d338-259">DecimalFloat</span></span> |<span data-ttu-id="2d338-260">Decimal</span><span class="sxs-lookup"><span data-stu-id="2d338-260">Decimal</span></span> |
| <span data-ttu-id="2d338-261">numeryczne</span><span class="sxs-lookup"><span data-stu-id="2d338-261">Numeric</span></span> |<span data-ttu-id="2d338-262">Decimal</span><span class="sxs-lookup"><span data-stu-id="2d338-262">Decimal</span></span> |
| <span data-ttu-id="2d338-263">Date</span><span class="sxs-lookup"><span data-stu-id="2d338-263">Date</span></span> |<span data-ttu-id="2d338-264">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="2d338-264">DateTime</span></span> |
| <span data-ttu-id="2d338-265">Time</span><span class="sxs-lookup"><span data-stu-id="2d338-265">Time</span></span> |<span data-ttu-id="2d338-266">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="2d338-266">TimeSpan</span></span> |
| <span data-ttu-id="2d338-267">Znacznik czasu</span><span class="sxs-lookup"><span data-stu-id="2d338-267">Timestamp</span></span> |<span data-ttu-id="2d338-268">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="2d338-268">DateTime</span></span> |
| <span data-ttu-id="2d338-269">XML</span><span class="sxs-lookup"><span data-stu-id="2d338-269">Xml</span></span> |<span data-ttu-id="2d338-270">Byte]</span><span class="sxs-lookup"><span data-stu-id="2d338-270">Byte[]</span></span> |
| <span data-ttu-id="2d338-271">char</span><span class="sxs-lookup"><span data-stu-id="2d338-271">Char</span></span> |<span data-ttu-id="2d338-272">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2d338-272">String</span></span> |
| <span data-ttu-id="2d338-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="2d338-273">VarChar</span></span> |<span data-ttu-id="2d338-274">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2d338-274">String</span></span> |
| <span data-ttu-id="2d338-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="2d338-275">LongVarChar</span></span> |<span data-ttu-id="2d338-276">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2d338-276">String</span></span> |
| <span data-ttu-id="2d338-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="2d338-277">DB2DynArray</span></span> |<span data-ttu-id="2d338-278">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2d338-278">String</span></span> |
| <span data-ttu-id="2d338-279">Binarne</span><span class="sxs-lookup"><span data-stu-id="2d338-279">Binary</span></span> |<span data-ttu-id="2d338-280">Byte]</span><span class="sxs-lookup"><span data-stu-id="2d338-280">Byte[]</span></span> |
| <span data-ttu-id="2d338-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="2d338-281">VarBinary</span></span> |<span data-ttu-id="2d338-282">Byte]</span><span class="sxs-lookup"><span data-stu-id="2d338-282">Byte[]</span></span> |
| <span data-ttu-id="2d338-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="2d338-283">LongVarBinary</span></span> |<span data-ttu-id="2d338-284">Byte]</span><span class="sxs-lookup"><span data-stu-id="2d338-284">Byte[]</span></span> |
| <span data-ttu-id="2d338-285">Grafika</span><span class="sxs-lookup"><span data-stu-id="2d338-285">Graphic</span></span> |<span data-ttu-id="2d338-286">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2d338-286">String</span></span> |
| <span data-ttu-id="2d338-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="2d338-287">VarGraphic</span></span> |<span data-ttu-id="2d338-288">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2d338-288">String</span></span> |
| <span data-ttu-id="2d338-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="2d338-289">LongVarGraphic</span></span> |<span data-ttu-id="2d338-290">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2d338-290">String</span></span> |
| <span data-ttu-id="2d338-291">CLOB</span><span class="sxs-lookup"><span data-stu-id="2d338-291">Clob</span></span> |<span data-ttu-id="2d338-292">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2d338-292">String</span></span> |
| <span data-ttu-id="2d338-293">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="2d338-293">Blob</span></span> |<span data-ttu-id="2d338-294">Byte]</span><span class="sxs-lookup"><span data-stu-id="2d338-294">Byte[]</span></span> |
| <span data-ttu-id="2d338-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="2d338-295">DbClob</span></span> |<span data-ttu-id="2d338-296">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2d338-296">String</span></span> |
| <span data-ttu-id="2d338-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="2d338-297">SmallInt</span></span> |<span data-ttu-id="2d338-298">Int16</span><span class="sxs-lookup"><span data-stu-id="2d338-298">Int16</span></span> |
| <span data-ttu-id="2d338-299">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="2d338-299">Integer</span></span> |<span data-ttu-id="2d338-300">Int32</span><span class="sxs-lookup"><span data-stu-id="2d338-300">Int32</span></span> |
| <span data-ttu-id="2d338-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="2d338-301">BigInt</span></span> |<span data-ttu-id="2d338-302">Int64</span><span class="sxs-lookup"><span data-stu-id="2d338-302">Int64</span></span> |
| <span data-ttu-id="2d338-303">Real</span><span class="sxs-lookup"><span data-stu-id="2d338-303">Real</span></span> |<span data-ttu-id="2d338-304">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="2d338-304">Single</span></span> |
| <span data-ttu-id="2d338-305">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="2d338-305">Double</span></span> |<span data-ttu-id="2d338-306">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="2d338-306">Double</span></span> |
| <span data-ttu-id="2d338-307">Float</span><span class="sxs-lookup"><span data-stu-id="2d338-307">Float</span></span> |<span data-ttu-id="2d338-308">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="2d338-308">Double</span></span> |
| <span data-ttu-id="2d338-309">Decimal</span><span class="sxs-lookup"><span data-stu-id="2d338-309">Decimal</span></span> |<span data-ttu-id="2d338-310">Decimal</span><span class="sxs-lookup"><span data-stu-id="2d338-310">Decimal</span></span> |
| <span data-ttu-id="2d338-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="2d338-311">DecimalFloat</span></span> |<span data-ttu-id="2d338-312">Decimal</span><span class="sxs-lookup"><span data-stu-id="2d338-312">Decimal</span></span> |
| <span data-ttu-id="2d338-313">numeryczne</span><span class="sxs-lookup"><span data-stu-id="2d338-313">Numeric</span></span> |<span data-ttu-id="2d338-314">Decimal</span><span class="sxs-lookup"><span data-stu-id="2d338-314">Decimal</span></span> |
| <span data-ttu-id="2d338-315">Date</span><span class="sxs-lookup"><span data-stu-id="2d338-315">Date</span></span> |<span data-ttu-id="2d338-316">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="2d338-316">DateTime</span></span> |
| <span data-ttu-id="2d338-317">Time</span><span class="sxs-lookup"><span data-stu-id="2d338-317">Time</span></span> |<span data-ttu-id="2d338-318">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="2d338-318">TimeSpan</span></span> |
| <span data-ttu-id="2d338-319">Znacznik czasu</span><span class="sxs-lookup"><span data-stu-id="2d338-319">Timestamp</span></span> |<span data-ttu-id="2d338-320">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="2d338-320">DateTime</span></span> |
| <span data-ttu-id="2d338-321">XML</span><span class="sxs-lookup"><span data-stu-id="2d338-321">Xml</span></span> |<span data-ttu-id="2d338-322">Byte]</span><span class="sxs-lookup"><span data-stu-id="2d338-322">Byte[]</span></span> |
| <span data-ttu-id="2d338-323">char</span><span class="sxs-lookup"><span data-stu-id="2d338-323">Char</span></span> |<span data-ttu-id="2d338-324">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2d338-324">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="2d338-325">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="2d338-325">Map source toosink columns</span></span>
<span data-ttu-id="2d338-326">toolearn toomap kolumn w powitania źródło zestawu danych toocolumns w zestawie danych zbiornika hello, zobacz temat [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2d338-326">toolearn how toomap columns in hello source dataset toocolumns in hello sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="2d338-327">Odczyty powtarzalne źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="2d338-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="2d338-328">Po skopiowaniu danych z magazynu danych relacyjnych zachować powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="2d338-328">When you copy data from a relational data store, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="2d338-329">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="2d338-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2d338-330">Można również skonfigurować ponawiania hello **zasad** właściwości zestawu danych toorerun wycinka, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="2d338-330">You can also configure hello retry **policy** property for a dataset toorerun a slice when a failure occurs.</span></span> <span data-ttu-id="2d338-331">Upewnij się, że hello te same dane jest do odczytu niezależnie od tego, jak wiele razy hello wycinek jest Uruchom ponownie i niezależnie od tego, jak ponownie uruchomić hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="2d338-331">Make sure that hello same data is read no matter how many times hello slice is rerun, and regardless of how you rerun hello slice.</span></span> <span data-ttu-id="2d338-332">Aby uzyskać więcej informacji, zobacz [Repeatable odczytuje z źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="2d338-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2d338-333">Wydajności i dostosowywanie</span><span class="sxs-lookup"><span data-stu-id="2d338-333">Performance and tuning</span></span>
<span data-ttu-id="2d338-334">Więcej informacji na temat kluczowych czynników wpływających na wydajność hello działanie kopiowania i sposoby wydajności toooptimize w hello [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="2d338-334">Learn about key factors that affect hello performance of Copy Activity and ways toooptimize performance in hello [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
