---
title: "przepustowość sieci maszyny Wirtualnej Azure aaaTesting | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootest maszyny wirtualnej platformy Azure sieci przepływności."
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
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="692db-103">Przepustowość/przepływność, testowanie (NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="692db-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="692db-104">Podczas testowania przepustowość sieci na platformie Azure, jest najlepszym toouse narzędzie, które dotyczy sieci hello do testowania i minimalizuje użycie hello inne zasoby, które mogą wpłynąć na wydajność.</span><span class="sxs-lookup"><span data-stu-id="692db-104">When testing network throughput performance in Azure, it's best toouse a tool that targets hello network for testing and minimizes hello use of other resources that could impact performance.</span></span> <span data-ttu-id="692db-105">NTTTCP jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="692db-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="692db-106">Skopiuj tootwo narzędzie hello maszynach wirtualnych Azure hello sam rozmiar.</span><span class="sxs-lookup"><span data-stu-id="692db-106">Copy hello tool tootwo Azure VMs of hello same size.</span></span> <span data-ttu-id="692db-107">Jedna maszyna wirtualna działa jako NADAWCĘ i hello innych jako ODBIORNIK.</span><span class="sxs-lookup"><span data-stu-id="692db-107">One VM functions as SENDER and hello other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="692db-108">Wdrażanie maszyn wirtualnych na potrzeby testowania</span><span class="sxs-lookup"><span data-stu-id="692db-108">Deploying VMs for testing</span></span>
<span data-ttu-id="692db-109">Dla celów hello ten test Witaj dwie maszyny wirtualne powinny znajdować się na hello tej samej usługi w chmurze lub hello tego samego zestawu dostępności, dzięki czemu możemy użyć ich wewnętrznych adresów IP i wykluczyć hello usługi równoważenia obciążenia z hello testu.</span><span class="sxs-lookup"><span data-stu-id="692db-109">For hello purposes of this test, hello two VMs should be in either hello same Cloud Service or hello same Availability Set so that we can use their internal IPs and exclude hello Load Balancers from hello test.</span></span> <span data-ttu-id="692db-110">Jest możliwe tootest z hello VIP, ale tego rodzaju testowania jest poza zakresem hello tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="692db-110">It is possible tootest with hello VIP but this kind of testing is outside hello scope of this document.</span></span>
 
<span data-ttu-id="692db-111">Zanotuj adres IP hello odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="692db-111">Make a note of hello RECEIVER's IP address.</span></span> <span data-ttu-id="692db-112">Umożliwia wywołanie tego adresu IP "a.b.c.r"</span><span class="sxs-lookup"><span data-stu-id="692db-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="692db-113">Zanotuj hello liczba rdzeni na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="692db-113">Make a note of hello number of cores on hello VM.</span></span> <span data-ttu-id="692db-114">Umożliwia to wywołanie "\#num\_rdzeni"</span><span class="sxs-lookup"><span data-stu-id="692db-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="692db-115">Uruchom hello NTTTCP testowania 300 sekund (czyli 5 minut) na powitania nadawcy maszyny Wirtualnej i odbiorcy maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="692db-115">Run hello NTTTCP test for 300 seconds (or 5 minutes) on hello sender VM and receiver VM.</span></span>

<span data-ttu-id="692db-116">Porada: Podczas konfigurowania tego testu dla powitania po raz pierwszy, spróbuj krótszą opinii okresu tooget testu wcześniej.</span><span class="sxs-lookup"><span data-stu-id="692db-116">Tip: When setting up this test for hello first time, you might try a shorter test period tooget feedback sooner.</span></span> <span data-ttu-id="692db-117">Po narzędzia hello działa zgodnie z oczekiwaniami, rozszerzanie hello testu okresu too300 sekund na powitania najdokładniejszych wyników.</span><span class="sxs-lookup"><span data-stu-id="692db-117">Once hello tool is working as expected, extend hello test period too300 seconds for hello most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="692db-118">nadawca Hello **i** odbiornika należy określić **hello sam** parametru czas trwania testu (-t).</span><span class="sxs-lookup"><span data-stu-id="692db-118">hello sender **and** receiver must specify **hello same** test duration parameter (-t).</span></span>

<span data-ttu-id="692db-119">tootest jednego strumienia TCP przez 10 sekund:</span><span class="sxs-lookup"><span data-stu-id="692db-119">tootest a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="692db-120">Odbiornik parametrów: - r ntttcp -t 10 - P 1</span><span class="sxs-lookup"><span data-stu-id="692db-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="692db-121">Nadawca parametry: ntttcp-s10.27.33.7 metoda "-t 10 - n" 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="692db-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="692db-122">Hello poprzedzających próbki powinien mieć tylko tooconfirm używanej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="692db-122">hello preceding sample should only be used tooconfirm your configuration.</span></span> <span data-ttu-id="692db-123">Prawidłowe przykłady testów są uwzględnione w dalszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="692db-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="692db-124">Testowanie maszyn wirtualnych z systemem WINDOWS:</span><span class="sxs-lookup"><span data-stu-id="692db-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-hello-vms"></a><span data-ttu-id="692db-125">Pobierz NTTTCP na powitania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="692db-125">Get NTTTCP onto hello VMs.</span></span>

<span data-ttu-id="692db-126">Pobieranie najnowszej wersji hello: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="692db-126">Download hello latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="692db-127">Lub wyszukaj go w przypadku przeniesienia: <https://www.bing.com/search?q=ntttcp+download> \< — należy najpierw trafień</span><span class="sxs-lookup"><span data-stu-id="692db-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="692db-128">Należy rozważyć umieszczenie w oddzielnym folderze, takich jak c: NTTTCP\\narzędzia</span><span class="sxs-lookup"><span data-stu-id="692db-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a><span data-ttu-id="692db-129">Zezwalaj na NTTTCP przez zaporę systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="692db-129">Allow NTTTCP through hello Windows firewall</span></span>
<span data-ttu-id="692db-130">Na powitania ODBIORNIK należy utworzyć regułę zezwalającą na tooallow zapory systemu Windows hello NTTTCP tooarrive ruchu.</span><span class="sxs-lookup"><span data-stu-id="692db-130">On hello RECEIVER, create an Allow rule on hello Windows Firewall tooallow the NTTTCP traffic tooarrive.</span></span> <span data-ttu-id="692db-131">Jest najprostszym tooallow hello cały NTTTCP według nazwy, a nie tooallow określone porty TCP ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="692db-131">It's easiest tooallow hello entire NTTTCP program by name rather than tooallow specific TCP ports inbound.</span></span>

<span data-ttu-id="692db-132">Zezwalaj na ntttcp za pośrednictwem zapory systemu Windows hello, jak to:</span><span class="sxs-lookup"><span data-stu-id="692db-132">Allow ntttcp through hello Windows Firewall like this:</span></span>

<span data-ttu-id="692db-133">netsh advfirewall zapory Dodawanie reguły programu =\<ścieżki\>\\ntttcp.exe nazwa = "ntttcp" protokołu żadnych dir = = w akcji = Zezwalaj enable = yes profile = ANY</span><span class="sxs-lookup"><span data-stu-id="692db-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="692db-134">Na przykład, jeśli został skopiowany ntttcp.exe toohello "c:\\narzędzia" folder, to polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="692db-134">For example, if you copied ntttcp.exe toohello "c:\\tools" folder, this would be hello command:</span></span> 

<span data-ttu-id="692db-135">netsh advfirewall zapory Dodawanie reguły programu = c:\\narzędzia\\ntttcp.exe nazwa = "ntttcp" protokołu żadnych dir = = w akcji = Zezwalaj enable = yes profile = ANY</span><span class="sxs-lookup"><span data-stu-id="692db-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="692db-136">Uruchamianie testów NTTTCP</span><span class="sxs-lookup"><span data-stu-id="692db-136">Running NTTTCP tests</span></span>

<span data-ttu-id="692db-137">Uruchom NTTTCP na powitania ODBIORNIKA (**Uruchom w powłoce CMD z**, a nie z programu PowerShell):</span><span class="sxs-lookup"><span data-stu-id="692db-137">Start NTTTCP on hello RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="692db-138">ntttcp - r — m [2\*\#num\_rdzeni],\*, a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="692db-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="692db-139">Jeśli hello maszyna wirtualna ma cztery rdzeni i adres IP 10.0.0.4, będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="692db-139">If hello VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="692db-140">ntttcp - r — m 8,\*, 10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="692db-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="692db-141">Uruchom NTTTCP na powitania nadawcy (**Uruchom w powłoce CMD z**, a nie z programu PowerShell):</span><span class="sxs-lookup"><span data-stu-id="692db-141">Start NTTTCP on hello SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="692db-142">ntttcp -s — m 8,\*, 10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="692db-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="692db-143">Poczekaj na powitania wyników.</span><span class="sxs-lookup"><span data-stu-id="692db-143">Wait for hello results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="692db-144">Testowanie maszyn wirtualnych z systemem LINUX:</span><span class="sxs-lookup"><span data-stu-id="692db-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="692db-145">Użyj nttcp dla systemu linux.</span><span class="sxs-lookup"><span data-stu-id="692db-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="692db-146">Jest ona dostępna z <https://github.com/Microsoft/ntttcp-for-linux></span><span class="sxs-lookup"><span data-stu-id="692db-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="692db-147">Na powitania maszyn wirtualnych systemu Linux (NADAWCĄ i odbiorcą) uruchom następujące polecenia, aby przygotować ntttcp dla linux na maszyny wirtualne:</span><span class="sxs-lookup"><span data-stu-id="692db-147">On hello Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="692db-148">CentOS - Install Git:</span><span class="sxs-lookup"><span data-stu-id="692db-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="692db-149">Ubuntu - Install Git:</span><span class="sxs-lookup"><span data-stu-id="692db-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="692db-150">Wprowadź, a następnie zainstalować zarówno:</span><span class="sxs-lookup"><span data-stu-id="692db-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="692db-151">Co w przykładzie Windows hello przyjęto założenie, że adres IP ODBIORNIKA Linux hello jest 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="692db-151">As in hello Windows example, we assume hello Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="692db-152">Uruchom NTTTCP dla systemu Linux na powitania ODBIORNIK:</span><span class="sxs-lookup"><span data-stu-id="692db-152">Start NTTTCP-for-Linux on hello RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="692db-153">I na powitania nadawcy, uruchom:</span><span class="sxs-lookup"><span data-stu-id="692db-153">And on hello SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="692db-154">Podano testu długość wartości domyślne too60 sekund, jeśli nie parametru czasu</span><span class="sxs-lookup"><span data-stu-id="692db-154">Test length defaults too60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="692db-155">Testowanie między maszynami wirtualnymi z systemem Windows i LINUX:</span><span class="sxs-lookup"><span data-stu-id="692db-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="692db-156">W tym scenariuszy firma Microsoft włącza tryb niesynchronizowanej hello, więc można uruchomić testu hello.</span><span class="sxs-lookup"><span data-stu-id="692db-156">On this scenarios we should enable hello no-sync mode so hello test can run.</span></span> <span data-ttu-id="692db-157">Jest to zrobić za pomocą hello **flagi -N** dla systemu Linux i **flagi -ns** dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="692db-157">This is done by using hello **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-toowindows"></a><span data-ttu-id="692db-158">Z Linux tooWindows:</span><span class="sxs-lookup"><span data-stu-id="692db-158">From Linux tooWindows:</span></span>

<span data-ttu-id="692db-159">Odbiornik <Windows>:</span><span class="sxs-lookup"><span data-stu-id="692db-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="692db-160">Nadawca <Linux> :</span><span class="sxs-lookup"><span data-stu-id="692db-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a><span data-ttu-id="692db-161">Z tooLinux systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="692db-161">From Windows tooLinux:</span></span>

<span data-ttu-id="692db-162">Odbiornik <Linux>:</span><span class="sxs-lookup"><span data-stu-id="692db-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="692db-163">Nadawca <Windows>:</span><span class="sxs-lookup"><span data-stu-id="692db-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="692db-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="692db-164">Next steps</span></span>
* <span data-ttu-id="692db-165">W zależności od wyników, może być miejsca zbyt[zoptymalizować maszyny przepustowość sieci](virtual-network-optimize-network-bandwidth.md) dla danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="692db-165">Depending on results, there may be room too[Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="692db-166">Dowiedz się więcej o [sieci wirtualnej platformy Azure — często zadawane pytania (FAQ)](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="692db-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
