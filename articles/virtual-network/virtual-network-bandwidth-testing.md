---
title: "Testowanie przepływność sieci maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przetestować przepływność sieci maszyny wirtualnej platformy Azure."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: ccebc722386a19014674d7a59757a3685bd50793
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="a0fab-103">Przepustowość/przepływność, testowanie (NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="a0fab-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="a0fab-104">Podczas testowania przepustowość sieci na platformie Azure, najlepiej użyć narzędzia dotyczy sieci do testowania i minimalizuje inne zasoby, które mogą wpłynąć na wydajność.</span><span class="sxs-lookup"><span data-stu-id="a0fab-104">When testing network throughput performance in Azure, it's best to use a tool that targets the network for testing and minimizes the use of other resources that could impact performance.</span></span> <span data-ttu-id="a0fab-105">NTTTCP jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="a0fab-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="a0fab-106">Skopiuj narzędzie do dwóch maszyn wirtualnych platformy Azure o tej samej wielkości.</span><span class="sxs-lookup"><span data-stu-id="a0fab-106">Copy the tool to two Azure VMs of the same size.</span></span> <span data-ttu-id="a0fab-107">Jedna maszyna wirtualna działa jak NADAWCA, a drugi jako ODBIORNIK.</span><span class="sxs-lookup"><span data-stu-id="a0fab-107">One VM functions as SENDER and the other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="a0fab-108">Wdrażanie maszyn wirtualnych na potrzeby testowania</span><span class="sxs-lookup"><span data-stu-id="a0fab-108">Deploying VMs for testing</span></span>
<span data-ttu-id="a0fab-109">Na potrzeby tego testu dwóch maszyn wirtualnych powinna być w tej samej usługi w chmurze lub tego samego zestawu dostępności, aby firma Microsoft może używać ich wewnętrznych adresów IP i wykluczyć usługi równoważenia obciążenia z testu.</span><span class="sxs-lookup"><span data-stu-id="a0fab-109">For the purposes of this test, the two VMs should be in either the same Cloud Service or the same Availability Set so that we can use their internal IPs and exclude the Load Balancers from the test.</span></span> <span data-ttu-id="a0fab-110">Można przetestować przy użyciu adresu VIP, ale tego rodzaju testowania wykracza poza zakres tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="a0fab-110">It is possible to test with the VIP but this kind of testing is outside the scope of this document.</span></span>
 
<span data-ttu-id="a0fab-111">Zanotuj adres IP ODBIORNIKA.</span><span class="sxs-lookup"><span data-stu-id="a0fab-111">Make a note of the RECEIVER's IP address.</span></span> <span data-ttu-id="a0fab-112">Umożliwia wywołanie tego adresu IP "a.b.c.r"</span><span class="sxs-lookup"><span data-stu-id="a0fab-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="a0fab-113">Zanotuj liczbę rdzeni na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0fab-113">Make a note of the number of cores on the VM.</span></span> <span data-ttu-id="a0fab-114">Umożliwia to wywołanie "\#num\_rdzeni"</span><span class="sxs-lookup"><span data-stu-id="a0fab-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="a0fab-115">Testu NTTTCP 300 sekund (lub 5 minut) na nadawcy maszyny Wirtualnej i odbiorcy maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a0fab-115">Run the NTTTCP test for 300 seconds (or 5 minutes) on the sender VM and receiver VM.</span></span>

<span data-ttu-id="a0fab-116">Porada: Podczas konfigurowania tego testu po raz pierwszy, spróbuj krótszy okres testu wcześniej uzyskanie opinii.</span><span class="sxs-lookup"><span data-stu-id="a0fab-116">Tip: When setting up this test for the first time, you might try a shorter test period to get feedback sooner.</span></span> <span data-ttu-id="a0fab-117">Po narzędziu działa zgodnie z oczekiwaniami, rozszerzyć 300 sekund dla najdokładniejszych wyników testu.</span><span class="sxs-lookup"><span data-stu-id="a0fab-117">Once the tool is working as expected, extend the test period to 300 seconds for the most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="a0fab-118">Nadawca **i** odbiornika należy określić **takie same** parametru czas trwania testu (-t).</span><span class="sxs-lookup"><span data-stu-id="a0fab-118">The sender **and** receiver must specify **the same** test duration parameter (-t).</span></span>

<span data-ttu-id="a0fab-119">Aby przetestować jednego strumienia TCP przez 10 sekund:</span><span class="sxs-lookup"><span data-stu-id="a0fab-119">To test a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="a0fab-120">Odbiornik parametrów: - r ntttcp -t 10 - P 1</span><span class="sxs-lookup"><span data-stu-id="a0fab-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="a0fab-121">Nadawca parametry: ntttcp-s10.27.33.7 metoda "-t 10 - n" 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="a0fab-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="a0fab-122">Powyższego przykładu należy używać tylko w celu potwierdzenia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a0fab-122">The preceding sample should only be used to confirm your configuration.</span></span> <span data-ttu-id="a0fab-123">Prawidłowe przykłady testów są uwzględnione w dalszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="a0fab-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="a0fab-124">Testowanie maszyn wirtualnych z systemem WINDOWS:</span><span class="sxs-lookup"><span data-stu-id="a0fab-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-the-vms"></a><span data-ttu-id="a0fab-125">Pobierz NTTTCP na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a0fab-125">Get NTTTCP onto the VMs.</span></span>

<span data-ttu-id="a0fab-126">Pobierz najnowszą wersję: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="a0fab-126">Download the latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="a0fab-127">Lub wyszukaj go w przypadku przeniesienia: <https://www.bing.com/search?q=ntttcp+download> \< — należy najpierw trafień</span><span class="sxs-lookup"><span data-stu-id="a0fab-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="a0fab-128">Należy rozważyć umieszczenie w oddzielnym folderze, takich jak c: NTTTCP\\narzędzia</span><span class="sxs-lookup"><span data-stu-id="a0fab-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-the-windows-firewall"></a><span data-ttu-id="a0fab-129">Zezwalaj na NTTTCP przez zaporę systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a0fab-129">Allow NTTTCP through the Windows firewall</span></span>
<span data-ttu-id="a0fab-130">Odbiornika należy utworzyć regułę Zezwalaj zaporę systemu Windows, aby zezwolić na ruch NTTTCP odebranie.</span><span class="sxs-lookup"><span data-stu-id="a0fab-130">On the RECEIVER, create an Allow rule on the Windows Firewall to allow the NTTTCP traffic to arrive.</span></span> <span data-ttu-id="a0fab-131">Najłatwiej Zezwalaj całego programu NTTTCP według nazwy, a nie umożliwia ruchu przychodzącego dla określonych portów TCP.</span><span class="sxs-lookup"><span data-stu-id="a0fab-131">It's easiest to allow the entire NTTTCP program by name rather than to allow specific TCP ports inbound.</span></span>

<span data-ttu-id="a0fab-132">Zezwalaj na ntttcp przez zaporę systemu Windows w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a0fab-132">Allow ntttcp through the Windows Firewall like this:</span></span>

<span data-ttu-id="a0fab-133">netsh advfirewall zapory Dodawanie reguły programu =\<ścieżki\>\\ntttcp.exe nazwa = "ntttcp" protokołu żadnych dir = = w akcji = Zezwalaj enable = yes profile = ANY</span><span class="sxs-lookup"><span data-stu-id="a0fab-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="a0fab-134">Na przykład, jeśli został skopiowany ntttcp.exe do "c:\\narzędzia" folder, to polecenie:</span><span class="sxs-lookup"><span data-stu-id="a0fab-134">For example, if you copied ntttcp.exe to the "c:\\tools" folder, this would be the command:</span></span> 

<span data-ttu-id="a0fab-135">netsh advfirewall zapory Dodawanie reguły programu = c:\\narzędzia\\ntttcp.exe nazwa = "ntttcp" protokołu żadnych dir = = w akcji = Zezwalaj enable = yes profile = ANY</span><span class="sxs-lookup"><span data-stu-id="a0fab-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="a0fab-136">Uruchamianie testów NTTTCP</span><span class="sxs-lookup"><span data-stu-id="a0fab-136">Running NTTTCP tests</span></span>

<span data-ttu-id="a0fab-137">Uruchom NTTTCP odbiornika (**Uruchom w powłoce CMD z**, a nie z programu PowerShell):</span><span class="sxs-lookup"><span data-stu-id="a0fab-137">Start NTTTCP on the RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="a0fab-138">ntttcp - r — m [2\*\#num\_rdzeni],\*, a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="a0fab-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="a0fab-139">Jeśli maszyna wirtualna ma cztery rdzeni i adres IP 10.0.0.4, będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="a0fab-139">If the VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="a0fab-140">ntttcp - r — m 8,\*, 10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="a0fab-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="a0fab-141">Uruchom NTTTCP na nadawcy (**Uruchom w powłoce CMD z**, a nie z programu PowerShell):</span><span class="sxs-lookup"><span data-stu-id="a0fab-141">Start NTTTCP on the SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="a0fab-142">ntttcp -s — m 8,\*, 10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="a0fab-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="a0fab-143">Poczekaj na wyniki.</span><span class="sxs-lookup"><span data-stu-id="a0fab-143">Wait for the results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="a0fab-144">Testowanie maszyn wirtualnych z systemem LINUX:</span><span class="sxs-lookup"><span data-stu-id="a0fab-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="a0fab-145">Użyj nttcp dla systemu linux.</span><span class="sxs-lookup"><span data-stu-id="a0fab-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="a0fab-146">Jest ona dostępna z <https://github.com/Microsoft/ntttcp-for-linux></span><span class="sxs-lookup"><span data-stu-id="a0fab-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="a0fab-147">Na maszyn wirtualnych systemu Linux (NADAWCĄ i odbiorcą) uruchom następujące polecenia, aby przygotować ntttcp dla linux na maszyny wirtualne:</span><span class="sxs-lookup"><span data-stu-id="a0fab-147">On the Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="a0fab-148">CentOS - Install Git:</span><span class="sxs-lookup"><span data-stu-id="a0fab-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="a0fab-149">Ubuntu - Install Git:</span><span class="sxs-lookup"><span data-stu-id="a0fab-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="a0fab-150">Wprowadź, a następnie zainstalować zarówno:</span><span class="sxs-lookup"><span data-stu-id="a0fab-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="a0fab-151">Jak pokazano w przykładzie Windows przyjęto założenie, że adres IP ODBIORNIKA Linux jest 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="a0fab-151">As in the Windows example, we assume the Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="a0fab-152">Uruchom NTTTCP dla systemu Linux odbiornika:</span><span class="sxs-lookup"><span data-stu-id="a0fab-152">Start NTTTCP-for-Linux on the RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="a0fab-153">I na nadawcy, uruchom:</span><span class="sxs-lookup"><span data-stu-id="a0fab-153">And on the SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="a0fab-154">Podano długość domyślnie 60 sekund, jeśli nie parametru czasu testu</span><span class="sxs-lookup"><span data-stu-id="a0fab-154">Test length defaults to 60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="a0fab-155">Testowanie między maszynami wirtualnymi z systemem Windows i LINUX:</span><span class="sxs-lookup"><span data-stu-id="a0fab-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="a0fab-156">Na tym scenariuszy możemy włączyć tryb synchronizacji nie, aby uruchomić test.</span><span class="sxs-lookup"><span data-stu-id="a0fab-156">On this scenarios we should enable the no-sync mode so the test can run.</span></span> <span data-ttu-id="a0fab-157">Jest to zrobić za pomocą **flagi -N** dla systemu Linux i **flagi -ns** dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a0fab-157">This is done by using the **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-to-windows"></a><span data-ttu-id="a0fab-158">Z systemu Linux w systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="a0fab-158">From Linux to Windows:</span></span>

<span data-ttu-id="a0fab-159">Odbiornik <Windows>:</span><span class="sxs-lookup"><span data-stu-id="a0fab-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="a0fab-160">Nadawca <Linux> :</span><span class="sxs-lookup"><span data-stu-id="a0fab-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-to-linux"></a><span data-ttu-id="a0fab-161">Z systemu Windows do systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="a0fab-161">From Windows to Linux:</span></span>

<span data-ttu-id="a0fab-162">Odbiornik <Linux>:</span><span class="sxs-lookup"><span data-stu-id="a0fab-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="a0fab-163">Nadawca <Windows>:</span><span class="sxs-lookup"><span data-stu-id="a0fab-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="a0fab-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a0fab-164">Next steps</span></span>
* <span data-ttu-id="a0fab-165">W zależności od wyników, może być miejsca, aby [zoptymalizować maszyny przepustowość sieci](virtual-network-optimize-network-bandwidth.md) dla danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="a0fab-165">Depending on results, there may be room to [Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="a0fab-166">Dowiedz się więcej o [sieci wirtualnej platformy Azure — często zadawane pytania (FAQ)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="a0fab-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
