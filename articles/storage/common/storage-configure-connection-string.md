---
title: "aaaConfigure ciąg połączenia dla usługi Azure Storage | Dokumentacja firmy Microsoft"
description: "Skonfiguruj parametry połączenia dla konta magazynu platformy Azure. Parametry połączenia zawierają informacje hello wymagany tooauthenticate dostępu konta magazynu tooa z aplikacji w czasie wykonywania."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: ac1d7d9bf11fa6f44243cda0c40d8faee12e513b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="3e159-104">Konfiguracja parametrów połączenia usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3e159-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="3e159-105">Ciąg połączenia zawiera informacje dotyczące uwierzytelniania hello wymagane dla danych aplikacji tooaccess na koncie magazynu Azure w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="3e159-105">A connection string includes hello authentication information required for your application tooaccess data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="3e159-106">Można skonfigurować parametry połączenia do:</span><span class="sxs-lookup"><span data-stu-id="3e159-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="3e159-107">Połącz toohello emulatora magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="3e159-107">Connect toohello Azure storage emulator.</span></span>
* <span data-ttu-id="3e159-108">Dostęp do konta magazynu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3e159-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="3e159-109">Dostęp do określonych zasobów na platformie Azure za pomocą sygnatury dostępu współdzielonego (SAS).</span><span class="sxs-lookup"><span data-stu-id="3e159-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="3e159-110">Przechowywanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="3e159-110">Storing your connection string</span></span>
<span data-ttu-id="3e159-111">Aplikacja wymaga parametrów połączenia hello tooaccess w tooAzure żądań tooauthenticate środowiska uruchomieniowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="3e159-111">Your application needs tooaccess hello connection string at runtime tooauthenticate requests made tooAzure Storage.</span></span> <span data-ttu-id="3e159-112">Istnieje kilka opcji do przechowywania parametrów połączenia:</span><span class="sxs-lookup"><span data-stu-id="3e159-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="3e159-113">Uruchomiona aplikacja hello pulpitu lub na urządzeniu mogą być przechowywane w ciągu połączenia hello **app.config** lub **web.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="3e159-113">An application running on hello desktop or on a device can store hello connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="3e159-114">Dodaj toohello ciąg połączenia hello **AppSettings** sekcji w tych plikach.</span><span class="sxs-lookup"><span data-stu-id="3e159-114">Add hello connection string toohello **AppSettings** section in these files.</span></span>
* <span data-ttu-id="3e159-115">Aplikacji uruchomionej w usłudze w chmurze platformy Azure można przechowywać parametry połączenia hello w hello [plik schematu (cscfg) konfiguracji usługi Azure](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e159-115">An application running in an Azure cloud service can store hello connection string in hello [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="3e159-116">Dodaj toohello ciąg połączenia hello **appSettings** sekcji pliku konfiguracji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="3e159-116">Add hello connection string toohello **ConfigurationSettings** section of hello service configuration file.</span></span>
* <span data-ttu-id="3e159-117">Parametry połączenia można użyć bezpośrednio w kodzie.</span><span class="sxs-lookup"><span data-stu-id="3e159-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="3e159-118">Firma Microsoft zaleca jednak przechowywanie parametrów połączenia w pliku konfiguracji, w większości przypadków.</span><span class="sxs-lookup"><span data-stu-id="3e159-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="3e159-119">Przechowywanie parametrów połączenia w pliku konfiguracji umożliwia łatwe tooupdate hello połączenia ciąg tooswitch między hello emulatora magazynu i konto magazynu platformy Azure w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="3e159-119">Storing your connection string in a configuration file makes it easy tooupdate hello connection string tooswitch between hello storage emulator and an Azure storage account in hello cloud.</span></span> <span data-ttu-id="3e159-120">Wystarczy tylko środowiska docelowego tooyour toopoint ciąg tooedit hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="3e159-120">You only need tooedit hello connection string toopoint tooyour target environment.</span></span>

<span data-ttu-id="3e159-121">Można użyć hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess ciągu połączenia w czasie wykonywania, niezależnie od tego, w którym aplikacja jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="3e159-121">You can use hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-hello-storage-emulator"></a><span data-ttu-id="3e159-122">Utworzyć parametry połączenia dla emulatora magazynu hello</span><span class="sxs-lookup"><span data-stu-id="3e159-122">Create a connection string for hello storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="3e159-123">Aby uzyskać więcej informacji na temat hello emulatora magazynu, zobacz [użyć emulatora magazynu Azure hello do projektowania i testowania](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="3e159-123">For more information about hello storage emulator, see [Use hello Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="3e159-124">Utworzyć parametry połączenia dla konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3e159-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="3e159-125">toocreate ciąg połączenia dla konta magazynu Azure, użyj następującego hello formatu.</span><span class="sxs-lookup"><span data-stu-id="3e159-125">toocreate a connection string for your Azure storage account, use hello following format.</span></span> <span data-ttu-id="3e159-126">Wskazuje, czy konto magazynu toohello tooconnect za pośrednictwem protokołu HTTPS (zalecane), czy HTTP, Zastąp `myAccountName` o nazwie hello swojego konta magazynu i Zastąp `myAccountKey` kluczem dostępu do konta:</span><span class="sxs-lookup"><span data-stu-id="3e159-126">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="3e159-127">Na przykład parametry połączenia mogą wyglądać podobnie do:</span><span class="sxs-lookup"><span data-stu-id="3e159-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="3e159-128">Mimo że usługa Azure Storage obsługuje protokołów HTTP i HTTPS w parametrach połączenia, *HTTPS jest zdecydowanie zalecane*.</span><span class="sxs-lookup"><span data-stu-id="3e159-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="3e159-129">Parametry połączenia konta magazynu można znaleźć w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3e159-129">You can find your storage account's connection strings in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3e159-130">Przejdź za**ustawienia** > **klucze dostępu** w parametry połączenia toosee bloku menu konta magazynu dla obu kluczy dostępu do podstawowego i pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="3e159-130">Navigate too**SETTINGS** > **Access keys** in your storage account's menu blade toosee connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="3e159-131">Utworzyć parametry połączenia przy użyciu sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="3e159-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="3e159-132">Utworzyć parametry połączenia dla punktu końcowego magazynu jawne</span><span class="sxs-lookup"><span data-stu-id="3e159-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="3e159-133">Punkty końcowe usługi jawne można określić w ciągu połączenia zamiast hello domyślne punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="3e159-133">You can specify explicit service endpoints in your connection string instead of using hello default endpoints.</span></span> <span data-ttu-id="3e159-134">toocreate ciąg połączenia, który określa jawne punktu końcowego, określić dla każdej usługi, w tym hello Specyfikacja protokołu (HTTPS (zalecane) lub HTTP), punkt końcowy usługi pełną hello hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="3e159-134">toocreate a connection string that specifies an explicit endpoint, specify hello complete service endpoint for each service, including hello protocol specification (HTTPS (recommended) or HTTP), in hello following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="3e159-135">Jest jeden scenariusz, który może mają toospecify jawne punktu końcowego, gdy Twoje tooa punktu końcowego magazynu obiektów Blob jest zamapowany [domeny niestandardowej](../blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="3e159-135">One scenario where you might wish toospecify an explicit endpoint is when you've mapped your Blob storage endpoint tooa [custom domain](../blobs/storage-custom-domain-name.md).</span></span> <span data-ttu-id="3e159-136">W takim przypadku można określić niestandardowe punktu końcowego magazynu obiektów Blob w ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="3e159-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="3e159-137">Opcjonalnie można określić hello domyślnymi punktami końcowymi hello innych usług, jeśli aplikacja korzysta z nich.</span><span class="sxs-lookup"><span data-stu-id="3e159-137">You can optionally specify hello default endpoints for hello other services if your application uses them.</span></span>

<span data-ttu-id="3e159-138">Oto przykład parametrów połączenia, które określa jawne punktu końcowego w celu hello usługa Blob:</span><span class="sxs-lookup"><span data-stu-id="3e159-138">Here is an example of a connection string that specifies an explicit endpoint for hello Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="3e159-139">W tym przykładzie określa jawne punkty końcowe dla wszystkich usług, w tym niestandardową domenę na potrzeby hello usługa Blob:</span><span class="sxs-lookup"><span data-stu-id="3e159-139">This example specifies explicit endpoints for all services, including a custom domain for hello Blob service:</span></span>

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="3e159-140">wartości punktu końcowego Hello w parametrach połączenia są używane tooconstruct hello żądania usług magazynu toohello identyfikatory URI, a hello formę wszystkie identyfikatory URI, które są zwracane tooyour kodu jest wymagane przez.</span><span class="sxs-lookup"><span data-stu-id="3e159-140">hello endpoint values in a connection string are used tooconstruct hello request URIs toohello storage services, and dictate hello form of any URIs that are returned tooyour code.</span></span>

<span data-ttu-id="3e159-141">Jeśli zamapowany magazynu domeny niestandardowej tooa punktu końcowego i pominąć ten punkt końcowy z parametrów połączenia, nie będzie możliwe toouse tego połączenia ciągu tooaccess danych w tej usłudze w kodzie.</span><span class="sxs-lookup"><span data-stu-id="3e159-141">If you've mapped a storage endpoint tooa custom domain and omit that endpoint from a connection string, then you will not be able toouse that connection string tooaccess data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e159-142">Wartości punktu końcowego usługi w parametry połączenia muszą być poprawnie sformułowanym identyfikatory URI, w tym `https://` (zalecane) lub `http://`.</span><span class="sxs-lookup"><span data-stu-id="3e159-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="3e159-143">Ponieważ Magazyn Azure nie obsługuje jeszcze HTTPS dla domen niestandardowych można *musi* określ `http://` dla dowolnego punktu końcowego identyfikator URI, który wskazuje tooa domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="3e159-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points tooa custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="3e159-144">Utworzyć parametry połączenia z sufiksem punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="3e159-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="3e159-145">toocreate parametrów połączenia dla usługi magazynu w regionach lub wystąpień z innym punktem końcowym sufiksów, takich jak dla Chińskiej wersji platformy Azure lub Azure dla instytucji rządowych, hello Użyj następującego formatu ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="3e159-145">toocreate a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use hello following connection string format.</span></span> <span data-ttu-id="3e159-146">Wskazuje, czy konto magazynu toohello tooconnect za pośrednictwem protokołu HTTPS (zalecane), czy HTTP, Zastąp `myAccountName` o nazwie hello konta magazynu, należy zastąpić `myAccountKey` z klucz dostępu do konta i Zastąp `mySuffix` z hello identyfikatora URI sufiks:</span><span class="sxs-lookup"><span data-stu-id="3e159-146">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with hello URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="3e159-147">Oto przykład parametry połączenia dla usług magazynu w chińskiej wersji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="3e159-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="3e159-148">Podczas analizowania parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="3e159-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="3e159-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3e159-149">Next steps</span></span>
* [<span data-ttu-id="3e159-150">Użyj hello emulatora magazynu Azure do programowania i testowania</span><span class="sxs-lookup"><span data-stu-id="3e159-150">Use hello Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="3e159-151">Eksploratory usługi Storage platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3e159-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="3e159-152">Przy użyciu sygnatury dostępu współdzielonego (SAS)</span><span class="sxs-lookup"><span data-stu-id="3e159-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

