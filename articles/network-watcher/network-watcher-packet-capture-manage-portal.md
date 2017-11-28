---
title: "Zarządzanie przechwytywania pakietów z obserwatora sieciowego Azure - Azure portal | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśnia sposób zarządzania funkcja przechwytywania pakietów obserwatora sieciowego przy użyciu portalu Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 33390532cc4fc1129a4f960d589f41bc95e5a1ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-the-portal"></a><span data-ttu-id="c3d0c-103">Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure przy użyciu portalu</span><span class="sxs-lookup"><span data-stu-id="c3d0c-103">Manage packet captures with Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c3d0c-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c3d0c-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="c3d0c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3d0c-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="c3d0c-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="c3d0c-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="c3d0c-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="c3d0c-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="c3d0c-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="c3d0c-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="c3d0c-109">Przechwytywania pakietów obserwatora sieciowego umożliwia tworzenie sesji przechwytywania, aby śledzić ruch do i z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="c3d0c-110">Filtry są dostępne dla sesji przechwytywania, aby upewnić się, że przechwytywać ruch, który ma.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="c3d0c-111">Przechwytywania pakietów ułatwia diagnozowanie anomalii sieci rozbudowy i aktywne.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="c3d0c-112">Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat wtargnięcia sieci, aby debugować komunikacja klient serwer i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="c3d0c-113">Dzięki możliwości zdalnie wywołać przechwytywania pakietów, ta funkcja ułatwia obciążeń uruchomionych przechwytywania pakietów, ręcznie i tylko na odpowiednią maszynę, która zapisuje cenny czas.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="c3d0c-114">Ten artykuł przedstawia za pomocą zadań zarządzania różnych, które są obecnie dostępne dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="c3d0c-115">**Uruchom przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="c3d0c-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="c3d0c-116">**Zatrzymaj przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="c3d0c-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="c3d0c-117">**Usuń przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="c3d0c-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="c3d0c-118">**Pobierz przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="c3d0c-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="c3d0c-119">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c3d0c-119">Before you begin</span></span>

<span data-ttu-id="c3d0c-120">W tym artykule przyjęto założenie, że masz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="c3d0c-120">This article assumes that you have the following resources:</span></span>

- <span data-ttu-id="c3d0c-121">Wystąpienia obserwatora sieciowego w regionie, w którym chcesz utworzyć przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c3d0c-121">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="c3d0c-122">Maszyna wirtualna z rozszerzeniem przechwytywania pakietów włączone.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-122">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3d0c-123">Rozszerzenie maszyny wirtualnej wymaga przechwytywania pakietów `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="c3d0c-124">Instalowanie rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="c3d0c-124">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-the-portal"></a><span data-ttu-id="c3d0c-125">Rozszerzenie agenta przechwytywania pakietów, za pośrednictwem portalu</span><span class="sxs-lookup"><span data-stu-id="c3d0c-125">Packet Capture agent extension through the portal</span></span>

<span data-ttu-id="c3d0c-126">Aby zainstalować agenta pakietu Przechwytywanie maszyny Wirtualnej za pośrednictwem portalu, przejdź do maszyny wirtualnej, kliknij przycisk **rozszerzenia** > **Dodaj** i wyszukaj **sieci obserwatorów agenta dla systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="c3d0c-126">To install the packet capture VM agent through the portal, navigate to your virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![Widok agenta][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="c3d0c-128">Omówienie przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c3d0c-128">Packet Capture overview</span></span>

<span data-ttu-id="c3d0c-129">Przejdź do [portalu Azure](https://portal.azure.com) i kliknij przycisk **sieci** > **obserwatora sieciowego** > **przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="c3d0c-129">Navigate to the [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="c3d0c-130">Strony Przegląd przedstawia listę wszystkich pakietów przechwytuje, który istnieje, bez względu na stan.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-130">The overview page shows a list of all packet captures that exist no matter the state.</span></span>

> [!NOTE]
> <span data-ttu-id="c3d0c-131">Przechwytywania pakietów wymaga łączności z kontem magazynu za pośrednictwem portu 443.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-131">Packet capture requires connectivity to the storage account over port 443.</span></span>

![ekran Przegląd przechwytywania pakietów][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="c3d0c-133">Uruchom przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c3d0c-133">Start a packet capture</span></span>

<span data-ttu-id="c3d0c-134">Kliknij przycisk **Dodaj** utworzyć przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-134">Click **Add** to create a packet capture.</span></span>

<span data-ttu-id="c3d0c-135">Właściwości, które mogą być definiowane w przechwytywania pakietów są:</span><span class="sxs-lookup"><span data-stu-id="c3d0c-135">The properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="c3d0c-136">**Ustawienia głównego**</span><span class="sxs-lookup"><span data-stu-id="c3d0c-136">**Main settings**</span></span>

- <span data-ttu-id="c3d0c-137">**Subskrypcja** — ta wartość jest subskrypcji, która jest używana, wystąpienia obserwatora sieciowego jest niezbędna w każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-137">**Subscription** - This value is the subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="c3d0c-138">**Grupa zasobów** -grupa zasobów do docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-138">**Resource group** - The resource group of the virtual machine that is being targeted.</span></span>
- <span data-ttu-id="c3d0c-139">**Docelowa maszyna wirtualna** -maszynę wirtualną, która działa przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c3d0c-139">**Target virtual machine** - The virtual machine that is running the packet capture</span></span>
- <span data-ttu-id="c3d0c-140">**Nazwa przechwytywania pakietów** — ta wartość jest nazwą przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-140">**Packet capture name** - This value is the name of the packet capture.</span></span>

<span data-ttu-id="c3d0c-141">**Przechwytywanie konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="c3d0c-141">**Capture configuration**</span></span>

- <span data-ttu-id="c3d0c-142">**Konto magazynu** — Określa, czy przechwytywania pakietów jest zapisywane na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="c3d0c-143">**Plik** — Określa, czy przechwytywania pakietów jest zapisywane lokalnie na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-143">**File** - Determines if a packet capture is saved locally on the virtual machine.</span></span>
- <span data-ttu-id="c3d0c-144">**Konta magazynu** — wybrać konto magazynu, aby zapisać pakiet w.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-144">**Storage Accounts** - The selected storage account to save the packet capture in.</span></span> <span data-ttu-id="c3d0c-145">Domyślna lokalizacja to identyfikator name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription konta https://{storage} /resourcegroups/ {Nazwa maszyny name}/providers/microsoft.compute/virtualmachines/{virtual grupy zasobów} / {YY} / {MM} / {DD} / {HH} packetcapture__{MM}_CAP _ {XXX} {SS}.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="c3d0c-146">(Włączone, tylko jeśli **magazynu** jest zaznaczone)</span><span class="sxs-lookup"><span data-stu-id="c3d0c-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="c3d0c-147">**Ścieżka do pliku lokalnego** — ścieżka lokalna na maszynie wirtualnej, aby zapisać przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-147">**Local file path** - The local path on a virtual machine to save the packet capture.</span></span> <span data-ttu-id="c3d0c-148">(Włączone, tylko jeśli **pliku** jest zaznaczona).</span><span class="sxs-lookup"><span data-stu-id="c3d0c-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="c3d0c-149">Należy podać prawidłową ścieżkę</span><span class="sxs-lookup"><span data-stu-id="c3d0c-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="c3d0c-150">**Maksymalna liczba bajtów na pakiet** — liczba bajtów z każdego pakietu, które są przechwytywane, wszystkie bajty są przechwytywane, jeśli pole pozostanie puste.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-150">**Maximum bytes per packet** - The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="c3d0c-151">**Maksymalna liczba bajtów na sesji** — jest to całkowita liczba bajtów, które są przechwytywane, gdy wartość osiągnięciu zatrzymuje przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-151">**Maximum bytes per session** - Total number of bytes that are captured, once the value is reached the packet capture stops.</span></span>
- <span data-ttu-id="c3d0c-152">**Limit czasu (w sekundach)** -ustawia limit czasu dla przechwytywania pakietów zatrzymać.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-152">**Time limit (seconds)** - Sets a time limit for the packet capture to stop.</span></span> <span data-ttu-id="c3d0c-153">Domyślna to 18000 sekund.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="c3d0c-154">Konta Premium magazynu nie są obecnie obsługiwane dla przechwytuje przechowywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="c3d0c-155">**Filtrowanie (opcjonalnie)**</span><span class="sxs-lookup"><span data-stu-id="c3d0c-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="c3d0c-156">**Protokół** — protokół, aby filtrować pod kątem przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-156">**Protocol** - The protocol to filter for the packet capture.</span></span> <span data-ttu-id="c3d0c-157">Dostępne wartości to TCP, UDP i dowolne.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-157">The available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="c3d0c-158">**Lokalny adres IP** — ta wartość filtry przechwytywania pakietów do pakietów Jeśli lokalny adres IP odpowiada to wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-158">**Local IP address** - This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>
- <span data-ttu-id="c3d0c-159">**Port lokalny** — ta wartość filtry przechwytywania pakietów do pakietów gdzie portu lokalnego zgodna z tą wartością filtru.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-159">**Local port** - This value filters the packet capture to packets where the local port matches this filter value.</span></span>
- <span data-ttu-id="c3d0c-160">**Zdalny adres IP** — ta wartość filtry przechwytywania pakietów do pakietów Jeśli zdalny adres IP odpowiada to wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-160">**Remote IP address** - This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>
- <span data-ttu-id="c3d0c-161">**Port zdalny** — ta wartość filtry przechwytywania pakietów do pakietów Jeśli port zdalny odpowiada to wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-161">**Remote port** - This value filters the packet capture to packets where the remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="c3d0c-162">Wartości adresów IP i port może być pojedynczą wartością, zakres wartości lub zestawu.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="c3d0c-163">(to znaczy port 80 – 1024 dla) Można określić dowolną liczbę filtry.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="c3d0c-164">Po wartości są wypełnione, kliknij przycisk **OK** utworzyć przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-164">Once the values are filled out, click **OK** to create the packet capture.</span></span>

![Utwórz przechwytywania pakietów][2]

<span data-ttu-id="c3d0c-166">Po upływie terminu na przechwytywania pakietów przechwytywania pakietów spowoduje zatrzymanie i mogą być przeglądane.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-166">After the time limit set on the packet capture has expired, the packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="c3d0c-167">Można też ręcznie zatrzymać sesji przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-167">You can also manually stop the packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="c3d0c-168">Usuń przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c3d0c-168">Delete a packet capture</span></span>

<span data-ttu-id="c3d0c-169">W widoku przechwytywania pakietów, kliknij przycisk **menu kontekstowe** (...) lub kliknij prawym przyciskiem myszy i kliknij przycisk **usunąć** przestanie przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c3d0c-169">In the packet capture view, click the **context menu** (...) or right click, and click **delete** to stop the packet capture</span></span>

![Usuń przechwytywania pakietów][3]

> [!NOTE]
> <span data-ttu-id="c3d0c-171">Usunięcie przechwytywania pakietów nie powoduje usunięcia plików na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-171">Deleting a packet capture does not delete the file in the storage account.</span></span>

<span data-ttu-id="c3d0c-172">Zostanie wyświetlona prośba o potwierdzenie usunięcia przechwytywania pakietów, kliknij przycisk **tak**</span><span class="sxs-lookup"><span data-stu-id="c3d0c-172">You are asked to confirm you want to delete the packet capture, click **Yes**</span></span>

![Potwierdzenie][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="c3d0c-174">Zatrzymaj przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c3d0c-174">Stop a packet capture</span></span>

<span data-ttu-id="c3d0c-175">W widoku przechwytywania pakietów, kliknij przycisk **menu kontekstowe** (...) lub kliknij prawym przyciskiem myszy i kliknij przycisk **zatrzymać** przestanie przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c3d0c-175">In the packet capture view, click the **context menu** (...) or right click, and click **Stop** to stop the packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="c3d0c-176">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="c3d0c-176">Download a packet capture</span></span>

<span data-ttu-id="c3d0c-177">Po zakończeniu sesji przechwytywania pakietów, plik przechwytywania jest przekazywany do magazynu obiektów blob lub do pliku lokalnego na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-177">Once your packet capture session has completed, the capture file is uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="c3d0c-178">Lokalizacja magazynu przechwytywania pakietów jest definiowany podczas tworzenia sesji.</span><span class="sxs-lookup"><span data-stu-id="c3d0c-178">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="c3d0c-179">Wygodne narzędzie one dostęp do plików przechwytywania na koncie magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="c3d0c-179">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="c3d0c-180">Jeśli określono konto magazynu, pliki przechwytywania pakietów są zapisywane na koncie magazynu w następującej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="c3d0c-180">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="c3d0c-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3d0c-181">Next steps</span></span>

<span data-ttu-id="c3d0c-182">Dowiedz się, jak można zautomatyzować przechwytywania pakietów z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="c3d0c-182">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="c3d0c-183">Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c3d0c-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













