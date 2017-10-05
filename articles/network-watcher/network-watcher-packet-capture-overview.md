---
title: "Wprowadzenie do przechwytywania pakietów w obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera przegląd możliwości przechwytywania pakietów obserwatora sieciowego"
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
ms.openlocfilehash: 4fdd007c2cfad7b42f26ab2cacfba06d95c8dad3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-variable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="4e251-103">Wprowadzenie do przechwytywania pakietów zmiennej w obserwatora sieciowego Azure</span><span class="sxs-lookup"><span data-stu-id="4e251-103">Introduction to variable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="4e251-104">Przechwytywania pakietów zmiennej obserwatora sieciowego umożliwia tworzenie sesji przechwytywania pakietów, aby śledzić ruch do i z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e251-104">Network Watcher variable packet capture allows you to create packet capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="4e251-105">Pomaga przechwytywania pakietów do diagnozowania sieci anomalii zarówno rozbudowy i proactivity.</span><span class="sxs-lookup"><span data-stu-id="4e251-105">Packet capture helps to diagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="4e251-106">Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat wtargnięcia sieci, aby debugować komunikacja klient serwer i o wiele więcej.</span><span class="sxs-lookup"><span data-stu-id="4e251-106">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span>

<span data-ttu-id="4e251-107">Przechwytywania pakietów jest uruchamiana zdalnie za pomocą Monitora sieci rozszerzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e251-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="4e251-108">Funkcja ta ułatwia obciążeń uruchomionych przechwytywania pakietów ręcznego na odpowiednią maszynę wirtualną, która zapisuje cenny czas.</span><span class="sxs-lookup"><span data-stu-id="4e251-108">This capability eases the burden of running a packet capture manually on the desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="4e251-109">Przechwytywania pakietów mogą być wyzwalane za pośrednictwem portalu, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="4e251-109">Packet capture can be triggered through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="4e251-110">Przykład sposobu przechwytywania pakietów mogą być wyzwalane jest z alertami maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4e251-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="4e251-111">Filtry są dostępne dla sesji przechwytywania, aby upewnić się, że Przechwytywanie ruchu, który chcesz monitorować.</span><span class="sxs-lookup"><span data-stu-id="4e251-111">Filters are provided for the capture session to ensure you capture traffic you want to monitor.</span></span> <span data-ttu-id="4e251-112">Filtry są oparte na krotce 5 (protokół, lokalny adres IP zdalnego adresu IP, portu lokalnego i portu zdalnego) informacje.</span><span class="sxs-lookup"><span data-stu-id="4e251-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="4e251-113">Przechwycone dane są przechowywane w lokalnych dysków lub obiektu blob magazynu.</span><span class="sxs-lookup"><span data-stu-id="4e251-113">The captured data is stored in the local disk or a storage blob.</span></span> <span data-ttu-id="4e251-114">Ma limitu 10 sesji przechwytywania pakietów, na region na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="4e251-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="4e251-115">Ten limit ma zastosowanie tylko do sesji i nie ma zastosowania do plików przechwytywania pakietów zapisanych lokalnie na maszynie Wirtualnej lub na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="4e251-115">This limit applies only to the sessions and does not apply to the saved packet capture files either locally on the VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e251-116">Rozszerzenie maszyny wirtualnej wymaga przechwytywania pakietów `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="4e251-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="4e251-117">Instalowanie rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="4e251-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="4e251-118">Aby ograniczyć liczbę potrzebnych informacji przechwycić informacje, które mają, sesji przechwytywania pakietów są dostępne następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="4e251-118">To reduce the information you capture to only the information you want, the following options are available for a packet capture session:</span></span>

<span data-ttu-id="4e251-119">**Przechwytywanie konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="4e251-119">**Capture configuration**</span></span>

|<span data-ttu-id="4e251-120">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4e251-120">Property</span></span>|<span data-ttu-id="4e251-121">Opis</span><span class="sxs-lookup"><span data-stu-id="4e251-121">Description</span></span>|
|---|---|
|<span data-ttu-id="4e251-122">**Maksymalna liczba bajtów na pakietu (w bajtach)**</span><span class="sxs-lookup"><span data-stu-id="4e251-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="4e251-123">Liczba bajtów z każdego pakietu, które są przechwytywane, wszystkie bajty są przechwytywane, jeśli pole pozostanie puste.</span><span class="sxs-lookup"><span data-stu-id="4e251-123">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="4e251-124">Liczba bajtów z każdego pakietu, które są przechwytywane, wszystkie bajty są przechwytywane, jeśli pole pozostanie puste.</span><span class="sxs-lookup"><span data-stu-id="4e251-124">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="4e251-125">Jeśli potrzebujesz tylko w nagłówku IPv4 — wskazuje 34 tutaj</span><span class="sxs-lookup"><span data-stu-id="4e251-125">If you need only the IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="4e251-126">**Maksymalna liczba bajtów na sesji (w bajtach)**</span><span class="sxs-lookup"><span data-stu-id="4e251-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="4e251-127">Całkowita liczba bajtów w tym są przechwytywane, gdy wartość osiągnięciu zakończenia sesji.</span><span class="sxs-lookup"><span data-stu-id="4e251-127">Total number of bytes in that are captured, once the value is reached the session ends.</span></span>|
|<span data-ttu-id="4e251-128">**Limit czasu (w sekundach)**</span><span class="sxs-lookup"><span data-stu-id="4e251-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="4e251-129">Ustawia czas ograniczenie pakiet przechwytywania sesji.</span><span class="sxs-lookup"><span data-stu-id="4e251-129">Sets a time constraint on the packet capture session.</span></span> <span data-ttu-id="4e251-130">Wartość domyślna to 5 godzin lub 18000 sekundach.</span><span class="sxs-lookup"><span data-stu-id="4e251-130">The default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="4e251-131">**Filtrowanie (opcjonalnie)**</span><span class="sxs-lookup"><span data-stu-id="4e251-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="4e251-132">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4e251-132">Property</span></span>|<span data-ttu-id="4e251-133">Opis</span><span class="sxs-lookup"><span data-stu-id="4e251-133">Description</span></span>|
|---|---|
|<span data-ttu-id="4e251-134">**Protokół**</span><span class="sxs-lookup"><span data-stu-id="4e251-134">**Protocol**</span></span> | <span data-ttu-id="4e251-135">Protokół, aby filtrować pod kątem przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="4e251-135">The protocol to filter for the packet capture.</span></span> <span data-ttu-id="4e251-136">Dostępne wartości to TCP, UDP i wszystkie.</span><span class="sxs-lookup"><span data-stu-id="4e251-136">The available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="4e251-137">**Lokalny adres IP**</span><span class="sxs-lookup"><span data-stu-id="4e251-137">**Local IP address**</span></span> | <span data-ttu-id="4e251-138">Ta wartość filtry przechwytywania pakietów do pakietów, jeśli lokalny adres IP odpowiada to wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="4e251-138">This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>|
|<span data-ttu-id="4e251-139">**Port lokalny**</span><span class="sxs-lookup"><span data-stu-id="4e251-139">**Local port**</span></span> | <span data-ttu-id="4e251-140">Ta wartość filtry przechwytywania pakietów do pakietów gdzie portu lokalnego zgodna z tą wartością filtru.</span><span class="sxs-lookup"><span data-stu-id="4e251-140">This value filters the packet capture to packets where the local port matches this filter value.</span></span>|
|<span data-ttu-id="4e251-141">**Zdalny adres IP**</span><span class="sxs-lookup"><span data-stu-id="4e251-141">**Remote IP address**</span></span> | <span data-ttu-id="4e251-142">Ta wartość filtry przechwytywania pakietów do pakietów, jeśli zdalny adres IP odpowiada to wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="4e251-142">This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>|
|<span data-ttu-id="4e251-143">**Port zdalny**</span><span class="sxs-lookup"><span data-stu-id="4e251-143">**Remote port**</span></span> | <span data-ttu-id="4e251-144">Ta wartość filtry przechwytywania pakietów do pakietów Jeśli port zdalny odpowiada to wartości filtru.</span><span class="sxs-lookup"><span data-stu-id="4e251-144">This value filters the packet capture to packets where the remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="4e251-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4e251-145">Next steps</span></span>

<span data-ttu-id="4e251-146">Dowiedz się, jak można zarządzać przechwytywania pakietów, za pośrednictwem portalu, odwiedzając [Zarządzanie przechwytywania pakietów w portalu Azure](network-watcher-packet-capture-manage-portal.md) lub przy użyciu programu PowerShell, odwiedzając [Zarządzanie przechwytywania pakietów przy użyciu programu PowerShell](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4e251-146">Learn how you can manage packet captures through the portal by visiting [Manage packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="4e251-147">Informacje o tworzeniu pakietów aktywnego przechwytywania na podstawie maszyny wirtualnej alertów, odwiedzając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="4e251-147">Learn how to create proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













