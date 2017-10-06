---
title: "aaaMove danych ze źródła HTTP - Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toomove danych z lokalnego lub w chmurze HTTP źródła przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="2aaea-103">Przenoszenie danych ze źródła HTTP przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="2aaea-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="2aaea-104">W tym artykule opisano, jak toouse hello działanie kopiowania danych toomove fabryki danych Azure z tooa punktu końcowego HTTP na lokalnej/w chmurze obsługiwana ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="2aaea-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud HTTP endpoint tooa supported sink data store.</span></span> <span data-ttu-id="2aaea-105">W tym artykule opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólne omówienie przepływu danych kopię działania i hello listy magazynów danych są obsługiwane jako źródła/sink.</span><span class="sxs-lookup"><span data-stu-id="2aaea-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="2aaea-106">Fabryka danych aktualnie obsługuje tylko przenoszenia danych z HTTP źródła tooother magazyny danych, ale nie przenoszenia danych z innych danych przechowuje docelowego tooan HTTP.</span><span class="sxs-lookup"><span data-stu-id="2aaea-106">Data factory currently supports only moving data from an HTTP source tooother data stores, but not moving data from other data stores tooan HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="2aaea-107">Obsługiwane scenariusze i typy uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="2aaea-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="2aaea-108">Można użyć tych danych tooretrieve łącznika HTTP z **zarówno w chmurze, jak i dla lokalnego punktu końcowego protokołu HTTP/s** przy użyciu protokołu HTTP **UZYSKAĆ** lub **POST** metody.</span><span class="sxs-lookup"><span data-stu-id="2aaea-108">You can use this HTTP connector tooretrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="2aaea-109">obsługiwane są następujące typy uwierzytelniania Hello: **anonimowe**, **podstawowe**, **szyfrowanego**, **Windows**, i  **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="2aaea-109">hello following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="2aaea-110">Należy zwrócić uwagę hello różnicę między tym łącznika i hello [łącznika sieci Web w tabeli](data-factory-web-table-connector.md) jest: hello ostatnie jest używane tooextract tabeli zawartości ze strony HTML sieci web.</span><span class="sxs-lookup"><span data-stu-id="2aaea-110">Note hello difference between this connector and hello [Web table connector](data-factory-web-table-connector.md) is: hello latter is used tooextract table content from web HTML page.</span></span>

<span data-ttu-id="2aaea-111">Podczas kopiowania danych z lokalnego punktu końcowego HTTP, należy zainstalować bramę zarządzania danymi w środowisku lokalnymi hello/Azure maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2aaea-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="2aaea-112">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) toolearn artykuł o brama zarządzania danymi i instrukcje krok po kroku dotyczące konfigurowania bramy hello.</span><span class="sxs-lookup"><span data-stu-id="2aaea-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2aaea-113">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="2aaea-113">Getting started</span></span>
<span data-ttu-id="2aaea-114">Można utworzyć potok z działania kopiowania, który przenosi dane ze źródła HTTP przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="2aaea-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="2aaea-115">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="2aaea-115">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="2aaea-116">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="2aaea-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="2aaea-117">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="2aaea-117">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2aaea-118">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2aaea-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="2aaea-119">Dla formatu JSON przykłady toocopy danych z tooAzure źródła HTTP magazynu obiektów Blob, zobacz [przykłady JSON](#json-examples) części w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="2aaea-119">For JSON samples toocopy data from HTTP source tooAzure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2aaea-120">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="2aaea-120">Linked service properties</span></span>
<span data-ttu-id="2aaea-121">Hello w poniższej tabeli przedstawiono opis usługi określonego tooHTTP połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="2aaea-121">hello following table provides description for JSON elements specific tooHTTP linked service.</span></span>

| <span data-ttu-id="2aaea-122">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2aaea-122">Property</span></span> | <span data-ttu-id="2aaea-123">Opis</span><span class="sxs-lookup"><span data-stu-id="2aaea-123">Description</span></span> | <span data-ttu-id="2aaea-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2aaea-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2aaea-125">type</span><span class="sxs-lookup"><span data-stu-id="2aaea-125">type</span></span> | <span data-ttu-id="2aaea-126">musi mieć ustawioną właściwość type Hello: `Http`.</span><span class="sxs-lookup"><span data-stu-id="2aaea-126">hello type property must be set to: `Http`.</span></span> | <span data-ttu-id="2aaea-127">Tak</span><span class="sxs-lookup"><span data-stu-id="2aaea-127">Yes</span></span> |
| <span data-ttu-id="2aaea-128">adres URL</span><span class="sxs-lookup"><span data-stu-id="2aaea-128">url</span></span> | <span data-ttu-id="2aaea-129">Podstawowa toohello adres URL serwera sieci Web</span><span class="sxs-lookup"><span data-stu-id="2aaea-129">Base URL toohello Web Server</span></span> | <span data-ttu-id="2aaea-130">Tak</span><span class="sxs-lookup"><span data-stu-id="2aaea-130">Yes</span></span> |
| <span data-ttu-id="2aaea-131">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="2aaea-131">authenticationType</span></span> | <span data-ttu-id="2aaea-132">Określa typ uwierzytelniania hello.</span><span class="sxs-lookup"><span data-stu-id="2aaea-132">Specifies hello authentication type.</span></span> <span data-ttu-id="2aaea-133">Dozwolone wartości to: **anonimowe**, **podstawowe**, **szyfrowanego**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="2aaea-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="2aaea-134">Dotyczą odpowiednio toosections pod tą tabelą więcej właściwości i przykłady JSON dla tych typów uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="2aaea-134">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="2aaea-135">Tak</span><span class="sxs-lookup"><span data-stu-id="2aaea-135">Yes</span></span> |
| <span data-ttu-id="2aaea-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="2aaea-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="2aaea-137">Określ, czy tooenable serwera SSL certyfikatu weryfikacji, jeśli źródło jest serwer sieci Web protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="2aaea-137">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="2aaea-138">Nie, domyślna to true</span><span class="sxs-lookup"><span data-stu-id="2aaea-138">No, default is true</span></span> |
| <span data-ttu-id="2aaea-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2aaea-139">gatewayName</span></span> | <span data-ttu-id="2aaea-140">Nazwa tooan tooconnect brama zarządzania danymi hello lokalnego źródła HTTP.</span><span class="sxs-lookup"><span data-stu-id="2aaea-140">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="2aaea-141">Tak, jeśli kopiowanie danych z lokalnego źródła HTTP.</span><span class="sxs-lookup"><span data-stu-id="2aaea-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="2aaea-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="2aaea-142">encryptedCredential</span></span> | <span data-ttu-id="2aaea-143">Zaszyfrowane poświadczenia tooaccess hello punkt końcowy HTTP.</span><span class="sxs-lookup"><span data-stu-id="2aaea-143">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="2aaea-144">Wygenerowany automatycznie podczas konfigurowania hello informacje o uwierzytelnianiu w kopii kreatora lub hello ClickOnce podręcznego okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2aaea-144">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="2aaea-145">Nie.</span><span class="sxs-lookup"><span data-stu-id="2aaea-145">No.</span></span> <span data-ttu-id="2aaea-146">Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera HTTP.</span><span class="sxs-lookup"><span data-stu-id="2aaea-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="2aaea-147">Zobacz [przenoszenie danych między lokalnych źródeł i w chmurze hello z brama zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md) szczegółowe informacje na temat ustawiania poświadczeń dla źródła danych łącznika HTTP lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="2aaea-147">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="2aaea-148">Uwierzytelnianie podstawowe, szyfrowane lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="2aaea-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="2aaea-149">Ustaw `authenticationType` jako `Basic`, `Digest`, lub `Windows`i określ następujące właściwości poza hello łącznika HTTP ogólnego tych wprowadzonych powyżej hello:</span><span class="sxs-lookup"><span data-stu-id="2aaea-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="2aaea-150">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2aaea-150">Property</span></span> | <span data-ttu-id="2aaea-151">Opis</span><span class="sxs-lookup"><span data-stu-id="2aaea-151">Description</span></span> | <span data-ttu-id="2aaea-152">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2aaea-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2aaea-153">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="2aaea-153">username</span></span> | <span data-ttu-id="2aaea-154">Nazwa użytkownika tooaccess hello punkt końcowy HTTP.</span><span class="sxs-lookup"><span data-stu-id="2aaea-154">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="2aaea-155">Tak</span><span class="sxs-lookup"><span data-stu-id="2aaea-155">Yes</span></span> |
| <span data-ttu-id="2aaea-156">hasło</span><span class="sxs-lookup"><span data-stu-id="2aaea-156">password</span></span> | <span data-ttu-id="2aaea-157">Hasło dla użytkownika hello (nazwa_użytkownika).</span><span class="sxs-lookup"><span data-stu-id="2aaea-157">Password for hello user (username).</span></span> | <span data-ttu-id="2aaea-158">Tak</span><span class="sxs-lookup"><span data-stu-id="2aaea-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="2aaea-159">Przykład: uwierzytelnianie podstawowe, szyfrowane lub systemu Windows</span><span class="sxs-lookup"><span data-stu-id="2aaea-159">Example: using Basic, Digest, or Windows authentication</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="2aaea-160">Przy użyciu uwierzytelniania ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="2aaea-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="2aaea-161">Ustaw toouse uwierzytelnianie podstawowe, `authenticationType` jako `ClientCertificate`i określ następujące właściwości poza hello łącznika HTTP ogólnego tych wprowadzonych powyżej hello:</span><span class="sxs-lookup"><span data-stu-id="2aaea-161">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="2aaea-162">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2aaea-162">Property</span></span> | <span data-ttu-id="2aaea-163">Opis</span><span class="sxs-lookup"><span data-stu-id="2aaea-163">Description</span></span> | <span data-ttu-id="2aaea-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2aaea-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2aaea-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="2aaea-165">embeddedCertData</span></span> | <span data-ttu-id="2aaea-166">zawartość algorytmem Base64 Hello danych binarnych hello pliku wymiany informacji osobistych (PFX).</span><span class="sxs-lookup"><span data-stu-id="2aaea-166">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="2aaea-167">Określ albo hello `embeddedCertData` lub `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="2aaea-167">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="2aaea-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="2aaea-168">certThumbprint</span></span> | <span data-ttu-id="2aaea-169">Witaj odcisk palca certyfikatu hello, który został zainstalowany na komputerze bramy magazynu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="2aaea-169">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="2aaea-170">Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego źródła HTTP.</span><span class="sxs-lookup"><span data-stu-id="2aaea-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="2aaea-171">Określ albo hello `embeddedCertData` lub `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="2aaea-171">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="2aaea-172">hasło</span><span class="sxs-lookup"><span data-stu-id="2aaea-172">password</span></span> | <span data-ttu-id="2aaea-173">Hasło skojarzone z certyfikatem hello.</span><span class="sxs-lookup"><span data-stu-id="2aaea-173">Password associated with hello certificate.</span></span> | <span data-ttu-id="2aaea-174">Nie</span><span class="sxs-lookup"><span data-stu-id="2aaea-174">No</span></span> |

<span data-ttu-id="2aaea-175">Jeśli używasz `certThumbprint` dla certyfikatu uwierzytelniania i hello jest zainstalowany w magazynie osobistym hello hello komputera lokalnego, należy Usługa bramy toohello toogrant hello uprawnienia do odczytu:</span><span class="sxs-lookup"><span data-stu-id="2aaea-175">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="2aaea-176">Uruchom program Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="2aaea-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="2aaea-177">Dodaj hello **certyfikaty** tego hello cele przystawki **komputera lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="2aaea-177">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="2aaea-178">Rozwiń węzeł **certyfikaty**, **osobistych**i kliknij przycisk **certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="2aaea-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="2aaea-179">Kliknij prawym przyciskiem myszy hello certyfikatu z magazynu osobistego hello, a następnie wybierz **wszystkie zadania**->**Zarządzaj kluczami prywatnymi...**</span><span class="sxs-lookup"><span data-stu-id="2aaea-179">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="2aaea-180">Na powitania **zabezpieczeń** , Dodaj konto użytkownika hello, pod którą jest uruchomiona usługa hosta bramy zarządzania danymi w certyfikatem toohello hello dostęp do odczytu.</span><span class="sxs-lookup"><span data-stu-id="2aaea-180">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="2aaea-181">Przykład: przy użyciu certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="2aaea-181">Example: using client certificate</span></span>
<span data-ttu-id="2aaea-182">To połączone usługi łączy danych fabryki tooan lokalnymi HTTP serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="2aaea-182">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="2aaea-183">Używa certyfikatu klienta, który jest zainstalowany na komputerze hello z zainstalowana brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="2aaea-183">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="2aaea-184">Przykład: przy użyciu certyfikatu klienta w pliku</span><span class="sxs-lookup"><span data-stu-id="2aaea-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="2aaea-185">To połączone usługi łączy danych fabryki tooan lokalnymi HTTP serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="2aaea-185">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="2aaea-186">Za pomocą pliku certyfikatu klienta na powitania maszyny i zainstalować bramę zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="2aaea-186">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="2aaea-187">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="2aaea-187">Dataset properties</span></span>
<span data-ttu-id="2aaea-188">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2aaea-188">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2aaea-189">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="2aaea-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2aaea-190">Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="2aaea-190">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="2aaea-191">Witaj typeProperties sekcja dla zestawu danych typu **Http** ma następujące właściwości hello</span><span class="sxs-lookup"><span data-stu-id="2aaea-191">hello typeProperties section for dataset of type **Http** has hello following properties</span></span>

| <span data-ttu-id="2aaea-192">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2aaea-192">Property</span></span> | <span data-ttu-id="2aaea-193">Opis</span><span class="sxs-lookup"><span data-stu-id="2aaea-193">Description</span></span> | <span data-ttu-id="2aaea-194">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2aaea-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2aaea-195">type</span><span class="sxs-lookup"><span data-stu-id="2aaea-195">type</span></span> | <span data-ttu-id="2aaea-196">Określony typ hello hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="2aaea-196">Specified hello type of hello dataset.</span></span> <span data-ttu-id="2aaea-197">musi być ustawiona zbyt`Http`.</span><span class="sxs-lookup"><span data-stu-id="2aaea-197">must be set too`Http`.</span></span> | <span data-ttu-id="2aaea-198">Tak</span><span class="sxs-lookup"><span data-stu-id="2aaea-198">Yes</span></span> |
| <span data-ttu-id="2aaea-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="2aaea-199">relativeUrl</span></span> | <span data-ttu-id="2aaea-200">Względny adres URL toohello zasób zawierający dane hello.</span><span class="sxs-lookup"><span data-stu-id="2aaea-200">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="2aaea-201">Jeśli ścieżka nie jest określona, tylko hello adresu URL określonego w definicji usługi połączone hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="2aaea-201">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="2aaea-202">tooconstruct dynamicznego adresu URL, można użyć [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md), np. "relativeUrl": "$$Text.Format (" / Moje/raport? miesiąca = {0: yyyy}-{0:MM} & formatowaniu = csv ", SliceStart)".</span><span class="sxs-lookup"><span data-stu-id="2aaea-202">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="2aaea-203">Nie</span><span class="sxs-lookup"><span data-stu-id="2aaea-203">No</span></span> |
| <span data-ttu-id="2aaea-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="2aaea-204">requestMethod</span></span> | <span data-ttu-id="2aaea-205">Metoda HTTP.</span><span class="sxs-lookup"><span data-stu-id="2aaea-205">Http method.</span></span> <span data-ttu-id="2aaea-206">Dozwolone wartości to **UZYSKAĆ** lub **POST**.</span><span class="sxs-lookup"><span data-stu-id="2aaea-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="2aaea-207">Nie.</span><span class="sxs-lookup"><span data-stu-id="2aaea-207">No.</span></span> <span data-ttu-id="2aaea-208">Domyślnie jest `GET`.</span><span class="sxs-lookup"><span data-stu-id="2aaea-208">Default is `GET`.</span></span> |
| <span data-ttu-id="2aaea-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="2aaea-209">additionalHeaders</span></span> | <span data-ttu-id="2aaea-210">Dodatkowych nagłówków żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="2aaea-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="2aaea-211">Nie</span><span class="sxs-lookup"><span data-stu-id="2aaea-211">No</span></span> |
| <span data-ttu-id="2aaea-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="2aaea-212">requestBody</span></span> | <span data-ttu-id="2aaea-213">Treść żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="2aaea-213">Body for HTTP request.</span></span> | <span data-ttu-id="2aaea-214">Nie</span><span class="sxs-lookup"><span data-stu-id="2aaea-214">No</span></span> |
| <span data-ttu-id="2aaea-215">Format</span><span class="sxs-lookup"><span data-stu-id="2aaea-215">format</span></span> | <span data-ttu-id="2aaea-216">Jeśli chcesz, aby toosimply **pobrać hello danych z punktu końcowego HTTP jako — jest** bez podczas analizowania, Pomiń ten ustawienia formatu.</span><span class="sxs-lookup"><span data-stu-id="2aaea-216">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="2aaea-217">Należy odpowiedzi hello HTTP tooparse zawartości podczas kopiowania są obsługiwane następujące typy format hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="2aaea-217">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="2aaea-218">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="2aaea-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="2aaea-219">Nie</span><span class="sxs-lookup"><span data-stu-id="2aaea-219">No</span></span> |
| <span data-ttu-id="2aaea-220">Kompresja</span><span class="sxs-lookup"><span data-stu-id="2aaea-220">compression</span></span> | <span data-ttu-id="2aaea-221">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="2aaea-221">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="2aaea-222">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="2aaea-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="2aaea-223">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="2aaea-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="2aaea-224">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="2aaea-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="2aaea-225">Nie</span><span class="sxs-lookup"><span data-stu-id="2aaea-225">No</span></span> |

### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="2aaea-226">Przykład: hello metoda GET (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="2aaea-226">Example: using hello GET (default) method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a><span data-ttu-id="2aaea-227">Przykład: przy użyciu metody POST hello</span><span class="sxs-lookup"><span data-stu-id="2aaea-227">Example: using hello POST method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="2aaea-228">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="2aaea-228">Copy activity properties</span></span>
<span data-ttu-id="2aaea-229">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2aaea-229">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2aaea-230">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="2aaea-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="2aaea-231">Właściwości dostępne w hello **typeProperties** sekcji aktywności hello na powitania drugiej zależą od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="2aaea-231">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="2aaea-232">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="2aaea-232">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="2aaea-233">Obecnie, gdy hello źródła w przypadku działania kopiowania jest typu **HttpSource**, hello następujące właściwości są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="2aaea-233">Currently, when hello source in copy activity is of type **HttpSource**, hello following properties are supported.</span></span>

| <span data-ttu-id="2aaea-234">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2aaea-234">Property</span></span> | <span data-ttu-id="2aaea-235">Opis</span><span class="sxs-lookup"><span data-stu-id="2aaea-235">Description</span></span> | <span data-ttu-id="2aaea-236">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2aaea-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="2aaea-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="2aaea-237">httpRequestTimeout</span></span> | <span data-ttu-id="2aaea-238">Witaj limitu czasu (TimeSpan) dla tooget żądania HTTP hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2aaea-238">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="2aaea-239">Jest tooget hello limitu czasu odpowiedzi, hello limitu czasu tooread odpowiedzi danych.</span><span class="sxs-lookup"><span data-stu-id="2aaea-239">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="2aaea-240">Nie.</span><span class="sxs-lookup"><span data-stu-id="2aaea-240">No.</span></span> <span data-ttu-id="2aaea-241">Wartość domyślna: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="2aaea-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="2aaea-242">Obsługiwane formaty plików i kompresji</span><span class="sxs-lookup"><span data-stu-id="2aaea-242">Supported file and compression formats</span></span>
<span data-ttu-id="2aaea-243">Zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md) artykuł na temat szczegółów.</span><span class="sxs-lookup"><span data-stu-id="2aaea-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="2aaea-244">Przykłady JSON</span><span class="sxs-lookup"><span data-stu-id="2aaea-244">JSON examples</span></span>
<span data-ttu-id="2aaea-245">Poniższy przykład Hello Podaj definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2aaea-245">hello following example provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2aaea-246">Przedstawiają sposób źródła danych toocopy z protokołu HTTP, tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="2aaea-246">They show how toocopy data from HTTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="2aaea-247">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła tooany z wychwytywanie hello wyrażony w [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="2aaea-247">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a><span data-ttu-id="2aaea-248">Przykład: Kopiowanie danych z tooAzure źródła HTTP magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="2aaea-248">Example: Copy data from HTTP source tooAzure Blob Storage</span></span>
<span data-ttu-id="2aaea-249">Witaj fabryki danych rozwiązania dla tego przykładu zawiera powitania po jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="2aaea-249">hello Data Factory solution for this sample contains hello following Data Factory entities:</span></span>

1. <span data-ttu-id="2aaea-250">Połączonej usługi typu [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2aaea-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="2aaea-251">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2aaea-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2aaea-252">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [Http](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2aaea-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="2aaea-253">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2aaea-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2aaea-254">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [HttpSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2aaea-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2aaea-255">przykład Witaj kopiuje dane z tooan źródła HTTP obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="2aaea-255">hello sample copies data from an HTTP source tooan Azure blob every hour.</span></span> <span data-ttu-id="2aaea-256">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="2aaea-256">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="2aaea-257">Usługa HTTP połączone</span><span class="sxs-lookup"><span data-stu-id="2aaea-257">HTTP linked service</span></span>
<span data-ttu-id="2aaea-258">W przykładzie używa hello HTTP połączonej usługi przy użyciu uwierzytelniania anonimowego.</span><span class="sxs-lookup"><span data-stu-id="2aaea-258">This example uses hello HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="2aaea-259">Zobacz [HTTP połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.</span><span class="sxs-lookup"><span data-stu-id="2aaea-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="2aaea-260">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2aaea-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="2aaea-261">Zestaw danych wejściowych HTTP</span><span class="sxs-lookup"><span data-stu-id="2aaea-261">HTTP input dataset</span></span>
<span data-ttu-id="2aaea-262">Ustawienie **zewnętrznych** za**true** informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="2aaea-262">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="2aaea-263">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2aaea-263">Azure Blob output dataset</span></span>

<span data-ttu-id="2aaea-264">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="2aaea-264">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="2aaea-265">W potoku z działanie kopiowania</span><span class="sxs-lookup"><span data-stu-id="2aaea-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="2aaea-266">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="2aaea-266">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="2aaea-267">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**HttpSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2aaea-267">In hello pipeline JSON definition, hello **source** type is set too**HttpSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="2aaea-268">Zobacz [HttpSource](#copy-activity-properties) hello listę obsługiwanych przez hello HttpSource właściwości.</span><span class="sxs-lookup"><span data-stu-id="2aaea-268">See [HttpSource](#copy-activity-properties) for hello list of properties supported by hello HttpSource.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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

> [!NOTE]
> <span data-ttu-id="2aaea-269">toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2aaea-269">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2aaea-270">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="2aaea-270">Performance and Tuning</span></span>
<span data-ttu-id="2aaea-271">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="2aaea-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
