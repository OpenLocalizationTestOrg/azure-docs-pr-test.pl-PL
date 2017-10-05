---
title: "Zarządzanie przechwytywania pakietów z obserwatora sieciowego Azure - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśnia sposób zarządzania funkcja przechwytywania pakietów obserwatora sieciowego przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0"
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
ms.openlocfilehash: 91588910334859c1ea77186674d5bfb31b311b36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="73838-103">Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="73838-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="73838-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="73838-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="73838-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="73838-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="73838-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="73838-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="73838-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="73838-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="73838-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="73838-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="73838-109">Przechwytywania pakietów obserwatora sieciowego umożliwia tworzenie sesji przechwytywania, aby śledzić ruch do i z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="73838-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="73838-110">Filtry są dostępne dla sesji przechwytywania, aby upewnić się, że przechwytywać ruch, który ma.</span><span class="sxs-lookup"><span data-stu-id="73838-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="73838-111">Przechwytywania pakietów ułatwia diagnozowanie anomalii sieci rozbudowy i aktywne.</span><span class="sxs-lookup"><span data-stu-id="73838-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="73838-112">Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat wtargnięcia sieci, aby debugować komunikacja klient serwer i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="73838-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="73838-113">Dzięki możliwości zdalnie wywołać przechwytywania pakietów, ta funkcja ułatwia obciążeń uruchomionych przechwytywania pakietów, ręcznie i tylko na odpowiednią maszynę, która zapisuje cenny czas.</span><span class="sxs-lookup"><span data-stu-id="73838-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="73838-114">W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="73838-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="73838-115">Ten artykuł przedstawia za pomocą zadań zarządzania różnych, które są obecnie dostępne dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="73838-115">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="73838-116">**Uruchom przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="73838-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="73838-117">**Zatrzymaj przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="73838-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="73838-118">**Usuń przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="73838-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="73838-119">**Pobierz przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="73838-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="73838-120">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="73838-120">Before you begin</span></span>

<span data-ttu-id="73838-121">W tym artykule przyjęto założenie, że masz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="73838-121">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="73838-122">Wystąpienia obserwatora sieciowego w regionie, w którym chcesz utworzyć przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="73838-122">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="73838-123">Maszyna wirtualna z rozszerzeniem przechwytywania pakietów włączone.</span><span class="sxs-lookup"><span data-stu-id="73838-123">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73838-124">Przechwytywania pakietów wymaga agenta należy uruchomić na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="73838-124">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="73838-125">Agent jest zainstalowany jako rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="73838-125">The Agent is installed as an extension.</span></span> <span data-ttu-id="73838-126">Aby uzyskać instrukcje dotyczące rozszerzenia maszyny Wirtualnej, odwiedź stronę [rozszerzenia maszyn wirtualnych i funkcji](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="73838-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="73838-127">Zainstaluj rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="73838-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="73838-128">Krok 1</span><span class="sxs-lookup"><span data-stu-id="73838-128">Step 1</span></span>

<span data-ttu-id="73838-129">Uruchom `azure vm extension set` polecenia cmdlet, aby zainstalować agenta przechwytywania pakietów na maszynie wirtualnej gościa.</span><span class="sxs-lookup"><span data-stu-id="73838-129">Run the `azure vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="73838-130">W przypadku maszyn wirtualnych systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="73838-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="73838-131">Dla maszyn wirtualnych systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="73838-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="73838-132">Krok 2</span><span class="sxs-lookup"><span data-stu-id="73838-132">Step 2</span></span>

<span data-ttu-id="73838-133">Aby upewnić się, że agent jest zainstalowany, należy uruchomić `vm extension get` polecenia cmdlet i przekaż go nazwy maszyn wirtualnych i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="73838-133">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="73838-134">Sprawdź listę wynikowy, aby upewnić się, że agent jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="73838-134">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="73838-135">Poniższy przykład jest przykładem uruchamianie odpowiedzi`azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="73838-135">The following sample is an example of the response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up the VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="73838-136">Uruchom przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="73838-136">Start a packet capture</span></span>

<span data-ttu-id="73838-137">Po zakończeniu powyższych kroków agent przechwytywania pakietów jest zainstalowany na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="73838-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="73838-138">Krok 1</span><span class="sxs-lookup"><span data-stu-id="73838-138">Step 1</span></span>

<span data-ttu-id="73838-139">Następnym krokiem jest w celu pobrania wystąpienia obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="73838-139">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="73838-140">Ta zmienna jest przekazywana do `network watcher show` polecenia cmdlet w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="73838-140">This variable is passed to the `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="73838-141">Krok 2</span><span class="sxs-lookup"><span data-stu-id="73838-141">Step 2</span></span>

<span data-ttu-id="73838-142">Pobierz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="73838-142">Retrieve a storage account.</span></span> <span data-ttu-id="73838-143">To konto magazynu jest używany do przechowywania pliku przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="73838-143">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="73838-144">Krok 3</span><span class="sxs-lookup"><span data-stu-id="73838-144">Step 3</span></span>

<span data-ttu-id="73838-145">Można używać filtrów w celu ograniczenia danych, który jest przechowywany przez przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="73838-145">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="73838-146">Poniższy przykład powoduje ustawienie przechwytywania pakietów z kilka filtrów.</span><span class="sxs-lookup"><span data-stu-id="73838-146">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="73838-147">Pierwsze trzy filtry Zbierz ruch wychodzący TCP tylko lokalny adres IP 10.0.0.3 do porty docelowe 20, 80 i 443.</span><span class="sxs-lookup"><span data-stu-id="73838-147">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="73838-148">Ten filtr zbiera tylko ruch UDP.</span><span class="sxs-lookup"><span data-stu-id="73838-148">The last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="73838-149">Można zdefiniować wiele filtrów dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="73838-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="73838-150">Jeśli używasz struktury złożonych filtrów, lepiej jest używać filtrów w formacie json, aby uniknąć błędów składni.</span><span class="sxs-lookup"><span data-stu-id="73838-150">If you are using a complex filter structure, it is better to use filters as a json file to avoid syntax errors.</span></span> <span data-ttu-id="73838-151">Na przykład użyć flagi "-r" (zamiast "-f"), a następnie przekaż lokalizację pliku json, który zawiera następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="73838-151">For example, use the flag "-r" (instead of "-f") and pass the location of a json file containing the following filters:</span></span>

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


<span data-ttu-id="73838-152">Poniższy przykład jest oczekiwane dane wyjściowe uruchamianie `network watcher packet-capture create` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="73838-152">The following example is the expected output from running the `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="73838-153">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="73838-153">Get a packet capture</span></span>

<span data-ttu-id="73838-154">Uruchomiona `network watcher packet-capture show` polecenie cmdlet pobiera stan przechwytywania pakietów aktualnie uruchomione lub zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="73838-154">Running the `network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="73838-155">Poniższy przykład jest wynikiem `network watcher packet-capture show` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="73838-155">The following example is the output from the `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="73838-156">Poniższy przykład jest po zakończeniu przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="73838-156">The following example is after the capture is complete.</span></span> <span data-ttu-id="73838-157">Wartość PacketCaptureStatus została zatrzymana z StopReason TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="73838-157">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="73838-158">Ta wartość pokazuje, że przechwytywania pakietów zakończyła się pomyślnie i jego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="73838-158">This value shows that the packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="73838-159">Zatrzymaj przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="73838-159">Stop a packet capture</span></span>

<span data-ttu-id="73838-160">Uruchamiając `network watcher packet-capture stop` polecenia cmdlet, jeśli sesja przechwytywania jest w toku jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="73838-160">By running the `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="73838-161">Polecenie cmdlet nie zwraca żadnej odpowiedzi podczas uruchomionego na aktualnie uruchomionych sesji przechwytywania lub istniejącej sesji, która już została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="73838-161">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="73838-162">Usuń przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="73838-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="73838-163">Usunięcie przechwytywania pakietów nie powoduje usunięcia plików na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="73838-163">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="73838-164">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="73838-164">Download a packet capture</span></span>

<span data-ttu-id="73838-165">Po zakończeniu sesji przechwytywania pakietów, plik przechwytywania można przekazać do magazynu obiektów blob lub do pliku lokalnego na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="73838-165">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="73838-166">Lokalizacja magazynu przechwytywania pakietów jest definiowany podczas tworzenia sesji.</span><span class="sxs-lookup"><span data-stu-id="73838-166">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="73838-167">Wygodne narzędzie one dostęp do plików przechwytywania na koncie magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="73838-167">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="73838-168">Jeśli określono konto magazynu, pliki przechwytywania pakietów są zapisywane na koncie magazynu w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="73838-168">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="73838-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="73838-169">Next steps</span></span>

<span data-ttu-id="73838-170">Dowiedz się, jak można zautomatyzować przechwytywania pakietów z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="73838-170">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="73838-171">Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="73838-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
