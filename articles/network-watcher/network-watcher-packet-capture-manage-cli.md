---
title: "Zarządzanie przechwytywania pakietów z obserwatora sieciowego Azure - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśnia sposób zarządzania funkcja przechwytywania pakietów obserwatora sieciowego używa interfejsu wiersza polecenia platformy Azure w wersji 2.0"
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
ms.openlocfilehash: c94eb46f31f2f19b843ccd7bf77b8a39943a07d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="a2223-103">Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure używa interfejsu wiersza polecenia platformy Azure w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="a2223-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a2223-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a2223-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="a2223-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2223-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="a2223-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="a2223-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="a2223-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="a2223-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="a2223-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="a2223-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="a2223-109">Przechwytywania pakietów obserwatora sieciowego umożliwia tworzenie sesji przechwytywania, aby śledzić ruch do i z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a2223-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="a2223-110">Filtry są dostępne dla sesji przechwytywania, aby upewnić się, że przechwytywać ruch, który ma.</span><span class="sxs-lookup"><span data-stu-id="a2223-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="a2223-111">Przechwytywania pakietów ułatwia diagnozowanie anomalii sieci rozbudowy i aktywne.</span><span class="sxs-lookup"><span data-stu-id="a2223-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="a2223-112">Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat wtargnięcia sieci, aby debugować komunikacja klient serwer i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="a2223-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="a2223-113">Dzięki możliwości zdalnie wywołać przechwytywania pakietów, ta funkcja ułatwia obciążeń uruchomionych przechwytywania pakietów, ręcznie i tylko na odpowiednią maszynę, która zapisuje cenny czas.</span><span class="sxs-lookup"><span data-stu-id="a2223-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="a2223-114">W tym artykule wykorzystano naszej nowej generacji interfejsu wiersza polecenia model wdrażania zarządzania zasobów, Azure CLI 2.0, który jest dostępny dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="a2223-114">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="a2223-115">Aby wykonać kroki opisane w tym artykule, należy [instalowanie interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="a2223-115">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="a2223-116">Ten artykuł przedstawia za pomocą zadań zarządzania różnych, które są obecnie dostępne dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="a2223-116">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="a2223-117">**Uruchom przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="a2223-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="a2223-118">**Zatrzymaj przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="a2223-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="a2223-119">**Usuń przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="a2223-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="a2223-120">**Pobierz przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="a2223-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="a2223-121">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="a2223-121">Before you begin</span></span>

<span data-ttu-id="a2223-122">W tym artykule przyjęto założenie, że masz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="a2223-122">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="a2223-123">Wystąpienia obserwatora sieciowego w regionie, w którym chcesz utworzyć przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="a2223-123">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="a2223-124">Maszyna wirtualna z rozszerzeniem przechwytywania pakietów włączone.</span><span class="sxs-lookup"><span data-stu-id="a2223-124">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2223-125">Przechwytywania pakietów wymaga agenta należy uruchomić na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a2223-125">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="a2223-126">Agent jest zainstalowany jako rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="a2223-126">The Agent is installed as an extension.</span></span> <span data-ttu-id="a2223-127">Aby uzyskać instrukcje dotyczące rozszerzenia maszyny Wirtualnej, odwiedź stronę [rozszerzenia maszyn wirtualnych i funkcji](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="a2223-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="a2223-128">Zainstaluj rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a2223-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="a2223-129">Krok 1</span><span class="sxs-lookup"><span data-stu-id="a2223-129">Step 1</span></span>

<span data-ttu-id="a2223-130">Uruchom `az vm extension set` polecenia cmdlet, aby zainstalować agenta przechwytywania pakietów na maszynie wirtualnej gościa.</span><span class="sxs-lookup"><span data-stu-id="a2223-130">Run the `az vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="a2223-131">W przypadku maszyn wirtualnych systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="a2223-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="a2223-132">Dla maszyn wirtualnych systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="a2223-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="a2223-133">Krok 2</span><span class="sxs-lookup"><span data-stu-id="a2223-133">Step 2</span></span>

<span data-ttu-id="a2223-134">Aby upewnić się, że agent jest zainstalowany, należy uruchomić `vm extension get` polecenia cmdlet i przekaż go nazwy maszyn wirtualnych i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="a2223-134">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="a2223-135">Sprawdź listę wynikowy, aby upewnić się, że agent jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="a2223-135">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="a2223-136">Poniższy przykład jest przykładem uruchamianie odpowiedzi`az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="a2223-136">The following sample is an example of the response from running `az vm extension show`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="a2223-137">Uruchom przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="a2223-137">Start a packet capture</span></span>

<span data-ttu-id="a2223-138">Po zakończeniu powyższych kroków agent przechwytywania pakietów jest zainstalowany na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a2223-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="a2223-139">Krok 1</span><span class="sxs-lookup"><span data-stu-id="a2223-139">Step 1</span></span>

<span data-ttu-id="a2223-140">Następnym krokiem jest w celu pobrania wystąpienia obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="a2223-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="a2223-141">Opcjonalna nazwa obserwatora sieciowego jest przekazywana do `az network watcher show` polecenia cmdlet w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="a2223-141">TThe name of the Network Watcher is passed to the `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="a2223-142">Krok 2</span><span class="sxs-lookup"><span data-stu-id="a2223-142">Step 2</span></span>

<span data-ttu-id="a2223-143">Pobierz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="a2223-143">Retrieve a storage account.</span></span> <span data-ttu-id="a2223-144">To konto magazynu jest używany do przechowywania pliku przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="a2223-144">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="a2223-145">Krok 3</span><span class="sxs-lookup"><span data-stu-id="a2223-145">Step 3</span></span>

<span data-ttu-id="a2223-146">Można używać filtrów w celu ograniczenia danych, który jest przechowywany przez przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="a2223-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="a2223-147">Poniższy przykład powoduje ustawienie przechwytywania pakietów z kilka filtrów.</span><span class="sxs-lookup"><span data-stu-id="a2223-147">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="a2223-148">Pierwsze trzy filtry Zbierz ruch wychodzący TCP tylko lokalny adres IP 10.0.0.3 do porty docelowe 20, 80 i 443.</span><span class="sxs-lookup"><span data-stu-id="a2223-148">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="a2223-149">Ten filtr zbiera tylko ruch UDP.</span><span class="sxs-lookup"><span data-stu-id="a2223-149">The last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="a2223-150">Poniższy przykład jest oczekiwane dane wyjściowe uruchamianie `az network watcher packet-capture create` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a2223-150">The following example is the expected output from running the `az network watcher packet-capture create` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="a2223-151">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="a2223-151">Get a packet capture</span></span>

<span data-ttu-id="a2223-152">Uruchomiona `az network watcher packet-capture show` polecenie cmdlet pobiera stan przechwytywania pakietów aktualnie uruchomione lub zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="a2223-152">Running the `az network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="a2223-153">Poniższy przykład jest wynikiem `az network watcher packet-capture show` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a2223-153">The following example is the output from the `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="a2223-154">Poniższy przykład jest po zakończeniu przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="a2223-154">The following example is after the capture is complete.</span></span> <span data-ttu-id="a2223-155">Wartość PacketCaptureStatus została zatrzymana z StopReason TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="a2223-155">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="a2223-156">Ta wartość pokazuje, że przechwytywania pakietów zakończyła się pomyślnie i jego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="a2223-156">This value shows that the packet capture was successful and ran its time.</span></span>

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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="a2223-157">Zatrzymaj przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="a2223-157">Stop a packet capture</span></span>

<span data-ttu-id="a2223-158">Uruchamiając `az network watcher packet-capture stop` polecenia cmdlet, jeśli sesja przechwytywania jest w toku jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="a2223-158">By running the `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="a2223-159">Polecenie cmdlet nie zwraca żadnej odpowiedzi podczas uruchomionego na aktualnie uruchomionych sesji przechwytywania lub istniejącej sesji, która już została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="a2223-159">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="a2223-160">Usuń przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="a2223-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="a2223-161">Usunięcie przechwytywania pakietów nie powoduje usunięcia plików na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="a2223-161">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="a2223-162">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="a2223-162">Download a packet capture</span></span>

<span data-ttu-id="a2223-163">Po zakończeniu sesji przechwytywania pakietów, plik przechwytywania można przekazać do magazynu obiektów blob lub do pliku lokalnego na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a2223-163">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="a2223-164">Lokalizacja magazynu przechwytywania pakietów jest definiowany podczas tworzenia sesji.</span><span class="sxs-lookup"><span data-stu-id="a2223-164">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="a2223-165">Wygodne narzędzie one dostęp do plików przechwytywania na koncie magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="a2223-165">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="a2223-166">Jeśli określono konto magazynu, pliki przechwytywania pakietów są zapisywane na koncie magazynu w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="a2223-166">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="a2223-167">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a2223-167">Next steps</span></span>

<span data-ttu-id="a2223-168">Dowiedz się, jak można zautomatyzować przechwytywania pakietów z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="a2223-168">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="a2223-169">Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a2223-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
