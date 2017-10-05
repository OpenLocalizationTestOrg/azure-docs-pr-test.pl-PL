---
title: "Konfigurowanie parametrów połączenia dla usługi Azure Storage | Dokumentacja firmy Microsoft"
description: "Skonfiguruj parametry połączenia dla konta magazynu platformy Azure. Parametry połączenia zawierają informacje wymagane do uwierzytelniania dostępu do konta magazynu z poziomu aplikacji w czasie wykonywania."
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
ms.openlocfilehash: 01aa506e2b47fc29a70592e670a206a2b74248a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="1dc89-104">Konfiguracja parametrów połączenia usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1dc89-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="1dc89-105">Parametry połączenia zawiera informacje dotyczące uwierzytelniania wymagane dla aplikacji dostęp do danych na koncie magazynu Azure w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="1dc89-105">A connection string includes the authentication information required for your application to access data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="1dc89-106">Można skonfigurować parametry połączenia do:</span><span class="sxs-lookup"><span data-stu-id="1dc89-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="1dc89-107">Podłącz do emulatora magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="1dc89-107">Connect to the Azure storage emulator.</span></span>
* <span data-ttu-id="1dc89-108">Dostęp do konta magazynu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1dc89-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="1dc89-109">Dostęp do określonych zasobów na platformie Azure za pomocą sygnatury dostępu współdzielonego (SAS).</span><span class="sxs-lookup"><span data-stu-id="1dc89-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="1dc89-110">Przechowywanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="1dc89-110">Storing your connection string</span></span>
<span data-ttu-id="1dc89-111">Aplikacja musi uzyskać dostępu do parametrów połączenia w czasie wykonywania do uwierzytelniania żądań wysyłanych do usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1dc89-111">Your application needs to access the connection string at runtime to authenticate requests made to Azure Storage.</span></span> <span data-ttu-id="1dc89-112">Istnieje kilka opcji do przechowywania parametrów połączenia:</span><span class="sxs-lookup"><span data-stu-id="1dc89-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="1dc89-113">Uruchamianie aplikacji na pulpicie lub na urządzeniu mogą być przechowywane w ciągu połączenia **app.config** lub **web.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="1dc89-113">An application running on the desktop or on a device can store the connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="1dc89-114">Dodaj parametry połączenia do **AppSettings** sekcji w tych plikach.</span><span class="sxs-lookup"><span data-stu-id="1dc89-114">Add the connection string to the **AppSettings** section in these files.</span></span>
* <span data-ttu-id="1dc89-115">Aplikacja działająca w usługi w chmurze platformy Azure można przechowywać w ciągu połączenia [plik schematu (cscfg) konfiguracji usługi Azure](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="1dc89-115">An application running in an Azure cloud service can store the connection string in the [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="1dc89-116">Dodaj parametry połączenia do **appSettings** sekcji pliku konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="1dc89-116">Add the connection string to the **ConfigurationSettings** section of the service configuration file.</span></span>
* <span data-ttu-id="1dc89-117">Parametry połączenia można użyć bezpośrednio w kodzie.</span><span class="sxs-lookup"><span data-stu-id="1dc89-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="1dc89-118">Firma Microsoft zaleca jednak przechowywanie parametrów połączenia w pliku konfiguracji, w większości przypadków.</span><span class="sxs-lookup"><span data-stu-id="1dc89-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="1dc89-119">Przechowywanie parametrów połączenia w pliku konfiguracji ułatwia zaktualizować parametry połączenia w celu przełączania się między emulator magazynu i konto usługi Azure storage w chmurze.</span><span class="sxs-lookup"><span data-stu-id="1dc89-119">Storing your connection string in a configuration file makes it easy to update the connection string to switch between the storage emulator and an Azure storage account in the cloud.</span></span> <span data-ttu-id="1dc89-120">Należy zmodyfikować parametry połączenia, aby wskazywał środowiska docelowego.</span><span class="sxs-lookup"><span data-stu-id="1dc89-120">You only need to edit the connection string to point to your target environment.</span></span>

<span data-ttu-id="1dc89-121">Można użyć [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) do parametrów połączenia w czasie wykonywania, niezależnie od tego, w którym aplikacja jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="1dc89-121">You can use the [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) to access your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-the-storage-emulator"></a><span data-ttu-id="1dc89-122">Utworzyć parametry połączenia dla emulatora magazynu</span><span class="sxs-lookup"><span data-stu-id="1dc89-122">Create a connection string for the storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="1dc89-123">Aby uzyskać więcej informacji na temat emulator magazynu, zobacz [użyć emulatora magazynu Azure do programowania i testowania](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="1dc89-123">For more information about the storage emulator, see [Use the Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="1dc89-124">Utworzyć parametry połączenia dla konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1dc89-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="1dc89-125">Aby utworzyć parametry połączenia dla konta magazynu Azure, użyj następującego formatu.</span><span class="sxs-lookup"><span data-stu-id="1dc89-125">To create a connection string for your Azure storage account, use the following format.</span></span> <span data-ttu-id="1dc89-126">Wskazuje, czy chcesz się połączyć z kontem magazynu za pośrednictwem protokołu HTTPS (zalecane) lub protokołu HTTP, Zastąp `myAccountName` z nazwą konta magazynu i Zastąp `myAccountKey` kluczem dostępu do konta:</span><span class="sxs-lookup"><span data-stu-id="1dc89-126">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="1dc89-127">Na przykład parametry połączenia mogą wyglądać podobnie do:</span><span class="sxs-lookup"><span data-stu-id="1dc89-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="1dc89-128">Mimo że usługa Azure Storage obsługuje protokołów HTTP i HTTPS w parametrach połączenia, *HTTPS jest zdecydowanie zalecane*.</span><span class="sxs-lookup"><span data-stu-id="1dc89-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="1dc89-129">Można znaleźć parametrów połączenia konta magazynu w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1dc89-129">You can find your storage account's connection strings in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1dc89-130">Przejdź do **ustawienia** > **klucze dostępu** w bloku menu konta magazynu, aby wyświetlić parametry połączenia dla obu kluczy dostępu do podstawowego i pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="1dc89-130">Navigate to **SETTINGS** > **Access keys** in your storage account's menu blade to see connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="1dc89-131">Utworzyć parametry połączenia przy użyciu sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="1dc89-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="1dc89-132">Utworzyć parametry połączenia dla punktu końcowego magazynu jawne</span><span class="sxs-lookup"><span data-stu-id="1dc89-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="1dc89-133">Punkty końcowe usługi jawne można określić w ciągu połączenia zamiast domyślnych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="1dc89-133">You can specify explicit service endpoints in your connection string instead of using the default endpoints.</span></span> <span data-ttu-id="1dc89-134">Aby utworzyć parametry połączenia, które określa jawne punktu końcowego, należy określić punkt końcowy usługi ukończenia dla każdej usługi, w tym specyfikacji protokołu (HTTP lub HTTPS (zalecane)), w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="1dc89-134">To create a connection string that specifies an explicit endpoint, specify the complete service endpoint for each service, including the protocol specification (HTTPS (recommended) or HTTP), in the following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="1dc89-135">Jest jeden scenariusz, w którym może chcesz określić jawne punktu końcowego, gdy został zamapowany punktu końcowego magazynu obiektów Blob do [domeny niestandardowej](storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="1dc89-135">One scenario where you might wish to specify an explicit endpoint is when you've mapped your Blob storage endpoint to a [custom domain](storage-custom-domain-name.md).</span></span> <span data-ttu-id="1dc89-136">W takim przypadku można określić niestandardowe punktu końcowego magazynu obiektów Blob w ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="1dc89-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="1dc89-137">Opcjonalnie można określić domyślne punkty końcowe dla innych usług, jeśli aplikacja korzysta z nich.</span><span class="sxs-lookup"><span data-stu-id="1dc89-137">You can optionally specify the default endpoints for the other services if your application uses them.</span></span>

<span data-ttu-id="1dc89-138">Oto przykład parametrów połączenia, które określa jawne punktu końcowego usługi Blob:</span><span class="sxs-lookup"><span data-stu-id="1dc89-138">Here is an example of a connection string that specifies an explicit endpoint for the Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="1dc89-139">W tym przykładzie określa jawne punkty końcowe dla wszystkich usług, w tym domeny niestandardowej dla usługi Blob:</span><span class="sxs-lookup"><span data-stu-id="1dc89-139">This example specifies explicit endpoints for all services, including a custom domain for the Blob service:</span></span>

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

<span data-ttu-id="1dc89-140">Wartości punktu końcowego w parametrach połączenia są używane do konstruowania żądania identyfikatory URI usługi magazynu i dyktowania formę wszystkie identyfikatory URI, które są zwracane do kodu.</span><span class="sxs-lookup"><span data-stu-id="1dc89-140">The endpoint values in a connection string are used to construct the request URIs to the storage services, and dictate the form of any URIs that are returned to your code.</span></span>

<span data-ttu-id="1dc89-141">Jeśli zamapowany na domenę niestandardową punktu końcowego magazynu i pominąć ten punkt końcowy z parametrów połączenia, następnie nie będzie mogła użyć tego ciągu połączenia w celu dostępu do danych w tej usłudze w kodzie.</span><span class="sxs-lookup"><span data-stu-id="1dc89-141">If you've mapped a storage endpoint to a custom domain and omit that endpoint from a connection string, then you will not be able to use that connection string to access data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1dc89-142">Wartości punktu końcowego usługi w parametry połączenia muszą być poprawnie sformułowanym identyfikatory URI, w tym `https://` (zalecane) lub `http://`.</span><span class="sxs-lookup"><span data-stu-id="1dc89-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="1dc89-143">Ponieważ Magazyn Azure nie obsługuje jeszcze HTTPS dla domen niestandardowych można *musi* określ `http://` dla dowolnego punktu końcowego identyfikator URI, który wskazuje na domenę niestandardową.</span><span class="sxs-lookup"><span data-stu-id="1dc89-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points to a custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="1dc89-144">Utworzyć parametry połączenia z sufiksem punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="1dc89-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="1dc89-145">Aby utworzyć parametry połączenia dla usługi magazynu w regionach lub wystąpień z innym punktem końcowym sufiksów, takich jak dla Chińskiej wersji platformy Azure lub Azure dla instytucji rządowych, użyj następującego formatu ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="1dc89-145">To create a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use the following connection string format.</span></span> <span data-ttu-id="1dc89-146">Wskazuje, czy chcesz się połączyć z kontem magazynu za pośrednictwem protokołu HTTPS (zalecane) lub protokołu HTTP, Zastąp `myAccountName` z nazwą konta magazynu, należy zastąpić `myAccountKey` z klucz dostępu do konta i Zastąp `mySuffix` wraz z sufiksem identyfikatora URI:</span><span class="sxs-lookup"><span data-stu-id="1dc89-146">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with the URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="1dc89-147">Oto przykład parametry połączenia dla usług magazynu w chińskiej wersji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="1dc89-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="1dc89-148">Podczas analizowania parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="1dc89-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="1dc89-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1dc89-149">Next steps</span></span>
* [<span data-ttu-id="1dc89-150">Użyć emulatora magazynu Azure do programowania i testowania</span><span class="sxs-lookup"><span data-stu-id="1dc89-150">Use the Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="1dc89-151">Eksploratory usługi Storage platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1dc89-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="1dc89-152">Przy użyciu sygnatury dostępu współdzielonego (SAS)</span><span class="sxs-lookup"><span data-stu-id="1dc89-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

