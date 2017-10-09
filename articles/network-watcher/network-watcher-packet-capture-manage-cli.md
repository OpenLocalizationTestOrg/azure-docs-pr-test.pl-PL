---
title: "Przechwytywanie pakietów aaaManage z obserwatora sieciowego Azure - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toomanage hello funkcja przechwytywania pakietów obserwatora sieciowego używa interfejsu wiersza polecenia platformy Azure w wersji 2.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d19cb7d0ca3b7a9bc0546859e07ef6d4df4f42d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="186cb-103">Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure używa interfejsu wiersza polecenia platformy Azure w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="186cb-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="186cb-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="186cb-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="186cb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="186cb-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="186cb-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="186cb-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="186cb-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="186cb-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="186cb-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="186cb-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="186cb-109">Przechwytywania pakietów obserwatora sieciowego umożliwia toocreate przechwytywania sesji tootrack ruch tooand z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="186cb-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="186cb-110">Filtry są przewidziane tooensure sesji przechwytywania hello przechwytywać tylko hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="186cb-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="186cb-111">Przechwytywania pakietów pomaga anomalii sieci toodiagnose rozbudowy i aktywne.</span><span class="sxs-lookup"><span data-stu-id="186cb-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="186cb-112">Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat sieci wtargnięcia toodebug klient serwer, komunikację i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="186cb-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="186cb-113">Jest przechwytywania pakietów wyzwalacza stanie tooremotely, ta funkcja ułatwia hello obciążeń uruchomionych przechwytywania pakietów ręcznego, jak i na powitania żądanego komputera, który zapisuje cenny czas.</span><span class="sxs-lookup"><span data-stu-id="186cb-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="186cb-114">W tym artykule wykorzystano naszej nowej generacji interfejsu wiersza polecenia model wdrażania hello zasobów management, Azure CLI 2.0, który jest dostępny dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="186cb-114">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="186cb-115">Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="186cb-115">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="186cb-116">Ten artykuł przedstawia hello zarządzania różnych zadań, które są obecnie dostępne dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="186cb-116">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="186cb-117">**Uruchom przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="186cb-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="186cb-118">**Zatrzymaj przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="186cb-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="186cb-119">**Usuń przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="186cb-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="186cb-120">**Pobierz przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="186cb-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="186cb-121">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="186cb-121">Before you begin</span></span>

<span data-ttu-id="186cb-122">W tym artykule przyjęto założenie, że masz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="186cb-122">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="186cb-123">Wystąpienia obserwatora sieciowego w regionie hello ma toocreate przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="186cb-123">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="186cb-124">Maszyna wirtualna o pakietów hello przechwytywania rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="186cb-124">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="186cb-125">Przechwytywania pakietów wymaga toobe agent uruchomiony na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="186cb-125">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="186cb-126">Witaj Agent jest instalowany jako rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="186cb-126">hello Agent is installed as an extension.</span></span> <span data-ttu-id="186cb-127">Aby uzyskać instrukcje dotyczące rozszerzenia maszyny Wirtualnej, odwiedź stronę [rozszerzenia maszyn wirtualnych i funkcji](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="186cb-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="186cb-128">Zainstaluj rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="186cb-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="186cb-129">Krok 1</span><span class="sxs-lookup"><span data-stu-id="186cb-129">Step 1</span></span>

<span data-ttu-id="186cb-130">Uruchom hello `az vm extension set` polecenia cmdlet tooinstall hello pakietów przechwytywania agenta na maszynie wirtualnej typu Gość hello.</span><span class="sxs-lookup"><span data-stu-id="186cb-130">Run hello `az vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="186cb-131">W przypadku maszyn wirtualnych systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="186cb-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="186cb-132">Dla maszyn wirtualnych systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="186cb-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="186cb-133">Krok 2</span><span class="sxs-lookup"><span data-stu-id="186cb-133">Step 2</span></span>

<span data-ttu-id="186cb-134">tooensure, który hello agent jest zainstalowany, uruchom hello `vm extension get` polecenia cmdlet i przekaż go hello grupy zasobów i nazwy maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="186cb-134">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="186cb-135">Sprawdź, czy hello wynikowej listy tooensure hello agent jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="186cb-135">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="186cb-136">następujące przykładowe Hello jest przykładem odpowiedź hello uruchamianie`az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="186cb-136">hello following sample is an example of hello response from running `az vm extension show`</span></span>

```json
{
  "autoUpgradeMinorVersion": true,
  "forceUpdateTag": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/NetworkWatcherAgentWindows",
  "instanceView": null,
  "location": "westcentralus",
  "name": "NetworkWatcherAgentWindows",
  "protectedSettings": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.NetworkWatcher",
  "resourceGroup": "{resourceGroupName}",
  "settings": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.4",
  "virtualMachineExtensionType": "NetworkWatcherAgentWindows"
}
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="186cb-137">Uruchom przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="186cb-137">Start a packet capture</span></span>

<span data-ttu-id="186cb-138">Po hello powyższych kroków są spełnione, agent przechwytywania pakietów hello jest zainstalowany na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="186cb-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="186cb-139">Krok 1</span><span class="sxs-lookup"><span data-stu-id="186cb-139">Step 1</span></span>

<span data-ttu-id="186cb-140">Witaj następnym krokiem jest tooretrieve hello obserwatora sieciowego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="186cb-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="186cb-141">Opcjonalna nazwa hello obserwatora sieciowego jest przekazywany toohello `az network watcher show` polecenia cmdlet w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="186cb-141">TThe name of hello Network Watcher is passed toohello `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="186cb-142">Krok 2</span><span class="sxs-lookup"><span data-stu-id="186cb-142">Step 2</span></span>

<span data-ttu-id="186cb-143">Pobierz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="186cb-143">Retrieve a storage account.</span></span> <span data-ttu-id="186cb-144">To konto magazynu jest plik przechwytywania pakietów hello toostore używane.</span><span class="sxs-lookup"><span data-stu-id="186cb-144">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="186cb-145">Krok 3</span><span class="sxs-lookup"><span data-stu-id="186cb-145">Step 3</span></span>

<span data-ttu-id="186cb-146">Filtry mogą być używane toolimit hello dane przechowywane przez przechwytywania pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="186cb-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="186cb-147">Witaj poniższy przykład konfiguruje przechwytywania pakietów z kilka filtrów.</span><span class="sxs-lookup"><span data-stu-id="186cb-147">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="186cb-148">Witaj pierwsze trzy filtry zbierania ruch wychodzący TCP tylko z lokalny adres IP 10.0.0.3 porty toodestination 20, 80 i 443.</span><span class="sxs-lookup"><span data-stu-id="186cb-148">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="186cb-149">Filtr Hello zbiera tylko ruch UDP.</span><span class="sxs-lookup"><span data-stu-id="186cb-149">hello last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="186cb-150">Witaj poniższym przykładzie jest hello oczekiwane dane wyjściowe systemem hello `az network watcher packet-capture create` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="186cb-150">hello following example is hello expected output from running hello `az network watcher packet-capture create` cmdlet.</span></span>

```json
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/p
roviders/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapture_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="186cb-151">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="186cb-151">Get a packet capture</span></span>

<span data-ttu-id="186cb-152">Uruchomiona hello `az network watcher packet-capture show` polecenie cmdlet pobiera stan hello przechwytywania pakietów aktualnie uruchomione lub zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="186cb-152">Running hello `az network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="186cb-153">Witaj poniższym przykładzie jest hello dane wyjściowe hello `az network watcher packet-capture show` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="186cb-153">hello following example is hello output from hello `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="186cb-154">Witaj poniższym przykładzie jest po zakończeniu hello przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="186cb-154">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="186cb-155">z StopReason TimeExceeded Hello wartość PacketCaptureStatus jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="186cb-155">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="186cb-156">Ta wartość pokazuje, że przechwytywania pakietów hello zakończyła się pomyślnie i jego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="186cb-156">This value shows that hello packet capture was successful and ran its time.</span></span>

```
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/providers/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapt
ure_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="186cb-157">Zatrzymaj przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="186cb-157">Stop a packet capture</span></span>

<span data-ttu-id="186cb-158">Uruchamiając hello `az network watcher packet-capture stop` polecenia cmdlet, jeśli sesja przechwytywania jest w toku jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="186cb-158">By running hello `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="186cb-159">Witaj polecenie cmdlet nie zwraca żadnej odpowiedzi podczas uruchomionego na aktualnie uruchomionych sesji przechwytywania lub istniejącej sesji, która już została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="186cb-159">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="186cb-160">Usuń przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="186cb-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="186cb-161">Usunięcie przechwytywania pakietów nie powoduje usunięcia pliku hello hello koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="186cb-161">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="186cb-162">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="186cb-162">Download a packet capture</span></span>

<span data-ttu-id="186cb-163">Po zakończeniu sesji przechwytywania pakietów hello pliku przechwytywania może być przekazane tooblob tooa lub magazynu lokalnego pliku na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="186cb-163">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="186cb-164">Lokalizacja przechowywania Hello przechwytywania pakietów hello jest definiowany podczas tworzenia hello sesji.</span><span class="sxs-lookup"><span data-stu-id="186cb-164">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="186cb-165">Tooaccess wygodne narzędzie te Przechwytywanie plików, tooa zapisane konto magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="186cb-165">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="186cb-166">Jeśli określono konto magazynu, zapisywane są pliki przechwytywania pakietów tooa konta magazynu w następującej lokalizacji hello:</span><span class="sxs-lookup"><span data-stu-id="186cb-166">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="186cb-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="186cb-167">Next steps</span></span>

<span data-ttu-id="186cb-168">Dowiedz się, jak przechwytywanie pakietów tooautomate z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="186cb-168">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="186cb-169">Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="186cb-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
