---
title: "Sprawdzanie poprawności sieci VPN tooa przepustowość sieci wirtualnej Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Witaj celem niniejszego dokumentu jest toohelp użytkownika zweryfikować hello przepływność sieci z ich tooan zasoby lokalne maszyny wirtualnej platformy Azure."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a><span data-ttu-id="e4237-103">Jak sieci wirtualnej przepływności tooa toovalidate sieci VPN</span><span class="sxs-lookup"><span data-stu-id="e4237-103">How toovalidate VPN throughput tooa virtual network</span></span>

<span data-ttu-id="e4237-104">Połączenie bramy sieci VPN włącza bezpieczny, łączności między lokalizacjami tooestablish między sieci wirtualnej w systemie Azure i lokalnej infrastruktury IT.</span><span class="sxs-lookup"><span data-stu-id="e4237-104">A VPN gateway connection enables you tooestablish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="e4237-105">W tym artykule przedstawiono sposób toovalidate przepływność sieci z hello lokalnymi tooan zasobów maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e4237-105">This article shows how toovalidate network throughput from hello on-premises resources tooan Azure virtual machine.</span></span> <span data-ttu-id="e4237-106">Umożliwia także wskazówki dotyczące rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="e4237-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="e4237-107">Ten artykuł dotyczy toohelp diagnozowanie i rozwiązywanie typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="e4237-107">This article is intended toohelp diagnose and fix common issues.</span></span> <span data-ttu-id="e4237-108">Jeśli masz problem hello toosolve przy użyciu następujących informacji, hello [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="e4237-108">If you're unable toosolve hello issue by using hello following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="e4237-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e4237-109">Overview</span></span>

<span data-ttu-id="e4237-110">Witaj połączenie bramy sieci VPN obejmuje hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="e4237-110">hello VPN gateway connection involves hello following components:</span></span>

- <span data-ttu-id="e4237-111">Lokalnego urządzenia sieci VPN (wyświetlanie listy [zweryfikowane urządzenia sieci VPN)](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="e4237-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="e4237-112">Publicznego Internetu</span><span class="sxs-lookup"><span data-stu-id="e4237-112">Public Internet</span></span>
- <span data-ttu-id="e4237-113">Brama sieci VPN</span><span class="sxs-lookup"><span data-stu-id="e4237-113">Azure VPN gateway</span></span>
- <span data-ttu-id="e4237-114">Maszyna wirtualna platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e4237-114">Azure virtual machine</span></span>

<span data-ttu-id="e4237-115">powitania po diagram przedstawia hello logicznej łączność tooan sieci lokalnej sieci wirtualnej platformy Azure za pośrednictwem sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="e4237-115">hello following diagram shows hello logical connectivity of an on-premises network tooan Azure virtual network through VPN.</span></span>

![Sieci logiczne tooMSFT sieci łączności klienta przy użyciu sieci VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a><span data-ttu-id="e4237-117">Oblicz hello maksymalna oczekiwana wejście/wyjście</span><span class="sxs-lookup"><span data-stu-id="e4237-117">Calculate hello maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="e4237-118">Ustal wymagania dotyczące przepływności linii bazowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4237-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="e4237-119">Określ swoje limity przepływność bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e4237-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="e4237-120">Aby uzyskać pomoc, zobacz sekcję hello "łącznej przepływności według jednostki SKU i sieci VPN typu" [planowania i projektowania dla bramy sieci VPN](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="e4237-120">For help, see hello "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="e4237-121">Określić hello [maszyny Wirtualnej Azure przepływności wskazówki](../virtual-machines/virtual-machines-windows-sizes.md) dla rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e4237-121">Determine hello [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="e4237-122">Określ przepustowość usługodawcy internetowego (ISP).</span><span class="sxs-lookup"><span data-stu-id="e4237-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="e4237-123">Obliczanie przepływności oczekiwanego - minimalnej przepustowości (maszyna wirtualna, brama usługodawcy internetowego) * 0,8.</span><span class="sxs-lookup"><span data-stu-id="e4237-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="e4237-124">Jeśli Twoje obliczeniowej przepływności nie spełnia wymagania dotyczące przepływności linii bazowej aplikacji, należy tooincrease hello przepustowości hello zasobu, który został zidentyfikowany jako "wąskie gardło" hello.</span><span class="sxs-lookup"><span data-stu-id="e4237-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need tooincrease hello bandwidth of hello resource that you identified as hello bottleneck.</span></span> <span data-ttu-id="e4237-125">tooresize bramy sieci VPN platformy Azure, zobacz [zmiana jednostka SKU bramy](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="e4237-125">tooresize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="e4237-126">tooresize maszyny wirtualnej, zobacz [Zmień rozmiar maszyny Wirtualnej](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="e4237-126">tooresize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="e4237-127">Jeśli nie występują oczekiwanego przepustowości połączenia z Internetem, można również toocontact usługodawcy.</span><span class="sxs-lookup"><span data-stu-id="e4237-127">If you are not experiencing expected Internet bandwidth, you may also want toocontact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="e4237-128">Sprawdź poprawność przepływność sieci przy użyciu narzędzia wydajności</span><span class="sxs-lookup"><span data-stu-id="e4237-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="e4237-129">Ta powinna być sprawdzana podczas godziny poza szczytem, jak nasycenie przepływności tunelu VPN podczas testowania nie daje prawidłowych wyników.</span><span class="sxs-lookup"><span data-stu-id="e4237-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="e4237-130">Narzędzie Hello, używanego dla tego testu jest dotyczące programu Iperf; która działa w systemach Windows i Linux i trybach klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="e4237-130">hello tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="e4237-131">Jest ograniczona too3 GB/s dla maszyn wirtualnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="e4237-131">It is limited too3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="e4237-132">To narzędzie nie wykonuje żadnych toodisk operacje odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="e4237-132">This tool does not perform any read/write operations toodisk.</span></span> <span data-ttu-id="e4237-133">Tworzy wyłącznie automatycznie wygenerowany ruch TCP z jednego toohello zakończenia, inne.</span><span class="sxs-lookup"><span data-stu-id="e4237-133">It solely produces self-generated TCP traffic from one end toohello other.</span></span> <span data-ttu-id="e4237-134">Statystyka oparta na eksperymenty, która hello dostępna przepustowość między klientem i serwerem węzłów on wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="e4237-134">It generated statistics based on experimentation that measures hello bandwidth available between client and server nodes.</span></span> <span data-ttu-id="e4237-135">Podczas testowania między dwoma węzłami, co działa jako serwer hello i hello innych jako klienta.</span><span class="sxs-lookup"><span data-stu-id="e4237-135">When testing between two nodes, one acts as hello server and hello other as a client.</span></span> <span data-ttu-id="e4237-136">Po zakończeniu tego testu, firma Microsoft zaleca, aby odwrócić hello ról tootest zarówno przekazywanie i pobieranie przepływności na obu węzłów.</span><span class="sxs-lookup"><span data-stu-id="e4237-136">Once this test is completed, we recommend that you reverse hello roles tootest both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="e4237-137">Pobierz dotyczące programu Iperf</span><span class="sxs-lookup"><span data-stu-id="e4237-137">Download iPerf</span></span>
<span data-ttu-id="e4237-138">Pobierz [dotyczące programu Iperf;](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="e4237-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="e4237-139">Aby uzyskać więcej informacji, zobacz [dokumentacji dotyczące programu Iperf;](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="e4237-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="e4237-140">produkty innych firm Hello omówione w tym artykule są wytwarzane przez producentów niezależnych od firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e4237-140">hello third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="e4237-141">Firma Microsoft nie udziela żadnych gwarancji, dorozumianych ani żadnego innego o hello wydajności ani niezawodności tych produktów.</span><span class="sxs-lookup"><span data-stu-id="e4237-141">Microsoft makes no warranty, implied or otherwise, about hello performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="e4237-142">Uruchom dotyczące programu Iperf; (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="e4237-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="e4237-143">Włącz reguły NSG/list kontroli dostępu zezwala na ruch hello (na potrzeby testowania na maszynie Wirtualnej Azure publiczny adres IP).</span><span class="sxs-lookup"><span data-stu-id="e4237-143">Enable an NSG/ACL rule allowing hello traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="e4237-144">W obu węzłach Włącz wyjątek zapory dla portu 5001.</span><span class="sxs-lookup"><span data-stu-id="e4237-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="e4237-145">**System Windows:** następujące hello Uruchom polecenie jako administrator:</span><span class="sxs-lookup"><span data-stu-id="e4237-145">**Windows:** Run hello following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="e4237-146">Reguła hello tooremove podczas testowania zostanie zakończone, uruchom to polecenie:</span><span class="sxs-lookup"><span data-stu-id="e4237-146">tooremove hello rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="e4237-147">**Azure Linux:** obrazów systemu Linux platformy Azure są ograniczająca zapory.</span><span class="sxs-lookup"><span data-stu-id="e4237-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="e4237-148">Czy aplikacja nasłuchuje na porcie, hello ruch jest dozwolony przez.</span><span class="sxs-lookup"><span data-stu-id="e4237-148">If there is an application listening on a port, hello traffic is allowed through.</span></span> <span data-ttu-id="e4237-149">Otwarte jawnie portów może być konieczne niestandardowych obrazów, które są zabezpieczone.</span><span class="sxs-lookup"><span data-stu-id="e4237-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="e4237-150">Typowe zapory systemu operacyjnego Linux warstwy obejmują `iptables`, `ufw`, lub `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="e4237-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="e4237-151">W węźle serwera hello Zmień katalog toohello, w której jest wyodrębniany iperf3.exe.</span><span class="sxs-lookup"><span data-stu-id="e4237-151">On hello server node, change toohello directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="e4237-152">Następnie uruchom dotyczące programu Iperf; w trybie serwera i ustaw go toolisten na porcie 5001 jako hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e4237-152">Then run iPerf in server mode and set it toolisten on port 5001 as hello following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="e4237-153">W węźle powitania klienta zmienić toohello katalogu zawierającego narzędzia dotyczące programu Iperf; jest wyodrębniany, a następnie uruchom hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e4237-153">On hello client node, change toohello directory where iperf tool is extracted and then run hello following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="e4237-154">powitania klienta to powoduje ruch na porcie 5001 toohello serwera przez 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="e4237-154">hello client is inducing traffic on port 5001 toohello server for 30 seconds.</span></span> <span data-ttu-id="e4237-155">Witaj flagi "-P" wskazujące, że użyto 32 węzeł serwera toohello równoczesnych połączeń.</span><span class="sxs-lookup"><span data-stu-id="e4237-155">hello flag '-P ' that indicates we are using 32 simultaneous connections toohello server node.</span></span>

    <span data-ttu-id="e4237-156">Hello poniższym ekranie przedstawiono hello dane w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="e4237-156">hello following screen shows hello output from this example:</span></span>

    ![Dane wyjściowe](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="e4237-158">Witaj toopreserve (OPCJONALNIE) testowanie wyników, uruchom to polecenie:</span><span class="sxs-lookup"><span data-stu-id="e4237-158">(OPTIONAL) toopreserve hello testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="e4237-159">Po wykonaniu poprzednich kroków hello, należy wykonać hello cofnąć te same czynności z rolami hello, tak, aby hello węzeł serwera teraz powitania klienta i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="e4237-159">After completing hello previous steps, execute hello same steps with hello roles reversed, so that hello server node will now be hello client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="e4237-160">Rozwiązać problemy kopii pliku powolne</span><span class="sxs-lookup"><span data-stu-id="e4237-160">Address slow file copy issues</span></span>
<span data-ttu-id="e4237-161">Mogą wystąpić powolne pliku kopiowanie przy użyciu Eksploratora Windows lub przeciągania i upuszczania za pomocą sesji protokołu RDP.</span><span class="sxs-lookup"><span data-stu-id="e4237-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="e4237-162">Tego problemu jest zwykle tooone lub oba hello następujące czynniki:</span><span class="sxs-lookup"><span data-stu-id="e4237-162">This problem is normally due tooone or both of hello following factors:</span></span>

- <span data-ttu-id="e4237-163">Podczas kopiowania plików, aplikacji kopiowania plików, takich jak Eksplorator Windows i protokołu RDP, nie należy używać wiele wątków.</span><span class="sxs-lookup"><span data-stu-id="e4237-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="e4237-164">W celu poprawy wydajności użyj aplikacji kopii pliku wielowątkowych takiego jak [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy plików za pomocą wątków 16 lub 32.</span><span class="sxs-lookup"><span data-stu-id="e4237-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy files by using 16 or 32 threads.</span></span> <span data-ttu-id="e4237-165">numer wątku hello toochange kopiowanie plików w programie Richcopy, kliknij przycisk **akcji** > **opcje kopiowania** > **skopiowanie pliku**.</span><span class="sxs-lookup"><span data-stu-id="e4237-165">toochange hello thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="e4237-166">
![Zagadnienia dotyczące kopiowania plików powolne](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="e4237-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="e4237-167">Za mało szybkość odczytu/zapisu dysku maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e4237-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="e4237-168">Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z magazynu Azure](../storage/common/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e4237-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="e4237-169">Interfejs połączonej zewnętrznego urządzenia lokalnego</span><span class="sxs-lookup"><span data-stu-id="e4237-169">On-premises device external facing interface</span></span>
<span data-ttu-id="e4237-170">Jeśli hello lokalnego urządzenia sieci VPN adres internetowy jest uwzględniona w hello [sieci lokalnej](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definicji na platformie Azure, mogą wystąpić toobring brakiem hello zakończy połączenie sieci VPN, sporadyczne lub problemów z wydajnością.</span><span class="sxs-lookup"><span data-stu-id="e4237-170">If hello on-premises VPN device Internet-facing IP address is included in hello [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability toobring up hello VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="e4237-171">Sprawdzanie opóźnienia</span><span class="sxs-lookup"><span data-stu-id="e4237-171">Checking latency</span></span>
<span data-ttu-id="e4237-172">Użyj tracert tootrace tooMicrosoft Azure krawędzi urządzenia toodetermine, jeśli istnieją wszelkich opóźnień powyżej 100 ms między przeskoków.</span><span class="sxs-lookup"><span data-stu-id="e4237-172">Use tracert tootrace tooMicrosoft Azure Edge device toodetermine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="e4237-173">Z sieci lokalnej hello, uruchom *tracert* toohello VIP hello Azure bramy lub maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e4237-173">From hello on-premises network, run *tracert* toohello VIP of hello Azure Gateway or VM.</span></span> <span data-ttu-id="e4237-174">Gdy zostanie wyświetlony tylko * zwrócone, wiadomo, został osiągnięty hello Azure krawędzi.</span><span class="sxs-lookup"><span data-stu-id="e4237-174">Once you see only * returned, you know you have reached hello Azure edge.</span></span> <span data-ttu-id="e4237-175">Po wyświetleniu nazwy DNS, które obejmują "MSN" zwrócił wiadomo, że został osiągnięty hello firmy Microsoft w sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="e4237-175">When you see DNS names that include "MSN" returned, you know you have reached hello Microsoft backbone.</span></span><br><br><span data-ttu-id="e4237-176">
![Sprawdzanie opóźnienia](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="e4237-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4237-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e4237-177">Next steps</span></span>
<span data-ttu-id="e4237-178">Aby uzyskać więcej informacji lub uzyskać pomoc zapoznaj się hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="e4237-178">For more information or help, check out hello following links:</span></span>

- [<span data-ttu-id="e4237-179">Zoptymalizować przepływność sieci maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e4237-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="e4237-180">Pomoc techniczna firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="e4237-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
