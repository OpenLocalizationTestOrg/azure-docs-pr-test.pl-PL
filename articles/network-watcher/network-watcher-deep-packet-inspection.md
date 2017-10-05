---
title: "Inspekcję pakietów z obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób użycia obserwatora sieciowego przeprowadzać inspekcję pakietów zebrane z maszyny Wirtualnej"
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
ms.openlocfilehash: 91c47bb8922a9be21dff72e7cf64b29b14a36e9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="64bf2-103">Inspekcję pakietów z obserwatora sieciowego Azure</span><span class="sxs-lookup"><span data-stu-id="64bf2-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="64bf2-104">Za pomocą funkcji przechwytywania pakietów obserwatora sieciowego, można zainicjować i zarządzanie sesjami przechwytywania na maszynach wirtualnych platformy Azure z portalu, programu PowerShell, interfejsu wiersza polecenia i programowo przy użyciu zestawu SDK i interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="64bf2-104">Using the packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from the portal, PowerShell, CLI, and programmatically through the SDK and REST API.</span></span> <span data-ttu-id="64bf2-105">Przechwytywania pakietów umożliwia scenariusze adresów, które wymagają danych na poziomie pakietów przez przekazywanie informacji w formacie łatwo można używać.</span><span class="sxs-lookup"><span data-stu-id="64bf2-105">Packet capture allows you to address scenarios that require packet level data by providing the information in a readily usable format.</span></span> <span data-ttu-id="64bf2-106">Wykorzystanie bezpłatnych narzędzi, aby sprawdzić dane, możesz sprawdzić łączności wysyłane do i z maszyn wirtualnych i uzyskać wgląd w ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="64bf2-106">Leveraging freely available tools to inspect the data, you can examine communications sent to and from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="64bf2-107">Niektóre przykładowe zastosowania danych przechwytywania pakietów obejmują: do badania problemów dotyczących sieci lub aplikacji, wykrywanie prób nieprawidłowego użycia i nieautoryzowanego dostępu sieciowego lub utrzymania zgodności z przepisami.</span><span class="sxs-lookup"><span data-stu-id="64bf2-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="64bf2-108">W tym artykule, zostanie przedstawiony sposób otwierania pliku przechwytywania pakietów dostarczonego przez obserwatora sieciowego przy użyciu narzędzia popularnych typu open source.</span><span class="sxs-lookup"><span data-stu-id="64bf2-108">In this article, we show how to open a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="64bf2-109">Firma Microsoft udostępni również przykładami przedstawiający sposób obliczania opóźnienie połączenia, identyfikowanie nietypowe ruchu i sprawdź statystyki sieci.</span><span class="sxs-lookup"><span data-stu-id="64bf2-109">We will also provide examples showing how to calculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="64bf2-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="64bf2-110">Before you begin</span></span>

<span data-ttu-id="64bf2-111">W tym artykule przechodzi przez niektóre scenariusze wstępnie skonfigurowane na przechwytywania pakietów, która została wcześniej uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="64bf2-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="64bf2-112">Te scenariusze przedstawiono możliwości, które są dostępne, przeglądając przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="64bf2-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="64bf2-113">W tym scenariuszu [WireShark](https://www.wireshark.org/) do zbadania przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="64bf2-113">This scenario uses [WireShark](https://www.wireshark.org/) to inspect the packet capture.</span></span>

<span data-ttu-id="64bf2-114">W tym scenariuszu przyjęto założenie, że był już uruchamiany przechwytywania pakietów na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64bf2-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="64bf2-115">Aby dowiedzieć się, jak utworzyć odwiedziny przechwytywania pakietów [Przechwytywanie pakietów Zarządzaj w portalu](network-watcher-packet-capture-manage-portal.md) lub REST odwiedzając [z interfejsu API REST zarządzania Przechwytywanie pakietów](network-watcher-packet-capture-manage-rest.md).</span><span class="sxs-lookup"><span data-stu-id="64bf2-115">To learn how to create a packet capture visit [Manage packet captures with the portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="64bf2-116">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="64bf2-116">Scenario</span></span>

<span data-ttu-id="64bf2-117">W tym scenariuszu należy:</span><span class="sxs-lookup"><span data-stu-id="64bf2-117">In this scenario, you:</span></span>

* <span data-ttu-id="64bf2-118">Przejrzyj przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="64bf2-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="64bf2-119">Oblicz opóźnienia sieci</span><span class="sxs-lookup"><span data-stu-id="64bf2-119">Calculate network latency</span></span>

<span data-ttu-id="64bf2-120">W tym scenariuszu zostanie przedstawiony sposób wyświetlania początkowy czas obiegu (RTT) między dwoma punktami końcowymi konwersacji Transmission Control Protocol (TCP).</span><span class="sxs-lookup"><span data-stu-id="64bf2-120">In this scenario, we show how to view the initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="64bf2-121">Po nawiązaniu połączenia TCP, pierwsze trzy pakiety wysyłane przez połączenie wykonaj zwanymi powszechnie trójstopniowego wzorca.</span><span class="sxs-lookup"><span data-stu-id="64bf2-121">When a TCP connection is established, the first three packets sent in the connection follow a pattern commonly referred to as the three-way handshake.</span></span> <span data-ttu-id="64bf2-122">Sprawdzając pierwsze dwa pakiety przesyłane w tym uzgadnianie początkowe żądanie od klienta i odpowiedzi z serwera, firma Microsoft obliczenia opóźnienia podczas tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="64bf2-122">By examining the first two packets sent in this handshake, an initial request from the client and a response from the server, we can calculate the latency when this connection was established.</span></span> <span data-ttu-id="64bf2-123">Czas ten jest określany jako czas obiegu (RTT).</span><span class="sxs-lookup"><span data-stu-id="64bf2-123">This latency is referred to as the Round Trip Time (RTT).</span></span> <span data-ttu-id="64bf2-124">Aby uzyskać więcej informacji na temat protokołu TCP i trójstopniowego odwoływać się do następujących zasobów.</span><span class="sxs-lookup"><span data-stu-id="64bf2-124">For more information on the TCP protocol and the three-way handshake refer to the following resource.</span></span> <span data-ttu-id="64bf2-125">https://support.microsoft.com/en-US/Help/172983/Explanation-of-the-three-way-Handshake-VIA-TCP-IP</span><span class="sxs-lookup"><span data-stu-id="64bf2-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="64bf2-126">Krok 1</span><span class="sxs-lookup"><span data-stu-id="64bf2-126">Step 1</span></span>

<span data-ttu-id="64bf2-127">Uruchamianie programu WireShark</span><span class="sxs-lookup"><span data-stu-id="64bf2-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="64bf2-128">Krok 2</span><span class="sxs-lookup"><span data-stu-id="64bf2-128">Step 2</span></span>

<span data-ttu-id="64bf2-129">Obciążenia **CAP** plik z sieci przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="64bf2-129">Load the **.cap** file from your packet capture.</span></span> <span data-ttu-id="64bf2-130">Ten plik znajduje się w obiekcie blob został zapisany w naszym lokalnie na maszynie wirtualnej, w zależności od tego, jak został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="64bf2-130">This file can be found in the blob it was saved in our locally on the virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="64bf2-131">Krok 3</span><span class="sxs-lookup"><span data-stu-id="64bf2-131">Step 3</span></span>

<span data-ttu-id="64bf2-132">Aby wyświetlić początkowy czas obiegu (RTT) konwersacji TCP, firma Microsoft będzie tylko patrzeć pierwsze dwa pakiety objętego uzgadnianie protokołu TCP.</span><span class="sxs-lookup"><span data-stu-id="64bf2-132">To view the initial Round Trip Time (RTT) in TCP conversations, we will only be looking at the first two packets involved in the TCP handshake.</span></span> <span data-ttu-id="64bf2-133">Użyjemy dwóch pierwszych pakietów trójstopniowego, które są [SYN], [SYN, potwierdzenia] pakietów.</span><span class="sxs-lookup"><span data-stu-id="64bf2-133">We will be using the first two packets in the three-way handshake, which are the [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="64bf2-134">Są one nazwane dla flag w nagłówku protokołu TCP.</span><span class="sxs-lookup"><span data-stu-id="64bf2-134">They are named for flags set in the TCP header.</span></span> <span data-ttu-id="64bf2-135">W tym scenariuszu nie użyjemy ostatnim pakiecie w uzgadnianie pakietu [ACK].</span><span class="sxs-lookup"><span data-stu-id="64bf2-135">The last packet in the handshake, the [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="64bf2-136">Pakiet [SYN] jest wysyłany przez klienta.</span><span class="sxs-lookup"><span data-stu-id="64bf2-136">The [SYN] packet is sent by the client.</span></span> <span data-ttu-id="64bf2-137">Po odebraniu serwer wysyła pakiet [potwierdzenia] jako potwierdzenia otrzymania SYN od klienta.</span><span class="sxs-lookup"><span data-stu-id="64bf2-137">Once it is received the server sends the [ACK] packet as an acknowledgement of receiving the SYN from the client.</span></span> <span data-ttu-id="64bf2-138">Wykorzystanie fakt, że odpowiedzi serwera wymaga nadmiernego obciążenia, możemy obliczyć RTT przez odjęcie ilości czasu [SYN, potwierdzenia] pakiet został odebrany przez klienta w czasie [SYN] pakiet został wysłany przez klienta.</span><span class="sxs-lookup"><span data-stu-id="64bf2-138">Leveraging the fact that the server’s response requires very little overhead, we calculate the RTT by subtracting the time the [SYN, ACK] packet was received by the client by the time [SYN] packet was sent by the client.</span></span>

<span data-ttu-id="64bf2-139">Za pomocą programu WireShark ta wartość jest obliczana firmie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="64bf2-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="64bf2-140">Aby łatwiej przeglądać pierwsze dwa pakiety w trójstopniowego TCP, firma Microsoft będzie wykorzystywać oferowana przez WireShark możliwość filtrowania.</span><span class="sxs-lookup"><span data-stu-id="64bf2-140">To more easily view the first two packets in the TCP three-way handshake, we will utilize the filtering capability provided by WireShark.</span></span>

<span data-ttu-id="64bf2-141">Aby zastosować filtr w WireShark, rozwiń segmentu "Transmission Control Protocol" [SYN] pakietu w Twojej przechwytywania i zbadać flagi w nagłówku protokołu TCP.</span><span class="sxs-lookup"><span data-stu-id="64bf2-141">To apply the filter in WireShark, expand the “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine the flags set in the TCP header.</span></span>

<span data-ttu-id="64bf2-142">Ponieważ czekamy filtrowanie wszystkich [SYN] i [SYN potwierdzenia] pakiety, w obszarze flagi cofirm Syn bit jest ustawiony na wartość 1, a następnie kliknij prawym przyciskiem Syn bit myszy -> Zastosuj jako filtr -> wybrane.</span><span class="sxs-lookup"><span data-stu-id="64bf2-142">Since we are looking to filter on all [SYN] and [SYN, ACK] packets, under flags cofirm that the Syn bit is set to 1, then right click on the Syn bit -> Apply as Filter -> Selected.</span></span>

![Rysunek 7][7]

### <a name="step-4"></a><span data-ttu-id="64bf2-144">Krok 4</span><span class="sxs-lookup"><span data-stu-id="64bf2-144">Step 4</span></span>

<span data-ttu-id="64bf2-145">Teraz, gdy okno, aby zobaczyć tylko pakiety z bitowego zestawu [SYN] zostały przefiltrowane, można łatwo wybrać konwersacji, które planuje się wyświetlić RTT początkowej.</span><span class="sxs-lookup"><span data-stu-id="64bf2-145">Now that you have filtered the window to only see packets with the [SYN] bit set, you can easily select conversations you are interested in to view the initial RTT.</span></span> <span data-ttu-id="64bf2-146">Prosty sposób, aby wyświetlić RTT w WireShark po prostu kliknij listę rozwijaną oznaczone jako "SEQ/potwierdzenia" analizy.</span><span class="sxs-lookup"><span data-stu-id="64bf2-146">A simple way to view the RTT in WireShark simply click the dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="64bf2-147">Zostanie wtedy wyświetlone RTT wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="64bf2-147">You will then see the RTT displayed.</span></span> <span data-ttu-id="64bf2-148">W takim przypadku RTT został 0.0022114 sekund lub 2.211 ms.</span><span class="sxs-lookup"><span data-stu-id="64bf2-148">In this case, the RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![rysunek 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="64bf2-150">Protokoły niechciane</span><span class="sxs-lookup"><span data-stu-id="64bf2-150">Unwanted protocols</span></span>

<span data-ttu-id="64bf2-151">Może mieć wiele aplikacji uruchomionych w wystąpieniu maszyny wirtualnej wdrożonej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="64bf2-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="64bf2-152">Wiele z tych aplikacji komunikują się za pośrednictwem sieci, może bez Twojej zgody jawnej.</span><span class="sxs-lookup"><span data-stu-id="64bf2-152">Many of these applications communicate over the network, perhaps without your explicit permission.</span></span> <span data-ttu-id="64bf2-153">Za pomocą przechwytywania pakietów do przechowywania komunikacji sieciowej możemy Sprawdź jak mówimy w sieci i Wyszukaj problemy w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="64bf2-153">Using packet capture to store network communication, we can investigate how application are talking on the network and look for any issues.</span></span>

<span data-ttu-id="64bf2-154">W tym przykładzie firma Microsoft analizuje poprzedniego uruchomienia przechwytywania pakietów dla niechciane protokołów, które mogą wskazywać nieautoryzowanego komunikacji z aplikacji na komputerze.</span><span class="sxs-lookup"><span data-stu-id="64bf2-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="64bf2-155">Krok 1</span><span class="sxs-lookup"><span data-stu-id="64bf2-155">Step 1</span></span>

<span data-ttu-id="64bf2-156">Przy użyciu tego samego przechwytywania w poprzednim scenariuszu kliknij **statystyki** > **protokołu hierarchii**</span><span class="sxs-lookup"><span data-stu-id="64bf2-156">Using the same capture in the previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![Protokół hierarchii menu][2]

<span data-ttu-id="64bf2-158">Zostanie wyświetlone okno hierarchii protokołu.</span><span class="sxs-lookup"><span data-stu-id="64bf2-158">The protocol hierarchy window appears.</span></span> <span data-ttu-id="64bf2-159">Ten widok zawiera listę wszystkich protokołów, które były używane podczas sesji przechwytywania i liczbę pakietów wysłanych i odebranych za pomocą protokołów.</span><span class="sxs-lookup"><span data-stu-id="64bf2-159">This view provides a list of all the protocols that were in use during the capture session and the number of packets transmitted and received using the protocols.</span></span> <span data-ttu-id="64bf2-160">Ten widok może być przydatne do znajdowania niechciane ruchu sieciowego na maszynach wirtualnych lub w sieci.</span><span class="sxs-lookup"><span data-stu-id="64bf2-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![Hierarchia elementów protokołu otwarty][3]

<span data-ttu-id="64bf2-162">Jak widać w następujących Przechwytywanie ekranu wystąpił ruchu przy użyciu protokołu BitTorrent, który jest używany do udostępniania plików równorzędnych.</span><span class="sxs-lookup"><span data-stu-id="64bf2-162">As you can see in the following screen capture, there was traffic using the BitTorrent protocol, which is used for peer to peer file sharing.</span></span> <span data-ttu-id="64bf2-163">Jako administrator nie powinny być widoczne BitTorrent ruchu w przypadku tego konkretnego maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="64bf2-163">As an administrator you do not expect to see BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="64bf2-164">Teraz należy pamiętać o tego rodzaju ruch, możesz można usunąć równorzędnych oprogramowanie zainstalowane na tej maszynie wirtualnej lub blokowania ruchu przy użyciu grup zabezpieczeń sieci i zapory.</span><span class="sxs-lookup"><span data-stu-id="64bf2-164">Now you aware of this traffic, you can remove the peer to peer software that installed on this virtual machine, or block the traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="64bf2-165">Ponadto może zdecydować się na uruchamiania przechwytywania pakietów zgodnie z harmonogramem, więc możesz przejrzeć Użyj protokołu regularnie na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="64bf2-165">Additionally, you may elect to run packet captures on a schedule, so you can review the protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="64bf2-166">Na przykład dotyczące automatyzacji zadań sieci na platformie azure, odwiedź stronę [monitorowania zasobów sieciowych przy użyciu usługi Automatyzacja azure](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="64bf2-166">For an example on how to automate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="64bf2-167">Znajdowanie Najpopularniejsze miejsca docelowe i porty</span><span class="sxs-lookup"><span data-stu-id="64bf2-167">Finding top destinations and ports</span></span>

<span data-ttu-id="64bf2-168">Opis typów ruchu, punkty końcowe i przekazywane za pośrednictwem portów jest ważne podczas monitorowania i rozwiązywania problemów z aplikacji i zasobów w sieci.</span><span class="sxs-lookup"><span data-stu-id="64bf2-168">Understanding the types of traffic, the endpoints, and the ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="64bf2-169">Przy użyciu pliku przechwytywania pakietów z powyższych, firma Microsoft szybko i można znaleźć górny miejsc docelowych, które naszym wirtualna komunikuje się z portów jej użycia.</span><span class="sxs-lookup"><span data-stu-id="64bf2-169">Utilizing a packet capture file from above, we can quickly learn the top destinations our VM is communicating with and the ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="64bf2-170">Krok 1</span><span class="sxs-lookup"><span data-stu-id="64bf2-170">Step 1</span></span>

<span data-ttu-id="64bf2-171">Przy użyciu tego samego przechwytywania w poprzednim scenariuszu kliknij **statystyki** > **statystyki IPv4** > **miejsc docelowych i porty**</span><span class="sxs-lookup"><span data-stu-id="64bf2-171">Using the same capture in the previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![Okno przechwytywania pakietów][4]

### <a name="step-2"></a><span data-ttu-id="64bf2-173">Krok 2</span><span class="sxs-lookup"><span data-stu-id="64bf2-173">Step 2</span></span>

<span data-ttu-id="64bf2-174">Jak możemy Przejrzyj wyniki linii będą się wystąpiły wiele połączeń na porcie 111.</span><span class="sxs-lookup"><span data-stu-id="64bf2-174">As we look through the results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="64bf2-175">Został najczęściej używanych portu 3389, czyli pulpitu zdalnego, a pozostałe są dynamiczne porty RPC.</span><span class="sxs-lookup"><span data-stu-id="64bf2-175">The most used port was 3389, which is remote desktop, and the remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="64bf2-176">Podczas tego ruchu może oznaczać nic, jest port, który był używany dla wielu połączeń i jest nieznany administratora.</span><span class="sxs-lookup"><span data-stu-id="64bf2-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown to the administrator.</span></span>

![Rysunek 5][5]

### <a name="step-3"></a><span data-ttu-id="64bf2-178">Krok 3</span><span class="sxs-lookup"><span data-stu-id="64bf2-178">Step 3</span></span>

<span data-ttu-id="64bf2-179">Teraz, Ustaliliśmy jest za mało miejsca portu firma Microsoft można filtrować naszych przechwytywania na podstawie portu.</span><span class="sxs-lookup"><span data-stu-id="64bf2-179">Now that we have determined an out of place port we can filter our capture based on the port.</span></span>

<span data-ttu-id="64bf2-180">Filtr w tym scenariuszu należy:</span><span class="sxs-lookup"><span data-stu-id="64bf2-180">The filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="64bf2-181">Firma Microsoft wprowadź tekst filtr z powyższych w polu tekstowym filtru i naciśnij klawisz enter.</span><span class="sxs-lookup"><span data-stu-id="64bf2-181">We enter the filter text from above in the filter textbox and hit enter.</span></span>

![Rysunek 6.][6]

<span data-ttu-id="64bf2-183">Spośród wyników możemy można zauważyć, że cały ruch jest pochodzi z lokalnej maszyny wirtualnej w tej samej podsieci.</span><span class="sxs-lookup"><span data-stu-id="64bf2-183">From the results, we can see all the traffic is coming from a local virtual machine on the same subnet.</span></span> <span data-ttu-id="64bf2-184">Jeśli nadal nie Rozumiemy Dlaczego występuje ten ruch, możemy dalsze inspekcję pakietów w celu ustalenia, dlaczego jest wprowadzenie tych połączeń na porcie 111.</span><span class="sxs-lookup"><span data-stu-id="64bf2-184">If we still don’t understand why this traffic is occurring, we can further inspect the packets to determine why it is making these calls on port 111.</span></span> <span data-ttu-id="64bf2-185">Dzięki tym informacjom możemy podejmij odpowiednie działanie.</span><span class="sxs-lookup"><span data-stu-id="64bf2-185">With this information we can take the appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64bf2-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="64bf2-186">Next steps</span></span>

<span data-ttu-id="64bf2-187">Więcej informacji na temat innych funkcji diagnostycznych obserwatora sieciowego odwiedzając [omówienie monitorowania sieci platformy Azure](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="64bf2-187">Learn about the other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













