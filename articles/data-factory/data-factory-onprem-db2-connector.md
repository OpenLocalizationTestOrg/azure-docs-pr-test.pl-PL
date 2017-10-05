---
title: "Przenieść dane z bazy danych DB2 przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przenieść dane z bazy danych DB2 lokalnie za pomocą działania kopiowania fabryki danych Azure"
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
ms.openlocfilehash: 6a89cc44724dbb5b46a9e89d6da24d9b35ddbbef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="b5b9d-103">Przenieść dane z bazy danych DB2 za pomocą działania kopiowania fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="b5b9d-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="b5b9d-104">W tym artykule opisano, jak używasz działanie kopiowania w fabryce danych Azure można skopiować danych z lokalną bazą danych DB2 w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-104">This article describes how you can use Copy Activity in Azure Data Factory to copy data from an on-premises DB2 database to a data store.</span></span> <span data-ttu-id="b5b9d-105">Można skopiować danych do dowolnego magazynu, który jest wymieniony jako obsługiwany zbiornika w [działań przepływu danych fabryki danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-105">You can copy data to any store that is listed as a supported sink in the [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="b5b9d-106">W tym temacie opiera się na artykułu fabryki danych, które zawiera omówienie przepływu danych za pomocą działania kopiowania i wyświetla kombinacje magazynu obsługiwane dane.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-106">This topic builds on the Data Factory article, which presents an overview of data movement by using Copy Activity and lists the supported data store combinations.</span></span> 

<span data-ttu-id="b5b9d-107">Fabryka danych aktualnie obsługuje tylko przenoszenia danych z bazy danych DB2 do [obsługiwanych ujścia magazynu danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b5b9d-107">Data Factory currently supports only moving data from a DB2 database to a [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="b5b9d-108">Przechowuje przenoszenia danych z innych danych do bazy danych DB2 bazy danych nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-108">Moving data from other data stores to a DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5b9d-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b5b9d-109">Prerequisites</span></span>
<span data-ttu-id="b5b9d-110">Fabryka danych obsługuje nawiązywania połączenia z lokalną bazą danych DB2 przy użyciu [brama zarządzania danymi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="b5b9d-110">Data Factory supports connecting to an on-premises DB2 database by using the [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="b5b9d-111">Aby uzyskać instrukcje krok po kroku do konfigurowania potoku bramy danych w celu przenoszenia danych, zobacz [przenoszenia danych z lokalnymi do chmury](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-111">For step-by-step instructions to set up the gateway data pipeline to move your data, see the [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="b5b9d-112">Wymagana jest brama, nawet jeśli programu DB2 znajduje się na maszynie Wirtualnej Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-112">A gateway is required even if the DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="b5b9d-113">Bramę można zainstalować na tej samej maszyny Wirtualnej IaaS do przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-113">You can install the gateway on the same IaaS VM as the data store.</span></span> <span data-ttu-id="b5b9d-114">Jeśli bramy można połączyć z bazą danych, można zainstalować bramę na innej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-114">If the gateway can connect to the database, you can install the gateway on a different VM.</span></span>

<span data-ttu-id="b5b9d-115">Brama zarządzania danymi zawiera wbudowane sterownik bazy danych DB2, dzięki czemu nie trzeba ręcznie zainstaluj sterownik na skopiowanie danych z bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-115">The data management gateway provides a built-in DB2 driver, so you don't need to manually install a driver to copy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="b5b9d-116">Aby uzyskać wskazówki dotyczące rozwiązywania problemów dotyczących połączenia i problemy bramy, zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-116">For tips on troubleshooting connection and gateway issues, see the [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="b5b9d-117">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="b5b9d-117">Supported versions</span></span>
<span data-ttu-id="b5b9d-118">Łącznik DB2 fabryki danych obsługuje następujące platformy IBM DB2 i wersje Menedżera dostępu programu SQL Distributed relacyjnej bazy danych architektury DRDA () w wersji 9, 10 lub 11:</span><span class="sxs-lookup"><span data-stu-id="b5b9d-118">The Data Factory DB2 connector supports the following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="b5b9d-119">IBM DB2 w wersji 11.1 z/OS</span><span class="sxs-lookup"><span data-stu-id="b5b9d-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="b5b9d-120">IBM DB2 w wersji 10.1 z/OS</span><span class="sxs-lookup"><span data-stu-id="b5b9d-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="b5b9d-121">IBM DB2 (AS400) i wersji 7.2</span><span class="sxs-lookup"><span data-stu-id="b5b9d-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="b5b9d-122">IBM DB2 i (AS400) w wersji 7.1</span><span class="sxs-lookup"><span data-stu-id="b5b9d-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="b5b9d-123">IBM DB2 dla systemu Linux, UNIX i systemu Windows (LUW) w wersji 11</span><span class="sxs-lookup"><span data-stu-id="b5b9d-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="b5b9d-124">IBM DB2 dla LUW wersji 10.5</span><span class="sxs-lookup"><span data-stu-id="b5b9d-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="b5b9d-125">IBM DB2 dla LUW wersji 10.1</span><span class="sxs-lookup"><span data-stu-id="b5b9d-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="b5b9d-126">Jeśli zostanie wyświetlony komunikat o błędzie "nie znaleziono pakietu odpowiadający żądania wykonania instrukcji SQL.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-126">If you receive the error message "The package corresponding to an SQL statement execution request was not found.</span></span> <span data-ttu-id="b5b9d-127">SQLSTATE 51002 SQLCODE =-805, = "przyczyną jest potrzebny pakiet nie został utworzony dla zwykłego użytkownika w systemie operacyjnym.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-127">SQLSTATE=51002 SQLCODE=-805," the reason is a necessary package is not created for the normal user on the OS.</span></span> <span data-ttu-id="b5b9d-128">Aby rozwiązać ten problem, wykonaj następujące instrukcje dla danego typu serwera bazy danych DB2:</span><span class="sxs-lookup"><span data-stu-id="b5b9d-128">To resolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="b5b9d-129">Bazy danych DB2 dla i (AS400): umożliwia użytkownikowi zasilania utworzyć kolekcję dla zwykłego użytkownika przed uruchomieniem działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-129">DB2 for i (AS400): Let a power user create the collection for the normal user before running Copy Activity.</span></span> <span data-ttu-id="b5b9d-130">Aby utworzyć kolekcję, użyj polecenia:`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="b5b9d-130">To create the collection, use the command: `create collection <username>`</span></span>
> - <span data-ttu-id="b5b9d-131">Bazy danych DB2 z/OS lub LUW: Użyj konta z wysokim poziomie uprawnień — użytkownik zaawansowany lub administrator urzędów pakietu i powiązania, BINDADD, PRZYZNAĆ uprawnienia publiczne — do skopiowania raz EXECUTE.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE TO PUBLIC permissions--to run the copy once.</span></span> <span data-ttu-id="b5b9d-132">Potrzebny pakiet jest tworzony automatycznie podczas kopiowania.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-132">The necessary package is automatically created during the copy.</span></span> <span data-ttu-id="b5b9d-133">Możesz później, przejdź do zwykłego użytkownika dla sekwencji kolejnych kopii.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-133">Afterward, you can switch back to the normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b5b9d-134">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="b5b9d-134">Getting started</span></span>
<span data-ttu-id="b5b9d-135">Można utworzyć potok z działaniem kopiowania do przenoszenia danych z magazynu danych programu DB2 lokalnie przy użyciu różnych narzędzi i interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="b5b9d-135">You can create a pipeline with a copy activity to move data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="b5b9d-136">Najprostszym sposobem, aby utworzyć potok jest użycie Kreatora kopiowania fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-136">The easiest way to create a pipeline is to use the Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="b5b9d-137">Szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania, zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="b5b9d-137">For a quick walkthrough on creating a pipeline by using the Copy Wizard, see the [Tutorial: Create a pipeline by using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="b5b9d-138">Umożliwia także narzędzia do tworzenia potoku, w tym portalu Azure, programu Visual Studio, programu Azure PowerShell szablonu usługi Azure Resource Manager, interfejsu API programu .NET i interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-138">You can also use tools to create a pipeline, including the Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, the .NET API, and the REST API.</span></span> <span data-ttu-id="b5b9d-139">Aby uzyskać instrukcje utworzyć potok z działania kopiowania, zobacz [samouczek działanie kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b5b9d-139">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="b5b9d-140">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="b5b9d-140">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="b5b9d-141">Utwórz połączone usługi, aby połączyć dane wejściowe i wyjściowe magazyny danych z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-141">Create linked services to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="b5b9d-142">Tworzenie zestawów danych do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-142">Create datasets to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="b5b9d-143">Utworzyć potok aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="b5b9d-144">Korzystając z Kreatora kopiowania, definicje JSON dla fabryki danych połączone usługi, zestawy danych i jednostek potoku są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-144">When you use the Copy Wizard, JSON definitions for the Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="b5b9d-145">Korzystając z narzędzia lub interfejsów API (z wyjątkiem interfejsu API programu .NET), należy zdefiniować jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-145">When you use tools or APIs (except the .NET API), you define the Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="b5b9d-146">[Przykład JSON: kopiowanie danych z bazy danych DB2 do magazynu obiektów Blob Azure](#json-example-copy-data-from-db2-to-azure-blob) zawiera definicje JSON dla jednostek fabryki danych, które są używane do kopiowania danych z magazynu danych programu DB2 lokalnie.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-146">The [JSON example: Copy data from DB2 to Azure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows the JSON definitions for the Data Factory entities that are used to copy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="b5b9d-147">Poniższe sekcje zawierają szczegółowe informacje o właściwościach JSON, które są używane do definiowania jednostek fabryki danych, które są specyficzne dla magazynu danych programu DB2.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-147">The following sections provide details about the JSON properties that are used to define the Data Factory entities that are specific to a DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="b5b9d-148">Właściwości usługi połączone bazy danych DB2</span><span class="sxs-lookup"><span data-stu-id="b5b9d-148">DB2 linked service properties</span></span>
<span data-ttu-id="b5b9d-149">W poniższej tabeli wymieniono właściwości JSON, które są specyficzne dla usługi bazy danych DB2 połączone.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-149">The following table lists the JSON properties that are specific to a DB2 linked service.</span></span>

| <span data-ttu-id="b5b9d-150">Właściwość</span><span class="sxs-lookup"><span data-stu-id="b5b9d-150">Property</span></span> | <span data-ttu-id="b5b9d-151">Opis</span><span class="sxs-lookup"><span data-stu-id="b5b9d-151">Description</span></span> | <span data-ttu-id="b5b9d-152">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b5b9d-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b5b9d-153">**Typ**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-153">**type**</span></span> |<span data-ttu-id="b5b9d-154">Ta właściwość musi mieć ustawioną **OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-154">This property must be set to **OnPremisesDB2**.</span></span> |<span data-ttu-id="b5b9d-155">Tak</span><span class="sxs-lookup"><span data-stu-id="b5b9d-155">Yes</span></span> |
| <span data-ttu-id="b5b9d-156">**Serwer**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-156">**server**</span></span> |<span data-ttu-id="b5b9d-157">Nazwa serwera bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-157">The name of the DB2 server.</span></span> |<span data-ttu-id="b5b9d-158">Tak</span><span class="sxs-lookup"><span data-stu-id="b5b9d-158">Yes</span></span> |
| <span data-ttu-id="b5b9d-159">**bazy danych**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-159">**database**</span></span> |<span data-ttu-id="b5b9d-160">Nazwa bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-160">The name of the DB2 database.</span></span> |<span data-ttu-id="b5b9d-161">Tak</span><span class="sxs-lookup"><span data-stu-id="b5b9d-161">Yes</span></span> |
| <span data-ttu-id="b5b9d-162">**Schemat**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-162">**schema**</span></span> |<span data-ttu-id="b5b9d-163">Nazwa schematu bazy danych DB2.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-163">The name of the schema in the DB2 database.</span></span> <span data-ttu-id="b5b9d-164">Ta właściwość jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-164">This property is case-sensitive.</span></span> |<span data-ttu-id="b5b9d-165">Nie</span><span class="sxs-lookup"><span data-stu-id="b5b9d-165">No</span></span> |
| <span data-ttu-id="b5b9d-166">**Typ authenticationType**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-166">**authenticationType**</span></span> |<span data-ttu-id="b5b9d-167">Typ uwierzytelniania używany do łączenia z bazą danych DB2.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-167">The type of authentication that is used to connect to the DB2 database.</span></span> <span data-ttu-id="b5b9d-168">Możliwe wartości to: anonimowe, podstawowe i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-168">The possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="b5b9d-169">Tak</span><span class="sxs-lookup"><span data-stu-id="b5b9d-169">Yes</span></span> |
| <span data-ttu-id="b5b9d-170">**Nazwa użytkownika**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-170">**username**</span></span> |<span data-ttu-id="b5b9d-171">Nazwa konta użytkownika, jeśli korzystasz z uwierzytelniania podstawowego lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-171">The name for the user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="b5b9d-172">Nie</span><span class="sxs-lookup"><span data-stu-id="b5b9d-172">No</span></span> |
| <span data-ttu-id="b5b9d-173">**hasło**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-173">**password**</span></span> |<span data-ttu-id="b5b9d-174">Hasło dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-174">The password for the user account.</span></span> |<span data-ttu-id="b5b9d-175">Nie</span><span class="sxs-lookup"><span data-stu-id="b5b9d-175">No</span></span> |
| <span data-ttu-id="b5b9d-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-176">**gatewayName**</span></span> |<span data-ttu-id="b5b9d-177">Nazwa bramy, która powinna być używana przez usługi fabryka danych nawiązać połączenia z lokalną bazą danych DB2.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-177">The name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="b5b9d-178">Tak</span><span class="sxs-lookup"><span data-stu-id="b5b9d-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="b5b9d-179">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="b5b9d-179">Dataset properties</span></span>
<span data-ttu-id="b5b9d-180">Listę sekcje i właściwości, które są dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-180">For a list of the sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b5b9d-181">Sekcje, takich jak **struktury**, **dostępności**i **zasad** dla zestawu danych JSON, są podobne dla wszystkich typów zestawu danych (Azure SQL, magazyn obiektów Blob platformy Azure, Magazyn tabel Azure itd.).</span><span class="sxs-lookup"><span data-stu-id="b5b9d-181">Sections, such as **structure**, **availability**, and the **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="b5b9d-182">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-182">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="b5b9d-183">**TypeProperties** sekcja dla zestawu danych typu **RelationalTable**, w tym zestawie danych DB2, ma następującą właściwość:</span><span class="sxs-lookup"><span data-stu-id="b5b9d-183">The **typeProperties** section for a dataset of type **RelationalTable**, which includes the DB2 dataset, has the following property:</span></span>

| <span data-ttu-id="b5b9d-184">Właściwość</span><span class="sxs-lookup"><span data-stu-id="b5b9d-184">Property</span></span> | <span data-ttu-id="b5b9d-185">Opis</span><span class="sxs-lookup"><span data-stu-id="b5b9d-185">Description</span></span> | <span data-ttu-id="b5b9d-186">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b5b9d-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b5b9d-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-187">**tableName**</span></span> |<span data-ttu-id="b5b9d-188">Nazwa tabeli w wystąpieniu bazy danych DB2 odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-188">The name of the table in the DB2 database instance that the linked service refers to.</span></span> <span data-ttu-id="b5b9d-189">Ta właściwość jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-189">This property is case-sensitive.</span></span> |<span data-ttu-id="b5b9d-190">Nie (Jeśli **zapytania** właściwości działania kopiowania typu **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="b5b9d-190">No (if the **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="b5b9d-191">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="b5b9d-191">Copy Activity properties</span></span>
<span data-ttu-id="b5b9d-192">Aby uzyskać listę sekcji i właściwości, które są dostępne do definiowania działania kopiowania, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-192">For a list of the sections and properties that are available for defining copy activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b5b9d-193">Kopiuj właściwości działania, takie jak **nazwa**, **opis**, **dane wejściowe** tabeli, **generuje** tabeli, i **zasad**, są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="b5b9d-194">Właściwości, które są dostępne w **typeProperties** sekcji działanie dla każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-194">The properties that are available in the **typeProperties** section of the activity for each activity type.</span></span> <span data-ttu-id="b5b9d-195">Dla działania kopiowania właściwości różnią się w zależności od typów źródeł danych i sink.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-195">For Copy Activity, the properties vary depending on the types of data sources and sinks.</span></span>

<span data-ttu-id="b5b9d-196">Dla działania kopiowania, gdy źródłem jest typu **RelationalSource** (która obejmuje bazy danych DB2), są dostępne w następujących właściwości **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="b5b9d-196">For Copy Activity, when the source is of type **RelationalSource** (which includes DB2), the following properties are available in the **typeProperties** section:</span></span>

| <span data-ttu-id="b5b9d-197">Właściwość</span><span class="sxs-lookup"><span data-stu-id="b5b9d-197">Property</span></span> | <span data-ttu-id="b5b9d-198">Opis</span><span class="sxs-lookup"><span data-stu-id="b5b9d-198">Description</span></span> | <span data-ttu-id="b5b9d-199">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="b5b9d-199">Allowed values</span></span> | <span data-ttu-id="b5b9d-200">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b5b9d-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b5b9d-201">**zapytania**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-201">**query**</span></span> |<span data-ttu-id="b5b9d-202">Użyj niestandardowych zapytania, aby odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-202">Use the custom query to read the data.</span></span> |<span data-ttu-id="b5b9d-203">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-203">SQL query string.</span></span> <span data-ttu-id="b5b9d-204">Na przykład: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="b5b9d-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="b5b9d-205">Nie (Jeśli **tableName** określono właściwości zestawu danych)</span><span class="sxs-lookup"><span data-stu-id="b5b9d-205">No (if the **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="b5b9d-206">Nazwy schematu i tabeli jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="b5b9d-207">W instrukcji zapytania, ujmij nazw właściwości, za pomocą "" (podwójne cudzysłowy).</span><span class="sxs-lookup"><span data-stu-id="b5b9d-207">In the query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="b5b9d-208">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b5b9d-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-to-azure-blob-storage"></a><span data-ttu-id="b5b9d-209">Przykład JSON: kopiowanie danych z bazy danych DB2 do magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b5b9d-209">JSON example: Copy data from DB2 to Azure Blob storage</span></span>
<span data-ttu-id="b5b9d-210">W poniższym przykładzie przedstawiono przykładowe definicje JSON, które można użyć, aby utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b5b9d-210">This example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b5b9d-211">Przykład przedstawia sposób kopiowania danych z bazy danych DB2 do magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-211">The example shows you how to copy data from a DB2 database to Blob storage.</span></span> <span data-ttu-id="b5b9d-212">Jednak dane mogą być kopiowane do [wszystkie obsługiwane dane przechowywane typ ujścia](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-212">However, data can be copied to [any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="b5b9d-213">Przykład zawiera następujące jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="b5b9d-213">The sample has the following Data Factory entities:</span></span>

- <span data-ttu-id="b5b9d-214">Bazy danych DB2 połączonej usługi typu [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="b5b9d-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="b5b9d-215">Połączonej usługi typu magazynu obiektów Blob platformy Azure [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="b5b9d-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="b5b9d-216">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="b5b9d-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="b5b9d-217">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="b5b9d-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="b5b9d-218">A [potoku](data-factory-create-pipelines.md) z działania kopiowania, która używa [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) właściwości</span><span class="sxs-lookup"><span data-stu-id="b5b9d-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses the [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="b5b9d-219">Przykład kopiuje dane z wyniku kwerendy w bazie danych DB2 do obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-219">The sample copies data from a query result in a DB2 database to an Azure blob hourly.</span></span> <span data-ttu-id="b5b9d-220">Właściwości JSON, które są używane w przykładowym są opisane w następnych sekcjach definicje jednostki.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-220">The JSON properties that are used in the sample are described in the sections that follow the entity definitions.</span></span>

<span data-ttu-id="b5b9d-221">Pierwszym krokiem Zainstaluj i skonfiguruj bramę danych.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="b5b9d-222">Instrukcje znajdują się w [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-222">Instructions are in the [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="b5b9d-223">**Bazy danych DB2 połączone usługi**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-223">**DB2 linked service**</span></span>

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

<span data-ttu-id="b5b9d-224">**Azure Blob połączoną usługą magazynu**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-224">**Azure Blob storage linked service**</span></span>

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

<span data-ttu-id="b5b9d-225">**Wejściowy zestaw danych DB2**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-225">**DB2 input dataset**</span></span>

<span data-ttu-id="b5b9d-226">Próbka przyjęto założenie, że utworzono tabelę w bazie danych DB2 o nazwie "MyTable", która zawiera kolumnę z etykietą "timestamp" dla czasu danych w serii.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-226">The sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for the time series data.</span></span>

<span data-ttu-id="b5b9d-227">**Zewnętrznych** właściwość jest ustawiona na wartość "true".</span><span class="sxs-lookup"><span data-stu-id="b5b9d-227">The **external** property is set to "true."</span></span> <span data-ttu-id="b5b9d-228">Usługi fabryka danych z tego ustawienia informuje o tym, że ten zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-228">This setting informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="b5b9d-229">Zwróć uwagę, że **typu** właściwość jest ustawiona na **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-229">Notice that the **type** property is set to **RelationalTable**.</span></span>


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

<span data-ttu-id="b5b9d-230">**Azure Blob wyjściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="b5b9d-231">Dane są zapisywane do nowego obiektu blob co godzinę, ustawiając **częstotliwość** dla właściwości "Godzina" i **interwał** właściwości na wartość 1.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-231">Data is written to a new blob every hour by setting the **frequency** property to "Hour" and the **interval** property to 1.</span></span> <span data-ttu-id="b5b9d-232">**FolderPath** właściwości dla obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-232">The **folderPath** property for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b5b9d-233">Ścieżka folderu używa rok, miesiąc, dzień i godzinę części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-233">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

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

<span data-ttu-id="b5b9d-234">**Potoku dla działania kopiowania**</span><span class="sxs-lookup"><span data-stu-id="b5b9d-234">**Pipeline for the copy activity**</span></span>

<span data-ttu-id="b5b9d-235">Potok zawiera działanie kopiowania skonfigurowanym do używania określonych danych wejściowych i wyjściowych zestawów danych, które jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-235">The pipeline contains a copy activity that is configured to use specified input and output datasets and which is scheduled to run every hour.</span></span> <span data-ttu-id="b5b9d-236">W definicji JSON dla potoku **źródła** ustawiono typ **RelationalSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-236">In the JSON definition for the pipeline, the **source** type is set to **RelationalSource** and the **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="b5b9d-237">Określony dla zapytania SQL **zapytania** właściwości wybiera danych z tabeli "Zamówienia".</span><span class="sxs-lookup"><span data-stu-id="b5b9d-237">The SQL query specified for the **query** property selects the data from the "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for the copy activity",
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

## <a name="type-mapping-for-db2"></a><span data-ttu-id="b5b9d-238">Mapowanie typu dla bazy danych DB2</span><span class="sxs-lookup"><span data-stu-id="b5b9d-238">Type mapping for DB2</span></span>
<span data-ttu-id="b5b9d-239">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, działanie kopiowania przeprowadza automatyczne konwersje typu źródłowego do zbiornika typu przy użyciu następujących rozwinięcie:</span><span class="sxs-lookup"><span data-stu-id="b5b9d-239">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type to sink type by using the following two-step approach:</span></span>

1. <span data-ttu-id="b5b9d-240">Konwertować z typu natywnego źródła do typu .NET</span><span class="sxs-lookup"><span data-stu-id="b5b9d-240">Convert from a native source type to a .NET type</span></span>
2. <span data-ttu-id="b5b9d-241">Konwertować z typu .NET do typu sink natywnego</span><span class="sxs-lookup"><span data-stu-id="b5b9d-241">Convert from a .NET type to a native sink type</span></span>

<span data-ttu-id="b5b9d-242">Następujące mapowania są używane, gdy działanie kopiowania konwertuje dane z bazy danych DB2 typu na typ architektury .NET:</span><span class="sxs-lookup"><span data-stu-id="b5b9d-242">The following mappings are used when Copy Activity converts the data from a DB2 type to a .NET type:</span></span>

| <span data-ttu-id="b5b9d-243">Typ bazy danych DB2</span><span class="sxs-lookup"><span data-stu-id="b5b9d-243">DB2 database type</span></span> | <span data-ttu-id="b5b9d-244">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="b5b9d-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="b5b9d-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="b5b9d-245">SmallInt</span></span> |<span data-ttu-id="b5b9d-246">Int16</span><span class="sxs-lookup"><span data-stu-id="b5b9d-246">Int16</span></span> |
| <span data-ttu-id="b5b9d-247">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="b5b9d-247">Integer</span></span> |<span data-ttu-id="b5b9d-248">Int32</span><span class="sxs-lookup"><span data-stu-id="b5b9d-248">Int32</span></span> |
| <span data-ttu-id="b5b9d-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="b5b9d-249">BigInt</span></span> |<span data-ttu-id="b5b9d-250">Int64</span><span class="sxs-lookup"><span data-stu-id="b5b9d-250">Int64</span></span> |
| <span data-ttu-id="b5b9d-251">Real</span><span class="sxs-lookup"><span data-stu-id="b5b9d-251">Real</span></span> |<span data-ttu-id="b5b9d-252">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="b5b9d-252">Single</span></span> |
| <span data-ttu-id="b5b9d-253">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="b5b9d-253">Double</span></span> |<span data-ttu-id="b5b9d-254">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="b5b9d-254">Double</span></span> |
| <span data-ttu-id="b5b9d-255">Float</span><span class="sxs-lookup"><span data-stu-id="b5b9d-255">Float</span></span> |<span data-ttu-id="b5b9d-256">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="b5b9d-256">Double</span></span> |
| <span data-ttu-id="b5b9d-257">Decimal</span><span class="sxs-lookup"><span data-stu-id="b5b9d-257">Decimal</span></span> |<span data-ttu-id="b5b9d-258">Decimal</span><span class="sxs-lookup"><span data-stu-id="b5b9d-258">Decimal</span></span> |
| <span data-ttu-id="b5b9d-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="b5b9d-259">DecimalFloat</span></span> |<span data-ttu-id="b5b9d-260">Decimal</span><span class="sxs-lookup"><span data-stu-id="b5b9d-260">Decimal</span></span> |
| <span data-ttu-id="b5b9d-261">numeryczne</span><span class="sxs-lookup"><span data-stu-id="b5b9d-261">Numeric</span></span> |<span data-ttu-id="b5b9d-262">Decimal</span><span class="sxs-lookup"><span data-stu-id="b5b9d-262">Decimal</span></span> |
| <span data-ttu-id="b5b9d-263">Date</span><span class="sxs-lookup"><span data-stu-id="b5b9d-263">Date</span></span> |<span data-ttu-id="b5b9d-264">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="b5b9d-264">DateTime</span></span> |
| <span data-ttu-id="b5b9d-265">Time</span><span class="sxs-lookup"><span data-stu-id="b5b9d-265">Time</span></span> |<span data-ttu-id="b5b9d-266">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="b5b9d-266">TimeSpan</span></span> |
| <span data-ttu-id="b5b9d-267">Znacznik czasu</span><span class="sxs-lookup"><span data-stu-id="b5b9d-267">Timestamp</span></span> |<span data-ttu-id="b5b9d-268">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="b5b9d-268">DateTime</span></span> |
| <span data-ttu-id="b5b9d-269">XML</span><span class="sxs-lookup"><span data-stu-id="b5b9d-269">Xml</span></span> |<span data-ttu-id="b5b9d-270">Byte]</span><span class="sxs-lookup"><span data-stu-id="b5b9d-270">Byte[]</span></span> |
| <span data-ttu-id="b5b9d-271">char</span><span class="sxs-lookup"><span data-stu-id="b5b9d-271">Char</span></span> |<span data-ttu-id="b5b9d-272">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b9d-272">String</span></span> |
| <span data-ttu-id="b5b9d-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="b5b9d-273">VarChar</span></span> |<span data-ttu-id="b5b9d-274">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b9d-274">String</span></span> |
| <span data-ttu-id="b5b9d-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="b5b9d-275">LongVarChar</span></span> |<span data-ttu-id="b5b9d-276">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b9d-276">String</span></span> |
| <span data-ttu-id="b5b9d-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="b5b9d-277">DB2DynArray</span></span> |<span data-ttu-id="b5b9d-278">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b9d-278">String</span></span> |
| <span data-ttu-id="b5b9d-279">Binarne</span><span class="sxs-lookup"><span data-stu-id="b5b9d-279">Binary</span></span> |<span data-ttu-id="b5b9d-280">Byte]</span><span class="sxs-lookup"><span data-stu-id="b5b9d-280">Byte[]</span></span> |
| <span data-ttu-id="b5b9d-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="b5b9d-281">VarBinary</span></span> |<span data-ttu-id="b5b9d-282">Byte]</span><span class="sxs-lookup"><span data-stu-id="b5b9d-282">Byte[]</span></span> |
| <span data-ttu-id="b5b9d-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="b5b9d-283">LongVarBinary</span></span> |<span data-ttu-id="b5b9d-284">Byte]</span><span class="sxs-lookup"><span data-stu-id="b5b9d-284">Byte[]</span></span> |
| <span data-ttu-id="b5b9d-285">Grafika</span><span class="sxs-lookup"><span data-stu-id="b5b9d-285">Graphic</span></span> |<span data-ttu-id="b5b9d-286">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b9d-286">String</span></span> |
| <span data-ttu-id="b5b9d-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="b5b9d-287">VarGraphic</span></span> |<span data-ttu-id="b5b9d-288">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b9d-288">String</span></span> |
| <span data-ttu-id="b5b9d-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="b5b9d-289">LongVarGraphic</span></span> |<span data-ttu-id="b5b9d-290">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b9d-290">String</span></span> |
| <span data-ttu-id="b5b9d-291">CLOB</span><span class="sxs-lookup"><span data-stu-id="b5b9d-291">Clob</span></span> |<span data-ttu-id="b5b9d-292">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b9d-292">String</span></span> |
| <span data-ttu-id="b5b9d-293">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="b5b9d-293">Blob</span></span> |<span data-ttu-id="b5b9d-294">Byte]</span><span class="sxs-lookup"><span data-stu-id="b5b9d-294">Byte[]</span></span> |
| <span data-ttu-id="b5b9d-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="b5b9d-295">DbClob</span></span> |<span data-ttu-id="b5b9d-296">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b9d-296">String</span></span> |
| <span data-ttu-id="b5b9d-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="b5b9d-297">SmallInt</span></span> |<span data-ttu-id="b5b9d-298">Int16</span><span class="sxs-lookup"><span data-stu-id="b5b9d-298">Int16</span></span> |
| <span data-ttu-id="b5b9d-299">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="b5b9d-299">Integer</span></span> |<span data-ttu-id="b5b9d-300">Int32</span><span class="sxs-lookup"><span data-stu-id="b5b9d-300">Int32</span></span> |
| <span data-ttu-id="b5b9d-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="b5b9d-301">BigInt</span></span> |<span data-ttu-id="b5b9d-302">Int64</span><span class="sxs-lookup"><span data-stu-id="b5b9d-302">Int64</span></span> |
| <span data-ttu-id="b5b9d-303">Real</span><span class="sxs-lookup"><span data-stu-id="b5b9d-303">Real</span></span> |<span data-ttu-id="b5b9d-304">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="b5b9d-304">Single</span></span> |
| <span data-ttu-id="b5b9d-305">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="b5b9d-305">Double</span></span> |<span data-ttu-id="b5b9d-306">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="b5b9d-306">Double</span></span> |
| <span data-ttu-id="b5b9d-307">Float</span><span class="sxs-lookup"><span data-stu-id="b5b9d-307">Float</span></span> |<span data-ttu-id="b5b9d-308">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="b5b9d-308">Double</span></span> |
| <span data-ttu-id="b5b9d-309">Decimal</span><span class="sxs-lookup"><span data-stu-id="b5b9d-309">Decimal</span></span> |<span data-ttu-id="b5b9d-310">Decimal</span><span class="sxs-lookup"><span data-stu-id="b5b9d-310">Decimal</span></span> |
| <span data-ttu-id="b5b9d-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="b5b9d-311">DecimalFloat</span></span> |<span data-ttu-id="b5b9d-312">Decimal</span><span class="sxs-lookup"><span data-stu-id="b5b9d-312">Decimal</span></span> |
| <span data-ttu-id="b5b9d-313">numeryczne</span><span class="sxs-lookup"><span data-stu-id="b5b9d-313">Numeric</span></span> |<span data-ttu-id="b5b9d-314">Decimal</span><span class="sxs-lookup"><span data-stu-id="b5b9d-314">Decimal</span></span> |
| <span data-ttu-id="b5b9d-315">Date</span><span class="sxs-lookup"><span data-stu-id="b5b9d-315">Date</span></span> |<span data-ttu-id="b5b9d-316">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="b5b9d-316">DateTime</span></span> |
| <span data-ttu-id="b5b9d-317">Time</span><span class="sxs-lookup"><span data-stu-id="b5b9d-317">Time</span></span> |<span data-ttu-id="b5b9d-318">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="b5b9d-318">TimeSpan</span></span> |
| <span data-ttu-id="b5b9d-319">Znacznik czasu</span><span class="sxs-lookup"><span data-stu-id="b5b9d-319">Timestamp</span></span> |<span data-ttu-id="b5b9d-320">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="b5b9d-320">DateTime</span></span> |
| <span data-ttu-id="b5b9d-321">XML</span><span class="sxs-lookup"><span data-stu-id="b5b9d-321">Xml</span></span> |<span data-ttu-id="b5b9d-322">Byte]</span><span class="sxs-lookup"><span data-stu-id="b5b9d-322">Byte[]</span></span> |
| <span data-ttu-id="b5b9d-323">char</span><span class="sxs-lookup"><span data-stu-id="b5b9d-323">Char</span></span> |<span data-ttu-id="b5b9d-324">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b5b9d-324">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="b5b9d-325">Obiekt sink kolumn mapy źródła</span><span class="sxs-lookup"><span data-stu-id="b5b9d-325">Map source to sink columns</span></span>
<span data-ttu-id="b5b9d-326">Informacje na temat mapowanie kolumn w zestawie źródła danych do kolumn w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b5b9d-326">To learn how to map columns in the source dataset to columns in the sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="b5b9d-327">Odczyty powtarzalne źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="b5b9d-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="b5b9d-328">Po skopiowaniu danych z magazynu danych relacyjnych należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-328">When you copy data from a relational data store, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="b5b9d-329">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="b5b9d-330">Można również skonfigurować retry **zasad** właściwości dla obiektu dataset ponownie uruchomić wycinek, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-330">You can also configure the retry **policy** property for a dataset to rerun a slice when a failure occurs.</span></span> <span data-ttu-id="b5b9d-331">Upewnij się, że te same dane jest odczytu, niezależnie od tego, ile razy wycinek zostanie uruchomiona ponownie, i niezależnie od tego, jak ponownie uruchomić wycinka.</span><span class="sxs-lookup"><span data-stu-id="b5b9d-331">Make sure that the same data is read no matter how many times the slice is rerun, and regardless of how you rerun the slice.</span></span> <span data-ttu-id="b5b9d-332">Aby uzyskać więcej informacji, zobacz [Repeatable odczytuje z źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="b5b9d-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b5b9d-333">Wydajności i dostosowywanie</span><span class="sxs-lookup"><span data-stu-id="b5b9d-333">Performance and tuning</span></span>
<span data-ttu-id="b5b9d-334">Więcej informacji na temat kluczowych czynników wpływających na wydajność działania kopiowania i sposobów w celu optymalizacji wydajności w [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="b5b9d-334">Learn about key factors that affect the performance of Copy Activity and ways to optimize performance in the [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>