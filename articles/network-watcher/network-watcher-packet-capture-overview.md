---
title: Przechwytywanie tooPacket aaaIntroduction w obserwatora sieciowego Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera przegląd możliwości przechwytywania pakietów obserwatora sieciowego hello"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="ed5ce-103">Wprowadzenie przechwytywania pakietów toovariable w obserwatora sieciowego Azure</span><span class="sxs-lookup"><span data-stu-id="ed5ce-103">Introduction toovariable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="ed5ce-104">Przechwytywania pakietów zmiennej obserwatora sieciowego umożliwia toocreate pakietów przechwytywania sesji tootrack ruch tooand z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-104">Network Watcher variable packet capture allows you toocreate packet capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="ed5ce-105">Przechwytywania pakietów pomaga anomalii sieci toodiagnose zarówno rozbudowy i proactivity.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-105">Packet capture helps toodiagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="ed5ce-106">Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat sieci wtargnięcia toodebug klient serwer, komunikację i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-106">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span>

<span data-ttu-id="ed5ce-107">Przechwytywania pakietów jest uruchamiana zdalnie za pomocą Monitora sieci rozszerzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="ed5ce-108">Funkcja ta ułatwia hello obciążeń uruchomionych przechwytywania pakietów ręcznego na potrzeby hello maszynę wirtualną, która zapisuje cenny czas.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-108">This capability eases hello burden of running a packet capture manually on hello desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="ed5ce-109">Przechwytywania pakietów mogą być wyzwalane za pośrednictwem portalu hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-109">Packet capture can be triggered through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="ed5ce-110">Przykład sposobu przechwytywania pakietów mogą być wyzwalane jest z alertami maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="ed5ce-111">Filtry są dostarczane do tooensure sesji przechwytywania hello przechwytywania ruchu sieciowego ma toomonitor.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-111">Filters are provided for hello capture session tooensure you capture traffic you want toomonitor.</span></span> <span data-ttu-id="ed5ce-112">Filtry są oparte na krotce 5 (protokół, lokalny adres IP zdalnego adresu IP, portu lokalnego i portu zdalnego) informacje.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="ed5ce-113">Witaj przechwycone dane są przechowywane w hello dysku lokalnego lub obiektu blob magazynu.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-113">hello captured data is stored in hello local disk or a storage blob.</span></span> <span data-ttu-id="ed5ce-114">Ma limitu 10 sesji przechwytywania pakietów, na region na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="ed5ce-115">Ten limit dotyczy tylko toohello sesje i nie ma zastosowania toohello zapisane pliki przechwytywania pakietów lokalnie na powitania maszyny Wirtualnej lub na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-115">This limit applies only toohello sessions and does not apply toohello saved packet capture files either locally on hello VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed5ce-116">Rozszerzenie maszyny wirtualnej wymaga przechwytywania pakietów `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="ed5ce-117">Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="ed5ce-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="ed5ce-118">informacje hello tooreduce przechwytywania tooonly hello informacje, które mają, hello poniższe opcje są dostępne dla sesji przechwytywania pakietów:</span><span class="sxs-lookup"><span data-stu-id="ed5ce-118">tooreduce hello information you capture tooonly hello information you want, hello following options are available for a packet capture session:</span></span>

<span data-ttu-id="ed5ce-119">**Przechwytywanie konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="ed5ce-119">**Capture configuration**</span></span>

|<span data-ttu-id="ed5ce-120">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ed5ce-120">Property</span></span>|<span data-ttu-id="ed5ce-121">Opis</span><span class="sxs-lookup"><span data-stu-id="ed5ce-121">Description</span></span>|
|---|---|
|<span data-ttu-id="ed5ce-122">**Maksymalna liczba bajtów na pakietu (w bajtach)**</span><span class="sxs-lookup"><span data-stu-id="ed5ce-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="ed5ce-123">Witaj liczbę bajtów z każdego pakietu, które są przechwytywane, wszystkie bajty są przechwytywane, jeśli pole pozostanie puste.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-123">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="ed5ce-124">Witaj liczbę bajtów z każdego pakietu, które są przechwytywane, wszystkie bajty są przechwytywane, jeśli pole pozostanie puste.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-124">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="ed5ce-125">Jeśli potrzebujesz tylko nagłówek IPv4 hello — wskazuje 34 tutaj</span><span class="sxs-lookup"><span data-stu-id="ed5ce-125">If you need only hello IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="ed5ce-126">**Maksymalna liczba bajtów na sesji (w bajtach)**</span><span class="sxs-lookup"><span data-stu-id="ed5ce-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="ed5ce-127">Całkowita liczba bajtów, w którym są przechwytywane po wartości hello osiągnięciu hello zakończenia sesji.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-127">Total number of bytes in that are captured, once hello value is reached hello session ends.</span></span>|
|<span data-ttu-id="ed5ce-128">**Limit czasu (w sekundach)**</span><span class="sxs-lookup"><span data-stu-id="ed5ce-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="ed5ce-129">Ustawia czas ograniczenie pakietów hello przechwytywania sesji.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-129">Sets a time constraint on hello packet capture session.</span></span> <span data-ttu-id="ed5ce-130">Wartość domyślna Hello jest 18000 sekund lub 5 godzin.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-130">hello default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="ed5ce-131">**Filtrowanie (opcjonalnie)**</span><span class="sxs-lookup"><span data-stu-id="ed5ce-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="ed5ce-132">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ed5ce-132">Property</span></span>|<span data-ttu-id="ed5ce-133">Opis</span><span class="sxs-lookup"><span data-stu-id="ed5ce-133">Description</span></span>|
|---|---|
|<span data-ttu-id="ed5ce-134">**Protokół**</span><span class="sxs-lookup"><span data-stu-id="ed5ce-134">**Protocol**</span></span> | <span data-ttu-id="ed5ce-135">Witaj toofilter protokołu dla pakietów hello przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-135">hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="ed5ce-136">Witaj dostępne wartości to TCP, UDP i wszystkie.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-136">hello available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="ed5ce-137">**Lokalny adres IP**</span><span class="sxs-lookup"><span data-stu-id="ed5ce-137">**Local IP address**</span></span> | <span data-ttu-id="ed5ce-138">Ta wartość filtruje toopackets przechwytywania pakietów hello, jeśli hello lokalny adres IP odpowiada to wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-138">This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>|
|<span data-ttu-id="ed5ce-139">**Port lokalny**</span><span class="sxs-lookup"><span data-stu-id="ed5ce-139">**Local port**</span></span> | <span data-ttu-id="ed5ce-140">Ten pakiet hello filtry wartość przechwytywania toopackets, jeśli port lokalny hello odpowiada tej wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-140">This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>|
|<span data-ttu-id="ed5ce-141">**Zdalny adres IP**</span><span class="sxs-lookup"><span data-stu-id="ed5ce-141">**Remote IP address**</span></span> | <span data-ttu-id="ed5ce-142">Ten pakiet hello filtry wartość przechwytywania toopackets Jeśli hello zdalny adres IP odpowiada to wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-142">This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>|
|<span data-ttu-id="ed5ce-143">**Port zdalny**</span><span class="sxs-lookup"><span data-stu-id="ed5ce-143">**Remote port**</span></span> | <span data-ttu-id="ed5ce-144">Ten pakiet hello filtry wartość przechwytywania toopackets, jeśli port zdalny hello odpowiada tej wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="ed5ce-144">This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="ed5ce-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ed5ce-145">Next steps</span></span>

<span data-ttu-id="ed5ce-146">Dowiedz się, jak można zarządzać przechwytywania pakietów, za pośrednictwem portalu hello odwiedzając [Zarządzanie przechwytywania pakietów w portalu Azure hello](network-watcher-packet-capture-manage-portal.md) lub przy użyciu programu PowerShell, odwiedzając [Zarządzanie przechwytywania pakietów przy użyciu programu PowerShell](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ed5ce-146">Learn how you can manage packet captures through hello portal by visiting [Manage packet capture in hello Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="ed5ce-147">Dowiedz się, jak przechwytywanie pakietów aktywnego toocreate na podstawie maszyny wirtualnej alertów, odwiedzając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="ed5ce-147">Learn how toocreate proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













