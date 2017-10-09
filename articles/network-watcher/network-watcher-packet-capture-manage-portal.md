---
title: "Przechwytywanie pakietów aaaManage z obserwatora sieciowego Azure - Azure portal | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toomanage hello funkcja przechwytywania pakietów obserwatora sieciowego przy użyciu portalu Azure"
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
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="d51fb-103">Zarządzanie przechwytywania pakietów za pomocą Monitora sieci Azure przy użyciu portalu hello</span><span class="sxs-lookup"><span data-stu-id="d51fb-103">Manage packet captures with Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d51fb-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d51fb-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="d51fb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d51fb-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="d51fb-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="d51fb-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="d51fb-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="d51fb-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="d51fb-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="d51fb-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="d51fb-109">Przechwytywania pakietów obserwatora sieciowego umożliwia toocreate przechwytywania sesji tootrack ruch tooand z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d51fb-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="d51fb-110">Filtry są przewidziane tooensure sesji przechwytywania hello przechwytywać tylko hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="d51fb-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="d51fb-111">Przechwytywania pakietów pomaga anomalii sieci toodiagnose rozbudowy i aktywne.</span><span class="sxs-lookup"><span data-stu-id="d51fb-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="d51fb-112">Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat sieci wtargnięcia toodebug klient serwer, komunikację i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="d51fb-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="d51fb-113">Jest przechwytywania pakietów wyzwalacza stanie tooremotely, ta funkcja ułatwia hello obciążeń uruchomionych przechwytywania pakietów ręcznego, jak i na powitania żądanego komputera, który zapisuje cenny czas.</span><span class="sxs-lookup"><span data-stu-id="d51fb-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="d51fb-114">Ten artykuł przedstawia hello zarządzania różnych zadań, które są obecnie dostępne dla przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="d51fb-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="d51fb-115">**Uruchom przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="d51fb-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="d51fb-116">**Zatrzymaj przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="d51fb-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="d51fb-117">**Usuń przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="d51fb-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="d51fb-118">**Pobierz przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="d51fb-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="d51fb-119">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="d51fb-119">Before you begin</span></span>

<span data-ttu-id="d51fb-120">W tym artykule przyjęto założenie, że hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="d51fb-120">This article assumes that you have hello following resources:</span></span>

- <span data-ttu-id="d51fb-121">Wystąpienia obserwatora sieciowego w regionie hello ma toocreate przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="d51fb-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="d51fb-122">Maszyna wirtualna o pakietów hello przechwytywania rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="d51fb-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d51fb-123">Rozszerzenie maszyny wirtualnej wymaga przechwytywania pakietów `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="d51fb-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="d51fb-124">Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="d51fb-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-hello-portal"></a><span data-ttu-id="d51fb-125">Rozszerzenie agenta przechwytywania pakietów, za pośrednictwem portalu hello</span><span class="sxs-lookup"><span data-stu-id="d51fb-125">Packet Capture agent extension through hello portal</span></span>

<span data-ttu-id="d51fb-126">przechwytywania pakietów hello tooinstall agenta maszyny Wirtualnej za pośrednictwem portalu hello Przejdź tooyour maszyny wirtualnej, kliknij pozycję **rozszerzenia** > **Dodaj** i wyszukaj **Agent obserwatorów sieci dla Systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="d51fb-126">tooinstall hello packet capture VM agent through hello portal, navigate tooyour virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![Widok agenta][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="d51fb-128">Omówienie przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="d51fb-128">Packet Capture overview</span></span>

<span data-ttu-id="d51fb-129">Przejdź toohello [portalu Azure](https://portal.azure.com) i kliknij przycisk **sieci** > **obserwatora sieciowego** > **przechwytywania pakietów**</span><span class="sxs-lookup"><span data-stu-id="d51fb-129">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="d51fb-130">Strona omówienia Hello przedstawia listę wszystkich pakietów przechwytuje, który istnieje, bez względu na stan hello.</span><span class="sxs-lookup"><span data-stu-id="d51fb-130">hello overview page shows a list of all packet captures that exist no matter hello state.</span></span>

> [!NOTE]
> <span data-ttu-id="d51fb-131">Przechwytywania pakietów wymaga konta magazynu toohello łączności za pośrednictwem portu 443.</span><span class="sxs-lookup"><span data-stu-id="d51fb-131">Packet capture requires connectivity toohello storage account over port 443.</span></span>

![ekran Przegląd przechwytywania pakietów][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="d51fb-133">Uruchom przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="d51fb-133">Start a packet capture</span></span>

<span data-ttu-id="d51fb-134">Kliknij przycisk **Dodaj** toocreate przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="d51fb-134">Click **Add** toocreate a packet capture.</span></span>

<span data-ttu-id="d51fb-135">właściwości Hello, które mogą być definiowane w przechwytywania pakietów są:</span><span class="sxs-lookup"><span data-stu-id="d51fb-135">hello properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="d51fb-136">**Ustawienia głównego**</span><span class="sxs-lookup"><span data-stu-id="d51fb-136">**Main settings**</span></span>

- <span data-ttu-id="d51fb-137">**Subskrypcja** — ta wartość jest hello subskrypcji, która jest używana, wystąpienia obserwatora sieciowego jest niezbędna w każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d51fb-137">**Subscription** - This value is hello subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="d51fb-138">**Grupa zasobów** -grupa zasobów hello hello maszyny wirtualnej, która docelowej.</span><span class="sxs-lookup"><span data-stu-id="d51fb-138">**Resource group** - hello resource group of hello virtual machine that is being targeted.</span></span>
- <span data-ttu-id="d51fb-139">**Docelowa maszyna wirtualna** -hello maszyny wirtualnej, która działa przechwytywania pakietów hello</span><span class="sxs-lookup"><span data-stu-id="d51fb-139">**Target virtual machine** - hello virtual machine that is running hello packet capture</span></span>
- <span data-ttu-id="d51fb-140">**Nazwa przechwytywania pakietów** — ta wartość jest nazwą hello przechwytywania pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="d51fb-140">**Packet capture name** - This value is hello name of hello packet capture.</span></span>

<span data-ttu-id="d51fb-141">**Przechwytywanie konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="d51fb-141">**Capture configuration**</span></span>

- <span data-ttu-id="d51fb-142">**Konto magazynu** — Określa, czy przechwytywania pakietów jest zapisywane na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="d51fb-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="d51fb-143">**Plik** — Określa, czy przechwytywania pakietów jest zapisywane lokalnie na maszynie wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="d51fb-143">**File** - Determines if a packet capture is saved locally on hello virtual machine.</span></span>
- <span data-ttu-id="d51fb-144">**Konta magazynu** -hello wybrane przechwytywania pakietów hello toosave konta magazynu w.</span><span class="sxs-lookup"><span data-stu-id="d51fb-144">**Storage Accounts** - hello selected storage account toosave hello packet capture in.</span></span> <span data-ttu-id="d51fb-145">Domyślna lokalizacja to identyfikator name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription konta https://{storage} /resourcegroups/ {Nazwa maszyny name}/providers/microsoft.compute/virtualmachines/{virtual grupy zasobów} / {YY} / {MM} / {DD} / {HH} packetcapture__{MM}_CAP _ {XXX} {SS}.</span><span class="sxs-lookup"><span data-stu-id="d51fb-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="d51fb-146">(Włączone, tylko jeśli **magazynu** jest zaznaczone)</span><span class="sxs-lookup"><span data-stu-id="d51fb-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="d51fb-147">**Ścieżka do pliku lokalnego** — ścieżka lokalna hello na przechwytywania pakietów hello toosave maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d51fb-147">**Local file path** - hello local path on a virtual machine toosave hello packet capture.</span></span> <span data-ttu-id="d51fb-148">(Włączone, tylko jeśli **pliku** jest zaznaczona).</span><span class="sxs-lookup"><span data-stu-id="d51fb-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="d51fb-149">Należy podać prawidłową ścieżkę</span><span class="sxs-lookup"><span data-stu-id="d51fb-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="d51fb-150">**Maksymalna liczba bajtów na pakiet** — Witaj liczbę bajtów z każdego pakietu, które są przechwytywane, wszystkie bajty są przechwytywane, jeśli pole pozostanie puste.</span><span class="sxs-lookup"><span data-stu-id="d51fb-150">**Maximum bytes per packet** - hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="d51fb-151">**Maksymalna liczba bajtów na sesji** — jest to całkowita liczba bajtów, które są przechwytywane, gdy wartość hello osiągnięciu zatrzymuje przechwytywania pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="d51fb-151">**Maximum bytes per session** - Total number of bytes that are captured, once hello value is reached hello packet capture stops.</span></span>
- <span data-ttu-id="d51fb-152">**Limit czasu (w sekundach)** -ustawia limit czasu dla toostop przechwytywania pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="d51fb-152">**Time limit (seconds)** - Sets a time limit for hello packet capture toostop.</span></span> <span data-ttu-id="d51fb-153">Domyślna to 18000 sekund.</span><span class="sxs-lookup"><span data-stu-id="d51fb-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="d51fb-154">Konta Premium magazynu nie są obecnie obsługiwane dla przechwytuje przechowywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="d51fb-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="d51fb-155">**Filtrowanie (opcjonalnie)**</span><span class="sxs-lookup"><span data-stu-id="d51fb-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="d51fb-156">**Protokół** — Witaj toofilter protokołu dla przechwytywania pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="d51fb-156">**Protocol** - hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="d51fb-157">Witaj dostępne wartości to TCP, UDP i dowolne.</span><span class="sxs-lookup"><span data-stu-id="d51fb-157">hello available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="d51fb-158">**Lokalny adres IP** — ta wartość filtry toopackets przechwytywania pakietów hello Jeśli hello lokalny adres IP odpowiada to wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="d51fb-158">**Local IP address** - This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>
- <span data-ttu-id="d51fb-159">**Port lokalny** — ta wartość filtry toopackets przechwytywania pakietów hello gdzie portów lokalnych hello zgodna z tą wartością filtru.</span><span class="sxs-lookup"><span data-stu-id="d51fb-159">**Local port** - This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>
- <span data-ttu-id="d51fb-160">**Zdalny adres IP** — ta wartość filtry toopackets przechwytywania pakietów hello Jeśli hello zdalny adres IP odpowiada to wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="d51fb-160">**Remote IP address** - This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>
- <span data-ttu-id="d51fb-161">**Port zdalny** — ta wartość filtry toopackets przechwytywania pakietów hello Jeśli port zdalny hello odpowiada tej wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="d51fb-161">**Remote port** - This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="d51fb-162">Wartości adresów IP i port może być pojedynczą wartością, zakres wartości lub zestawu.</span><span class="sxs-lookup"><span data-stu-id="d51fb-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="d51fb-163">(to znaczy port 80 – 1024 dla) Można określić dowolną liczbę filtry.</span><span class="sxs-lookup"><span data-stu-id="d51fb-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="d51fb-164">Po wartości hello są wypełnione, kliknij przycisk **OK** przechwytywania pakietów hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d51fb-164">Once hello values are filled out, click **OK** toocreate hello packet capture.</span></span>

![Utwórz przechwytywania pakietów][2]

<span data-ttu-id="d51fb-166">Po ustawieniu limitu czasu hello na przechwytywania pakietów hello wygasła, przechwytywania pakietów hello jest zatrzymywane, można wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="d51fb-166">After hello time limit set on hello packet capture has expired, hello packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="d51fb-167">Można też ręcznie zatrzymać sesji przechwytywania pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="d51fb-167">You can also manually stop hello packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="d51fb-168">Usuń przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="d51fb-168">Delete a packet capture</span></span>

<span data-ttu-id="d51fb-169">W pakiecie hello przechwytywania widok, kliknij przycisk hello **menu kontekstowe** (...) lub kliknij prawym przyciskiem myszy i kliknij przycisk **usunąć** przechwytywania pakietów hello toostop</span><span class="sxs-lookup"><span data-stu-id="d51fb-169">In hello packet capture view, click hello **context menu** (...) or right click, and click **delete** toostop hello packet capture</span></span>

![Usuń przechwytywania pakietów][3]

> [!NOTE]
> <span data-ttu-id="d51fb-171">Usunięcie przechwytywania pakietów nie powoduje usunięcia pliku hello hello koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="d51fb-171">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

<span data-ttu-id="d51fb-172">Zostanie wyświetlona prośba tooconfirm ma przechwytywania pakietów hello toodelete, kliknij przycisk **tak**</span><span class="sxs-lookup"><span data-stu-id="d51fb-172">You are asked tooconfirm you want toodelete hello packet capture, click **Yes**</span></span>

![Potwierdzenie][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="d51fb-174">Zatrzymaj przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="d51fb-174">Stop a packet capture</span></span>

<span data-ttu-id="d51fb-175">W pakiecie hello przechwytywania widok, kliknij przycisk hello **menu kontekstowe** (...) lub kliknij prawym przyciskiem myszy i kliknij przycisk **zatrzymać** przechwytywania pakietów hello toostop</span><span class="sxs-lookup"><span data-stu-id="d51fb-175">In hello packet capture view, click hello **context menu** (...) or right click, and click **Stop** toostop hello packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="d51fb-176">Pobierz przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="d51fb-176">Download a packet capture</span></span>

<span data-ttu-id="d51fb-177">Po zakończeniu sesji przechwytywania pakietów, plik przechwytywania hello jest przekazane tooblob tooa lub magazynu lokalnego pliku na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d51fb-177">Once your packet capture session has completed, hello capture file is uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="d51fb-178">Lokalizacja przechowywania Hello przechwytywania pakietów hello jest definiowany podczas tworzenia hello sesji.</span><span class="sxs-lookup"><span data-stu-id="d51fb-178">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="d51fb-179">Tooaccess wygodne narzędzie te Przechwytywanie plików, tooa zapisane konto magazynu jest Microsoft Azure Eksploratora usługi Storage, który można pobrać tutaj: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="d51fb-179">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="d51fb-180">Jeśli określono konto magazynu, zapisywane są pliki przechwytywania pakietów tooa konta magazynu w następującej lokalizacji hello:</span><span class="sxs-lookup"><span data-stu-id="d51fb-180">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="d51fb-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d51fb-181">Next steps</span></span>

<span data-ttu-id="d51fb-182">Dowiedz się, jak przechwytywanie pakietów tooautomate z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="d51fb-182">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="d51fb-183">Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d51fb-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













