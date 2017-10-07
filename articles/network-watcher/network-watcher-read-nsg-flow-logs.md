---
title: "aaaRead NSG przepływu dzienniki | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób rejestrowania tooparse NSG przepływu"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: gwallace
ms.openlocfilehash: b4f0f64639c7b2a6b4db50e54d15056bfd809e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="read-nsg-flow-logs"></a><span data-ttu-id="502a1-103">Dzienniki przepływu odczytu NSG</span><span class="sxs-lookup"><span data-stu-id="502a1-103">Read NSG flow logs</span></span>

<span data-ttu-id="502a1-104">Dowiedz się, jak przepływu NSG tooread dzienniki wpisy przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="502a1-104">Learn how tooread NSG flow logs entries with PowerShell.</span></span>

<span data-ttu-id="502a1-105">Grupa NSG przepływu dzienniki są przechowywane na koncie magazynu w [blokowe obiekty BLOB](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span><span class="sxs-lookup"><span data-stu-id="502a1-105">NSG flow logs are stored in a storage account in [block blobs](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span></span> <span data-ttu-id="502a1-106">Blokowe obiekty BLOB składają się z mniejszych bloków.</span><span class="sxs-lookup"><span data-stu-id="502a1-106">Block blobs are made up of smaller blocks.</span></span> <span data-ttu-id="502a1-107">Każdy dziennik jest oddzielne blokowych obiektów blob, który jest generowany co godzinę.</span><span class="sxs-lookup"><span data-stu-id="502a1-107">Each log is a separate block blob that is generated every hour.</span></span> <span data-ttu-id="502a1-108">Nowe dzienniki są generowane co godzinę, dzienniki hello są aktualizowane przy użyciu nowych wpisów co kilka minut z hello najnowsze dane.</span><span class="sxs-lookup"><span data-stu-id="502a1-108">New logs are generated every hour, hello logs are updated with new entries every few minutes with hello latest data.</span></span> <span data-ttu-id="502a1-109">W tym artykule dowiesz się, jak tooread części hello przepływu dzienników.</span><span class="sxs-lookup"><span data-stu-id="502a1-109">In this article you learn how tooread portions of hello flow logs.</span></span>

## <a name="scenario"></a><span data-ttu-id="502a1-110">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="502a1-110">Scenario</span></span>

<span data-ttu-id="502a1-111">W powitania od scenariusza znajduje się przykład dziennika przepływu, który znajduje się na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="502a1-111">In hello following scenario, you have an example flow log that is stored in a storage account.</span></span> <span data-ttu-id="502a1-112">Możemy wykonywać krokowo jak selektywnie odczytu hello najnowsze zdarzeń w dziennikach przepływu NSG.</span><span class="sxs-lookup"><span data-stu-id="502a1-112">we step through how you can selectively read hello latest events in NSG flow logs.</span></span> <span data-ttu-id="502a1-113">W tym artykule używamy środowiska PowerShell, jednak hello omówione w artykule hello nie są ograniczone toohello język programowania i tooall stosowanych językach obsługiwanych przez hello interfejsy API usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="502a1-113">In this article we will use PowerShell, however, hello concepts discussed in hello article are not limited toohello programming language and are applicable tooall languages supported by hello Azure Storage APIs</span></span>

## <a name="setup"></a><span data-ttu-id="502a1-114">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="502a1-114">Setup</span></span>

<span data-ttu-id="502a1-115">Przed rozpoczęciem, musi mieć sieci grupy przepływu rejestrowanie zabezpieczeń włączone w jednej lub wielu grup zabezpieczeń sieci na Twoim koncie.</span><span class="sxs-lookup"><span data-stu-id="502a1-115">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="502a1-116">Instrukcje dotyczące włączania zabezpieczenia sieci przepływu dzienniki, można znaleźć toohello poniższego artykułu: [wprowadzenie tooflow rejestrowania dla grup zabezpieczeń sieci](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="502a1-116">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="retrieve-hello-block-list"></a><span data-ttu-id="502a1-117">Pobieranie listy zablokowanych hello</span><span class="sxs-lookup"><span data-stu-id="502a1-117">Retrieve hello block list</span></span>

<span data-ttu-id="502a1-118">Witaj, następujące zestawy środowiska PowerShell zmiennych hello potrzebne hello tooquery NSG przepływu logowania obiektów blob i listy bloków hello hello [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="502a1-118">hello following PowerShell sets up hello variables needed tooquery hello NSG flow log blob and list hello blocks within hello [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) block blob.</span></span> <span data-ttu-id="502a1-119">Zaktualizuj hello skryptu toocontain prawidłowe wartości dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="502a1-119">Update hello script toocontain valid values for your environment.</span></span>

```powershell
# hello SubscriptionID toouse
$subscriptionId = "00000000-0000-0000-0000-000000000000"

# Resource group that contains hello Network Security Group
$resourceGroupName = "<resourceGroupName>"

# hello name of hello Network Security Group
$nsgName = "NSGName"

# hello storage account name that contains hello NSG logs
$storageAccountName = "<storageAccountName>" 

# hello date and time for hello log toobe queried, logs are stored in hour intervals.
[datetime]$logtime = "06/16/2017 20:00"

# Retrieve hello primary storage account key tooaccess hello NSG logs
$StorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName).Value[0]

# Setup a new storage context toobe used tooquery hello logs
$ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

# Container name used by NSG flow logs
$ContainerName = "insights-logs-networksecuritygroupflowevent"

# Name of hello blob that contains hello NSG flow log
$BlobName = "resourceId=/SUBSCRIPTIONS/${subscriptionId}/RESOURCEGROUPS/${resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/${nsgName}/y=$($logtime.Year)/m=$(($logtime).ToString("MM"))/d=$(($logtime).ToString("dd"))/h=$(($logtime).ToString("HH"))/m=00/PT1H.json"

# Gets hello storage blog
$Blob = Get-AzureStorageBlob -Context $ctx -Container $ContainerName -Blob $BlobName

# Gets hello block blog of type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from hello storage blob
$CloudBlockBlob = [Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob] $Blob.ICloudBlob

# Stores hello block list in a variable from hello block blob.
$blockList = $CloudBlockBlob.DownloadBlockList()
```

<span data-ttu-id="502a1-120">Witaj `$blockList` zmiennej zwraca listę hello bloków w obiekcie blob hello.</span><span class="sxs-lookup"><span data-stu-id="502a1-120">hello `$blockList` variable returns a list of hello blocks in hello blob.</span></span> <span data-ttu-id="502a1-121">Każdy obiekt blob blokowy zawiera co najmniej dwa bloki.</span><span class="sxs-lookup"><span data-stu-id="502a1-121">Each block blob contains at least two blocks.</span></span>  <span data-ttu-id="502a1-122">Witaj pierwszego bloku ma długość `21` bajtów, blok ten zawiera hello otwierających nawiasów kwadratowych hello json dziennika.</span><span class="sxs-lookup"><span data-stu-id="502a1-122">hello first block has a length of `21` bytes, this block contains hello opening brackets of hello json log.</span></span> <span data-ttu-id="502a1-123">Witaj innych bloku jest hello zamykających nawiasów kwadratowych i o długości `9` bajtów.</span><span class="sxs-lookup"><span data-stu-id="502a1-123">hello other block is hello closing brackets and has a length of `9` bytes.</span></span>  <span data-ttu-id="502a1-124">Jak widać powitania po przykładowy dziennik zawiera wpisy siedmiu, każdego jest pojedynczy wpis.</span><span class="sxs-lookup"><span data-stu-id="502a1-124">As you can see hello following example log has seven entries in it, each being an individual entry.</span></span> <span data-ttu-id="502a1-125">Wszystkie nowe wpisy w dzienniku hello są dodawane zakończenia toohello bezpośrednio poprzedzający hello bloku końcowego.</span><span class="sxs-lookup"><span data-stu-id="502a1-125">All new entries in hello log are added toohello end right before hello final block.</span></span>

```
Name                                         Length Committed
----                                         ------ ---------
ZDk5MTk5N2FkNGE0MmY5MTk5ZWViYjA0YmZhODRhYzY=     21      True
NzQxNDA5MTRhNDUzMGI2M2Y1MDMyOWZlN2QwNDZiYzQ=   2685      True
ODdjM2UyMWY3NzFhZTU3MmVlMmU5MDNlOWEwNWE3YWY=   2586      True
ZDU2MjA3OGQ2ZDU3MjczMWQ4MTRmYWNhYjAzOGJkMTg=   2688      True
ZmM3ZWJjMGQ0ZDA1ODJlOWMyODhlOWE3MDI1MGJhMTc=   2775      True
ZGVkYTc4MzQzNjEyMzlmZWE5MmRiNjc1OWE5OTc0OTQ=   2676      True
ZmY2MjUzYTIwYWIyOGU1OTA2ZDY1OWYzNmY2NmU4ZTY=   2777      True
Mzk1YzQwM2U0ZWY1ZDRhOWFlMTNhYjQ3OGVhYmUzNjk=   2675      True
ZjAyZTliYWE3OTI1YWZmYjFmMWI0MjJhNzMxZTI4MDM=      9      True
```

## <a name="read-hello-block-blob"></a><span data-ttu-id="502a1-126">Odczyt hello blokowych obiektów blob</span><span class="sxs-lookup"><span data-stu-id="502a1-126">Read hello block blob</span></span>

<span data-ttu-id="502a1-127">Następnie potrzebujemy tooread hello `$blocklist` zmiennej tooretrieve hello danych.</span><span class="sxs-lookup"><span data-stu-id="502a1-127">Next we need tooread hello `$blocklist` variable tooretrieve hello data.</span></span> <span data-ttu-id="502a1-128">W tym przykładzie, który mamy iterację hello blocklist odczytuj bajty hello z każdego bloku i Wątek je w tablicy.</span><span class="sxs-lookup"><span data-stu-id="502a1-128">In this example we iterate through hello blocklist, read hello bytes from each block and story them in an array.</span></span> <span data-ttu-id="502a1-129">Używamy hello [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) metody tooretrieve hello danych.</span><span class="sxs-lookup"><span data-stu-id="502a1-129">We use hello [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) method tooretrieve hello data.</span></span>

```powershell
# Set hello size of hello byte array toohello largest block
$maxvalue = ($blocklist | measure Length -Maximum).Maximum

# Create an array toostore values in
$valuearray = @()

# Define hello starting index tootrack hello current block being read
$index = 0

# Loop through each block in hello block list
for($i=0; $i -lt $blocklist.count; $i++)
{

# Create a byte array object toostory hello bytes from hello block
$downloadArray = New-Object -TypeName byte[] -ArgumentList $maxvalue

# Download hello data into hello ByteArray, starting with hello current index, for hello number of bytes in hello current block. Index is increased by 3 when reading tooremove preceding comma.
$CloudBlockBlob.DownloadRangeToByteArray($downloadArray,0,$index+3,$($blockList[$i].Length-1)) | Out-Null

# Increment hello index by adding hello current block length toohello previous index
$index = $index + $blockList[$i].Length

# Retrieve hello string from hello byte array

$value = [System.Text.Encoding]::ASCII.GetString($downloadArray)

# Add hello log entry toohello value array
$valuearray += $value
}
```

<span data-ttu-id="502a1-130">Teraz hello `$valuearray` tablica zawiera ciąg hello każdego bloku.</span><span class="sxs-lookup"><span data-stu-id="502a1-130">Now hello `$valuearray` array contains hello string value of each block.</span></span> <span data-ttu-id="502a1-131">tooverify hello wpisu, get hello drugi toohello ostatnią wartość z tablicy hello uruchamiając `$valuearray[$valuearray.Length-2]`.</span><span class="sxs-lookup"><span data-stu-id="502a1-131">tooverify hello entry, get hello second toohello last value from hello array by running `$valuearray[$valuearray.Length-2]`.</span></span> <span data-ttu-id="502a1-132">Firma Microsoft nie chcę ostatnią wartość hello jest po prostu hello zamykającego nawiasu.</span><span class="sxs-lookup"><span data-stu-id="502a1-132">We do not want hello last value is just hello closing bracket.</span></span>

<span data-ttu-id="502a1-133">na poniższy przykład hello są wyświetlane wyniki Hello tej wartości:</span><span class="sxs-lookup"><span data-stu-id="502a1-133">hello results of this value are shown in hello following example:</span></span>

```json
        {
             "time": "2017-06-16T20:59:43.7340000Z",
             "systemId": "5f4d02d3-a7d0-4ed4-9ce8-c0ae9377951c",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/CONTOSORG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/CONTOSONSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_AllowInternetOutBound","flows":[{"mac":"000D3A18077E","flowTuples":["1497646722,10.0.0.4,168.62.32.14,44904,443,T,O,A","1497646722,10.0.0.4,52.240.48.24,45218,443,T,O,A","1497646725,10.
0.0.4,168.62.32.14,44910,443,T,O,A","1497646725,10.0.0.4,52.240.48.24,45224,443,T,O,A","1497646728,10.0.0.4,168.62.32.14,44916,443,T,O,A","1497646728,10.0.0.4,52.240.48.24,45230,443,T,O,A","1497646732,10.0.0.4,168.62.32.14,44922,443,T,O,A","14976
46732,10.0.0.4,52.240.48.24,45236,443,T,O,A","1497646735,10.0.0.4,168.62.32.14,44928,443,T,O,A","1497646735,10.0.0.4,52.240.48.24,45242,443,T,O,A","1497646738,10.0.0.4,168.62.32.14,44934,443,T,O,A","1497646738,10.0.0.4,52.240.48.24,45248,443,T,O,
A","1497646742,10.0.0.4,168.62.32.14,44942,443,T,O,A","1497646742,10.0.0.4,52.240.48.24,45256,443,T,O,A","1497646745,10.0.0.4,168.62.32.14,44948,443,T,O,A","1497646745,10.0.0.4,52.240.48.24,45262,443,T,O,A","1497646749,10.0.0.4,168.62.32.14,44954
,443,T,O,A","1497646749,10.0.0.4,52.240.48.24,45268,443,T,O,A","1497646753,10.0.0.4,168.62.32.14,44960,443,T,O,A","1497646753,10.0.0.4,52.240.48.24,45274,443,T,O,A","1497646756,10.0.0.4,168.62.32.14,44966,443,T,O,A","1497646756,10.0.0.4,52.240.48
.24,45280,443,T,O,A","1497646759,10.0.0.4,168.62.32.14,44972,443,T,O,A","1497646759,10.0.0.4,52.240.48.24,45286,443,T,O,A","1497646763,10.0.0.4,168.62.32.14,44978,443,T,O,A","1497646763,10.0.0.4,52.240.48.24,45292,443,T,O,A","1497646766,10.0.0.4,
168.62.32.14,44984,443,T,O,A","1497646766,10.0.0.4,52.240.48.24,45298,443,T,O,A","1497646769,10.0.0.4,168.62.32.14,44990,443,T,O,A","1497646769,10.0.0.4,52.240.48.24,45304,443,T,O,A","1497646773,10.0.0.4,168.62.32.14,44996,443,T,O,A","1497646773,
10.0.0.4,52.240.48.24,45310,443,T,O,A","1497646776,10.0.0.4,168.62.32.14,45002,443,T,O,A","1497646776,10.0.0.4,52.240.48.24,45316,443,T,O,A","1497646779,10.0.0.4,168.62.32.14,45008,443,T,O,A","1497646779,10.0.0.4,52.240.48.24,45322,443,T,O,A"]}]}
,{"rule":"DefaultRule_DenyAllInBound","flows":[]},{"rule":"UserRule_ssh-rule","flows":[]},{"rule":"UserRule_web-rule","flows":[{"mac":"000D3A18077E","flowTuples":["1497646738,13.82.225.93,10.0.0.4,1180,80,T,I,A","1497646750,13.82.225.93,10.0.0.4,
1184,80,T,I,A","1497646768,13.82.225.93,10.0.0.4,1181,80,T,I,A","1497646780,13.82.225.93,10.0.0.4,1336,80,T,I,A"]}]}]}
        }
```

<span data-ttu-id="502a1-134">Ten scenariusz jest przykładem sposobu tooread wpisy w grupie NSG przepływu dzienniki bez konieczności tooparse hello cały dziennik.</span><span class="sxs-lookup"><span data-stu-id="502a1-134">This scenario is an example of how tooread entries in NSG flow logs without having tooparse hello entire log.</span></span> <span data-ttu-id="502a1-135">Nowe wpisy w dzienniku hello mogą odczytywać, ponieważ są one zapisywane za pomocą identyfikator bloku hello lub śledzenia długość hello bloków przechowywane w hello blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="502a1-135">You can read new entries in hello log as they are written by using hello block ID or by tracking hello length of blocks stored in hello block blob.</span></span> <span data-ttu-id="502a1-136">Dzięki temu tooread tylko hello nowe wpisy.</span><span class="sxs-lookup"><span data-stu-id="502a1-136">This allows you tooread only hello new entries.</span></span>


## <a name="next-steps"></a><span data-ttu-id="502a1-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="502a1-137">Next steps</span></span>

<span data-ttu-id="502a1-138">Odwiedź stronę [wizualizacji dzienników przepływu NSG obserwatora sieci Azure przy użyciu narzędzi typu open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) toolearn więcej informacji na temat innych sposobów tooview NSG przepływu dzienników.</span><span class="sxs-lookup"><span data-stu-id="502a1-138">Visit [visualize Azure Network Watcher NSG flow logs using open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) toolearn more about other ways tooview NSG flow logs.</span></span>

<span data-ttu-id="502a1-139">toolearn można znaleźć więcej informacji na temat magazynu obiektów blob: [powiązania magazynu obiektów Blob platformy Azure funkcji](../azure-functions/functions-bindings-storage-blob.md)</span><span class="sxs-lookup"><span data-stu-id="502a1-139">toolearn more about storage blobs visit: [Azure Functions Blob storage bindings](../azure-functions/functions-bindings-storage-blob.md)</span></span>
