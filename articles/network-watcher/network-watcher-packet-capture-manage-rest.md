---
title: "Przechwytywanie pakietów aaaManage z obserwatora sieciowego Azure - interfejsu API REST | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toomanage hello funkcja przechwytywania pakietów obserwatora sieciowego przy użyciu interfejsu API REST Azure"
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
ms.openlocfilehash: 7a531fbe796e85e94961bd192d171defb299be05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="6d339-103">Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure przy użyciu interfejsu API REST Azure</span><span class="sxs-lookup"><span data-stu-id="6d339-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6d339-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6d339-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="6d339-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d339-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="6d339-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="6d339-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="6d339-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="6d339-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="6d339-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="6d339-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="6d339-109">Przechwytywania pakietów obserwatora sieciowego umożliwia toocreate przechwytywania sesji tootrack ruch tooand z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6d339-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="6d339-110">Filtry są przewidziane tooensure sesji przechwytywania hello przechwytywać tylko hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="6d339-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="6d339-111">Przechwytywania pakietów pomaga anomalii sieci toodiagnose rozbudowy i aktywne.</span><span class="sxs-lookup"><span data-stu-id="6d339-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="6d339-112">Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat sieci wtargnięcia toodebug klient serwer, komunikację i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="6d339-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="6d339-113">Jest przechwytywania pakietów wyzwalacza stanie tooremotely, ta funkcja ułatwia hello obciążeń uruchomionych przechwytywania pakietów ręcznego, jak i na powitania żądanego komputera, który zapisuje cenny czas.</span><span class="sxs-lookup"><span data-stu-id="6d339-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="6d339-114">Ten artykuł przedstawia hello zarządzania różnych zadań, które są obecnie dostępne dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="6d339-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="6d339-115">**Pobierz przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="6d339-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="6d339-116">**Wyświetl listę wszystkich przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="6d339-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="6d339-117">**Badanie stanu hello przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="6d339-117">**Query hello status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="6d339-118">**Uruchom przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="6d339-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="6d339-119">**Zatrzymaj przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="6d339-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="6d339-120">**Usuń przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="6d339-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="6d339-121">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="6d339-121">Before you begin</span></span>

<span data-ttu-id="6d339-122">W tym scenariuszu należy wywołać toorun interfejsu API Rest obserwatora sieciowego hello Sprawdź przepływ IP.</span><span class="sxs-lookup"><span data-stu-id="6d339-122">In this scenario, you call hello Network Watcher Rest API toorun IP Flow Verify.</span></span> <span data-ttu-id="6d339-123">ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d339-123">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="6d339-124">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="6d339-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="6d339-125">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="6d339-125">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> <span data-ttu-id="6d339-126">Rozszerzenie maszyny wirtualnej wymaga przechwytywania pakietów `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="6d339-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="6d339-127">Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="6d339-127">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="6d339-128">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="6d339-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="6d339-129">Pobieranie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6d339-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="6d339-130">Uruchom maszynę wirtualną powitania po tooreturn skryptu.</span><span class="sxs-lookup"><span data-stu-id="6d339-130">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="6d339-131">Te informacje są potrzebne do uruchomienia przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="6d339-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="6d339-132">Witaj następujący kod wymaga zmiennych:</span><span class="sxs-lookup"><span data-stu-id="6d339-132">hello following code needs variables:</span></span>

- <span data-ttu-id="6d339-133">**Identyfikator subskrypcji** -hello identyfikator subskrypcji można również pobrać z hello **Get-AzureRMSubscription** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6d339-133">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="6d339-134">**resourceGroupName** — Witaj Nazwa grupy zasobów, która zawiera maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="6d339-134">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="6d339-135">Z danych wyjściowych poniżej hello, hello identyfikator maszyny wirtualnej hello jest używany w następnym przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="6d339-135">From hello following output, hello id of hello virtual machine is used in hello next example.</span></span>

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


## <a name="get-a-packet-capture"></a><span data-ttu-id="6d339-136">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="6d339-136">Get a packet capture</span></span>

<span data-ttu-id="6d339-137">Witaj poniższy przykład pobiera stan hello przechwytywania pojedynczy pakiet</span><span class="sxs-lookup"><span data-stu-id="6d339-137">hello following example gets hello status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="6d339-138">Hello są następujące odpowiedzi przykłady typowych odpowiedzi zwracany, gdy badanie stanu hello przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="6d339-138">hello following responses are examples of a typical response returned when querying hello status of a packet capture.</span></span>

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

## <a name="list-all-packet-captures"></a><span data-ttu-id="6d339-139">Wyświetl listę wszystkich przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="6d339-139">List all packet captures</span></span>

<span data-ttu-id="6d339-140">Poniższy przykład Hello pobiera wszystkie sesje przechwytywania pakietów w regionie.</span><span class="sxs-lookup"><span data-stu-id="6d339-140">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="6d339-141">Witaj następującą odpowiedź jest przechwytuje przykład typowej odpowiedzi zwracany podczas pobierania wszystkich pakietów</span><span class="sxs-lookup"><span data-stu-id="6d339-141">hello following response is an example of a typical response returned when getting all packet captures</span></span>

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

## <a name="query-packet-capture-status"></a><span data-ttu-id="6d339-142">Kwerenda o stan przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="6d339-142">Query packet capture status</span></span>

<span data-ttu-id="6d339-143">Poniższy przykład Hello pobiera wszystkie sesje przechwytywania pakietów w regionie.</span><span class="sxs-lookup"><span data-stu-id="6d339-143">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="6d339-144">Witaj następującą odpowiedź jest przykładem typowych odpowiedzi zwracany, gdy badanie stanu hello przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="6d339-144">hello following response is an example of a typical response returned when querying hello status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="6d339-145">Uruchom przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="6d339-145">Start packet capture</span></span>

<span data-ttu-id="6d339-146">Witaj poniższy przykład tworzy przechwytywania pakietów na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6d339-146">hello following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="6d339-147">przykład Witaj jest sparametryzowane tooallow elastyczność tworzenia przykładem.</span><span class="sxs-lookup"><span data-stu-id="6d339-147">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

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

## <a name="stop-packet-capture"></a><span data-ttu-id="6d339-148">Zatrzymaj przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="6d339-148">Stop packet capture</span></span>

<span data-ttu-id="6d339-149">Poniższy przykład Hello zatrzymuje przechwytywania pakietów na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6d339-149">hello following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="6d339-150">przykład Witaj jest sparametryzowane tooallow elastyczność tworzenia przykładem.</span><span class="sxs-lookup"><span data-stu-id="6d339-150">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="6d339-151">Usuń przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="6d339-151">Delete packet capture</span></span>

<span data-ttu-id="6d339-152">Poniższy przykład Hello usuwa przechwytywania pakietów, na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6d339-152">hello following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="6d339-153">przykład Witaj jest sparametryzowane tooallow elastyczność tworzenia przykładem.</span><span class="sxs-lookup"><span data-stu-id="6d339-153">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="6d339-154">Usunięcie przechwytywania pakietów nie powoduje usunięcia pliku hello na koncie magazynu hello</span><span class="sxs-lookup"><span data-stu-id="6d339-154">Deleting a packet capture does not delete hello file in hello storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d339-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d339-155">Next steps</span></span>

<span data-ttu-id="6d339-156">Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu azure, zobacz zbyt[Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="6d339-156">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="6d339-157">Kolejnym narzędziem, który może służyć jest Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="6d339-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="6d339-158">Więcej informacji na temat Eksploratora usługi Storage można znaleźć tutaj na powitania następującego łącza: [Eksploratora usługi Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="6d339-158">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="6d339-159">Dowiedz się, jak przechwytywanie pakietów tooautomate z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="6d339-159">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













