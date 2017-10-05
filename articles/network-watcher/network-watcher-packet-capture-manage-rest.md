---
title: "Zarządzanie przechwytywania pakietów z obserwatora sieciowego Azure - interfejsu API REST | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśnia sposób zarządzania funkcja przechwytywania pakietów obserwatora sieciowego przy użyciu interfejsu API REST Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 53fe0324-835f-4005-afc8-145eeb314aeb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 49ec20802a252258d8493eb26510270b925e851a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="c41f6-103">Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure przy użyciu interfejsu API REST Azure</span><span class="sxs-lookup"><span data-stu-id="c41f6-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c41f6-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c41f6-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="c41f6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c41f6-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="c41f6-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="c41f6-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="c41f6-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="c41f6-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="c41f6-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="c41f6-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="c41f6-109">Przechwytywania pakietów obserwatora sieciowego umożliwia tworzenie sesji przechwytywania, aby śledzić ruch do i z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c41f6-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="c41f6-110">Filtry są dostępne dla sesji przechwytywania, aby upewnić się, że przechwytywać ruch, który ma.</span><span class="sxs-lookup"><span data-stu-id="c41f6-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="c41f6-111">Przechwytywania pakietów ułatwia diagnozowanie anomalii sieci rozbudowy i aktywne.</span><span class="sxs-lookup"><span data-stu-id="c41f6-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="c41f6-112">Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat wtargnięcia sieci, aby debugować komunikacja klient serwer i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="c41f6-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="c41f6-113">Dzięki możliwości zdalnie wywołać przechwytywania pakietów, ta funkcja ułatwia obciążeń uruchomionych przechwytywania pakietów, ręcznie i tylko na odpowiednią maszynę, która zapisuje cenny czas.</span><span class="sxs-lookup"><span data-stu-id="c41f6-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="c41f6-114">Ten artykuł przedstawia za pomocą zadań zarządzania różnych, które są obecnie dostępne dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c41f6-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="c41f6-115">**Pobierz przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="c41f6-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="c41f6-116">**Wyświetl listę wszystkich przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="c41f6-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="c41f6-117">**Zapytać o stan przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="c41f6-117">**Query the status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="c41f6-118">**Uruchom przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="c41f6-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="c41f6-119">**Zatrzymaj przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="c41f6-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="c41f6-120">**Usuń przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="c41f6-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="c41f6-121">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c41f6-121">Before you begin</span></span>

<span data-ttu-id="c41f6-122">W tym scenariuszu można wywołać interfejsu API Rest obserwatora sieciowego do uruchomienia przepływu Sprawdź IP.</span><span class="sxs-lookup"><span data-stu-id="c41f6-122">In this scenario, you call the Network Watcher Rest API to run IP Flow Verify.</span></span> <span data-ttu-id="c41f6-123">ARMclient służy do wywołania interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c41f6-123">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="c41f6-124">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="c41f6-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="c41f6-125">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) utworzyć obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="c41f6-125">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> <span data-ttu-id="c41f6-126">Rozszerzenie maszyny wirtualnej wymaga przechwytywania pakietów `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="c41f6-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="c41f6-127">Instalowanie rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="c41f6-127">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="c41f6-128">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="c41f6-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="c41f6-129">Pobieranie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c41f6-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="c41f6-130">Uruchom następujący skrypt, aby wrócić do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c41f6-130">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="c41f6-131">Te informacje są potrzebne do uruchomienia przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c41f6-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="c41f6-132">Poniższy kod wymaga zmiennych:</span><span class="sxs-lookup"><span data-stu-id="c41f6-132">The following code needs variables:</span></span>

- <span data-ttu-id="c41f6-133">**Identyfikator subskrypcji** — identyfikator subskrypcji można również pobrać z **Get-AzureRMSubscription** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c41f6-133">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="c41f6-134">**resourceGroupName** — Nazwa grupy zasobów, która zawiera maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="c41f6-134">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="c41f6-135">Z następujących danych wyjściowych identyfikator maszyny wirtualnej jest używany w następnym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c41f6-135">From the following output, the id of the virtual machine is used in the next example.</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```


## <a name="get-a-packet-capture"></a><span data-ttu-id="c41f6-136">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c41f6-136">Get a packet capture</span></span>

<span data-ttu-id="c41f6-137">Poniższy przykład pobiera stan przechwytywania pojedynczy pakiet</span><span class="sxs-lookup"><span data-stu-id="c41f6-137">The following example gets the status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="c41f6-138">Przykłady typowych odpowiedzi zwracany podczas wysyłania zapytania o stan przechwytywania pakietów są następujące odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="c41f6-138">The following responses are examples of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Running",
  "packetCaptureError": []
}
```

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Stopped",
  "stopReason": "TimeExceeded",
  "packetCaptureError": []
}
```

## <a name="list-all-packet-captures"></a><span data-ttu-id="c41f6-139">Wyświetl listę wszystkich przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c41f6-139">List all packet captures</span></span>

<span data-ttu-id="c41f6-140">Poniższy przykład pobiera wszystkie sesje przechwytywania pakietów w regionie.</span><span class="sxs-lookup"><span data-stu-id="c41f6-140">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="c41f6-141">Następującą odpowiedź jest przechwytuje przykład typowej odpowiedzi zwracany podczas pobierania wszystkich pakietów</span><span class="sxs-lookup"><span data-stu-id="c41f6-141">The following response is an example of a typical response returned when getting all packet captures</span></span>

```json
{
  "value": [
    {
      "name": "TestPacketCapture6",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Succeeded",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_19_53_056.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    },
    {
      "name": "TestPacketCapture7",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture7",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Failed",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_23_15_364.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    }
  ]
}
```

## <a name="query-packet-capture-status"></a><span data-ttu-id="c41f6-142">Kwerenda o stan przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c41f6-142">Query packet capture status</span></span>

<span data-ttu-id="c41f6-143">Poniższy przykład pobiera wszystkie sesje przechwytywania pakietów w regionie.</span><span class="sxs-lookup"><span data-stu-id="c41f6-143">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="c41f6-144">Następującą odpowiedź jest przykładem typowych odpowiedzi zwracany podczas wysyłania zapytania o stan przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c41f6-144">The following response is an example of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="c41f6-145">Uruchom przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c41f6-145">Start packet capture</span></span>

<span data-ttu-id="c41f6-146">Poniższy przykład tworzy przechwytywania pakietów na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c41f6-146">The following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="c41f6-147">Przykład jest parametry umożliwiające elastyczność tworzenia przykładem.</span><span class="sxs-lookup"><span data-stu-id="c41f6-147">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
$storageaccountname = "contosoexamplergdiag374"
$vmName = "ContosoVM"
$bytestoCaptureperPacket = "0"
$bytesPerSession = "1073741824"
$captureTimeinSeconds = "60"
$localIP = ""
$localPort = "" # Examples are: 80, or 80-120
$remoteIP = ""
$remotePort = "" # Examples are: 80, or 80-120
$protocol = "" # Valid values are TCP, UDP and Any.
$targetUri = "" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName
$storageId = "" # Example: "https://mytestaccountname.blob.core.windows.net/capture/vm1Capture.cap"
$storagePath = ""
$localFilePath = "c:\\temp\\packetcapture.cap" # Example: "d:\capture\vm1Capture.cap"

$requestBody = @"
{
    'properties':  {
                       'target':  '/${targetUri}',
                       'bytesToCapturePerPacket':  '${bytestoCaptureperPacket}',
                       'totalBytesPerSession':  '${bytesPerSession}',
                       'timeLimitinSeconds':  '${captureTimeinSeconds}',
                       'storageLocation':  {
                                               'storageId':  '${storageId}',
                                               'storagePath':  '${storagePath}',
                                               'filePath':  '${localFilePath}'
                                           },
                       'filters':  [
                                       {
                                           'protocol':  '${protocol}',
                                           'localIPAddress':  '${localIP}',
                                           'localPort':  '${localPort}',
                                           'remoteIPAddress':  '${remoteIP}',
                                           'remotePort':  '${remotePort}'
                                       }
                                   ]
                   }
}
"@

armclient PUT "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-07-01" $requestbody
```

## <a name="stop-packet-capture"></a><span data-ttu-id="c41f6-148">Zatrzymaj przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c41f6-148">Stop packet capture</span></span>

<span data-ttu-id="c41f6-149">Poniższy przykład zatrzymuje przechwytywania pakietów na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c41f6-149">The following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="c41f6-150">Przykład jest parametry umożliwiające elastyczność tworzenia przykładem.</span><span class="sxs-lookup"><span data-stu-id="c41f6-150">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="c41f6-151">Usuń przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c41f6-151">Delete packet capture</span></span>

<span data-ttu-id="c41f6-152">W następującym przykładzie przechwytywania pakietów, na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c41f6-152">The following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="c41f6-153">Przykład jest parametry umożliwiające elastyczność tworzenia przykładem.</span><span class="sxs-lookup"><span data-stu-id="c41f6-153">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="c41f6-154">Usunięcie przechwytywania pakietów nie powoduje usunięcia plików na koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="c41f6-154">Deleting a packet capture does not delete the file in the storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="c41f6-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c41f6-155">Next steps</span></span>

<span data-ttu-id="c41f6-156">Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu azure, zapoznaj się [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="c41f6-156">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="c41f6-157">Kolejnym narzędziem, który może służyć jest Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="c41f6-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="c41f6-158">Więcej informacji na temat Eksploratora usługi Storage można znaleźć tutaj przy użyciu następującego łącza: [Eksploratora usługi Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="c41f6-158">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="c41f6-159">Dowiedz się, jak można zautomatyzować przechwytywania pakietów z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="c41f6-159">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













