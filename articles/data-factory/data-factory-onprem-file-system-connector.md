---
title: "aaaCopy danych do/z systemem plików przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocopy tooand danych z lokalnego systemu plików przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="6c36e-103">Skopiuj tooand danych z lokalnego systemu plików przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="6c36e-103">Copy data tooand from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="6c36e-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toocopy danych z lokalnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="6c36e-104">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data to/from an on-premises file system.</span></span> <span data-ttu-id="6c36e-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="6c36e-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="6c36e-106">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="6c36e-106">Supported scenarios</span></span>
<span data-ttu-id="6c36e-107">Dane należy skopiować **z lokalnego systemu plików** toohello po magazynów danych:</span><span class="sxs-lookup"><span data-stu-id="6c36e-107">You can copy data **from an on-premises file system** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="6c36e-108">Można skopiować danych z powitania po magazyny danych **tooan lokalnego systemu plików**:</span><span class="sxs-lookup"><span data-stu-id="6c36e-108">You can copy data from hello following data stores **tooan on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="6c36e-109">Aktywność kopiowania nie powoduje usunięcia pliku źródłowego hello po pomyślnie skopiowane toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="6c36e-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="6c36e-110">Jeśli potrzebujesz pliku źródłowego hello toodelete po pomyślnym kopiowania, Utwórz plik hello toodelete działań niestandardowych i użyj hello działania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="6c36e-111">Włączenie łączności</span><span class="sxs-lookup"><span data-stu-id="6c36e-111">Enabling connectivity</span></span>
<span data-ttu-id="6c36e-112">Fabryka danych obsługuje tooand nawiązujący połączenie z lokalnego systemu plików za pomocą **brama zarządzania danymi**.</span><span class="sxs-lookup"><span data-stu-id="6c36e-112">Data Factory supports connecting tooand from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="6c36e-113">Należy zainstalować hello brama zarządzania danymi w środowisku lokalnym dla hello fabryki danych usługi tooconnect tooany obsługiwanych na lokalnym magazynem danych w tym systemie plików.</span><span class="sxs-lookup"><span data-stu-id="6c36e-113">You must install hello Data Management Gateway in your on-premises environment for hello Data Factory service tooconnect tooany supported on-premises data store including file system.</span></span> <span data-ttu-id="6c36e-114">Zobacz toolearn o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello [przenoszenie danych między lokalnych źródeł i w chmurze hello z brama zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="6c36e-114">toolearn about Data Management Gateway and for step-by-step instructions on setting up hello gateway, see [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="6c36e-115">Oprócz brama zarządzania danymi inne pliki binarne muszą tooand toocommunicate toobe zainstalowane z lokalnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="6c36e-115">Apart from Data Management Gateway, no other binary files need toobe installed toocommunicate tooand from an on-premises file system.</span></span> <span data-ttu-id="6c36e-116">Należy zainstalować i używać hello brama zarządzania danymi, nawet jeśli hello systemu plików jest maszyn wirtualnych IaaS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c36e-116">You must install and use hello Data Management Gateway even if hello file system is in Azure IaaS VM.</span></span> <span data-ttu-id="6c36e-117">Aby uzyskać szczegółowe informacje na temat bramy hello, zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="6c36e-117">For detailed information about hello gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="6c36e-118">Zainstaluj toouse udział plików Linux [Samba](https://www.samba.org/) na serwerze Linux i instalacja bramy zarządzania danymi w systemie Windows server.</span><span class="sxs-lookup"><span data-stu-id="6c36e-118">toouse a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="6c36e-119">Instalowanie bramy zarządzania danymi na serwerze z systemem Linux nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="6c36e-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6c36e-120">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="6c36e-120">Getting started</span></span>
<span data-ttu-id="6c36e-121">Można utworzyć potok z działaniem kopiowania przenoszenia danych w systemie plików przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="6c36e-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="6c36e-122">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="6c36e-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="6c36e-123">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="6c36e-124">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="6c36e-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6c36e-125">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="6c36e-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="6c36e-126">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="6c36e-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="6c36e-127">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="6c36e-127">Create a **data factory**.</span></span> <span data-ttu-id="6c36e-128">Fabryka danych może zawierać co najmniej jeden potoków.</span><span class="sxs-lookup"><span data-stu-id="6c36e-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="6c36e-129">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6c36e-129">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="6c36e-130">Na przykład jeśli dane są kopiowane z system plików lokalnych tooan magazynu obiektów blob platformy Azure, utworzysz dwie toolink połączone usługi lokalnego systemu plików i fabryki danych tooyour konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c36e-130">For example, if you are copying data from an Azure blob storage tooan on-premises file system, you create two linked services toolink your on-premises file system and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="6c36e-131">Dla właściwości połączonej usługi, które są tooan określonych lokalnego systemu plików, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6c36e-131">For linked service properties that are specific tooan on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="6c36e-132">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="6c36e-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="6c36e-133">Przykład Witaj wymienionych w ostatnim kroku hello służy do tworzenia kontenera obiektów blob hello toospecify zestawu danych i folderu zawierającego hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="6c36e-133">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="6c36e-134">I utworzeniu innego zestawu danych toospecify hello folder i nazwę pliku (opcjonalnie) w systemie plików.</span><span class="sxs-lookup"><span data-stu-id="6c36e-134">And, you create another dataset toospecify hello folder and file name (optional) in your file system.</span></span> <span data-ttu-id="6c36e-135">Dla właściwości zestawu danych, które są określonych tooon lokalnego systemu plików, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6c36e-135">For dataset properties that are specific tooon-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="6c36e-136">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="6c36e-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="6c36e-137">W przykładzie hello wspomniano wcześniej używa BlobSource jako źródło i FileSystemSink jako zbiorniku dla aktywności kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-137">In hello example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for hello copy activity.</span></span> <span data-ttu-id="6c36e-138">Podobnie są kopiowane z lokalnego pliku system tooAzure magazynu obiektów Blob, należy użyć FileSystemSource i BlobSink w przypadku działania kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-138">Similarly, if you are copying from on-premises file system tooAzure Blob Storage, you use FileSystemSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="6c36e-139">Dla właściwości działania kopiowania określonych firmą tooon systemu plików, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6c36e-139">For copy activity properties that are specific tooon-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="6c36e-140">Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="6c36e-140">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="6c36e-141">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="6c36e-141">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="6c36e-142">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="6c36e-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="6c36e-143">Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z systemu plików, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-file-system) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="6c36e-143">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="6c36e-144">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek toofile określonego systemu:</span><span class="sxs-lookup"><span data-stu-id="6c36e-144">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific toofile system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6c36e-145">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="6c36e-145">Linked service properties</span></span>
<span data-ttu-id="6c36e-146">Możesz połączyć fabrykę danych Azure lokalnego pliku system tooan z hello **na lokalnym serwerze plików** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="6c36e-146">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="6c36e-147">Witaj w poniższej tabeli przedstawiono opis elementów JSON, które są określone toohello połączony serwer plików lokalnej usługi.</span><span class="sxs-lookup"><span data-stu-id="6c36e-147">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="6c36e-148">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6c36e-148">Property</span></span> | <span data-ttu-id="6c36e-149">Opis</span><span class="sxs-lookup"><span data-stu-id="6c36e-149">Description</span></span> | <span data-ttu-id="6c36e-150">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6c36e-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c36e-151">type</span><span class="sxs-lookup"><span data-stu-id="6c36e-151">type</span></span> |<span data-ttu-id="6c36e-152">Sprawdź, czy właściwość type hello jest ustawiony za**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="6c36e-152">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="6c36e-153">Tak</span><span class="sxs-lookup"><span data-stu-id="6c36e-153">Yes</span></span> |
| <span data-ttu-id="6c36e-154">Host</span><span class="sxs-lookup"><span data-stu-id="6c36e-154">host</span></span> |<span data-ttu-id="6c36e-155">Określa ścieżkę katalogu głównego hello folderu hello, które mają toocopy.</span><span class="sxs-lookup"><span data-stu-id="6c36e-155">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="6c36e-156">Użyj znaku ucieczki hello ' \ ' znaków specjalnych w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-156">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="6c36e-157">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="6c36e-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="6c36e-158">Tak</span><span class="sxs-lookup"><span data-stu-id="6c36e-158">Yes</span></span> |
| <span data-ttu-id="6c36e-159">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="6c36e-159">userid</span></span> |<span data-ttu-id="6c36e-160">Określ identyfikator hello hello użytkownik, który ma dostęp do serwera toohello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-160">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="6c36e-161">Nie (Jeśli wybierzesz encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="6c36e-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="6c36e-162">hasło</span><span class="sxs-lookup"><span data-stu-id="6c36e-162">password</span></span> |<span data-ttu-id="6c36e-163">Określ hasło hello hello użytkownika (nazwa użytkownika).</span><span class="sxs-lookup"><span data-stu-id="6c36e-163">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="6c36e-164">Nie (Jeśli wybierzesz encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6c36e-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="6c36e-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6c36e-165">encryptedCredential</span></span> |<span data-ttu-id="6c36e-166">Określ poświadczenia hello zaszyfrowane, które można uzyskać, uruchamiając polecenie cmdlet hello AzureRmDataFactoryEncryptValue nowy.</span><span class="sxs-lookup"><span data-stu-id="6c36e-166">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="6c36e-167">Nie (Jeśli wybierzesz toospecify identyfikatora użytkownika i hasła w postaci zwykłego tekstu)</span><span class="sxs-lookup"><span data-stu-id="6c36e-167">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="6c36e-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6c36e-168">gatewayName</span></span> |<span data-ttu-id="6c36e-169">Określa nazwę hello hello bramy, że fabryka danych powinien używać serwera plików lokalnych toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="6c36e-169">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="6c36e-170">Tak</span><span class="sxs-lookup"><span data-stu-id="6c36e-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="6c36e-171">Przykładowe połączonej usługi i definicji zestawu danych</span><span class="sxs-lookup"><span data-stu-id="6c36e-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="6c36e-172">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="6c36e-172">Scenario</span></span> | <span data-ttu-id="6c36e-173">Host w definicji usługi połączonej</span><span class="sxs-lookup"><span data-stu-id="6c36e-173">Host in linked service definition</span></span> | <span data-ttu-id="6c36e-174">folderPath w definicji zestawu danych</span><span class="sxs-lookup"><span data-stu-id="6c36e-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c36e-175">Folder lokalny na komputerze bramy zarządzania danymi:</span><span class="sxs-lookup"><span data-stu-id="6c36e-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="6c36e-176">Przykłady: D:\\ \* lub D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="6c36e-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="6c36e-177">D:\\ \\ (dla danych zarządzania bramy 2.0 i nowsze wersje)</span><span class="sxs-lookup"><span data-stu-id="6c36e-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="6c36e-178">localhost (dla starszych niż 2.0 bramy zarządzania danych)</span><span class="sxs-lookup"><span data-stu-id="6c36e-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="6c36e-179">. \\ \\ lub folderu\\\\podfolder (dla danych zarządzania bramy 2.0 i nowsze wersje)</span><span class="sxs-lookup"><span data-stu-id="6c36e-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="6c36e-180">D:\\ \\ lub D:\\\\folderu\\\\podfolder (dla wersji bramy poniżej 2.0)</span><span class="sxs-lookup"><span data-stu-id="6c36e-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="6c36e-181">Zdalny folder udostępniony:</span><span class="sxs-lookup"><span data-stu-id="6c36e-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="6c36e-182">Przykłady: \\ \\MójSerwer\\udostępnianie\\ \* lub \\ \\MójSerwer\\udostępnianie\\folderu\\podfolderu\\*</span><span class="sxs-lookup"><span data-stu-id="6c36e-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="6c36e-183">\\\\\\\\MójSerwer\\\\udziału</span><span class="sxs-lookup"><span data-stu-id="6c36e-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="6c36e-184">. \\ \\ lub folderu\\\\podfolderu</span><span class="sxs-lookup"><span data-stu-id="6c36e-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="6c36e-185">Przykład: Przy użyciu nazwy użytkownika i hasła w postaci zwykłego tekstu</span><span class="sxs-lookup"><span data-stu-id="6c36e-185">Example: Using username and password in plain text</span></span>

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

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="6c36e-186">Przykład: Użycie encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="6c36e-186">Example: Using encryptedcredential</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="6c36e-187">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="6c36e-187">Dataset properties</span></span>
<span data-ttu-id="6c36e-188">Aby uzyskać pełną listę sekcje i właściwości, które są dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="6c36e-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="6c36e-189">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="6c36e-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="6c36e-190">sekcja typeProperties Hello jest różne dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="6c36e-190">hello typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="6c36e-191">Zawiera informacje, takie jak lokalizacja hello i format hello danych w magazynie danych hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-191">It provides information such as hello location and format of hello data in hello data store.</span></span> <span data-ttu-id="6c36e-192">Hello typeProperties sekcja dla zestawu danych hello typu **FileShare** ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="6c36e-192">hello typeProperties section for hello dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="6c36e-193">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6c36e-193">Property</span></span> | <span data-ttu-id="6c36e-194">Opis</span><span class="sxs-lookup"><span data-stu-id="6c36e-194">Description</span></span> | <span data-ttu-id="6c36e-195">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6c36e-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c36e-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="6c36e-196">folderPath</span></span> |<span data-ttu-id="6c36e-197">Określa folder toohello podrzędną hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-197">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="6c36e-198">Użyj znaku ucieczki hello ' \' znaków specjalnych w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-198">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="6c36e-199">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="6c36e-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="6c36e-200">Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka.</span><span class="sxs-lookup"><span data-stu-id="6c36e-200">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="6c36e-201">Tak</span><span class="sxs-lookup"><span data-stu-id="6c36e-201">Yes</span></span> |
| <span data-ttu-id="6c36e-202">fileName</span><span class="sxs-lookup"><span data-stu-id="6c36e-202">fileName</span></span> |<span data-ttu-id="6c36e-203">Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-203">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="6c36e-204">Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-204">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="6c36e-205">Gdy **fileName** dla wyjściowego zestawu danych nie został określony i **preserveHierarchy** nie została określona w zbiornika działania hello nazwa hello wygenerowany plik jest zgodny z formatem hello:</span><span class="sxs-lookup"><span data-stu-id="6c36e-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="6c36e-206">`Data.<Guid>.txt`(Przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="6c36e-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="6c36e-207">Nie</span><span class="sxs-lookup"><span data-stu-id="6c36e-207">No</span></span> |
| <span data-ttu-id="6c36e-208">obiektu fileFilter</span><span class="sxs-lookup"><span data-stu-id="6c36e-208">fileFilter</span></span> |<span data-ttu-id="6c36e-209">Określ toobe filtru używane tooselect podzbiór plików w hello folderPath, a nie wszystkich plików.</span><span class="sxs-lookup"><span data-stu-id="6c36e-209">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="6c36e-210">Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).</span><span class="sxs-lookup"><span data-stu-id="6c36e-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="6c36e-211">Przykład 1: "obiektu"fileFilter: "* .log"</span><span class="sxs-lookup"><span data-stu-id="6c36e-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="6c36e-212">Przykład 2: "obiektu"fileFilter: 2014 - 1-?. txt"</span><span class="sxs-lookup"><span data-stu-id="6c36e-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="6c36e-213">Należy pamiętać, że tego obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików.</span><span class="sxs-lookup"><span data-stu-id="6c36e-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="6c36e-214">Nie</span><span class="sxs-lookup"><span data-stu-id="6c36e-214">No</span></span> |
| <span data-ttu-id="6c36e-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="6c36e-215">partitionedBy</span></span> |<span data-ttu-id="6c36e-216">Toospecify partitionedBy dynamiczne folderPath/fileName służącego do dane szeregów czasowych.</span><span class="sxs-lookup"><span data-stu-id="6c36e-216">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="6c36e-217">Przykładem jest folderPath sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="6c36e-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="6c36e-218">Nie</span><span class="sxs-lookup"><span data-stu-id="6c36e-218">No</span></span> |
| <span data-ttu-id="6c36e-219">Format</span><span class="sxs-lookup"><span data-stu-id="6c36e-219">format</span></span> | <span data-ttu-id="6c36e-220">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="6c36e-220">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="6c36e-221">Zestaw hello **typu** właściwości w formacie tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="6c36e-221">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="6c36e-222">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="6c36e-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="6c36e-223">Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6c36e-223">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="6c36e-224">Nie</span><span class="sxs-lookup"><span data-stu-id="6c36e-224">No</span></span> |
| <span data-ttu-id="6c36e-225">Kompresja</span><span class="sxs-lookup"><span data-stu-id="6c36e-225">compression</span></span> | <span data-ttu-id="6c36e-226">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-226">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="6c36e-227">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="6c36e-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="6c36e-228">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="6c36e-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="6c36e-229">zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="6c36e-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="6c36e-230">Nie</span><span class="sxs-lookup"><span data-stu-id="6c36e-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="6c36e-231">Nie można użyć nazwy pliku i obiektu fileFilter jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="6c36e-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="6c36e-232">Za pomocą właściwości partitionedBy</span><span class="sxs-lookup"><span data-stu-id="6c36e-232">Using partitionedBy property</span></span>
<span data-ttu-id="6c36e-233">Jak wspomniano w poprzedniej sekcji hello, można określić folderPath dynamiczne i nazwę pliku dla danych serii czasu z hello **partitionedBy** właściwość [funkcje fabryki danych i zmienne systemu hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="6c36e-233">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="6c36e-234">Zobacz więcej informacji na temat zestawów danych szeregu czasowego, planowanie i wycinków, toounderstand [Tworzenie zbiorów danych](data-factory-create-datasets.md), [planowania i wykonywania](data-factory-scheduling-and-execution.md), i [tworzenie potoków](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6c36e-234">toounderstand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="6c36e-235">Przykład 1:</span><span class="sxs-lookup"><span data-stu-id="6c36e-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="6c36e-236">W tym przykładzie {wycinka} zostanie zastąpiony wartością hello hello fabryki danych zmiennej systemowej SliceStart w formacie hello (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="6c36e-236">In this example, {Slice} is replaced with hello value of hello Data Factory system variable SliceStart in hello format (YYYYMMDDHH).</span></span> <span data-ttu-id="6c36e-237">SliceStart odwołuje się czas toostart hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="6c36e-237">SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="6c36e-238">Witaj folderPath jest różne dla każdego wycinka.</span><span class="sxs-lookup"><span data-stu-id="6c36e-238">hello folderPath is different for each slice.</span></span> <span data-ttu-id="6c36e-239">Na przykład: wikidatagateway/wikisampledataout/2014100103 lub wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="6c36e-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="6c36e-240">Przykład 2:</span><span class="sxs-lookup"><span data-stu-id="6c36e-240">Sample 2:</span></span>

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

<span data-ttu-id="6c36e-241">W tym przykładzie rok, miesiąc, dzień i czas SliceStart są wyodrębniane do oddzielnych zmiennych, korzystających z hello folderPath i nazwę właściwości.</span><span class="sxs-lookup"><span data-stu-id="6c36e-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that hello folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="6c36e-242">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="6c36e-242">Copy activity properties</span></span>
<span data-ttu-id="6c36e-243">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="6c36e-243">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6c36e-244">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe zestawy danych i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="6c36e-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="6c36e-245">Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania.</span><span class="sxs-lookup"><span data-stu-id="6c36e-245">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span>

<span data-ttu-id="6c36e-246">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="6c36e-246">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="6c36e-247">Są przenoszenia danych z lokalnego systemu plików, należy ustawić typ źródła hello w przypadku działania kopiowania hello zbyt**FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="6c36e-247">If you are moving data from an on-premises file system, you set hello source type in hello copy activity too**FileSystemSource**.</span></span> <span data-ttu-id="6c36e-248">Podobnie jeśli przenosisz dane tooan lokalnego systemu plików, w przypadku działania kopiowania hello ustawić także typ ujścia hello**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="6c36e-248">Similarly, if you are moving data tooan on-premises file system, you set hello sink type in hello copy activity too**FileSystemSink**.</span></span> <span data-ttu-id="6c36e-249">Ta sekcja zawiera listę obsługiwanych przez FileSystemSource i FileSystemSink właściwości.</span><span class="sxs-lookup"><span data-stu-id="6c36e-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="6c36e-250">**FileSystemSource** obsługuje hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="6c36e-250">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="6c36e-251">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6c36e-251">Property</span></span> | <span data-ttu-id="6c36e-252">Opis</span><span class="sxs-lookup"><span data-stu-id="6c36e-252">Description</span></span> | <span data-ttu-id="6c36e-253">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="6c36e-253">Allowed values</span></span> | <span data-ttu-id="6c36e-254">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6c36e-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6c36e-255">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="6c36e-255">recursive</span></span> |<span data-ttu-id="6c36e-256">Wskazuje, czy hello są odczytywane dane rekursywnie z podfoldery hello lub tylko hello określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="6c36e-256">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="6c36e-257">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="6c36e-257">True, False (default)</span></span> |<span data-ttu-id="6c36e-258">Nie</span><span class="sxs-lookup"><span data-stu-id="6c36e-258">No</span></span> |

<span data-ttu-id="6c36e-259">**FileSystemSink** obsługuje hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="6c36e-259">**FileSystemSink** supports hello following properties:</span></span>

| <span data-ttu-id="6c36e-260">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6c36e-260">Property</span></span> | <span data-ttu-id="6c36e-261">Opis</span><span class="sxs-lookup"><span data-stu-id="6c36e-261">Description</span></span> | <span data-ttu-id="6c36e-262">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="6c36e-262">Allowed values</span></span> | <span data-ttu-id="6c36e-263">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6c36e-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6c36e-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="6c36e-264">copyBehavior</span></span> |<span data-ttu-id="6c36e-265">Definiuje zachowanie kopii hello, gdy źródłem hello jest BlobSource lub systemu plików.</span><span class="sxs-lookup"><span data-stu-id="6c36e-265">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="6c36e-266">**PreserveHierarchy:** zachowuje hello hierarchii plików w folderze docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-266">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="6c36e-267">Oznacza to, że hello względnej ścieżki folderu źródłowego toohello pliku źródłowego hello jest hello taka sama jak ścieżka względna hello hello docelowego pliku toohello docelowy folderu.</span><span class="sxs-lookup"><span data-stu-id="6c36e-267">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="6c36e-268">**FlattenHierarchy:** wszystkie pliki z folderu źródłowego hello są tworzone w hello pierwszy poziom folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="6c36e-268">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="6c36e-269">pliki docelowe Hello są tworzone z automatycznie generowaną nazwą.</span><span class="sxs-lookup"><span data-stu-id="6c36e-269">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="6c36e-270">**MergeFiles:** scala wszystkie pliki z pliku tooone folderu źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-270">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="6c36e-271">Jeśli określono hello pliku nazwy/nazwa obiektu blob, hello scalony plik nazwa jest hello określonej nazwy.</span><span class="sxs-lookup"><span data-stu-id="6c36e-271">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="6c36e-272">W przeciwnym razie jest nazwa pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="6c36e-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="6c36e-273">Nie</span><span class="sxs-lookup"><span data-stu-id="6c36e-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="6c36e-274">Przykłady cyklicznego i copyBehavior</span><span class="sxs-lookup"><span data-stu-id="6c36e-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="6c36e-275">W tej sekcji opisano hello efekty hello operacji kopiowania dla różnych kombinacji wartości dla właściwości cyklicznego i copyBehavior hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-275">This section describes hello resulting behavior of hello Copy operation for different combinations of values for hello recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="6c36e-276">wartości cykliczne</span><span class="sxs-lookup"><span data-stu-id="6c36e-276">recursive value</span></span> | <span data-ttu-id="6c36e-277">wartość copyBehavior</span><span class="sxs-lookup"><span data-stu-id="6c36e-277">copyBehavior value</span></span> | <span data-ttu-id="6c36e-278">Efekty</span><span class="sxs-lookup"><span data-stu-id="6c36e-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c36e-279">Wartość true</span><span class="sxs-lookup"><span data-stu-id="6c36e-279">true</span></span> |<span data-ttu-id="6c36e-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="6c36e-280">preserveHierarchy</span></span> |<span data-ttu-id="6c36e-281">Dla folderu źródłowego Folder1 z hello następujące struktury</span><span class="sxs-lookup"><span data-stu-id="6c36e-281">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="6c36e-282">Folder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-282">Folder1</span></span><br/><span data-ttu-id="6c36e-283">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6c36e-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6c36e-284">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6c36e-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6c36e-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6c36e-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6c36e-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6c36e-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6c36e-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6c36e-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6c36e-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6c36e-289">folder docelowy Hello Folder1 jest tworzony z hello takie same struktury jako źródło hello:</span><span class="sxs-lookup"><span data-stu-id="6c36e-289">hello target folder Folder1 is created with hello same structure as hello source:</span></span><br/><br/><span data-ttu-id="6c36e-290">Folder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-290">Folder1</span></span><br/><span data-ttu-id="6c36e-291">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6c36e-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6c36e-292">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6c36e-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6c36e-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6c36e-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6c36e-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6c36e-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6c36e-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6c36e-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6c36e-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="6c36e-297">Wartość true</span><span class="sxs-lookup"><span data-stu-id="6c36e-297">true</span></span> |<span data-ttu-id="6c36e-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="6c36e-298">flattenHierarchy</span></span> |<span data-ttu-id="6c36e-299">Dla folderu źródłowego Folder1 z hello następujące struktury</span><span class="sxs-lookup"><span data-stu-id="6c36e-299">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="6c36e-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-300">Folder1</span></span><br/><span data-ttu-id="6c36e-301">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6c36e-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6c36e-302">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6c36e-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6c36e-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6c36e-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6c36e-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6c36e-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6c36e-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6c36e-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6c36e-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6c36e-307">docelowy Hello Folder1 jest tworzony z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6c36e-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="6c36e-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-308">Folder1</span></span><br/><span data-ttu-id="6c36e-309">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="6c36e-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="6c36e-310">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2</span><span class="sxs-lookup"><span data-stu-id="6c36e-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="6c36e-311">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik3</span><span class="sxs-lookup"><span data-stu-id="6c36e-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="6c36e-312">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File4</span><span class="sxs-lookup"><span data-stu-id="6c36e-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="6c36e-313">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File5</span><span class="sxs-lookup"><span data-stu-id="6c36e-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="6c36e-314">Wartość true</span><span class="sxs-lookup"><span data-stu-id="6c36e-314">true</span></span> |<span data-ttu-id="6c36e-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="6c36e-315">mergeFiles</span></span> |<span data-ttu-id="6c36e-316">Dla folderu źródłowego Folder1 z hello następujące struktury</span><span class="sxs-lookup"><span data-stu-id="6c36e-316">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="6c36e-317">Folder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-317">Folder1</span></span><br/><span data-ttu-id="6c36e-318">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6c36e-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6c36e-319">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6c36e-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6c36e-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6c36e-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6c36e-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6c36e-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6c36e-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6c36e-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6c36e-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6c36e-324">docelowy Hello Folder1 jest tworzony z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6c36e-324">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="6c36e-325">Folder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-325">Folder1</span></span><br/><span data-ttu-id="6c36e-326">&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 + plik3 + File4 + pliku 5 zawartości są scalane w jeden plik o nazwie pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="6c36e-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="6c36e-327">wartość false</span><span class="sxs-lookup"><span data-stu-id="6c36e-327">false</span></span> |<span data-ttu-id="6c36e-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="6c36e-328">preserveHierarchy</span></span> |<span data-ttu-id="6c36e-329">Dla folderu źródłowego Folder1 z hello następujące struktury</span><span class="sxs-lookup"><span data-stu-id="6c36e-329">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="6c36e-330">Folder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-330">Folder1</span></span><br/><span data-ttu-id="6c36e-331">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6c36e-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6c36e-332">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6c36e-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6c36e-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6c36e-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6c36e-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6c36e-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6c36e-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6c36e-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6c36e-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6c36e-337">folder docelowy Hello Folder1 jest tworzony z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6c36e-337">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="6c36e-338">Folder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-338">Folder1</span></span><br/><span data-ttu-id="6c36e-339">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6c36e-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6c36e-340">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6c36e-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="6c36e-341">Subfolder1 plik3, File4 i File5 nie zostaje pobrana.</span><span class="sxs-lookup"><span data-stu-id="6c36e-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="6c36e-342">wartość false</span><span class="sxs-lookup"><span data-stu-id="6c36e-342">false</span></span> |<span data-ttu-id="6c36e-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="6c36e-343">flattenHierarchy</span></span> |<span data-ttu-id="6c36e-344">Dla folderu źródłowego Folder1 z hello następujące struktury</span><span class="sxs-lookup"><span data-stu-id="6c36e-344">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="6c36e-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-345">Folder1</span></span><br/><span data-ttu-id="6c36e-346">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6c36e-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6c36e-347">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6c36e-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6c36e-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6c36e-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6c36e-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6c36e-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6c36e-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6c36e-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6c36e-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6c36e-352">folder docelowy Hello Folder1 jest tworzony z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6c36e-352">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="6c36e-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-353">Folder1</span></span><br/><span data-ttu-id="6c36e-354">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="6c36e-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="6c36e-355">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2</span><span class="sxs-lookup"><span data-stu-id="6c36e-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="6c36e-356">Subfolder1 plik3, File4 i File5 nie zostaje pobrana.</span><span class="sxs-lookup"><span data-stu-id="6c36e-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="6c36e-357">wartość false</span><span class="sxs-lookup"><span data-stu-id="6c36e-357">false</span></span> |<span data-ttu-id="6c36e-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="6c36e-358">mergeFiles</span></span> |<span data-ttu-id="6c36e-359">Dla folderu źródłowego Folder1 z hello następujące struktury</span><span class="sxs-lookup"><span data-stu-id="6c36e-359">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="6c36e-360">Folder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-360">Folder1</span></span><br/><span data-ttu-id="6c36e-361">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6c36e-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6c36e-362">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6c36e-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6c36e-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6c36e-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6c36e-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6c36e-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6c36e-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6c36e-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6c36e-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6c36e-367">folder docelowy Hello Folder1 jest tworzony z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6c36e-367">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="6c36e-368">Folder1</span><span class="sxs-lookup"><span data-stu-id="6c36e-368">Folder1</span></span><br/><span data-ttu-id="6c36e-369">&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 zawartości są scalane w jeden plik o nazwie pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="6c36e-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="6c36e-370">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="6c36e-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="6c36e-371">Subfolder1 plik3, File4 i File5 nie zostaje pobrana.</span><span class="sxs-lookup"><span data-stu-id="6c36e-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="6c36e-372">Obsługiwane formaty plików i kompresji</span><span class="sxs-lookup"><span data-stu-id="6c36e-372">Supported file and compression formats</span></span>
<span data-ttu-id="6c36e-373">Zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md) artykuł na temat szczegółów.</span><span class="sxs-lookup"><span data-stu-id="6c36e-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a><span data-ttu-id="6c36e-374">Przykłady JSON do kopiowania tooand danych z systemu plików</span><span class="sxs-lookup"><span data-stu-id="6c36e-374">JSON examples for copying data tooand from file system</span></span>
<span data-ttu-id="6c36e-375">Witaj poniższe przykłady zapewniają definicje JSON przy użyciu hello można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6c36e-375">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6c36e-376">Przedstawiają sposób toocopy tooand danych z lokalnego systemu plików i magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c36e-376">They show how toocopy data tooand from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="6c36e-377">Można jednak skopiować dane *bezpośrednio* za pomocą dowolnego hello tooany źródeł z wychwytywanie hello na liście [obsługiwanych źródeł i wychwytywanie](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="6c36e-377">However, you can copy data *directly* from any of hello sources tooany of hello sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a><span data-ttu-id="6c36e-378">Przykład: Kopiowanie danych z tooAzure systemu lokalnego pliku magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="6c36e-378">Example: Copy data from an on-premises file system tooAzure Blob storage</span></span>
<span data-ttu-id="6c36e-379">W tym przykładzie pokazano sposób toocopy danych z tooAzure systemu lokalnego pliku magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="6c36e-379">This sample shows how toocopy data from an on-premises file system tooAzure Blob storage.</span></span> <span data-ttu-id="6c36e-380">przykład Witaj ma powitania po jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="6c36e-380">hello sample has hello following Data Factory entities:</span></span>

* <span data-ttu-id="6c36e-381">Połączonej usługi typu [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6c36e-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="6c36e-382">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6c36e-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="6c36e-383">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6c36e-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="6c36e-384">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6c36e-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="6c36e-385">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [FileSystemSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6c36e-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6c36e-386">następujące przykładowe Hello kopiuje dane szeregów czasowych z tooAzure systemu lokalnego pliku magazynu obiektów Blob, co godzinę.</span><span class="sxs-lookup"><span data-stu-id="6c36e-386">hello following sample copies time-series data from an on-premises file system tooAzure Blob storage every hour.</span></span> <span data-ttu-id="6c36e-387">Witaj JSON właściwości, które są używane w te przykłady są opisane w sekcjach hello po hello próbek.</span><span class="sxs-lookup"><span data-stu-id="6c36e-387">hello JSON properties that are used in these samples are described in hello sections after hello samples.</span></span>

<span data-ttu-id="6c36e-388">Pierwszym krokiem skonfigurować bramę zarządzania danymi zgodnie z instrukcjami hello [przenoszenie danych między lokalnych źródeł i w chmurze hello z brama zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="6c36e-388">As a first step, set up Data Management Gateway as per hello instructions in [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="6c36e-389">**Serwer plików lokalnych połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="6c36e-389">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="6c36e-390">Firma Microsoft zaleca używanie hello **encryptedCredential** właściwości zamiast hello **userid** i **hasło** właściwości.</span><span class="sxs-lookup"><span data-stu-id="6c36e-390">We recommend using hello **encryptedCredential** property instead hello **userid** and **password** properties.</span></span> <span data-ttu-id="6c36e-391">Zobacz [serwera plików połączona usługa](#linked-service-properties) szczegółowe informacje o tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="6c36e-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="6c36e-392">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="6c36e-392">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="6c36e-393">**Lokalnego pliku zestawu danych wejściowych systemu:**</span><span class="sxs-lookup"><span data-stu-id="6c36e-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="6c36e-394">Dane są pobierane z nowego pliku co godzinę.</span><span class="sxs-lookup"><span data-stu-id="6c36e-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="6c36e-395">Witaj folderPath i nazwę pliku, właściwości są określane na podstawie czasu rozpoczęcia hello hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="6c36e-395">hello folderPath and fileName properties are determined based on hello start time of hello slice.</span></span>  

<span data-ttu-id="6c36e-396">Ustawienie `"external": "true"` informuje fabryki danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-396">Setting `"external": "true"` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="6c36e-397">**Magazyn obiektów Blob Azure wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="6c36e-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="6c36e-398">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="6c36e-398">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6c36e-399">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="6c36e-399">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6c36e-400">Ścieżka folderu Hello używa hello rok, miesiąc, dzień i godzinę części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="6c36e-400">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

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

<span data-ttu-id="6c36e-401">**Działanie kopiowania w potoku z systemu plików źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="6c36e-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="6c36e-402">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="6c36e-402">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="6c36e-403">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**FileSystemSource**, i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6c36e-403">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a><span data-ttu-id="6c36e-404">Przykład: Skopiuj dane z bazy danych SQL Azure tooan lokalnego systemu plików</span><span class="sxs-lookup"><span data-stu-id="6c36e-404">Example: Copy data from Azure SQL Database tooan on-premises file system</span></span>
<span data-ttu-id="6c36e-405">następujące przykładowe pokazuje Hello:</span><span class="sxs-lookup"><span data-stu-id="6c36e-405">hello following sample shows:</span></span>

* <span data-ttu-id="6c36e-406">Połączonej usługi typu [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="6c36e-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="6c36e-407">Połączonej usługi typu [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6c36e-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="6c36e-408">Zestaw danych wejściowych typu [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6c36e-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="6c36e-409">Wyjściowy zestaw danych typu [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6c36e-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="6c36e-410">Potok z działania kopiowania, która używa [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) i [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6c36e-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="6c36e-411">Przykładowe Hello kopiuje dane szeregów czasowych z system plików lokalnych tooan tabeli Azure SQL co godzinę.</span><span class="sxs-lookup"><span data-stu-id="6c36e-411">hello sample copies time-series data from an Azure SQL table tooan on-premises file system every hour.</span></span> <span data-ttu-id="6c36e-412">Witaj JSON właściwości, które są używane w te przykłady zostały opisane w sekcjach po hello próbek.</span><span class="sxs-lookup"><span data-stu-id="6c36e-412">hello JSON properties that are used in these samples are described in sections after hello samples.</span></span>

<span data-ttu-id="6c36e-413">**Baza danych SQL Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="6c36e-413">**Azure SQL Database linked service:**</span></span>

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

<span data-ttu-id="6c36e-414">**Serwer plików lokalnych połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="6c36e-414">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="6c36e-415">Firma Microsoft zaleca używanie hello **encryptedCredential** właściwości zamiast hello **userid** i **hasło** właściwości.</span><span class="sxs-lookup"><span data-stu-id="6c36e-415">We recommend using hello **encryptedCredential** property instead of using hello **userid** and **password** properties.</span></span> <span data-ttu-id="6c36e-416">Zobacz [System plików połączona usługa](#linked-service-properties) szczegółowe informacje o tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="6c36e-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="6c36e-417">**Azure SQL wejściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="6c36e-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="6c36e-418">przykład Witaj założono, że po utworzeniu tabeli "MyTable" w języku SQL Azure i zawiera kolumnę o nazwie "timestampcolumn", szeregów czasowych danych.</span><span class="sxs-lookup"><span data-stu-id="6c36e-418">hello sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="6c36e-419">Ustawienie ``“external”: ”true”`` informuje fabryki danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-419">Setting ``“external”: ”true”`` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="6c36e-420">**Lokalnego pliku systemu wyjściowego zestawu danych:**</span><span class="sxs-lookup"><span data-stu-id="6c36e-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="6c36e-421">Dane są kopiowane tooa nowy plik co godzinę.</span><span class="sxs-lookup"><span data-stu-id="6c36e-421">Data is copied tooa new file every hour.</span></span> <span data-ttu-id="6c36e-422">Hello folderPath i nazwę pliku dla obiekt blob hello są określane na podstawie czasu rozpoczęcia hello hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="6c36e-422">hello folderPath and fileName for hello blob are determined based on hello start time of hello slice.</span></span>

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

<span data-ttu-id="6c36e-423">**Działanie kopiowania w potoku z SQL źródłowy i odbiorczy systemu plików:**</span><span class="sxs-lookup"><span data-stu-id="6c36e-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="6c36e-424">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="6c36e-424">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="6c36e-425">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**SqlSource**i hello **zbiornika** typu ustawiono zbyt**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="6c36e-425">In hello pipeline JSON definition, hello **source** type is set too**SqlSource**, and hello **sink** type is set too**FileSystemSink**.</span></span> <span data-ttu-id="6c36e-426">Zapytanie SQL Hello określony dla hello **SqlReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="6c36e-426">hello SQL query that is specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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


<span data-ttu-id="6c36e-427">Można również mapować kolumn z źródła toocolumns zestawu danych z zestawu danych zbiornika w definicji działania kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="6c36e-427">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="6c36e-428">Aby uzyskać więcej informacji, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6c36e-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6c36e-429">Wydajności i dostosowywanie</span><span class="sxs-lookup"><span data-stu-id="6c36e-429">Performance and tuning</span></span>
 <span data-ttu-id="6c36e-430">toolearn o kluczu czynniki tego wydajność hello wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize, zobacz hello [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="6c36e-430">toolearn about key factors that impact hello performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
