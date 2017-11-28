---
title: "aaaMove danych z lokalnego programu SQL Server tooSQL Azure z fabryką danych Azure | Dokumentacja firmy Microsoft"
description: "Skonfiguruj potok fabryki danych AZURE, który Redaguj dwa działania migracji danych, które razem przenoszenia danych w trybie dziennym między bazami danych lokalnych i w chmurze hello."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a><span data-ttu-id="237b1-103">Przenoszenia danych z lokalnego tooSQL serwera SQL Azure z fabryką danych Azure</span><span class="sxs-lookup"><span data-stu-id="237b1-103">Move data from an on-premises SQL server tooSQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="237b1-104">W tym temacie przedstawiono, jak dane toomove z lokalnej bazy danych SQL Server tooa bazy danych SQL Azure za pomocą usługi Azure Blob Storage za pomocą hello fabryki danych Azure (ADF).</span><span class="sxs-lookup"><span data-stu-id="237b1-104">This topic shows how toomove data from an on-premises SQL Server Database tooa SQL Azure Database via Azure Blob Storage using hello Azure Data Factory (ADF).</span></span>

<span data-ttu-id="237b1-105">Dla tabeli, która zawiera podsumowanie różne opcje przenoszenia danych tooan bazy danych SQL Azure, zobacz [Przenieś tooan danych bazy danych SQL Azure dla usługi Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="237b1-105">For a table that summarizes various options for moving data tooan Azure SQL Database, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="237b1-106"><a name="intro"></a>Wprowadzenie: Co to jest ADF i kiedy ma być używane toomigrate danych?</span><span class="sxs-lookup"><span data-stu-id="237b1-106"><a name="intro"></a>Introduction: What is ADF and when should it be used toomigrate data?</span></span>
<span data-ttu-id="237b1-107">Fabryka danych Azure to usługa integracji pełni zarządzanych danych oparte na chmurze, która organizuje i zautomatyzować przepływ hello i przekształcania danych.</span><span class="sxs-lookup"><span data-stu-id="237b1-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="237b1-108">Witaj klucza w modelu ADF hello dotyczy potoku.</span><span class="sxs-lookup"><span data-stu-id="237b1-108">hello key concept in hello ADF model is pipeline.</span></span> <span data-ttu-id="237b1-109">Potok to logiczne grupowanie działań, z których każdy definiuje tooperform akcje hello na powitania danych zawartych w zestawach danych.</span><span class="sxs-lookup"><span data-stu-id="237b1-109">A pipeline is a logical grouping of Activities, each of which defines hello actions tooperform on hello data contained in Datasets.</span></span> <span data-ttu-id="237b1-110">Połączone usługi są używane toodefine hello informacji potrzebnych do zasobów danych toohello tooconnect fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="237b1-110">Linked services are used toodefine hello information needed for Data Factory tooconnect toohello data resources.</span></span>

<span data-ttu-id="237b1-111">Z fabryki danych AZURE istniejące usługi przetwarzania danych mogą być składane w potokach danych, które są wysokiej dostępności i zarządzane w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="237b1-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in hello cloud.</span></span> <span data-ttu-id="237b1-112">Potoki tych danych może zostać zaplanowane tooingest, przygotowanie, przekształcenie, analizowanie i publikować dane, a ADF zarządza i organizuje dane złożone hello i przetwarzania zależności.</span><span class="sxs-lookup"><span data-stu-id="237b1-112">These data pipelines can be scheduled tooingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates hello complex data and processing dependencies.</span></span> <span data-ttu-id="237b1-113">Można hello szybkie wbudowanych i wdrożone w chmury, łączenie coraz lokalnych rozwiązań i źródeł danych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="237b1-113">Solutions can be quickly built and deployed in hello cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="237b1-114">Należy rozważyć użycie ADF:</span><span class="sxs-lookup"><span data-stu-id="237b1-114">Consider using ADF:</span></span>

* <span data-ttu-id="237b1-115">Po toobe potrzeb stale migracji w scenariuszu hybrydowym, który uzyskuje dostęp zarówno do danych lokalnych i w chmurze zasobów</span><span class="sxs-lookup"><span data-stu-id="237b1-115">when data needs toobe continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="237b1-116">gdy danych hello jest nietransakcyjnego lub toobe potrzeb modyfikacji lub mieć logiki biznesowej dodać tooit, gdy migrowane.</span><span class="sxs-lookup"><span data-stu-id="237b1-116">when hello data is transacted or needs toobe modified or have business logic added tooit when being migrated.</span></span>

<span data-ttu-id="237b1-117">ADF umożliwia hello planowania i monitorowania zadań przy użyciu prostych skryptów JSON, które zarządzają hello przepływu danych w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="237b1-117">ADF allows for hello scheduling and monitoring of jobs using simple JSON scripts that manage hello movement of data on a periodic basis.</span></span> <span data-ttu-id="237b1-118">ADF ma również innych funkcji, takich jak obsługa złożonych operacji.</span><span class="sxs-lookup"><span data-stu-id="237b1-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="237b1-119">Aby uzyskać więcej informacji dotyczących fabryki danych AZURE, zobacz dokumentację hello na [fabryki danych Azure (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="237b1-119">For more information on ADF, see hello documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="237b1-120"><a name="scenario"></a>Witaj scenariusza</span><span class="sxs-lookup"><span data-stu-id="237b1-120"><a name="scenario"></a>hello Scenario</span></span>
<span data-ttu-id="237b1-121">Skonfigurowanie potok fabryki danych AZURE, który Redaguj dwóch działań migracji danych.</span><span class="sxs-lookup"><span data-stu-id="237b1-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="237b1-122">Razem one przenoszenie danych w trybie dziennym między lokalną bazą danych SQL i bazy danych SQL Azure w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="237b1-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in hello cloud.</span></span> <span data-ttu-id="237b1-123">dwa działania Hello są:</span><span class="sxs-lookup"><span data-stu-id="237b1-123">hello two activities are:</span></span>

* <span data-ttu-id="237b1-124">Kopiowanie danych z tooan bazy danych programu SQL Server lokalne konto magazynu obiektów Blob Azure</span><span class="sxs-lookup"><span data-stu-id="237b1-124">copy data from an on-premises SQL Server database tooan Azure Blob Storage account</span></span>
* <span data-ttu-id="237b1-125">Kopiowanie danych z tooan konta magazynu obiektów Blob Azure hello bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="237b1-125">copy data from hello Azure Blob Storage account tooan Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="237b1-126">Witaj kroki opisane w tym miejscu zostały dostosowane z hello bardziej szczegółowe samouczek dostarczone przez zespół ADF hello: [przenoszenie danych między lokalnych źródeł i w chmurze z brama zarządzania danymi](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) odwołuje się do toohello odpowiednich sekcjach tego tematu podano, gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="237b1-126">hello steps shown here have been adapted from hello more detailed tutorial provided by hello ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References toohello relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="237b1-127"><a name="prereqs"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="237b1-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="237b1-128">Ten samouczek zakłada, że masz:</span><span class="sxs-lookup"><span data-stu-id="237b1-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="237b1-129">**Subskrypcji platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="237b1-129">An **Azure subscription**.</span></span> <span data-ttu-id="237b1-130">Jeśli nie masz subskrypcji, możesz zarejestrować się, aby uzyskać dostęp do [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="237b1-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="237b1-131">**Konto magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="237b1-131">An **Azure storage account**.</span></span> <span data-ttu-id="237b1-132">Używasz konta magazynu Azure do przechowywania danych hello w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="237b1-132">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="237b1-133">Jeśli nie masz konta magazynu platformy Azure, zobacz hello [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykułu.</span><span class="sxs-lookup"><span data-stu-id="237b1-133">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="237b1-134">Po utworzeniu konta magazynu hello, musisz mieć konto hello tooobtain się, że klucz używany tooaccess hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="237b1-134">After you have created hello storage account, you need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="237b1-135">Zobacz [zarządzanie kluczami dostępu do magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="237b1-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="237b1-136">Dostęp tooan **bazy danych SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="237b1-136">Access tooan **Azure SQL Database**.</span></span> <span data-ttu-id="237b1-137">Jeśli konieczne jest ustawienie bazy danych SQL Azure, hello tpoic [wprowadzenie do korzystania z bazy danych SQL Azure Microsoft ](../sql-database/sql-database-get-started.md) informacje na temat sposobu tooprovision nowe wystąpienie bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="237b1-137">If you must set up an Azure SQL Database, hello tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how tooprovision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="237b1-138">Zainstalowano i skonfigurowano **programu Azure PowerShell** lokalnie.</span><span class="sxs-lookup"><span data-stu-id="237b1-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="237b1-139">Aby uzyskać instrukcje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="237b1-139">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="237b1-140">Ta procedura wykorzystuje hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="237b1-140">This procedure uses hello [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="237b1-141"><a name="upload-data"></a>Przekazywanie hello danych tooyour lokalnego programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="237b1-141"><a name="upload-data"></a> Upload hello data tooyour on-premises SQL Server</span></span>
<span data-ttu-id="237b1-142">Używamy hello [dataset taksówki NYC](http://chriswhong.com/open-data/foil_nyc_taxi/) procesu migracji hello toodemonstrate.</span><span class="sxs-lookup"><span data-stu-id="237b1-142">We use hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate hello migration process.</span></span> <span data-ttu-id="237b1-143">Witaj taksówki NYC zestaw danych jest dostępne, zgodnie z opisem w tym blogu w magazynie obiektów blob platformy Azure [danych taksówki NYC](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="237b1-143">hello NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="237b1-144">dane Hello ma dwa pliki, hello trip_data.csv pliku, który zawiera szczegóły podróży, oraz hello trip_far.csv pliku, który zawiera szczegółowe informacje o klasie hello płatnej w odniesieniu do każdej podróży.</span><span class="sxs-lookup"><span data-stu-id="237b1-144">hello data has two files, hello trip_data.csv file, which contains trip details, and hello  trip_far.csv file, which contains details of hello fare paid for each trip.</span></span> <span data-ttu-id="237b1-145">Przykładowe i opis te pliki znajdują się w [opis zestawu danych rund taksówki NYC](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="237b1-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="237b1-146">Można dostosować procedury hello podaną poniżej tooa zbiór danych użytkownika lub wykonaj kroki hello, zgodnie z opisem przy użyciu hello taksówki NYC zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="237b1-146">You can either adapt hello procedure provided here tooa set of your own data or follow hello steps as described by using hello NYC Taxi dataset.</span></span> <span data-ttu-id="237b1-147">tooupload hello dataset taksówki NYC do lokalnej bazy danych programu SQL Server, wykonaj procedurę hello opisane w temacie [zbiorczego importowania danych do bazy danych serwera SQL](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="237b1-147">tooupload hello NYC Taxi dataset into your on-premises SQL Server database, follow hello procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="237b1-148">Te instrukcje dotyczą programu SQL Server na maszynie wirtualnej platformy Azure, ale hello procedurę przekazywania toohello lokalnego programu SQL Server jest hello takie same.</span><span class="sxs-lookup"><span data-stu-id="237b1-148">These instructions are for a SQL Server on an Azure Virtual Machine, but hello procedure for uploading toohello on-premises SQL Server is hello same.</span></span>

## <span data-ttu-id="237b1-149"><a name="create-adf"></a>Tworzenie fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="237b1-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="237b1-150">instrukcje dotyczące tworzenia nowych fabryki danych Azure i grupy zasobów w hello Hello [portalu Azure](https://portal.azure.com/) podano [tworzenie fabryki danych Azure](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="237b1-150">hello instructions for creating a new Azure Data Factory and a resource group in hello [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="237b1-151">Nowe wystąpienie ADF nazwa hello *adfdsp* i nazwę grupy zasobów dla hello utworzony *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="237b1-151">Name hello new ADF instance *adfdsp* and name hello resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-hello-data-management-gateway"></a><span data-ttu-id="237b1-152">Instalowanie i konfigurowanie zapasowej hello brama zarządzania danymi</span><span class="sxs-lookup"><span data-stu-id="237b1-152">Install and configure up hello Data Management Gateway</span></span>
<span data-ttu-id="237b1-153">tooenable Twojego potoki w toowork fabryki danych Azure z lokalnym programem SQL Server należy tooadd go jako fabryki danych toohello połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="237b1-153">tooenable your pipelines in an Azure data factory toowork with an on-premises SQL Server, you need tooadd it as a Linked Service toohello data factory.</span></span> <span data-ttu-id="237b1-154">toocreate połączonej usługi dla lokalnego programu SQL Server, należy:</span><span class="sxs-lookup"><span data-stu-id="237b1-154">toocreate a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="237b1-155">Pobierz i zainstaluj bramę zarządzania danymi firmy Microsoft na powitania na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="237b1-155">download and install Microsoft Data Management Gateway onto hello on-premises computer.</span></span>
* <span data-ttu-id="237b1-156">Skonfiguruj usługę hello połączone hello lokalnych danych źródła toouse hello bramy.</span><span class="sxs-lookup"><span data-stu-id="237b1-156">configure hello linked service for hello on-premises data source toouse hello gateway.</span></span>

<span data-ttu-id="237b1-157">Brama zarządzania danymi Hello serializuje i deserializuje hello źródłowy i odbiorczy danych na komputerze hello, gdzie jest hostowana.</span><span class="sxs-lookup"><span data-stu-id="237b1-157">hello Data Management Gateway serializes and deserializes hello source and sink data on hello computer where it is hosted.</span></span>

<span data-ttu-id="237b1-158">Aby uzyskać instrukcje dotyczące konfiguracji oraz szczegółowe informacje w bramie zarządzania danymi, zobacz [przenoszenie danych między lokalnych źródeł i w chmurze z brama zarządzania danymi](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="237b1-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="237b1-159"><a name="adflinkedservices"></a>Tworzenie połączonej usługi tooconnect toohello zasobów danych</span><span class="sxs-lookup"><span data-stu-id="237b1-159"><a name="adflinkedservices"></a>Create linked services tooconnect toohello data resources</span></span>
<span data-ttu-id="237b1-160">Połączona usługa definiuje hello informacji potrzebnych do fabryki danych Azure tooconnect tooa danych zasobów.</span><span class="sxs-lookup"><span data-stu-id="237b1-160">A linked service defines hello information needed for Azure Data Factory tooconnect tooa data resource.</span></span> <span data-ttu-id="237b1-161">Hello procedury krok po kroku tworzenia połączonych usług znajduje się w [utworzenia połączonych usług](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span><span class="sxs-lookup"><span data-stu-id="237b1-161">hello step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="237b1-162">Firma Microsoft udostępnia trzy zasoby w tym scenariuszu, dla którego połączone usługi są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="237b1-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="237b1-163">Połączona usługa dla lokalnego programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="237b1-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="237b1-164">Połączonej usługi magazynu obiektów Blob Azure</span><span class="sxs-lookup"><span data-stu-id="237b1-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="237b1-165">Połączonej usługi bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="237b1-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="237b1-166"><a name="adf-linked-service-onprem-sql"></a>Połączona usługa lokalnej bazy danych SQL Server</span><span class="sxs-lookup"><span data-stu-id="237b1-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="237b1-167">Usługa hello połączone toocreate hello lokalnego programu SQL Server:</span><span class="sxs-lookup"><span data-stu-id="237b1-167">toocreate hello linked service for hello on-premises SQL Server:</span></span>

* <span data-ttu-id="237b1-168">Kliknij przycisk hello **magazynu danych** w strony docelowej ADF hello w klasycznym portalu Azure</span><span class="sxs-lookup"><span data-stu-id="237b1-168">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="237b1-169">Wybierz **SQL** , a następnie wprowadź hello *username* i *hasło* poświadczeń dla hello lokalnego programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="237b1-169">select **SQL** and enter hello *username* and *password* credentials for hello on-premises SQL Server.</span></span> <span data-ttu-id="237b1-170">Należy servername hello tooenter jako **nazwa wystąpienia pełną servername ukośnik odwrotny (servername\instancename)**.</span><span class="sxs-lookup"><span data-stu-id="237b1-170">You need tooenter hello servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="237b1-171">Nazwa hello połączona usługa *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="237b1-171">Name hello linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="237b1-172"><a name="adf-linked-service-blob-store"></a>Połączona usługa obiektu blob</span><span class="sxs-lookup"><span data-stu-id="237b1-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="237b1-173">toocreate hello połączonej usługi dla konta magazynu obiektów Blob Azure hello:</span><span class="sxs-lookup"><span data-stu-id="237b1-173">toocreate hello linked service for hello Azure Blob Storage account:</span></span>

* <span data-ttu-id="237b1-174">Kliknij przycisk hello **magazynu danych** w strony docelowej ADF hello w klasycznym portalu Azure</span><span class="sxs-lookup"><span data-stu-id="237b1-174">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="237b1-175">Wybierz **konta magazynu Azure**</span><span class="sxs-lookup"><span data-stu-id="237b1-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="237b1-176">Wprowadź hello Azure Blob Storage klucza i kontener nazwę konta.</span><span class="sxs-lookup"><span data-stu-id="237b1-176">enter hello Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="237b1-177">Witaj nazwy połączonej usługi *adfds*.</span><span class="sxs-lookup"><span data-stu-id="237b1-177">Name hello Linked Service *adfds*.</span></span>

### <span data-ttu-id="237b1-178"><a name="adf-linked-service-azure-sql"></a>Połączonej usługi bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="237b1-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="237b1-179">toocreate hello połączonej usługi dla bazy danych SQL Azure hello:</span><span class="sxs-lookup"><span data-stu-id="237b1-179">toocreate hello linked service for hello Azure SQL Database:</span></span>

* <span data-ttu-id="237b1-180">Kliknij przycisk hello **magazynu danych** w strony docelowej ADF hello w klasycznym portalu Azure</span><span class="sxs-lookup"><span data-stu-id="237b1-180">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="237b1-181">Wybierz **Azure SQL** , a następnie wprowadź hello *username* i *hasło* poświadczenia hello bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="237b1-181">select **Azure SQL** and enter hello *username* and *password* credentials for hello Azure SQL Database.</span></span> <span data-ttu-id="237b1-182">Witaj *username* muszą być określone jako  *user@servername* .</span><span class="sxs-lookup"><span data-stu-id="237b1-182">hello *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="237b1-183"><a name="adf-tables"></a>Definiowanie i tworzenie tabel toospecify jak tooaccess hello zbiory danych</span><span class="sxs-lookup"><span data-stu-id="237b1-183"><a name="adf-tables"></a>Define and create tables toospecify how tooaccess hello datasets</span></span>
<span data-ttu-id="237b1-184">Tworzenie tabel zawierających dostępności hello zestawów danych, lokalizacji i struktura hello hello zgodnie z procedurami opartych na skryptach.</span><span class="sxs-lookup"><span data-stu-id="237b1-184">Create tables that specify hello structure, location, and availability of hello datasets with hello following script-based procedures.</span></span> <span data-ttu-id="237b1-185">Pliki w formacie JSON są używane toodefine hello tabel.</span><span class="sxs-lookup"><span data-stu-id="237b1-185">JSON files are used toodefine hello tables.</span></span> <span data-ttu-id="237b1-186">Aby uzyskać więcej informacji o strukturze hello tych plików, zobacz [zestawów danych](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="237b1-186">For more information on hello structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="237b1-187">Należy wykonać hello `Add-AzureAccount` polecenia cmdlet przed wykonaniem hello [AzureDataFactoryTable nowy](https://msdn.microsoft.com/library/azure/dn835096.aspx) tooconfirm polecenia cmdlet, które hello subskrypcji prawo Azure jest wybrany do wykonania polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="237b1-187">You should execute hello `Add-AzureAccount` cmdlet before executing hello [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet tooconfirm that hello right Azure subscription is selected for hello command execution.</span></span> <span data-ttu-id="237b1-188">Aby uzyskać dokumentację tego polecenia cmdlet, zobacz [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="237b1-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="237b1-189">definicje Hello opartych na formacie JSON w tabelach hello Użyj hello następujące nazwy:</span><span class="sxs-lookup"><span data-stu-id="237b1-189">hello JSON-based definitions in hello tables use hello following names:</span></span>

* <span data-ttu-id="237b1-190">Witaj **nazwy tabeli** hello lokalnego programu SQL server jest *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="237b1-190">hello **table name** in hello on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="237b1-191">Witaj **nazwa kontenera** w hello magazynu obiektów Blob Azure jest konto *containername*</span><span class="sxs-lookup"><span data-stu-id="237b1-191">hello **container name** in hello Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="237b1-192">Trzy definicje tabel są wymagane dla tego potoku ADF:</span><span class="sxs-lookup"><span data-stu-id="237b1-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="237b1-193">SQL lokalnej tabeli</span><span class="sxs-lookup"><span data-stu-id="237b1-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="237b1-194">Tabela obiektów blob</span><span class="sxs-lookup"><span data-stu-id="237b1-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="237b1-195">SQL tabeli platformy Azure</span><span class="sxs-lookup"><span data-stu-id="237b1-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="237b1-196">Te procedury użyj toodefine programu Azure PowerShell i Utwórz hello działania ADF.</span><span class="sxs-lookup"><span data-stu-id="237b1-196">These procedures use Azure PowerShell toodefine and create hello ADF activities.</span></span> <span data-ttu-id="237b1-197">Jednak te zadania może być również wykonywane przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="237b1-197">But these tasks can also be accomplished using hello Azure portal.</span></span> <span data-ttu-id="237b1-198">Aby uzyskać więcej informacji, zobacz [utworzyć zestawy danych](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="237b1-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="237b1-199"><a name="adf-table-onprem-sql"></a>SQL lokalnej tabeli</span><span class="sxs-lookup"><span data-stu-id="237b1-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="237b1-200">Definicja tabeli Hello hello lokalnego programu SQL Server jest określony w hello następującego pliku JSON:</span><span class="sxs-lookup"><span data-stu-id="237b1-200">hello table definition for hello on-premises SQL Server is specified in hello following JSON file:</span></span>

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

<span data-ttu-id="237b1-201">nazwy kolumn Hello nie były dołączane tutaj.</span><span class="sxs-lookup"><span data-stu-id="237b1-201">hello column names were not included here.</span></span> <span data-ttu-id="237b1-202">Można wybrać podrzędna na nazwy kolumn hello przez włączenie ich w tym miejscu (Aby uzyskać szczegółowe informacje, przejrzyj hello [dokumentacji ADF](../data-factory/data-factory-data-movement-activities.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="237b1-202">You can sub-select on hello column names by including them here (for details check hello [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="237b1-203">Skopiuj hello JSON definicji tabeli hello w pliku o nazwie *onpremtabledef.json* pliku i zapisz go tooa znane lokalizacji (tutaj zakłada, że toobe *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="237b1-203">Copy hello JSON definition of hello table into a file called *onpremtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="237b1-204">Tworzenie tabeli hello w ADF za hello następującego polecenia cmdlet programu Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="237b1-204">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="237b1-205"><a name="adf-table-blob-store"></a>Tabela obiektów blob</span><span class="sxs-lookup"><span data-stu-id="237b1-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="237b1-206">Definicja tabeli hello hello danych wyjściowych lokalizacji obiektu blob znajduje się w następujących hello (mapuje hello pozyskanych danych z obiektu blob tooAzure lokalnych):</span><span class="sxs-lookup"><span data-stu-id="237b1-206">Definition for hello table for hello output blob location is in hello following (this maps hello ingested data from on-premises tooAzure blob):</span></span>

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

<span data-ttu-id="237b1-207">Skopiuj hello JSON definicji tabeli hello w pliku o nazwie *bloboutputtabledef.json* pliku i zapisz go tooa znane lokalizacji (tutaj zakłada, że toobe *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="237b1-207">Copy hello JSON definition of hello table into a file called *bloboutputtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="237b1-208">Tworzenie tabeli hello w ADF za hello następującego polecenia cmdlet programu Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="237b1-208">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="237b1-209"><a name="adf-table-azure-sq"></a>SQL tabeli platformy Azure</span><span class="sxs-lookup"><span data-stu-id="237b1-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="237b1-210">Definicja tabeli hello powitalne danych wyjściowych SQL Azure znajduje się w następujących hello (w tym schemacie mapuje dane hello pochodzące z obiektu blob hello):</span><span class="sxs-lookup"><span data-stu-id="237b1-210">Definition for hello table for hello SQL Azure output is in hello following (this schema maps hello data coming from hello blob):</span></span>

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

<span data-ttu-id="237b1-211">Skopiuj hello JSON definicji tabeli hello w pliku o nazwie *AzureSqlTable.json* pliku i zapisz go tooa znane lokalizacji (tutaj zakłada, że toobe *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="237b1-211">Copy hello JSON definition of hello table into a file called *AzureSqlTable.json* file and save it tooa known location (here assumed toobe *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="237b1-212">Tworzenie tabeli hello w ADF za hello następującego polecenia cmdlet programu Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="237b1-212">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="237b1-213"><a name="adf-pipeline"></a>Definiowanie i utworzyć potok hello</span><span class="sxs-lookup"><span data-stu-id="237b1-213"><a name="adf-pipeline"></a>Define and create hello pipeline</span></span>
<span data-ttu-id="237b1-214">Określ hello działań, które należy toohello potoku i utworzyć potok hello z hello zgodnie z procedurami opartych na skryptach.</span><span class="sxs-lookup"><span data-stu-id="237b1-214">Specify hello activities that belong toohello pipeline and create hello pipeline with hello following script-based procedures.</span></span> <span data-ttu-id="237b1-215">Plik JSON jest używane toodefine hello potoku właściwości.</span><span class="sxs-lookup"><span data-stu-id="237b1-215">A JSON file is used toodefine hello pipeline properties.</span></span>

* <span data-ttu-id="237b1-216">Witaj skryptu przyjęto założenie, że hello **nazwy potoku** jest *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="237b1-216">hello script assumes that hello **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="237b1-217">Należy również zauważyć, że ustawiliśmy hello okresowości toobe potoku hello wykonane na codziennie podstawę i użyj hello domyślny czas wykonania zadania hello (00: 00 UTC).</span><span class="sxs-lookup"><span data-stu-id="237b1-217">Also note that we set hello periodicity of hello pipeline toobe executed on daily basis and use hello default execution time for hello job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="237b1-218">Hello następujące procedury przy użyciu programu Azure PowerShell toodefine a utworzyć potok fabryki danych AZURE hello.</span><span class="sxs-lookup"><span data-stu-id="237b1-218">hello following procedures use Azure PowerShell toodefine and create hello ADF pipeline.</span></span> <span data-ttu-id="237b1-219">Jednak to zadanie może być również wykonywane przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="237b1-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="237b1-220">Aby uzyskać więcej informacji, zobacz [tworzenie potoku](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="237b1-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="237b1-221">Przy użyciu definicji tabeli hello podane wcześniej, definicja potoku hello hello ADF jest określana w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="237b1-221">Using hello table definitions provided previously, hello pipeline definition for hello ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

<span data-ttu-id="237b1-222">Skopiuj tej definicji JSON potoku hello w pliku o nazwie *pipelinedef.json* pliku i zapisz go tooa znane lokalizacji (w tym miejscu zakłada, że toobe *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="237b1-222">Copy this JSON definition of hello pipeline into a file called *pipelinedef.json* file and save it tooa known location (here assumed toobe *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="237b1-223">Tworzenie potoku hello w ADF z następującego polecenia cmdlet programu Azure PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="237b1-223">Create hello pipeline in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="237b1-224">Upewnij się, że można wyświetlić potoku hello na powitania wyświetlani ADF w hello klasycznego portalu Azure w następujący (po kliknięciu przycisku hello diagram)</span><span class="sxs-lookup"><span data-stu-id="237b1-224">Confirm that you can see hello pipeline on hello ADF in hello Azure Classic Portal show up as following (when you click hello diagram)</span></span>

![Potok fabryki danych AZURE](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="237b1-226"><a name="adf-pipeline-start"></a>Uruchom hello potoku</span><span class="sxs-lookup"><span data-stu-id="237b1-226"><a name="adf-pipeline-start"></a>Start hello Pipeline</span></span>
<span data-ttu-id="237b1-227">Obecnie można uruchomić potoku Hello przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="237b1-227">hello pipeline can now be run using hello following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="237b1-228">Witaj *datą rozpoczęcia* i *enddate* wartości parametru muszą toobe zastąpione hello rzeczywistej daty, między którymi ma hello toorun potoku.</span><span class="sxs-lookup"><span data-stu-id="237b1-228">hello *startdate* and *enddate* parameter values need toobe replaced with hello actual dates between which you want hello pipeline toorun.</span></span>

<span data-ttu-id="237b1-229">Po potoku hello jest wykonywana, powinno być możliwe toosee hello danych będą wyświetlane w kontenerze hello wybrane dla obiektu blob hello, jeden plik na dzień.</span><span class="sxs-lookup"><span data-stu-id="237b1-229">Once hello pipeline executes, you should be able toosee hello data show up in hello container selected for hello blob, one file per day.</span></span>

<span data-ttu-id="237b1-230">Należy pamiętać, że nie ma możemy wykorzystać hello funkcjonalność danych toopipe ADF przyrostowo.</span><span class="sxs-lookup"><span data-stu-id="237b1-230">Note that we have not leveraged hello functionality provided by ADF toopipe data incrementally.</span></span> <span data-ttu-id="237b1-231">Aby uzyskać więcej informacji na temat toodo to i inne funkcje udostępniane przez ADF, zobacz temat hello [dokumentacji ADF](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="237b1-231">For more information on how toodo this and other capabilities provided by ADF, see hello [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
