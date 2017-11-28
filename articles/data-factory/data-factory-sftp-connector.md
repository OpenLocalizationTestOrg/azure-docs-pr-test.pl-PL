---
title: "aaaMove danych z serwera SFTP przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o danych toomove z lokalnymi lub serwer SFTP chmury przy użyciu fabryki danych Azure."
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
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="a1ca2-103">Przenoszenie danych z serwera SFTP przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="a1ca2-103">Move data from an SFTP server using Azure Data Factory</span></span>
<span data-ttu-id="a1ca2-104">W tym artykule opisano, jak toouse hello działanie kopiowania danych toomove fabryki danych Azure z tooa serwera SFTP na lokalnej/w chmurze obsługiwana ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud SFTP server tooa supported sink data store.</span></span> <span data-ttu-id="a1ca2-105">W tym artykule opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólne omówienie przepływu danych kopię działania i hello listy magazynów danych są obsługiwane jako źródła/sink.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="a1ca2-106">Fabryka danych aktualnie obsługuje tylko do przenoszenia danych z danych tooother serwera SFTP przechowuje, ale nie w przypadku przenoszenia danych z innych danych przechowują tooan SFTP serwera.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-106">Data factory currently supports only moving data from an SFTP server tooother data stores, but not for moving data from other data stores tooan SFTP server.</span></span> <span data-ttu-id="a1ca2-107">Obsługuje ona zarówno lokalnie i w chmurze. serwery SFTP.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-107">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="a1ca2-108">Aktywność kopiowania nie powoduje usunięcia pliku źródłowego hello po pomyślnie skopiowane toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-108">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="a1ca2-109">Jeśli potrzebujesz pliku źródłowego hello toodelete po pomyślnym kopiowania, Utwórz plik hello toodelete działań niestandardowych i użyj hello działania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-109">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="a1ca2-110">Obsługiwane scenariusze i typy uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="a1ca2-110">Supported scenarios and authentication types</span></span>
<span data-ttu-id="a1ca2-111">Można użyć tych danych toocopy łącznika SFTP z **zarówno w chmurze SFTP serwerów i serwerów lokalnych SFTP**.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-111">You can use this SFTP connector toocopy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="a1ca2-112">**Podstawowe** i **parametry SshPublicKey** podczas łączenia serwera SFTP toohello są obsługiwane typy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-112">**Basic** and **SshPublicKey** authentication types are supported when connecting toohello SFTP server.</span></span>

<span data-ttu-id="a1ca2-113">Podczas kopiowania danych z lokalnego serwera SFTP, należy zainstalować bramę zarządzania danymi w środowisku lokalnymi hello/Azure maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-113">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="a1ca2-114">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) szczegółowe informacje na temat hello bramy.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-114">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on hello gateway.</span></span> <span data-ttu-id="a1ca2-115">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykuł, aby uzyskać szczegółowe instrukcje dotyczące konfigurowania bramy hello i przy jego użyciu.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a1ca2-116">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="a1ca2-116">Getting started</span></span>
<span data-ttu-id="a1ca2-117">Można utworzyć potok z działania kopiowania, który przenosi dane ze źródła SFTP przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-117">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="a1ca2-118">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="a1ca2-119">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="a1ca2-120">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a1ca2-121">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="a1ca2-122">Dla formatu JSON przykłady toocopy danych z tooAzure serwera SFTP magazynu obiektów Blob, zobacz [przykład JSON: kopiowanie danych z obiektu blob tooAzure serwera SFTP](#json-example-copy-data-from-sftp-server-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-122">For JSON samples toocopy data from SFTP server tooAzure Blob Storage, see [JSON Example: Copy data from SFTP server tooAzure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a1ca2-123">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="a1ca2-123">Linked service properties</span></span>
<span data-ttu-id="a1ca2-124">Hello w poniższej tabeli przedstawiono opis usługi określonego tooFTP połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-124">hello following table provides description for JSON elements specific tooFTP linked service.</span></span>

| <span data-ttu-id="a1ca2-125">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a1ca2-125">Property</span></span> | <span data-ttu-id="a1ca2-126">Opis</span><span class="sxs-lookup"><span data-stu-id="a1ca2-126">Description</span></span> | <span data-ttu-id="a1ca2-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a1ca2-127">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a1ca2-128">type</span><span class="sxs-lookup"><span data-stu-id="a1ca2-128">type</span></span> | <span data-ttu-id="a1ca2-129">zbyt należy ustawić właściwość typu Hello`Sftp`.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-129">hello type property must be set too`Sftp`.</span></span> |<span data-ttu-id="a1ca2-130">Tak</span><span class="sxs-lookup"><span data-stu-id="a1ca2-130">Yes</span></span> |
| <span data-ttu-id="a1ca2-131">Host</span><span class="sxs-lookup"><span data-stu-id="a1ca2-131">host</span></span> | <span data-ttu-id="a1ca2-132">Nazwa lub adres IP serwera SFTP hello.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-132">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="a1ca2-133">Tak</span><span class="sxs-lookup"><span data-stu-id="a1ca2-133">Yes</span></span> |
| <span data-ttu-id="a1ca2-134">port</span><span class="sxs-lookup"><span data-stu-id="a1ca2-134">port</span></span> |<span data-ttu-id="a1ca2-135">Port, na którym hello SFTP serwer nasłuchuje.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-135">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="a1ca2-136">Witaj, wartość domyślna to: 21</span><span class="sxs-lookup"><span data-stu-id="a1ca2-136">hello default value is: 21</span></span> |<span data-ttu-id="a1ca2-137">Nie</span><span class="sxs-lookup"><span data-stu-id="a1ca2-137">No</span></span> |
| <span data-ttu-id="a1ca2-138">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="a1ca2-138">authenticationType</span></span> |<span data-ttu-id="a1ca2-139">Określ typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-139">Specify authentication type.</span></span> <span data-ttu-id="a1ca2-140">Dozwolone wartości: **podstawowe**, **parametry SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-140">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="a1ca2-141">Odwołuje się zbyt[używanie uwierzytelniania podstawowego](#using-basic-authentication) i [przy użyciu publicznego klucza uwierzytelniania SSH](#using-ssh-public-key-authentication) odpowiednio sekcje więcej właściwości i przykłady JSON.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-141">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="a1ca2-142">Tak</span><span class="sxs-lookup"><span data-stu-id="a1ca2-142">Yes</span></span> |
| <span data-ttu-id="a1ca2-143">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="a1ca2-143">skipHostKeyValidation</span></span> | <span data-ttu-id="a1ca2-144">Określ, czy tooskip hosta klucza weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-144">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="a1ca2-145">Nie.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-145">No.</span></span> <span data-ttu-id="a1ca2-146">Witaj wartość domyślna: false</span><span class="sxs-lookup"><span data-stu-id="a1ca2-146">hello default value: false</span></span> |
| <span data-ttu-id="a1ca2-147">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="a1ca2-147">hostKeyFingerprint</span></span> | <span data-ttu-id="a1ca2-148">Podaj odcisk palca hello hello klucza hosta.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-148">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="a1ca2-149">Tak, jeśli hello `skipHostKeyValidation` ustawiono toofalse.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-149">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="a1ca2-150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a1ca2-150">gatewayName</span></span> |<span data-ttu-id="a1ca2-151">Nazwa tooan tooconnect brama zarządzania danymi hello SFTP serwerem lokalnym.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-151">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="a1ca2-152">Tak, jeśli kopiowanie danych z lokalnego serwera SFTP.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-152">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="a1ca2-153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="a1ca2-153">encryptedCredential</span></span> | <span data-ttu-id="a1ca2-154">Serwer protokołu SFTP hello tooaccess zaszyfrowane poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-154">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="a1ca2-155">Wygenerowany automatycznie po określeniu opcji Uwierzytelnianie podstawowe (nazwy użytkownika i hasła) lub uwierzytelniania parametry SshPublicKey (nazwy użytkownika i ścieżki do klucza prywatnego lub zawartości) kopiowania kreatora lub hello ClickOnce podręcznego okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-155">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="a1ca2-156">Nie.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-156">No.</span></span> <span data-ttu-id="a1ca2-157">Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera SFTP.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-157">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="a1ca2-158">Przy użyciu uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="a1ca2-158">Using basic authentication</span></span>

<span data-ttu-id="a1ca2-159">Ustaw toouse uwierzytelnianie podstawowe, `authenticationType` jako `Basic`, a następnie określ następujące właściwości poza hello łącznika SFTP ogólnego z nich wprowadzone w ostatniej sekcji hello hello:</span><span class="sxs-lookup"><span data-stu-id="a1ca2-159">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="a1ca2-160">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a1ca2-160">Property</span></span> | <span data-ttu-id="a1ca2-161">Opis</span><span class="sxs-lookup"><span data-stu-id="a1ca2-161">Description</span></span> | <span data-ttu-id="a1ca2-162">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a1ca2-162">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a1ca2-163">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="a1ca2-163">username</span></span> | <span data-ttu-id="a1ca2-164">Użytkownik, który ma dostęp toohello SFTP serwera.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-164">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="a1ca2-165">Tak</span><span class="sxs-lookup"><span data-stu-id="a1ca2-165">Yes</span></span> |
| <span data-ttu-id="a1ca2-166">hasło</span><span class="sxs-lookup"><span data-stu-id="a1ca2-166">password</span></span> | <span data-ttu-id="a1ca2-167">Hasło dla użytkownika hello (nazwa_użytkownika).</span><span class="sxs-lookup"><span data-stu-id="a1ca2-167">Password for hello user (username).</span></span> | <span data-ttu-id="a1ca2-168">Tak</span><span class="sxs-lookup"><span data-stu-id="a1ca2-168">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="a1ca2-169">Przykład: Uwierzytelnianie podstawowe</span><span class="sxs-lookup"><span data-stu-id="a1ca2-169">Example: Basic authentication</span></span>
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="a1ca2-170">Przykład: Uwierzytelnianie podstawowe z zaszyfrowanych poświadczeniach</span><span class="sxs-lookup"><span data-stu-id="a1ca2-170">Example: Basic authentication with encrypted credential</span></span>

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="a1ca2-171">Przy użyciu uwierzytelniania klucza publicznego SSH</span><span class="sxs-lookup"><span data-stu-id="a1ca2-171">Using SSH public key authentication</span></span>

<span data-ttu-id="a1ca2-172">Ustaw toouse SSH uwierzytelniania klucza publicznego, `authenticationType` jako `SshPublicKey`, a następnie określ następujące właściwości poza hello łącznika SFTP ogólnego z nich wprowadzone w ostatniej sekcji hello hello:</span><span class="sxs-lookup"><span data-stu-id="a1ca2-172">toouse SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="a1ca2-173">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a1ca2-173">Property</span></span> | <span data-ttu-id="a1ca2-174">Opis</span><span class="sxs-lookup"><span data-stu-id="a1ca2-174">Description</span></span> | <span data-ttu-id="a1ca2-175">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a1ca2-175">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a1ca2-176">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="a1ca2-176">username</span></span> |<span data-ttu-id="a1ca2-177">Użytkownik, który ma dostęp toohello SFTP serwera</span><span class="sxs-lookup"><span data-stu-id="a1ca2-177">User who has access toohello SFTP server</span></span> |<span data-ttu-id="a1ca2-178">Tak</span><span class="sxs-lookup"><span data-stu-id="a1ca2-178">Yes</span></span> |
| <span data-ttu-id="a1ca2-179">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="a1ca2-179">privateKeyPath</span></span> | <span data-ttu-id="a1ca2-180">Określ ścieżkę bezwzględną toohello pliku klucza prywatnego może dostęp do tej bramy.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-180">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="a1ca2-181">Określ albo hello `privateKeyPath` lub `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-181">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="a1ca2-182">Mają zastosowanie tylko wtedy, gdy kopiowanie danych z lokalnego serwera SFTP.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-182">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="a1ca2-183">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="a1ca2-183">privateKeyContent</span></span> | <span data-ttu-id="a1ca2-184">Zserializowany ciąg hello prywatnego klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-184">A serialized string of hello private key content.</span></span> <span data-ttu-id="a1ca2-185">Witaj kreatora kopiowania może odczytywać hello pliku klucza prywatnego i Wyodrębnij zawartość klucza prywatnego hello automatycznie.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-185">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="a1ca2-186">Jeśli używane są wszystkie inne narzędzie/pakiet SDK, należy użyć właściwości privateKeyPath hello.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-186">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="a1ca2-187">Określ albo hello `privateKeyPath` lub `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-187">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="a1ca2-188">Hasło</span><span class="sxs-lookup"><span data-stu-id="a1ca2-188">passPhrase</span></span> | <span data-ttu-id="a1ca2-189">Określ hello przebiegu frazy/hasło toodecrypt hello prywatny klucz, jeśli plik klucza hello jest chroniony przez hasło.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-189">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="a1ca2-190">Tak, czy plik klucza prywatnego hello jest chroniony przez hasło.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-190">Yes if hello private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> <span data-ttu-id="a1ca2-191">Łącznik SFTP obsługują tylko klucz OpenSSH.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-191">SFTP connector only support OpenSSH key.</span></span> <span data-ttu-id="a1ca2-192">Upewnij się, że plik klucza jest w nieprawidłowym formacie hello.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-192">Make sure your key file is in hello proper format.</span></span> <span data-ttu-id="a1ca2-193">Możesz użyć narzędzia Putty tooconvert z formatu tooOpenSSH ppk.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-193">You can use Putty tool tooconvert from .ppk tooOpenSSH format.</span></span>

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="a1ca2-194">Przykład: Parametry SshPublicKey uwierzytelnianie przy użyciu filePath klucza prywatnego</span><span class="sxs-lookup"><span data-stu-id="a1ca2-194">Example: SshPublicKey authentication using private key filePath</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="a1ca2-195">Przykład: Parametry SshPublicKey uwierzytelniania za pomocą prywatnego klucza zawartości</span><span class="sxs-lookup"><span data-stu-id="a1ca2-195">Example: SshPublicKey authentication using private key content</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="a1ca2-196">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="a1ca2-196">Dataset properties</span></span>
<span data-ttu-id="a1ca2-197">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-197">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a1ca2-198">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-198">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="a1ca2-199">Witaj **typeProperties** sekcja jest różne dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-199">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="a1ca2-200">Zawiera informacje, które jest toohello określonego typu dataset.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-200">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="a1ca2-201">Hello typeProperties sekcja dla zestawu danych typu **FileShare** dataset zawiera hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="a1ca2-201">hello typeProperties section for a dataset of type **FileShare** dataset has hello following properties:</span></span>

| <span data-ttu-id="a1ca2-202">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a1ca2-202">Property</span></span> | <span data-ttu-id="a1ca2-203">Opis</span><span class="sxs-lookup"><span data-stu-id="a1ca2-203">Description</span></span> | <span data-ttu-id="a1ca2-204">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a1ca2-204">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1ca2-205">folderPath</span><span class="sxs-lookup"><span data-stu-id="a1ca2-205">folderPath</span></span> |<span data-ttu-id="a1ca2-206">Folder toohello ścieżki Sub.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-206">Sub path toohello folder.</span></span> <span data-ttu-id="a1ca2-207">Użyj znaku ucieczki "\" dla znaków specjalnych w ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-207">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="a1ca2-208">Zobacz [próbki połączone definicje usługi i zestawu danych](#sample-linked-service-and-dataset-definitions) przykłady.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-208">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="a1ca2-209">Możesz łączyć tej właściwości z **partitionBy** daty i godziny rozpoczęcia/zakończenia ścieżki folderu toohave oparte na wycinka.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-209">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="a1ca2-210">Tak</span><span class="sxs-lookup"><span data-stu-id="a1ca2-210">Yes</span></span> |
| <span data-ttu-id="a1ca2-211">fileName</span><span class="sxs-lookup"><span data-stu-id="a1ca2-211">fileName</span></span> |<span data-ttu-id="a1ca2-212">Określ nazwę hello pliku hello w hello **folderPath** Jeśli chcesz hello tabeli toorefer tooa określonego pliku w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-212">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="a1ca2-213">Jeśli nie określono żadnej wartości dla tej właściwości, tabeli hello punktów tooall pliki w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-213">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="a1ca2-214">Jeśli nie określono nazwy pliku dla wyjściowego zestawu danych, nazwą hello hello wygenerowany plik będzie w powitania po tego formatu:</span><span class="sxs-lookup"><span data-stu-id="a1ca2-214">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="a1ca2-215">Dane. <Guid>.txt (przykład: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="a1ca2-215">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="a1ca2-216">Nie</span><span class="sxs-lookup"><span data-stu-id="a1ca2-216">No</span></span> |
| <span data-ttu-id="a1ca2-217">obiektu fileFilter</span><span class="sxs-lookup"><span data-stu-id="a1ca2-217">fileFilter</span></span> |<span data-ttu-id="a1ca2-218">Określ toobe filtru używane tooselect podzbiór plików w hello folderPath, a nie wszystkich plików.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-218">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="a1ca2-219">Dozwolone wartości to: `*` (wielu znaków) i `?` (pojedynczy znak).</span><span class="sxs-lookup"><span data-stu-id="a1ca2-219">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="a1ca2-220">Przykład 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="a1ca2-220">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="a1ca2-221">Przykład 2:`"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="a1ca2-221">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="a1ca2-222">obiektu fileFilter jest odpowiednie dla wejściowego zestawu danych z udziału plików.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-222">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="a1ca2-223">Ta właściwość nie jest obsługiwana z systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-223">This property is not supported with HDFS.</span></span> |<span data-ttu-id="a1ca2-224">Nie</span><span class="sxs-lookup"><span data-stu-id="a1ca2-224">No</span></span> |
| <span data-ttu-id="a1ca2-225">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="a1ca2-225">partitionedBy</span></span> |<span data-ttu-id="a1ca2-226">partitionedBy mogą być używane toospecify folderPath dynamicznych, nazwę pliku dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-226">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="a1ca2-227">Na przykład folderPath sparametryzowana dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-227">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="a1ca2-228">Nie</span><span class="sxs-lookup"><span data-stu-id="a1ca2-228">No</span></span> |
| <span data-ttu-id="a1ca2-229">Format</span><span class="sxs-lookup"><span data-stu-id="a1ca2-229">format</span></span> | <span data-ttu-id="a1ca2-230">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-230">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="a1ca2-231">Zestaw hello **typu** właściwości w formacie tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-231">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="a1ca2-232">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="a1ca2-233">Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-233">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="a1ca2-234">Nie</span><span class="sxs-lookup"><span data-stu-id="a1ca2-234">No</span></span> |
| <span data-ttu-id="a1ca2-235">Kompresja</span><span class="sxs-lookup"><span data-stu-id="a1ca2-235">compression</span></span> | <span data-ttu-id="a1ca2-236">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-236">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="a1ca2-237">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="a1ca2-238">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="a1ca2-239">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="a1ca2-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="a1ca2-240">Nie</span><span class="sxs-lookup"><span data-stu-id="a1ca2-240">No</span></span> |
| <span data-ttu-id="a1ca2-241">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="a1ca2-241">useBinaryTransfer</span></span> |<span data-ttu-id="a1ca2-242">Określ, czy używany tryb transferu binarnego.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-242">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="a1ca2-243">Wartość true dla trybie binarnym i wartość false ASCII.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-243">True for binary mode and false ASCII.</span></span> <span data-ttu-id="a1ca2-244">Wartość domyślna: wartość True.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-244">Default value: True.</span></span> <span data-ttu-id="a1ca2-245">Ta właściwość jest używana tylko w przypadku typu skojarzonej połączonej usługi typu: SerwerFTP.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-245">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="a1ca2-246">Nie</span><span class="sxs-lookup"><span data-stu-id="a1ca2-246">No</span></span> |

> [!NOTE]
> <span data-ttu-id="a1ca2-247">Nie można jednocześnie używać nazwy pliku i obiektu fileFilter.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-247">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="a1ca2-248">Za pomocą właściwości partionedBy</span><span class="sxs-lookup"><span data-stu-id="a1ca2-248">Using partionedBy property</span></span>
<span data-ttu-id="a1ca2-249">Jak wspomniano w poprzedniej sekcji hello, można określić dynamiczne folderPath, nazwę pliku dla danych szeregów czasowych ze partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-249">As mentioned in hello previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="a1ca2-250">Możesz to zrobić z hello makra fabryki danych i zmiennej systemowej hello SliceStart, SliceEnd sygnalizujące hello logicznej okresu wycinek podanych danych.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-250">You can do so with hello Data Factory macros and hello system variable SliceStart, SliceEnd that indicate hello logical time period for a given data slice.</span></span>

<span data-ttu-id="a1ca2-251">toolearn dotyczące zestawów danych serii czasu, planowania i wycinków, zobacz [tworzenie zestawów danych](data-factory-create-datasets.md), [planowanie i wykonanie](data-factory-scheduling-and-execution.md), i [tworzenie potoków](data-factory-create-pipelines.md) artykułów.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-251">toolearn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="a1ca2-252">Przykład 1:</span><span class="sxs-lookup"><span data-stu-id="a1ca2-252">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="a1ca2-253">W tym przykładzie {wycinka} zostanie zastąpiony hello wartość zmiennej fabryki danych systemu SliceStart w formacie hello (YYYYMMDDHH) określona.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-253">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="a1ca2-254">Witaj SliceStart odwołuje się czas toostart hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-254">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="a1ca2-255">Witaj folderPath jest różne dla każdego wycinka.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-255">hello folderPath is different for each slice.</span></span> <span data-ttu-id="a1ca2-256">Przykład: wikidatagateway/wikisampledataout/2014100103 lub wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-256">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="a1ca2-257">Przykład 2:</span><span class="sxs-lookup"><span data-stu-id="a1ca2-257">Sample 2:</span></span>

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
<span data-ttu-id="a1ca2-258">W tym przykładzie rok, miesiąc, dzień i czas SliceStart są wyodrębniane do oddzielnych zmiennych, które są używane przez właściwości folderPath i nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-258">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="a1ca2-259">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="a1ca2-259">Copy activity properties</span></span>
<span data-ttu-id="a1ca2-260">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-260">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a1ca2-261">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-261">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="a1ca2-262">Właściwości hello dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-262">Whereas, hello properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="a1ca2-263">Dla działania kopiowania właściwości typu hello zależy od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-263">For Copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="a1ca2-264">Obsługiwane formaty plików i kompresji</span><span class="sxs-lookup"><span data-stu-id="a1ca2-264">Supported file and compression formats</span></span>
<span data-ttu-id="a1ca2-265">Zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md) artykuł na temat szczegółów.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-265">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a><span data-ttu-id="a1ca2-266">Przykład JSON: Kopiowanie danych z obiektu blob tooAzure serwera SFTP</span><span class="sxs-lookup"><span data-stu-id="a1ca2-266">JSON Example: Copy data from SFTP server tooAzure blob</span></span>
<span data-ttu-id="a1ca2-267">Witaj poniższym przykładzie przedstawiono przykładowe definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a1ca2-267">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a1ca2-268">Przedstawiają sposób toocopy danych z użyciem protokołu SFTP źródła tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-268">They show how toocopy data from SFTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="a1ca2-269">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła tooany z wychwytywanie hello wyrażony w [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-269">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1ca2-270">W tym przykładzie przedstawiono fragmenty kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-270">This sample provides JSON snippets.</span></span> <span data-ttu-id="a1ca2-271">Zawiera instrukcje krok po kroku dotyczące tworzenia hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-271">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="a1ca2-272">Zobacz [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-272">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="a1ca2-273">przykład Witaj ma hello następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="a1ca2-273">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="a1ca2-274">Połączonej usługi typu [sftp](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a1ca2-274">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="a1ca2-275">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a1ca2-275">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="a1ca2-276">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a1ca2-276">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="a1ca2-277">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a1ca2-277">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="a1ca2-278">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [FileSystemSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a1ca2-278">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a1ca2-279">przykład Witaj kopiuje dane z tooan serwera SFTP obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-279">hello sample copies data from an SFTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="a1ca2-280">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-280">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="a1ca2-281">**Usługa SFTP połączone**</span><span class="sxs-lookup"><span data-stu-id="a1ca2-281">**SFTP linked service**</span></span>

<span data-ttu-id="a1ca2-282">W tym przykładzie używane uwierzytelnianie podstawowe hello z nazwy użytkownika i hasła w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-282">This example uses hello basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="a1ca2-283">Można także użyć jednej z hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="a1ca2-283">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="a1ca2-284">Uwierzytelnianie podstawowe z zaszyfrowane poświadczenia</span><span class="sxs-lookup"><span data-stu-id="a1ca2-284">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="a1ca2-285">Uwierzytelnianie klucza publicznego SSH</span><span class="sxs-lookup"><span data-stu-id="a1ca2-285">SSH public key authentication</span></span>

<span data-ttu-id="a1ca2-286">Zobacz [FTP połączona usługa](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-286">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
<span data-ttu-id="a1ca2-287">**Połączona usługa Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="a1ca2-287">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="a1ca2-288">**Zestaw danych wejściowych SFTP**</span><span class="sxs-lookup"><span data-stu-id="a1ca2-288">**SFTP input dataset**</span></span>

<span data-ttu-id="a1ca2-289">Ten zestaw danych odwołuje się toohello SFTP folder `mysharedfolder` i plik `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-289">This dataset refers toohello SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="a1ca2-290">Witaj potoku kopie hello toohello docelowej lokalizacji plików.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-290">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="a1ca2-291">Ustawienie "external": "prawda" informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-291">Setting "external": "true" informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="a1ca2-292">**Azure Blob wyjściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="a1ca2-292">**Azure Blob output dataset**</span></span>

<span data-ttu-id="a1ca2-293">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="a1ca2-293">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a1ca2-294">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-294">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="a1ca2-295">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-295">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="a1ca2-296">**W potoku z działanie kopiowania**</span><span class="sxs-lookup"><span data-stu-id="a1ca2-296">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="a1ca2-297">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-297">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="a1ca2-298">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**FileSystemSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-298">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a><span data-ttu-id="a1ca2-299">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="a1ca2-299">Performance and Tuning</span></span>
<span data-ttu-id="a1ca2-300">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-300">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1ca2-301">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a1ca2-301">Next Steps</span></span>
<span data-ttu-id="a1ca2-302">Zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="a1ca2-302">See hello following articles:</span></span>

* <span data-ttu-id="a1ca2-303">[Samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku do tworzenia potoku z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="a1ca2-303">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
