---
title: "Przechwytywanie pakietów aaaManage z obserwatora sieciowego Azure - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toomanage hello funkcja przechwytywania pakietów obserwatora sieciowego przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0"
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
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="aa443-103">Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="aa443-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="aa443-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="aa443-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="aa443-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa443-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="aa443-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="aa443-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="aa443-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="aa443-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="aa443-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="aa443-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="aa443-109">Przechwytywania pakietów obserwatora sieciowego umożliwia toocreate przechwytywania sesji tootrack ruch tooand z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="aa443-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="aa443-110">Filtry są przewidziane tooensure sesji przechwytywania hello przechwytywać tylko hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="aa443-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="aa443-111">Przechwytywania pakietów pomaga anomalii sieci toodiagnose rozbudowy i aktywne.</span><span class="sxs-lookup"><span data-stu-id="aa443-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="aa443-112">Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat sieci wtargnięcia toodebug klient serwer, komunikację i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="aa443-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="aa443-113">Jest przechwytywania pakietów wyzwalacza stanie tooremotely, ta funkcja ułatwia hello obciążeń uruchomionych przechwytywania pakietów ręcznego, jak i na powitania żądanego komputera, który zapisuje cenny czas.</span><span class="sxs-lookup"><span data-stu-id="aa443-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="aa443-114">W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="aa443-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="aa443-115">Ten artykuł przedstawia hello zarządzania różnych zadań, które są obecnie dostępne dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="aa443-115">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="aa443-116">**Uruchom przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="aa443-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="aa443-117">**Zatrzymaj przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="aa443-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="aa443-118">**Usuń przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="aa443-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="aa443-119">**Pobierz przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="aa443-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="aa443-120">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="aa443-120">Before you begin</span></span>

<span data-ttu-id="aa443-121">W tym artykule przyjęto założenie, że masz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="aa443-121">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="aa443-122">Wystąpienia obserwatora sieciowego w regionie hello ma toocreate przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="aa443-122">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="aa443-123">Maszyna wirtualna o pakietów hello przechwytywania rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="aa443-123">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa443-124">Przechwytywania pakietów wymaga toobe agent uruchomiony na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="aa443-124">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="aa443-125">Witaj Agent jest instalowany jako rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="aa443-125">hello Agent is installed as an extension.</span></span> <span data-ttu-id="aa443-126">Aby uzyskać instrukcje dotyczące rozszerzenia maszyny Wirtualnej, odwiedź stronę [rozszerzenia maszyn wirtualnych i funkcji](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="aa443-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="aa443-127">Zainstaluj rozszerzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="aa443-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="aa443-128">Krok 1</span><span class="sxs-lookup"><span data-stu-id="aa443-128">Step 1</span></span>

<span data-ttu-id="aa443-129">Uruchom hello `azure vm extension set` polecenia cmdlet tooinstall hello pakietów przechwytywania agenta na maszynie wirtualnej typu Gość hello.</span><span class="sxs-lookup"><span data-stu-id="aa443-129">Run hello `azure vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="aa443-130">W przypadku maszyn wirtualnych systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="aa443-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="aa443-131">Dla maszyn wirtualnych systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="aa443-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="aa443-132">Krok 2</span><span class="sxs-lookup"><span data-stu-id="aa443-132">Step 2</span></span>

<span data-ttu-id="aa443-133">tooensure, który hello agent jest zainstalowany, uruchom hello `vm extension get` polecenia cmdlet i przekaż go hello grupy zasobów i nazwy maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="aa443-133">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="aa443-134">Sprawdź, czy hello wynikowej listy tooensure hello agent jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="aa443-134">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="aa443-135">następujące przykładowe Hello jest przykładem odpowiedź hello uruchamianie`azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="aa443-135">hello following sample is an example of hello response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="aa443-136">Uruchom przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="aa443-136">Start a packet capture</span></span>

<span data-ttu-id="aa443-137">Po hello powyższych kroków są spełnione, agent przechwytywania pakietów hello jest zainstalowany na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="aa443-137">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="aa443-138">Krok 1</span><span class="sxs-lookup"><span data-stu-id="aa443-138">Step 1</span></span>

<span data-ttu-id="aa443-139">Witaj następnym krokiem jest tooretrieve hello obserwatora sieciowego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="aa443-139">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="aa443-140">Ta zmienna jest przekazywana toohello `network watcher show` polecenia cmdlet w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="aa443-140">This variable is passed toohello `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="aa443-141">Krok 2</span><span class="sxs-lookup"><span data-stu-id="aa443-141">Step 2</span></span>

<span data-ttu-id="aa443-142">Pobierz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="aa443-142">Retrieve a storage account.</span></span> <span data-ttu-id="aa443-143">To konto magazynu jest plik przechwytywania pakietów hello toostore używane.</span><span class="sxs-lookup"><span data-stu-id="aa443-143">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="aa443-144">Krok 3</span><span class="sxs-lookup"><span data-stu-id="aa443-144">Step 3</span></span>

<span data-ttu-id="aa443-145">Filtry mogą być używane toolimit hello dane przechowywane przez przechwytywania pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="aa443-145">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="aa443-146">Witaj poniższy przykład konfiguruje przechwytywania pakietów z kilka filtrów.</span><span class="sxs-lookup"><span data-stu-id="aa443-146">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="aa443-147">Witaj pierwsze trzy filtry zbierania ruch wychodzący TCP tylko z lokalny adres IP 10.0.0.3 porty toodestination 20, 80 i 443.</span><span class="sxs-lookup"><span data-stu-id="aa443-147">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="aa443-148">Filtr Hello zbiera tylko ruch UDP.</span><span class="sxs-lookup"><span data-stu-id="aa443-148">hello last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="aa443-149">Można zdefiniować wiele filtrów dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="aa443-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="aa443-150">Jeśli używasz struktury złożonych filtru jest lepsze filtry toouse jako błędy składniowe tooavoid pliku json.</span><span class="sxs-lookup"><span data-stu-id="aa443-150">If you are using a complex filter structure, it is better toouse filters as a json file tooavoid syntax errors.</span></span> <span data-ttu-id="aa443-151">Na przykład użyć hello flagi "-r" (zamiast "-f") i przekaż hello lokalizację pliku json zawierający hello następujące filtry:</span><span class="sxs-lookup"><span data-stu-id="aa443-151">For example, use hello flag "-r" (instead of "-f") and pass hello location of a json file containing hello following filters:</span></span>

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


<span data-ttu-id="aa443-152">Witaj poniższym przykładzie jest hello oczekiwane dane wyjściowe systemem hello `network watcher packet-capture create` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aa443-152">hello following example is hello expected output from running hello `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="aa443-153">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="aa443-153">Get a packet capture</span></span>

<span data-ttu-id="aa443-154">Uruchomiona hello `network watcher packet-capture show` polecenie cmdlet pobiera stan hello przechwytywania pakietów aktualnie uruchomione lub zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="aa443-154">Running hello `network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="aa443-155">Witaj poniższym przykładzie jest hello dane wyjściowe hello `network watcher packet-capture show` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aa443-155">hello following example is hello output from hello `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="aa443-156">Witaj poniższym przykładzie jest po zakończeniu hello przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="aa443-156">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="aa443-157">z StopReason TimeExceeded Hello wartość PacketCaptureStatus jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="aa443-157">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="aa443-158">Ta wartość pokazuje, że przechwytywania pakietów hello zakończyła się pomyślnie i jego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="aa443-158">This value shows that hello packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="aa443-159">Zatrzymaj przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="aa443-159">Stop a packet capture</span></span>

<span data-ttu-id="aa443-160">Uruchamiając hello `network watcher packet-capture stop` polecenia cmdlet, jeśli sesja przechwytywania jest w toku jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="aa443-160">By running hello `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="aa443-161">Witaj polecenie cmdlet nie zwraca żadnej odpowiedzi podczas uruchomionego na aktualnie uruchomionych sesji przechwytywania lub istniejącej sesji, która już została zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="aa443-161">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="aa443-162">Usuń przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="aa443-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="aa443-163">Usunięcie przechwytywania pakietów nie powoduje usunięcia pliku hello hello koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="aa443-163">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="aa443-164">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="aa443-164">Download a packet capture</span></span>

<span data-ttu-id="aa443-165">Po zakończeniu sesji przechwytywania pakietów hello pliku przechwytywania może być przekazane tooblob tooa lub magazynu lokalnego pliku na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="aa443-165">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="aa443-166">Lokalizacja przechowywania Hello przechwytywania pakietów hello jest definiowany podczas tworzenia hello sesji.</span><span class="sxs-lookup"><span data-stu-id="aa443-166">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="aa443-167">Tooaccess wygodne narzędzie te Przechwytywanie plików, tooa zapisane konto magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="aa443-167">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="aa443-168">Jeśli określono konto magazynu, zapisywane są pliki przechwytywania pakietów tooa konta magazynu w następującej lokalizacji hello:</span><span class="sxs-lookup"><span data-stu-id="aa443-168">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="aa443-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aa443-169">Next steps</span></span>

<span data-ttu-id="aa443-170">Dowiedz się, jak przechwytywanie pakietów tooautomate z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="aa443-170">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="aa443-171">Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="aa443-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
