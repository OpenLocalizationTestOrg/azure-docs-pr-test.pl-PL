---
title: "wzorce ruchu w sieci aaaVisualize obserwatora sieciowego Azure i narzędzi typu open source | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera opis sposobu przechwytywania pakietów obserwatora sieciowego toouse z Capanalysis toovisualize ruchu wzorce tooand z maszyn wirtualnych."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a><span data-ttu-id="87a55-103">Wizualizuj tooand wzorce ruchu sieciowego z maszyn wirtualnych za pomocą narzędzi typu open source</span><span class="sxs-lookup"><span data-stu-id="87a55-103">Visualize network traffic patterns tooand from your VMs using open source tools</span></span>

<span data-ttu-id="87a55-104">Przechwytywanie pakietów zawierają dane sieci, które pozwalają danych dowodowych sieci tooperform i inspekcję pakietów.</span><span class="sxs-lookup"><span data-stu-id="87a55-104">Packet captures contain network data that allow you tooperform network forensics and deep packet inspection.</span></span> <span data-ttu-id="87a55-105">Istnieją otwiera wiele narzędzia źródła można użyć tooanalyze pakiet przechwyconych obrazów toogain insights dotyczących sieci użytkownika.</span><span class="sxs-lookup"><span data-stu-id="87a55-105">There are many opens source tools you can use tooanalyze packet captures toogain insights about your network.</span></span> <span data-ttu-id="87a55-106">Jednym z takich narzędzi jest CapAnalysis, narzędzie do wizualizacji przechwytywania pakietów typu open source.</span><span class="sxs-lookup"><span data-stu-id="87a55-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="87a55-107">Wizualizacja danych przechwytywania pakietów jest przydatna sposób tooquickly uzyskania szczegółowych informacji na wzorce i anomalii w sieci.</span><span class="sxs-lookup"><span data-stu-id="87a55-107">Visualizing packet capture data is a valuable way tooquickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="87a55-108">Wizualizacje również oferują możliwość udostępniania tych wgląd w sposób łatwo dostępne.</span><span class="sxs-lookup"><span data-stu-id="87a55-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="87a55-109">Zawiera obserwatora sieciowego Azure hello toocapture możliwości, który przechwytuje tego cennych danych, umożliwiając tooperform pakietów w sieci.</span><span class="sxs-lookup"><span data-stu-id="87a55-109">Azure’s Network Watcher provides you hello ability toocapture this valuable data by allowing you tooperform packet captures on your network.</span></span> <span data-ttu-id="87a55-110">W tym artykule firma Microsoft udostępnia Przewodnik jak toovisualize i uzyskanie wgląd w dane dotyczące pakietów przechwytuje przy użyciu CapAnalysis z obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="87a55-110">In this article, we provide a walkthrough of how toovisualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="87a55-111">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="87a55-111">Scenario</span></span>

<span data-ttu-id="87a55-112">Masz prostą aplikację sieci web wdrożone na maszynie Wirtualnej w toovisualize narzędzi typu open source toouse Azure chcesz jego tooquickly ruchu sieciowego zidentyfikować wzorce przepływu i wszelkich możliwych nieprawidłowości.</span><span class="sxs-lookup"><span data-stu-id="87a55-112">You have a simple web application deployed on a VM in Azure want toouse open source tools toovisualize its network traffic tooquickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="87a55-113">Z obserwatora sieciowego można uzyskać przechwytywania pakietów, środowiska sieci i zapisz go bezpośrednio na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="87a55-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="87a55-114">CapAnalysis można pozyskiwania hello przechwytywania pakietów bezpośrednio z obiektu blob magazynu hello i wizualizacji jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="87a55-114">CapAnalysis can then ingest hello packet capture directly from hello storage blob and visualize its contents.</span></span>

![scenariusz][1]

## <a name="steps"></a><span data-ttu-id="87a55-116">Kroki</span><span class="sxs-lookup"><span data-stu-id="87a55-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="87a55-117">Zainstaluj CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="87a55-117">Install CapAnalysis</span></span>

<span data-ttu-id="87a55-118">tooinstall CapAnalysis na maszynie wirtualnej, można odwoływać się instrukcje oficjalnego toohello https://www.capanalysis.net/ca/how-to-install-capanalysis tutaj.</span><span class="sxs-lookup"><span data-stu-id="87a55-118">tooinstall CapAnalysis on a virtual machine, you can refer toohello official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="87a55-119">W kolejności CapAnalysis zdalnego dostępu, potrzebujemy portu tooopen 9877 na maszynie Wirtualnej przez dodanie nowej reguły zabezpieczeń dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="87a55-119">In order access CapAnalysis remotely, we need tooopen port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="87a55-120">Aby uzyskać więcej informacji o tworzeniu reguł grup zabezpieczeń sieci, można znaleźć zbyt[tworzenia reguł w istniejącej grupy NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="87a55-120">For more about creating rules in Network Security Groups, refer too[Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="87a55-121">Po została pomyślnie dodana reguła hello, powinno być możliwe tooaccess CapAnalysis z`http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="87a55-121">Once hello rule has been successfully added, you should be able tooaccess CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a><span data-ttu-id="87a55-122">Użyj toostart obserwatora sieciowego Azure sesji przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="87a55-122">Use Azure Network Watcher toostart a packet capture session</span></span>

<span data-ttu-id="87a55-123">Obserwatora sieciowego umożliwia toocapture pakiety tootrack ruch do i z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="87a55-123">Network Watcher allows you toocapture packets tootrack traffic in and out of a virtual machine.</span></span> <span data-ttu-id="87a55-124">Może się odwoływać toohello instrukcje [Przechwytywanie pakietów zarządzania z obserwatora sieciowego](network-watcher-packet-capture-manage-portal.md) toostart sesję przechwytywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="87a55-124">You can refer toohello instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) toostart a packet capture session.</span></span> <span data-ttu-id="87a55-125">To Przechwytywanie pakietów mogą być przechowywane w toobe obiektu blob magazynu, CapAnalysis z niego.</span><span class="sxs-lookup"><span data-stu-id="87a55-125">This packet capture can be stored in a storage blob toobe accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-toocapanalysis"></a><span data-ttu-id="87a55-126">Przekaż tooCapAnalysis przechwytywania pakietów</span><span class="sxs-lookup"><span data-stu-id="87a55-126">Upload a packet capture tooCapAnalysis</span></span>
<span data-ttu-id="87a55-127">Możesz przekazać bezpośrednio przechwytywania pakietów, wykonywaną przez obserwatora sieciowego przy użyciu karty "Z adresu URL importowania" hello i zapewnianie obiektu blob magazynu toohello łącza, gdzie przechwytywania pakietów hello jest przechowywany.</span><span class="sxs-lookup"><span data-stu-id="87a55-127">You can directly upload a packet capture taken by network watcher using hello “Import from URL” tab and providing a link toohello storage blob where hello packet capture is stored.</span></span>

<span data-ttu-id="87a55-128">Podczas dostarczania tooCapAnalysis łącza, upewnij się, że tooappend adres URL SAS tokenu toohello magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="87a55-128">When providing a link tooCapAnalysis, make sure tooappend a SAS token toohello storage blob URL.</span></span>  <span data-ttu-id="87a55-129">toodo, przejdź tooShared sygnatury dostępu z konta magazynu hello, wyznaczyć hello uprawnienia i naciśnij klawisz toocreate przycisk Generuj SAS hello tokenu.</span><span class="sxs-lookup"><span data-stu-id="87a55-129">toodo this, navigate tooShared access signature from hello storage account, designate hello allowed permissions, and press hello Generate SAS button toocreate a token.</span></span> <span data-ttu-id="87a55-130">Następnie można dodać ten token toohello pakietów przechwytywania magazynu obiektów blob adres URL SAS.</span><span class="sxs-lookup"><span data-stu-id="87a55-130">You can then append this SAS token toohello packet capture storage blob URL.</span></span>

<span data-ttu-id="87a55-131">Witaj wynikowego adresu URL będzie wyglądać następująco: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="87a55-131">hello resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="87a55-132">Przechwytywanie analizowania pakietów</span><span class="sxs-lookup"><span data-stu-id="87a55-132">Analyzing packet captures</span></span>

<span data-ttu-id="87a55-133">CapAnalysis oferuje różne opcje toovisualize Twojego przechwytywania pakietów, każda udostępnienie analiza z różnych perspektyw.</span><span class="sxs-lookup"><span data-stu-id="87a55-133">CapAnalysis offers various options toovisualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="87a55-134">Te podsumowania visual możesz zrozumieć trendy ruchu sieciowego i szybko dodatkowe wszelkie nietypowe działania związane z.</span><span class="sxs-lookup"><span data-stu-id="87a55-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="87a55-135">Niektóre z tych funkcji są wyświetlane w hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="87a55-135">A few of these features are shown in hello following list:</span></span>

1. <span data-ttu-id="87a55-136">Tabele przepływu</span><span class="sxs-lookup"><span data-stu-id="87a55-136">Flow Tables</span></span>

    <span data-ttu-id="87a55-137">Dzięki temu tabeli hello listy przepływów danych pakietów hello, hello sygnatura czasowa skojarzona z przepływami hello i hello różnych protokołów powiązanych z przepływem hello, a także źródłowego i docelowego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="87a55-137">This table gives you hello list of flows in hello packet data, hello time stamp associated with hello flows and hello various protocols associated with hello flow, as well as source and destination IP.</span></span>

    ![Strona przepływu capanalysis][5]

1. <span data-ttu-id="87a55-139">Omówienie protokołu</span><span class="sxs-lookup"><span data-stu-id="87a55-139">Protocol Overview</span></span>

    <span data-ttu-id="87a55-140">W tym okienku pozwala tooquickly Zobacz dystrybucji hello ruchu sieciowego za pośrednictwem hello różnych protokołów i lokalizacji geograficznych.</span><span class="sxs-lookup"><span data-stu-id="87a55-140">This pane allows you tooquickly see hello distribution of network traffic over hello various protocols and geographies.</span></span>

    ![Omówienie protokołu capanalysis][6]

1. <span data-ttu-id="87a55-142">Statystyki</span><span class="sxs-lookup"><span data-stu-id="87a55-142">Statistics</span></span>

    <span data-ttu-id="87a55-143">W tym okienku umożliwia statystyki ruchu sieciowego tooview — bajtów wysłanych i odebranych z źródłowe i docelowe adresy IP, przepływów dla każdego z hello źródłowe i docelowe adresy IP, protokół używany dla różnych przepływów i czas trwania hello przepływów.</span><span class="sxs-lookup"><span data-stu-id="87a55-143">This pane allows you tooview network traffic statistics – bytes sent and received from source and destination IPs, flows for each of hello source and destination IPs, protocol used for various flows, and hello duration of flows.</span></span>

    ![statystyki capanalysis][7]

1. <span data-ttu-id="87a55-145">geomap</span><span class="sxs-lookup"><span data-stu-id="87a55-145">Geomap</span></span>

    <span data-ttu-id="87a55-146">W tym okienku zawiera widoku mapy ruchu sieciowego, z kolorami skalowanie toohello ilość ruchu każdego z krajów.</span><span class="sxs-lookup"><span data-stu-id="87a55-146">This pane provides you with a map view of your network traffic, with colors scaling toohello volume of traffic from each country.</span></span> <span data-ttu-id="87a55-147">Możesz wybrać wyróżnione krajach tooview przepływu dodatkowe statystyki takich jak hello część danych wysłanych i odebranych z adresów IP, w tym kraju.</span><span class="sxs-lookup"><span data-stu-id="87a55-147">You can select highlighted countries tooview additional flow statistics such as hello proportion of data sent and received from IPs in that country.</span></span>

    ![geomap][8]

1. <span data-ttu-id="87a55-149">Filtry</span><span class="sxs-lookup"><span data-stu-id="87a55-149">Filters</span></span>

    <span data-ttu-id="87a55-150">CapAnalysis zawiera zestaw filtrów do szybkiego analizy określonych pakietów.</span><span class="sxs-lookup"><span data-stu-id="87a55-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="87a55-151">Na przykład można toofilter hello danych przez protokół toogain określonych szczegółowych informacji na ten podzestaw ruchu.</span><span class="sxs-lookup"><span data-stu-id="87a55-151">For example, you can choose toofilter hello data by protocol toogain specific insights on that subset of traffic.</span></span>

    ![filtry][11]

    <span data-ttu-id="87a55-153">Odwiedź stronę [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn więcej informacji na temat wszystkich CapAnalysis możliwości.</span><span class="sxs-lookup"><span data-stu-id="87a55-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="87a55-154">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="87a55-154">Conclusion</span></span>

<span data-ttu-id="87a55-155">Funkcja przechwytywania pakietów obserwatora sieciowego umożliwia toocapture hello danych konieczne tooperform sieci dowodowe oraz lepsze zrozumienie ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="87a55-155">Network Watcher’s packet capture feature allows you toocapture hello data necessary tooperform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="87a55-156">W tym scenariuszu firma Microsoft pokazano, jak przechwytywanie pakietów z obserwatora sieciowego łatwo można zintegrować z narzędzi wizualizacji typu open source.</span><span class="sxs-lookup"><span data-stu-id="87a55-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="87a55-157">Za pomocą narzędzi typu open source, takie jak przechwytuje CapAnalysis toovisualize pakietów, możesz głębokiej inspekcji pakietów i szybkie Określanie trendów w ramach ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="87a55-157">By using open source tools such as CapAnalysis toovisualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87a55-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="87a55-158">Next steps</span></span>

<span data-ttu-id="87a55-159">toolearn więcej informacji na temat dzienniki przepływu NSG, odwiedź stronę [dzienniki przepływu NSG](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="87a55-159">toolearn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="87a55-160">Dowiedz się, jak toovisualize Twojego przepływu NSG dzienniki przy użyciu usługi Power BI odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="87a55-160">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
