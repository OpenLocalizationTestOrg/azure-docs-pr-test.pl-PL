---
title: "aaaMove danych z serwera FTP przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toomove danych z serwera FTP przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="3d933-103">Przenoszenie danych z serwera FTP przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="3d933-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="3d933-104">W tym artykule opisano, jak toouse hello aktywności kopiowania w fabryce danych Azure toomove danych z serwera FTP.</span><span class="sxs-lookup"><span data-stu-id="3d933-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from an FTP server.</span></span> <span data-ttu-id="3d933-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3d933-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="3d933-106">Można skopiować danych z magazynu FTP serwera tooany obsługiwane ujścia danych.</span><span class="sxs-lookup"><span data-stu-id="3d933-106">You can copy data from an FTP server tooany supported sink data store.</span></span> <span data-ttu-id="3d933-107">Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="3d933-107">For a list of data stores supported as sinks by hello copy activity, see hello [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="3d933-108">Fabryka danych aktualnie obsługuje tylko przechowuje przenoszenia danych z danych tooother serwera FTP, ale nie przenoszenia danych z innych danych są przechowywane na serwerze tooan FTP.</span><span class="sxs-lookup"><span data-stu-id="3d933-108">Data Factory currently supports only moving data from an FTP server tooother data stores, but not moving data from other data stores tooan FTP server.</span></span> <span data-ttu-id="3d933-109">Obsługuje ona zarówno lokalnie i w chmurze, serwerami FTP.</span><span class="sxs-lookup"><span data-stu-id="3d933-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="3d933-110">działanie kopiowania Hello nie powoduje usunięcia pliku źródłowego hello po pomyślnie skopiowane toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="3d933-110">hello copy activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="3d933-111">Jeśli potrzebujesz pliku źródłowego hello toodelete po pomyślnym kopiowania, należy utworzyć plik hello toodelete działań niestandardowych i użyj hello działania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="3d933-111">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file, and use hello activity in hello pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="3d933-112">Włącz połączenie</span><span class="sxs-lookup"><span data-stu-id="3d933-112">Enable connectivity</span></span>
<span data-ttu-id="3d933-113">Jeśli przenosisz dane z **lokalnymi** magazynu danych chmury tooa serwera FTP (na przykład tooAzure magazynu obiektów Blob), zainstalować i używać bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="3d933-113">If you are moving data from an **on-premises** FTP server tooa cloud data store (for example, tooAzure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="3d933-114">Witaj brama zarządzania danymi jest agent klienta, który jest zainstalowany na komputerze lokalnym i umożliwia chmury usługi tooconnect tooan lokalnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="3d933-114">hello Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services tooconnect tooan on-premises resource.</span></span> <span data-ttu-id="3d933-115">Aby uzyskać więcej informacji, zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="3d933-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="3d933-116">Aby uzyskać instrukcje krok po kroku na temat ustawiania hello bramy i przy jego użyciu, zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="3d933-116">For step-by-step instructions on setting up hello gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="3d933-117">Używasz powitania serwera tooan FTP tooconnect bramy, nawet jeśli serwer hello znajduje się na infrastrukturę platformy Azure jako usługa (IaaS) maszynę wirtualną (VM).</span><span class="sxs-lookup"><span data-stu-id="3d933-117">You use hello gateway tooconnect tooan FTP server, even if hello server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="3d933-118">Jest możliwe tooinstall hello bramy na powitania sam lokalnymi maszyny lub maszyn wirtualnych IaaS hello serwera FTP.</span><span class="sxs-lookup"><span data-stu-id="3d933-118">It is possible tooinstall hello gateway on hello same on-premises machine or IaaS VM as hello FTP server.</span></span> <span data-ttu-id="3d933-119">Jednak zaleca się zainstalowanie bramy hello na osobnym komputerze fizycznym lub maszyn wirtualnych IaaS tooavoid rywalizacji i w celu zapewnienia lepszej wydajności.</span><span class="sxs-lookup"><span data-stu-id="3d933-119">However, we recommend that you install hello gateway on a separate machine or IaaS VM tooavoid resource contention, and for better performance.</span></span> <span data-ttu-id="3d933-120">Po zainstalowaniu bramy hello na osobnym komputerze maszyny hello powinien być serwer FTP hello tooaccess stanie.</span><span class="sxs-lookup"><span data-stu-id="3d933-120">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="3d933-121">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="3d933-121">Get started</span></span>
<span data-ttu-id="3d933-122">Można utworzyć potoku o działanie kopiowania, który przenosi dane ze źródła FTP przy użyciu różnych narzędzi lub interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="3d933-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="3d933-123">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="3d933-123">hello easiest way toocreate a pipeline is toouse hello **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="3d933-124">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) Przewodnik Szybki.</span><span class="sxs-lookup"><span data-stu-id="3d933-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="3d933-125">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **PowerShell**, **szablonu usługi Azure Resource Manager**, **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="3d933-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3d933-126">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3d933-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="3d933-127">Czy za pomocą narzędzia hello lub interfejsów API, wykonaj następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="3d933-127">Whether you use hello tools or APIs, perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="3d933-128">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="3d933-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="3d933-129">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3d933-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="3d933-130">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="3d933-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="3d933-131">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="3d933-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="3d933-132">Korzystając z narzędzia lub interfejsów API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="3d933-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="3d933-133">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z magazynu danych FTP, zobacz hello [przykład JSON: kopiowanie danych z obiektu blob tooAzure serwera FTP](#json-example-copy-data-from-ftp-server-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="3d933-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an FTP data store, see hello [JSON example: Copy data from FTP server tooAzure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="3d933-134">Aby uzyskać szczegółowe informacje o obsługiwanych toouse formaty plików i ich kompresji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="3d933-134">For details about supported file and compression formats toouse, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="3d933-135">Witaj następujące sekcje zawierają szczegółowe informacje o właściwościach JSON, które są używane toodefine fabryki danych jednostek określonych tooFTP.</span><span class="sxs-lookup"><span data-stu-id="3d933-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooFTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="3d933-136">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="3d933-136">Linked service properties</span></span>
<span data-ttu-id="3d933-137">Witaj w poniższej tabeli opisano usługi FTP połączone tooan określone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="3d933-137">hello following table describes JSON elements specific tooan FTP linked service.</span></span>

| <span data-ttu-id="3d933-138">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3d933-138">Property</span></span> | <span data-ttu-id="3d933-139">Opis</span><span class="sxs-lookup"><span data-stu-id="3d933-139">Description</span></span> | <span data-ttu-id="3d933-140">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3d933-140">Required</span></span> | <span data-ttu-id="3d933-141">Domyślne</span><span class="sxs-lookup"><span data-stu-id="3d933-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3d933-142">type</span><span class="sxs-lookup"><span data-stu-id="3d933-142">type</span></span> |<span data-ttu-id="3d933-143">Ustaw ten tooFtpServer.</span><span class="sxs-lookup"><span data-stu-id="3d933-143">Set this tooFtpServer.</span></span> |<span data-ttu-id="3d933-144">Tak</span><span class="sxs-lookup"><span data-stu-id="3d933-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="3d933-145">Host</span><span class="sxs-lookup"><span data-stu-id="3d933-145">host</span></span> |<span data-ttu-id="3d933-146">Określ nazwę hello lub adres IP powitania serwera FTP.</span><span class="sxs-lookup"><span data-stu-id="3d933-146">Specify hello name or IP address of hello FTP server.</span></span> |<span data-ttu-id="3d933-147">Tak</span><span class="sxs-lookup"><span data-stu-id="3d933-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="3d933-148">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="3d933-148">authenticationType</span></span> |<span data-ttu-id="3d933-149">Określ typ uwierzytelniania hello.</span><span class="sxs-lookup"><span data-stu-id="3d933-149">Specify hello authentication type.</span></span> |<span data-ttu-id="3d933-150">Tak</span><span class="sxs-lookup"><span data-stu-id="3d933-150">Yes</span></span> |<span data-ttu-id="3d933-151">Basic anonimowe</span><span class="sxs-lookup"><span data-stu-id="3d933-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="3d933-152">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="3d933-152">username</span></span> |<span data-ttu-id="3d933-153">Określ hello użytkownik, który ma serwer FTP toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="3d933-153">Specify hello user who has access toohello FTP server.</span></span> |<span data-ttu-id="3d933-154">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-154">No</span></span> |&nbsp; |
| <span data-ttu-id="3d933-155">hasło</span><span class="sxs-lookup"><span data-stu-id="3d933-155">password</span></span> |<span data-ttu-id="3d933-156">Określ hasło hello hello użytkownika (username).</span><span class="sxs-lookup"><span data-stu-id="3d933-156">Specify hello password for hello user (username).</span></span> |<span data-ttu-id="3d933-157">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-157">No</span></span> |&nbsp; |
| <span data-ttu-id="3d933-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3d933-158">encryptedCredential</span></span> |<span data-ttu-id="3d933-159">Określ serwer hello FTP tooaccess poświadczeń hello szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="3d933-159">Specify hello encrypted credential tooaccess hello FTP server.</span></span> |<span data-ttu-id="3d933-160">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-160">No</span></span> |&nbsp; |
| <span data-ttu-id="3d933-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3d933-161">gatewayName</span></span> |<span data-ttu-id="3d933-162">Określ nazwę hello hello bramy w serwer FTP lokalnymi tooan tooconnect brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="3d933-162">Specify hello name of hello gateway in Data Management Gateway tooconnect tooan on-premises FTP server.</span></span> |<span data-ttu-id="3d933-163">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-163">No</span></span> |&nbsp; |
| <span data-ttu-id="3d933-164">port</span><span class="sxs-lookup"><span data-stu-id="3d933-164">port</span></span> |<span data-ttu-id="3d933-165">Określ port hello, na które hello FTP nasłuchuje serwer.</span><span class="sxs-lookup"><span data-stu-id="3d933-165">Specify hello port on which hello FTP server is listening.</span></span> |<span data-ttu-id="3d933-166">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-166">No</span></span> |<span data-ttu-id="3d933-167">21</span><span class="sxs-lookup"><span data-stu-id="3d933-167">21</span></span> |
| <span data-ttu-id="3d933-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="3d933-168">enableSsl</span></span> |<span data-ttu-id="3d933-169">Określ, czy toouse FTP za pośrednictwem kanału SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="3d933-169">Specify whether toouse FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="3d933-170">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-170">No</span></span> |<span data-ttu-id="3d933-171">Wartość true</span><span class="sxs-lookup"><span data-stu-id="3d933-171">true</span></span> |
| <span data-ttu-id="3d933-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="3d933-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="3d933-173">Określ, czy tooenable serwera SSL certyfikatu weryfikacji, jeśli używasz FTP za pośrednictwem kanału SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="3d933-173">Specify whether tooenable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="3d933-174">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-174">No</span></span> |<span data-ttu-id="3d933-175">Wartość true</span><span class="sxs-lookup"><span data-stu-id="3d933-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="3d933-176">Uwierzytelnianie anonimowe</span><span class="sxs-lookup"><span data-stu-id="3d933-176">Use Anonymous authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="3d933-177">Użyj nazwy użytkownika i hasła w postaci zwykłego tekstu dla uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="3d933-177">Use username and password in plain text for basic authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="3d933-178">Użyj portu, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="3d933-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="3d933-179">EncryptedCredential używany do uwierzytelniania i bramy</span><span class="sxs-lookup"><span data-stu-id="3d933-179">Use encryptedCredential for authentication and gateway</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="3d933-180">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="3d933-180">Dataset properties</span></span>
<span data-ttu-id="3d933-181">Aby uzyskać pełną listę właściwości dostępnych do definiowania zestawów danych i sekcje, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="3d933-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="3d933-182">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="3d933-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="3d933-183">Witaj **typeProperties** sekcja jest różne dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="3d933-183">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="3d933-184">Zawiera informacje, które jest toohello określonego typu dataset.</span><span class="sxs-lookup"><span data-stu-id="3d933-184">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="3d933-185">Witaj **typeProperties** sekcja dla zestawu danych typu **FileShare** ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="3d933-185">hello **typeProperties** section for a dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="3d933-186">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3d933-186">Property</span></span> | <span data-ttu-id="3d933-187">Opis</span><span class="sxs-lookup"><span data-stu-id="3d933-187">Description</span></span> | <span data-ttu-id="3d933-188">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3d933-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3d933-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="3d933-189">folderPath</span></span> |<span data-ttu-id="3d933-190">Folder toohello podrzędną.</span><span class="sxs-lookup"><span data-stu-id="3d933-190">Subpath toohello folder.</span></span> <span data-ttu-id="3d933-191">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="3d933-191">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="3d933-192">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="3d933-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="3d933-193">Możesz łączyć tej właściwości z **partitionBy** ścieżki folderu toohave oparte na wycinku rozpoczęcia i zakończenia daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="3d933-193">You can combine this property with **partitionBy** toohave folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="3d933-194">Tak</span><span class="sxs-lookup"><span data-stu-id="3d933-194">Yes</span></span> |
| <span data-ttu-id="3d933-195">fileName</span><span class="sxs-lookup"><span data-stu-id="3d933-195">fileName</span></span> |<span data-ttu-id="3d933-196">Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="3d933-196">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="3d933-197">Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="3d933-197">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="3d933-198">Gdy **fileName** nie jest określony dla wyjściowego zestawu danych, nazwa hello hello wygenerowany plik jest zgodny z formatem hello:</span><span class="sxs-lookup"><span data-stu-id="3d933-198">When **fileName** is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="3d933-199">Dane. <Guid>.txt (przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="3d933-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="3d933-200">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-200">No</span></span> |
| <span data-ttu-id="3d933-201">obiektu fileFilter</span><span class="sxs-lookup"><span data-stu-id="3d933-201">fileFilter</span></span> |<span data-ttu-id="3d933-202">Określ filtr tooselect toobe używane podzbiór plików w hello **folderPath**, a nie wszystkich plików.</span><span class="sxs-lookup"><span data-stu-id="3d933-202">Specify a filter toobe used tooselect a subset of files in hello **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="3d933-203">Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).</span><span class="sxs-lookup"><span data-stu-id="3d933-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="3d933-204">Przykład 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="3d933-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="3d933-205">Przykład 2:`"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="3d933-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="3d933-206">**obiektu fileFilter** dotyczy wejściowy zestaw danych z udziału plików.</span><span class="sxs-lookup"><span data-stu-id="3d933-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="3d933-207">Ta właściwość nie jest obsługiwana z Hadoop Distributed pliku System (HDFS).</span><span class="sxs-lookup"><span data-stu-id="3d933-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="3d933-208">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-208">No</span></span> |
| <span data-ttu-id="3d933-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="3d933-209">partitionedBy</span></span> |<span data-ttu-id="3d933-210">Używane toospecify dynamicznym **folderPath** i **fileName** czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="3d933-210">Used toospecify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="3d933-211">Na przykład można określić **folderPath** który jest sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="3d933-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="3d933-212">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-212">No</span></span> |
| <span data-ttu-id="3d933-213">Format</span><span class="sxs-lookup"><span data-stu-id="3d933-213">format</span></span> | <span data-ttu-id="3d933-214">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="3d933-214">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="3d933-215">Zestaw hello **typu** właściwości w formacie tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="3d933-215">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="3d933-216">Aby uzyskać więcej informacji, zobacz hello [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format ](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="3d933-216">For more information, see hello [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="3d933-217">Jeśli chcesz toocopy pliki, są one między magazynów opartych na plikach (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="3d933-217">If you want toocopy files as they are between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="3d933-218">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-218">No</span></span> |
| <span data-ttu-id="3d933-219">Kompresja</span><span class="sxs-lookup"><span data-stu-id="3d933-219">compression</span></span> | <span data-ttu-id="3d933-220">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="3d933-220">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="3d933-221">Obsługiwane typy to **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**, i są obsługiwane poziomy **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="3d933-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="3d933-222">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="3d933-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="3d933-223">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-223">No</span></span> |
| <span data-ttu-id="3d933-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="3d933-224">useBinaryTransfer</span></span> |<span data-ttu-id="3d933-225">Określ, czy dane binarne hello toouse tryb transferu.</span><span class="sxs-lookup"><span data-stu-id="3d933-225">Specify whether toouse hello binary transfer mode.</span></span> <span data-ttu-id="3d933-226">Witaj wartości to PRAWDA dla trybu binarnego (jest to wartość domyślna hello), a wartość false dla ASCII.</span><span class="sxs-lookup"><span data-stu-id="3d933-226">hello values are true for binary mode (this is hello default value), and false for ASCII.</span></span> <span data-ttu-id="3d933-227">Ta właściwość jest używana tylko w przypadku hello typu skojarzonej połączonej usługi typu: SerwerFTP.</span><span class="sxs-lookup"><span data-stu-id="3d933-227">This property can only be used when hello associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="3d933-228">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="3d933-229">**Nazwa pliku** i **obiektu fileFilter** nie mogą być używane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="3d933-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-hello-partionedby-property"></a><span data-ttu-id="3d933-230">Użyj właściwości partionedBy hello</span><span class="sxs-lookup"><span data-stu-id="3d933-230">Use hello partionedBy property</span></span>
<span data-ttu-id="3d933-231">Jak wspomniano w poprzedniej sekcji hello, można określić dynamicznym **folderPath** i **fileName** czasu serii danych z hello **partitionedBy** właściwości.</span><span class="sxs-lookup"><span data-stu-id="3d933-231">As mentioned in hello previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with hello **partitionedBy** property.</span></span>

<span data-ttu-id="3d933-232">toolearn dotyczące zestawów danych serii czasu, planowania i wycinków, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md), [planowania i wykonywania](data-factory-scheduling-and-execution.md), i [tworzenie potoków](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="3d933-232">toolearn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="3d933-233">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="3d933-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="3d933-234">W tym przykładzie {wycinka} zostanie zastąpiony hello wartość zmiennej fabryki danych systemu SliceStart, w hello z formatem określonym (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="3d933-234">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart, in hello format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="3d933-235">Witaj SliceStart odwołuje się czas toostart hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="3d933-235">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="3d933-236">Ścieżka folderu Hello jest różne dla każdego wycinka.</span><span class="sxs-lookup"><span data-stu-id="3d933-236">hello folder path is different for each slice.</span></span> <span data-ttu-id="3d933-237">(Na przykład wikidatagateway/wikisampledataout/2014100103 lub wikidatagateway/wikisampledataout/2014100104).</span><span class="sxs-lookup"><span data-stu-id="3d933-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="3d933-238">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="3d933-238">Sample 2</span></span>

```json
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
<span data-ttu-id="3d933-239">W tym przykładzie hello rok, miesiąc, dzień i czas SliceStart są wyodrębniane do oddzielnych zmiennych, które są używane przez hello **folderPath** i **fileName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="3d933-239">In this example, hello year, month, day, and time of SliceStart are extracted into separate variables that are used by hello **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="3d933-240">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="3d933-240">Copy activity properties</span></span>
<span data-ttu-id="3d933-241">Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="3d933-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="3d933-242">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="3d933-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="3d933-243">Właściwości dostępne w hello **typeProperties** sekcji hello działania na powitania drugiej strony, zależą od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="3d933-243">Properties available in hello **typeProperties** section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="3d933-244">Dla działania kopiowania hello właściwości typu hello zależy od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="3d933-244">For hello copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="3d933-245">W przypadku działania kopiowania, gdy źródłem hello jest typu **FileSystemSource**, hello następujące właściwości są dostępne w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="3d933-245">In copy activity, when hello source is of type **FileSystemSource**, hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="3d933-246">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3d933-246">Property</span></span> | <span data-ttu-id="3d933-247">Opis</span><span class="sxs-lookup"><span data-stu-id="3d933-247">Description</span></span> | <span data-ttu-id="3d933-248">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="3d933-248">Allowed values</span></span> | <span data-ttu-id="3d933-249">Wymagane</span><span class="sxs-lookup"><span data-stu-id="3d933-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3d933-250">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="3d933-250">recursive</span></span> |<span data-ttu-id="3d933-251">Wskazuje, czy hello są odczytywane dane rekursywnie z podfoldery hello lub tylko hello określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="3d933-251">Indicates whether hello data is read recursively from hello subfolders, or only from hello specified folder.</span></span> |<span data-ttu-id="3d933-252">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="3d933-252">True, False (default)</span></span> |<span data-ttu-id="3d933-253">Nie</span><span class="sxs-lookup"><span data-stu-id="3d933-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a><span data-ttu-id="3d933-254">Przykład JSON: kopiowanie danych z tooAzure serwera FTP obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="3d933-254">JSON example: Copy data from FTP server tooAzure Blob</span></span>
<span data-ttu-id="3d933-255">W tym przykładzie pokazano sposób toocopy danych z tooAzure serwera FTP magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="3d933-255">This sample shows how toocopy data from an FTP server tooAzure Blob storage.</span></span> <span data-ttu-id="3d933-256">Jednak dane mogą być kopiowane bezpośrednio tooany hello wychwytywanie hello podane w [obsługiwane formaty i magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats), za pomocą działania kopiowania hello w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="3d933-256">However, data can be copied directly tooany of hello sinks stated in hello [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using hello copy activity in Data Factory.</span></span>  

<span data-ttu-id="3d933-257">Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="3d933-257">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="3d933-258">Połączonej usługi typu [SerwerFTP](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="3d933-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="3d933-259">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="3d933-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="3d933-260">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [udziału plików](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="3d933-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="3d933-261">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="3d933-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="3d933-262">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [FileSystemSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="3d933-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="3d933-263">przykład Witaj kopiuje dane z tooan serwera FTP obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="3d933-263">hello sample copies data from an FTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="3d933-264">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="3d933-264">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="3d933-265">Połączona usługa FTP</span><span class="sxs-lookup"><span data-stu-id="3d933-265">FTP linked service</span></span>

<span data-ttu-id="3d933-266">W tym przykładzie używane uwierzytelnianie podstawowe, hello nazwy użytkownika i hasła w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="3d933-266">This example uses basic authentication, with hello user name and password in plain text.</span></span> <span data-ttu-id="3d933-267">Można także użyć jednej z hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="3d933-267">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="3d933-268">Uwierzytelnianie anonimowe</span><span class="sxs-lookup"><span data-stu-id="3d933-268">Anonymous authentication</span></span>
* <span data-ttu-id="3d933-269">Uwierzytelnianie podstawowe z zaszyfrowane poświadczenia</span><span class="sxs-lookup"><span data-stu-id="3d933-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="3d933-270">FTP over SSL/TLS (FTPS)</span><span class="sxs-lookup"><span data-stu-id="3d933-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="3d933-271">Zobacz hello [FTP połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.</span><span class="sxs-lookup"><span data-stu-id="3d933-271">See hello [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a><span data-ttu-id="3d933-272">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3d933-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="3d933-273">Zestaw danych wejściowych FTP</span><span class="sxs-lookup"><span data-stu-id="3d933-273">FTP input dataset</span></span>

<span data-ttu-id="3d933-274">Ten zestaw danych odwołuje się folder toohello FTP `mysharedfolder` i plik `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="3d933-274">This dataset refers toohello FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="3d933-275">Witaj potoku kopie hello toohello docelowej lokalizacji plików.</span><span class="sxs-lookup"><span data-stu-id="3d933-275">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="3d933-276">Ustawienie **zewnętrznych** za**true** informuje usługi fabryka danych hello tego zestawu danych hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="3d933-276">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory, and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="3d933-277">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3d933-277">Azure Blob output dataset</span></span>

<span data-ttu-id="3d933-278">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="3d933-278">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3d933-279">Ścieżka folderu Hello obiektu blob hello dynamicznie jest obliczane, na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="3d933-279">hello folder path for hello blob is dynamically evaluated, based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="3d933-280">Ścieżka folderu Hello używa hello rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="3d933-280">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="3d933-281">Działanie kopiowania w potoku z zbiornika źródła i obiektów blob systemu plików</span><span class="sxs-lookup"><span data-stu-id="3d933-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="3d933-282">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="3d933-282">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="3d933-283">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**FileSystemSource**i hello **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="3d933-283">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and hello **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="3d933-284">toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="3d933-284">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d933-285">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d933-285">Next steps</span></span>
<span data-ttu-id="3d933-286">Zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="3d933-286">See hello following articles:</span></span>

* <span data-ttu-id="3d933-287">toolearn o kluczu czynniki tego wydajności wpływ przenoszenia danych (działanie kopiowania) w fabryce danych i różne sposoby toooptimize, zobacz hello [skopiuj wydajności działania i dostrajania przewodnik](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="3d933-287">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="3d933-288">Aby uzyskać instrukcje tworzenia potoku z działaniem kopiowania, zobacz hello [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="3d933-288">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
