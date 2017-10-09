---
title: "inspekcję aaaPacket z obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak zbierane toouse inspekcję pakietów tooperform obserwatora sieciowego z maszyny Wirtualnej"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="a5c07-103">Inspekcję pakietów z obserwatora sieciowego Azure</span><span class="sxs-lookup"><span data-stu-id="a5c07-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="a5c07-104">Za pomocą funkcji przechwytywania pakietów hello obserwatora sieciowego, można zainicjować i zarządzanie sesjami przechwytywania na maszynach wirtualnych platformy Azure z hello portalu programu PowerShell, interfejsu wiersza polecenia i programowo przy użyciu hello zestawu SDK i interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="a5c07-104">Using hello packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from hello portal, PowerShell, CLI, and programmatically through hello SDK and REST API.</span></span> <span data-ttu-id="a5c07-105">Przechwytywania pakietów umożliwia scenariusze tooaddress, które wymagają danych na poziomie pakietów, zapewniając hello informacji w formacie łatwo można używać.</span><span class="sxs-lookup"><span data-stu-id="a5c07-105">Packet capture allows you tooaddress scenarios that require packet level data by providing hello information in a readily usable format.</span></span> <span data-ttu-id="a5c07-106">Wykorzystanie danych hello tooinspect bezpłatnych narzędzi, możesz sprawdzić tooand komunikacji z maszyn wirtualnych i uzyskać wgląd w ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="a5c07-106">Leveraging freely available tools tooinspect hello data, you can examine communications sent tooand from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="a5c07-107">Niektóre przykładowe zastosowania danych przechwytywania pakietów obejmują: do badania problemów dotyczących sieci lub aplikacji, wykrywanie prób nieprawidłowego użycia i nieautoryzowanego dostępu sieciowego lub utrzymania zgodności z przepisami.</span><span class="sxs-lookup"><span data-stu-id="a5c07-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="a5c07-108">W tym artykule zostanie przedstawiony sposób tooopen pliku przechwytywania pakietów udostępniane przez obserwatora sieciowego przy użyciu narzędzia popularnych typu open source.</span><span class="sxs-lookup"><span data-stu-id="a5c07-108">In this article, we show how tooopen a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="a5c07-109">Firma Microsoft udostępni również przykładami przedstawiający sposób zidentyfikować ruch nietypowe toocalculate opóźnienie połączenia i sprawdź statystyki sieci.</span><span class="sxs-lookup"><span data-stu-id="a5c07-109">We will also provide examples showing how toocalculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a5c07-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="a5c07-110">Before you begin</span></span>

<span data-ttu-id="a5c07-111">W tym artykule przechodzi przez niektóre scenariusze wstępnie skonfigurowane na przechwytywania pakietów, która została wcześniej uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="a5c07-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="a5c07-112">Te scenariusze przedstawiono możliwości, które są dostępne, przeglądając przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="a5c07-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="a5c07-113">W tym scenariuszu [WireShark](https://www.wireshark.org/) przechwytywania pakietów hello tooinspect.</span><span class="sxs-lookup"><span data-stu-id="a5c07-113">This scenario uses [WireShark](https://www.wireshark.org/) tooinspect hello packet capture.</span></span>

<span data-ttu-id="a5c07-114">W tym scenariuszu przyjęto założenie, że był już uruchamiany przechwytywania pakietów na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5c07-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="a5c07-115">toolearn jak toocreate przechwytywania pakietów, odwiedź [Przechwytywanie pakietów zarządzania za pomocą portalu hello](network-watcher-packet-capture-manage-portal.md) lub REST odwiedzając [z interfejsu API REST zarządzania Przechwytywanie pakietów](network-watcher-packet-capture-manage-rest.md).</span><span class="sxs-lookup"><span data-stu-id="a5c07-115">toolearn how toocreate a packet capture visit [Manage packet captures with hello portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="a5c07-116">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="a5c07-116">Scenario</span></span>

<span data-ttu-id="a5c07-117">W tym scenariuszu należy:</span><span class="sxs-lookup"><span data-stu-id="a5c07-117">In this scenario, you:</span></span>

* <span data-ttu-id="a5c07-118">Przejrzyj przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="a5c07-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="a5c07-119">Oblicz opóźnienia sieci</span><span class="sxs-lookup"><span data-stu-id="a5c07-119">Calculate network latency</span></span>

<span data-ttu-id="a5c07-120">W tym scenariuszu zostanie przedstawiony sposób tooview hello początkowej obiegu czasu (RTT) między dwoma punktami końcowymi konwersacji Transmission Control Protocol (TCP).</span><span class="sxs-lookup"><span data-stu-id="a5c07-120">In this scenario, we show how tooview hello initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="a5c07-121">Po nawiązaniu połączenia TCP hello pierwsze trzy pakiety wysyłane w ramach połączenia hello wykonaj wzorzec często określana tooas hello trójstopniowego.</span><span class="sxs-lookup"><span data-stu-id="a5c07-121">When a TCP connection is established, hello first three packets sent in hello connection follow a pattern commonly referred tooas hello three-way handshake.</span></span> <span data-ttu-id="a5c07-122">Sprawdzając hello najpierw dwa pakiety przesyłane w tym uzgadniania, żądania początkowego powitania klienta i odpowiedzi z serwera hello możemy obliczyć hello opóźnienia podczas tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="a5c07-122">By examining hello first two packets sent in this handshake, an initial request from hello client and a response from hello server, we can calculate hello latency when this connection was established.</span></span> <span data-ttu-id="a5c07-123">To opóźnienie jest hello tooas określonego czasu obiegu (RTT).</span><span class="sxs-lookup"><span data-stu-id="a5c07-123">This latency is referred tooas hello Round Trip Time (RTT).</span></span> <span data-ttu-id="a5c07-124">Więcej informacji na temat protokołu TCP hello i uzgadniania trójstopniowego hello można znaleźć toohello następującego zasobu.</span><span class="sxs-lookup"><span data-stu-id="a5c07-124">For more information on hello TCP protocol and hello three-way handshake refer toohello following resource.</span></span> <span data-ttu-id="a5c07-125">https://support.microsoft.com/en-US/Help/172983/Explanation-of-the-three-way-Handshake-VIA-TCP-IP</span><span class="sxs-lookup"><span data-stu-id="a5c07-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="a5c07-126">Krok 1</span><span class="sxs-lookup"><span data-stu-id="a5c07-126">Step 1</span></span>

<span data-ttu-id="a5c07-127">Uruchamianie programu WireShark</span><span class="sxs-lookup"><span data-stu-id="a5c07-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="a5c07-128">Krok 2</span><span class="sxs-lookup"><span data-stu-id="a5c07-128">Step 2</span></span>

<span data-ttu-id="a5c07-129">Witaj obciążenia **CAP** plik z sieci przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="a5c07-129">Load hello **.cap** file from your packet capture.</span></span> <span data-ttu-id="a5c07-130">Ten plik znajduje się w obiekcie blob hello został zapisany w naszym lokalnie na maszynie wirtualnej hello, w zależności od tego, jak został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="a5c07-130">This file can be found in hello blob it was saved in our locally on hello virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="a5c07-131">Krok 3</span><span class="sxs-lookup"><span data-stu-id="a5c07-131">Step 3</span></span>

<span data-ttu-id="a5c07-132">tooview hello początkowej obiegu czasu (RTT) konwersacji TCP, firma Microsoft będzie tylko patrzeć dwóch pierwszych pakietów hello objętego hello uzgadnianie protokołu TCP.</span><span class="sxs-lookup"><span data-stu-id="a5c07-132">tooview hello initial Round Trip Time (RTT) in TCP conversations, we will only be looking at hello first two packets involved in hello TCP handshake.</span></span> <span data-ttu-id="a5c07-133">Użyjemy dwóch pierwszych pakietów hello w hello trójstopniowego, które są hello [SYN], [SYN, potwierdzenia] pakietów.</span><span class="sxs-lookup"><span data-stu-id="a5c07-133">We will be using hello first two packets in hello three-way handshake, which are hello [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="a5c07-134">Są one nazwane dla flag w nagłówku TCP hello.</span><span class="sxs-lookup"><span data-stu-id="a5c07-134">They are named for flags set in hello TCP header.</span></span> <span data-ttu-id="a5c07-135">w tym scenariuszu nie użyjemy ostatnim pakiecie Hello w hello uzgadniania pakietów hello [potwierdzenia].</span><span class="sxs-lookup"><span data-stu-id="a5c07-135">hello last packet in hello handshake, hello [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="a5c07-136">Pakiet HELLO [SYN] jest wysyłany przez powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="a5c07-136">hello [SYN] packet is sent by hello client.</span></span> <span data-ttu-id="a5c07-137">Po odebraniu hello serwer wysyła pakietów hello [potwierdzenia] jako potwierdzenia otrzymania hello SYN z powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="a5c07-137">Once it is received hello server sends hello [ACK] packet as an acknowledgement of receiving hello SYN from hello client.</span></span> <span data-ttu-id="a5c07-138">Wykorzystanie hello fakt, że odpowiedź serwera hello wymaga bardzo małego obciążenia, możemy obliczyć powitalne RTT przez odjęcie czas hello pakietów hello [SYN, potwierdzenia] otrzymała przez klienta na powitania hello czasu [SYN] pakiet został wysłany przez powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="a5c07-138">Leveraging hello fact that hello server’s response requires very little overhead, we calculate hello RTT by subtracting hello time hello [SYN, ACK] packet was received by hello client by hello time [SYN] packet was sent by hello client.</span></span>

<span data-ttu-id="a5c07-139">Za pomocą programu WireShark ta wartość jest obliczana firmie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a5c07-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="a5c07-140">toomore łatwe przeglądanie dwóch pierwszych pakietów hello w hello TCP trójstopniowego, firma Microsoft będzie wykorzystywać hello oferowana przez WireShark możliwość filtrowania.</span><span class="sxs-lookup"><span data-stu-id="a5c07-140">toomore easily view hello first two packets in hello TCP three-way handshake, we will utilize hello filtering capability provided by WireShark.</span></span>

<span data-ttu-id="a5c07-141">Filtr hello tooapply w WireShark, rozwiń hello segmentu "Transmission Control Protocol" [SYN] pakietu w Twojej przechwytywania i zbadać flag hello w nagłówku TCP hello.</span><span class="sxs-lookup"><span data-stu-id="a5c07-141">tooapply hello filter in WireShark, expand hello “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine hello flags set in hello TCP header.</span></span>

<span data-ttu-id="a5c07-142">Ponieważ czekamy toofilter na wszystkich [SYN] i [SYN potwierdzenia] pakiety, w obszarze flagi cofirm ustawiono hello Syn bit too1, a następnie kliknięcie prawym przyciskiem na powitania Syn bit -> Zastosuj jako filtr -> wybrane.</span><span class="sxs-lookup"><span data-stu-id="a5c07-142">Since we are looking toofilter on all [SYN] and [SYN, ACK] packets, under flags cofirm that hello Syn bit is set too1, then right click on hello Syn bit -> Apply as Filter -> Selected.</span></span>

![Rysunek 7][7]

### <a name="step-4"></a><span data-ttu-id="a5c07-144">Krok 4</span><span class="sxs-lookup"><span data-stu-id="a5c07-144">Step 4</span></span>

<span data-ttu-id="a5c07-145">Teraz, gdy zostały przefiltrowane hello okna tooonly Zobacz pakiety z hello [SYN] bitu, można łatwo wybrać konwersacje myślisz tooview hello RTT początkowej.</span><span class="sxs-lookup"><span data-stu-id="a5c07-145">Now that you have filtered hello window tooonly see packets with hello [SYN] bit set, you can easily select conversations you are interested in tooview hello initial RTT.</span></span> <span data-ttu-id="a5c07-146">Prosty sposób tooview hello RTT w WireShark wystarczy kliknąć listy rozwijanej hello oznaczone jako "SEQ/potwierdzenia" analizy.</span><span class="sxs-lookup"><span data-stu-id="a5c07-146">A simple way tooview hello RTT in WireShark simply click hello dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="a5c07-147">Zostanie wtedy wyświetlone powitalne RTT wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="a5c07-147">You will then see hello RTT displayed.</span></span> <span data-ttu-id="a5c07-148">W takim przypadku hello RTT został 0.0022114 sekund lub 2.211 ms.</span><span class="sxs-lookup"><span data-stu-id="a5c07-148">In this case, hello RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![rysunek 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="a5c07-150">Protokoły niechciane</span><span class="sxs-lookup"><span data-stu-id="a5c07-150">Unwanted protocols</span></span>

<span data-ttu-id="a5c07-151">Może mieć wiele aplikacji uruchomionych w wystąpieniu maszyny wirtualnej wdrożonej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a5c07-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="a5c07-152">Wiele z tych aplikacji komunikują się za pośrednictwem sieci hello, być może bez Twojej zgody jawnej.</span><span class="sxs-lookup"><span data-stu-id="a5c07-152">Many of these applications communicate over hello network, perhaps without your explicit permission.</span></span> <span data-ttu-id="a5c07-153">Za pomocą komunikacji sieciowej toostore przechwytywania pakietów, możemy Sprawdź jak mówimy więc na powitania sieci i Wyszukaj problemy w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a5c07-153">Using packet capture toostore network communication, we can investigate how application are talking on hello network and look for any issues.</span></span>

<span data-ttu-id="a5c07-154">W tym przykładzie firma Microsoft analizuje poprzedniego uruchomienia przechwytywania pakietów dla niechciane protokołów, które mogą wskazywać nieautoryzowanego komunikacji z aplikacji na komputerze.</span><span class="sxs-lookup"><span data-stu-id="a5c07-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="a5c07-155">Krok 1</span><span class="sxs-lookup"><span data-stu-id="a5c07-155">Step 1</span></span>

<span data-ttu-id="a5c07-156">Przy użyciu hello tego samego przechwytywania w poprzednim kliknij scenariusz hello **statystyki** > **protokołu hierarchii**</span><span class="sxs-lookup"><span data-stu-id="a5c07-156">Using hello same capture in hello previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![Protokół hierarchii menu][2]

<span data-ttu-id="a5c07-158">zostanie wyświetlone okno hierarchii protokołu Hello.</span><span class="sxs-lookup"><span data-stu-id="a5c07-158">hello protocol hierarchy window appears.</span></span> <span data-ttu-id="a5c07-159">Ten widok zawiera listę wszystkich protokołów hello, które były używane podczas sesji przechwytywania hello i hello liczba pakietów wysłanych i odebranych za pomocą protokołów hello.</span><span class="sxs-lookup"><span data-stu-id="a5c07-159">This view provides a list of all hello protocols that were in use during hello capture session and hello number of packets transmitted and received using hello protocols.</span></span> <span data-ttu-id="a5c07-160">Ten widok może być przydatne do znajdowania niechciane ruchu sieciowego na maszynach wirtualnych lub w sieci.</span><span class="sxs-lookup"><span data-stu-id="a5c07-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![Hierarchia elementów protokołu otwarty][3]

<span data-ttu-id="a5c07-162">Jak widać w powitania po Przechwytywanie ekranu wystąpił ruchu przy użyciu protokołu BitTorrent hello, który jest używany do udostępniania plików toopeer elementu równorzędnego.</span><span class="sxs-lookup"><span data-stu-id="a5c07-162">As you can see in hello following screen capture, there was traffic using hello BitTorrent protocol, which is used for peer toopeer file sharing.</span></span> <span data-ttu-id="a5c07-163">Jako administrator nie będzie toosee BitTorrent ruchu w przypadku tego konkretnego maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a5c07-163">As an administrator you do not expect toosee BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="a5c07-164">Teraz należy pamiętać o tego rodzaju ruch, usunięciem hello równorzędnej toopeer oprogramowania instalowanego na tej maszynie wirtualnej lub bloku hello ruchu przy użyciu grup zabezpieczeń sieci i zapory.</span><span class="sxs-lookup"><span data-stu-id="a5c07-164">Now you aware of this traffic, you can remove hello peer toopeer software that installed on this virtual machine, or block hello traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="a5c07-165">Ponadto może wybrać przechwytywania pakietów toorun zgodnie z harmonogramem, możesz przejrzeć hello Użyj protokołu regularnie na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a5c07-165">Additionally, you may elect toorun packet captures on a schedule, so you can review hello protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="a5c07-166">Na przykład na jak sieci tooautomate zadania w programie azure odwiedziny [monitorowania zasobów sieciowych przy użyciu usługi Automatyzacja azure](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="a5c07-166">For an example on how tooautomate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="a5c07-167">Znajdowanie Najpopularniejsze miejsca docelowe i porty</span><span class="sxs-lookup"><span data-stu-id="a5c07-167">Finding top destinations and ports</span></span>

<span data-ttu-id="a5c07-168">Opis typów hello ruchu, hello punktów końcowych i przekazywane za pośrednictwem portów hello jest ważne podczas monitorowania i rozwiązywania problemów z aplikacji i zasobów w sieci.</span><span class="sxs-lookup"><span data-stu-id="a5c07-168">Understanding hello types of traffic, hello endpoints, and hello ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="a5c07-169">Przy użyciu pliku przechwytywania pakietów z powyższych, firma Microsoft szybko informacje hello Najpopularniejsze miejsca docelowe naszych maszyny Wirtualnej komunikuje się i hello porty jej użycia.</span><span class="sxs-lookup"><span data-stu-id="a5c07-169">Utilizing a packet capture file from above, we can quickly learn hello top destinations our VM is communicating with and hello ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="a5c07-170">Krok 1</span><span class="sxs-lookup"><span data-stu-id="a5c07-170">Step 1</span></span>

<span data-ttu-id="a5c07-171">Przy użyciu hello tego samego przechwytywania w poprzednim kliknij scenariusz hello **statystyki** > **statystyki IPv4** > **miejsc docelowych i porty**</span><span class="sxs-lookup"><span data-stu-id="a5c07-171">Using hello same capture in hello previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![Okno przechwytywania pakietów][4]

### <a name="step-2"></a><span data-ttu-id="a5c07-173">Krok 2</span><span class="sxs-lookup"><span data-stu-id="a5c07-173">Step 2</span></span>

<span data-ttu-id="a5c07-174">Szukamy za pośrednictwem wyników hello oznaczyć linii, było wiele połączeń na porcie 111.</span><span class="sxs-lookup"><span data-stu-id="a5c07-174">As we look through hello results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="a5c07-175">został Hello najczęściej używane portu 3389, czyli pulpitu zdalnego, a pozostałe hello są dynamiczne porty RPC.</span><span class="sxs-lookup"><span data-stu-id="a5c07-175">hello most used port was 3389, which is remote desktop, and hello remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="a5c07-176">Podczas tego ruchu może oznaczać nic, jest port, który był używany dla wielu połączeń i jest administratorem toohello nieznany.</span><span class="sxs-lookup"><span data-stu-id="a5c07-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown toohello administrator.</span></span>

![Rysunek 5][5]

### <a name="step-3"></a><span data-ttu-id="a5c07-178">Krok 3</span><span class="sxs-lookup"><span data-stu-id="a5c07-178">Step 3</span></span>

<span data-ttu-id="a5c07-179">Teraz, Ustaliliśmy jest za mało miejsca portu firma Microsoft można filtrować naszych przechwytywania na podstawie hello portu.</span><span class="sxs-lookup"><span data-stu-id="a5c07-179">Now that we have determined an out of place port we can filter our capture based on hello port.</span></span>

<span data-ttu-id="a5c07-180">Filtr Hello w tym scenariuszu należy:</span><span class="sxs-lookup"><span data-stu-id="a5c07-180">hello filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="a5c07-181">Możemy wprowadzić w polu tekstowym filtru hello tekstem filtru hello z powyższych i naciśnij klawisz enter.</span><span class="sxs-lookup"><span data-stu-id="a5c07-181">We enter hello filter text from above in hello filter textbox and hit enter.</span></span>

![Rysunek 6.][6]

<span data-ttu-id="a5c07-183">Z wyników hello możemy stwierdzić, cały ruch hello pochodzi z lokalnej maszyny wirtualnej na powitania tej samej podsieci.</span><span class="sxs-lookup"><span data-stu-id="a5c07-183">From hello results, we can see all hello traffic is coming from a local virtual machine on hello same subnet.</span></span> <span data-ttu-id="a5c07-184">Jeśli nadal nie Rozumiemy Dlaczego występuje ten ruch, możemy dalsze inspekcję toodetermine pakietów hello dlaczego jest wprowadzenie tych połączeń na porcie 111.</span><span class="sxs-lookup"><span data-stu-id="a5c07-184">If we still don’t understand why this traffic is occurring, we can further inspect hello packets toodetermine why it is making these calls on port 111.</span></span> <span data-ttu-id="a5c07-185">Dzięki tym informacjom firma Microsoft może potrwać hello odpowiednią akcję.</span><span class="sxs-lookup"><span data-stu-id="a5c07-185">With this information we can take hello appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5c07-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a5c07-186">Next steps</span></span>

<span data-ttu-id="a5c07-187">Dowiedz się więcej o hello inne funkcje diagnostyczne obserwatora sieciowego odwiedzając [omówienie monitorowania sieci platformy Azure](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a5c07-187">Learn about hello other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













