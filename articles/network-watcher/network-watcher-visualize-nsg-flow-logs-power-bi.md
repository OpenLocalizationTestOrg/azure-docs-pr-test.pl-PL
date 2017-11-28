---
title: "rejestruje aaaVisualizing przepływu grupy zabezpieczeń sieci Azure przy użyciu usługi Power BI | Dokumentacja firmy Microsoft"
description: "Na tej stronie opisano sposób rejestrowania toovisualize NSG przepływu z usługi Power BI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="4f365-103">Dzienniki przepływu visualizing sieciową grupę zabezpieczeń z usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="4f365-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="4f365-104">Grupy zabezpieczeń sieci przepływu dzienniki pozwalają tooview informacje na temat przychodzące i wychodzące ruchu IP na grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="4f365-104">Network Security Group flow logs allow you tooview information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="4f365-105">Te dzienniki przepływu Pokaż wychodzących i przepływów przychodzących na podstawie reguł na, hello kart hello przepływu dotyczy, 5-elementowej informacji na temat przepływu hello (źródłowego i docelowego adresu IP, portu źródłowego i docelowego protokołu), i jeśli ruch hello został dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="4f365-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="4f365-106">Może być trudne toogain wgląd w informacje rejestrowania danych przez ręcznie wyszukiwania plików dziennika hello przepływu.</span><span class="sxs-lookup"><span data-stu-id="4f365-106">It can be difficult toogain insights into flow logging data by manually searching hello log files.</span></span> <span data-ttu-id="4f365-107">W tym artykule udostępniamy toovisualize rozwiązania z najnowszych przepływ dzienniki i Dowiedz się więcej o ruchu w sieci.</span><span class="sxs-lookup"><span data-stu-id="4f365-107">In this article, we provide a solution toovisualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="4f365-108">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="4f365-108">Scenario</span></span>

<span data-ttu-id="4f365-109">Powitania od scenariusza połączymy konto magazynu pulpitu toohello usługi Power BI, którego możemy skonfigurowano jako hello odbioru dla grupy NSG przepływu rejestrowania danych.</span><span class="sxs-lookup"><span data-stu-id="4f365-109">In hello following scenario, we connect Power BI desktop toohello storage account we have configured as hello sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="4f365-110">Po połączymy tooour konta magazynu usługi Power BI pobiera i analizuje tooprovide dzienniki hello wizualną reprezentację hello ruchu, który jest rejestrowane przez grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="4f365-110">After we connect tooour storage account, Power BI downloads and parses hello logs tooprovide a visual representation of hello traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="4f365-111">Przy użyciu elementów wizualnych hello podane w szablonie hello, który można sprawdzić:</span><span class="sxs-lookup"><span data-stu-id="4f365-111">Using hello visuals supplied in hello template you can examine:</span></span>

* <span data-ttu-id="4f365-112">Górny Talkers</span><span class="sxs-lookup"><span data-stu-id="4f365-112">Top Talkers</span></span>
* <span data-ttu-id="4f365-113">Czas serii przepływu danych decyzją kierunek i reguły</span><span class="sxs-lookup"><span data-stu-id="4f365-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="4f365-114">Przepływy według adresu MAC interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="4f365-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="4f365-115">Przepływy NSG i reguły</span><span class="sxs-lookup"><span data-stu-id="4f365-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="4f365-116">Przepływy przez Port docelowy</span><span class="sxs-lookup"><span data-stu-id="4f365-116">Flows by Destination Port</span></span>

<span data-ttu-id="4f365-117">dostarczonego szablonu Hello jest edytowalny, więc można modyfikować tooadd nowe dane, elementy wizualne, lub edytowanie zapytań toosuit potrzeb.</span><span class="sxs-lookup"><span data-stu-id="4f365-117">hello template provided is editable so you can modify it tooadd new data, visuals, or edit queries toosuit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="4f365-118">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="4f365-118">Setup</span></span>

<span data-ttu-id="4f365-119">Przed rozpoczęciem, musi mieć sieci grupy przepływu rejestrowanie zabezpieczeń włączone w jednej lub wielu grup zabezpieczeń sieci na Twoim koncie.</span><span class="sxs-lookup"><span data-stu-id="4f365-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="4f365-120">Instrukcje dotyczące włączania zabezpieczenia sieci przepływu dzienniki, można znaleźć toohello poniższego artykułu: [wprowadzenie tooflow rejestrowania dla grup zabezpieczeń sieci](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4f365-120">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="4f365-121">Musi mieć również hello Power BI Desktop zainstalowanego klienta na komputerze i wystarczającej ilości wolnego miejsca na maszynie toodownload obciążenia hello dziennika danych i czy istnieje na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="4f365-121">You must also have hello Power BI Desktop client installed on your machine, and enough free space on your machine toodownload and load hello log data that exists in your storage account.</span></span>

![Diagram programu Visio][1]

### <a name="steps"></a><span data-ttu-id="4f365-123">Kroki</span><span class="sxs-lookup"><span data-stu-id="4f365-123">Steps</span></span>

1. <span data-ttu-id="4f365-124">Pobierz i otwórz hello następującego szablonu usługi Power BI w programie Power BI Desktop aplikacji hello [przepływu PowerBI obserwatora sieciowego rejestruje szablonu](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="4f365-124">Download and open hello following Power BI template in hello Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="4f365-125">Wprowadź hello wymaganych parametrów zapytania</span><span class="sxs-lookup"><span data-stu-id="4f365-125">Enter hello required Query parameters</span></span>
    1. <span data-ttu-id="4f365-126">**StorageAccountName** — Określa nazwę toohello hello konta magazynu zawierającego przepływ NSG hello dzienniki, które chcesz tooload i wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="4f365-126">**StorageAccountName** – Specifies toohello name of hello storage account containing hello NSG flow logs that you would like tooload and visualize.</span></span>
    1. <span data-ttu-id="4f365-127">**NumberOfLogFiles** — określa hello liczbę plików dziennika, że chcesz toodownload i wizualizacji w usłudze Power BI.</span><span class="sxs-lookup"><span data-stu-id="4f365-127">**NumberOfLogFiles** – Specifies hello number of log files that you would like toodownload and visualize in Power BI.</span></span> <span data-ttu-id="4f365-128">Na przykład jeśli określono 50, hello 50 najnowszych plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="4f365-128">For example, if 50 is specified, hello 50 latest log files.</span></span> <span data-ttu-id="4f365-129">Mamy 2 grup NSG FF włączona i skonfigurowana toosend NSG przepływu dzienniki toothis konta, a następnie hello ostatnich 25 godzin dzienników mogą być wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="4f365-129">Ff we have 2 NSGs enabled and configured toosend NSG flow logs toothis account, then hello past 25 hours of logs can be viewed.</span></span>

    ![main Power BI][2]

1. <span data-ttu-id="4f365-131">Wprowadź hello klucza dostępu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="4f365-131">Enter hello Access Key for your storage account.</span></span> <span data-ttu-id="4f365-132">Klawisze dostępu prawidłowy można znaleźć przechodząc tooyour konta magazynu w hello Azure portalu i wybierając **klucze dostępu** z menu ustawień hello.</span><span class="sxs-lookup"><span data-stu-id="4f365-132">You can find valid access keys by navigating tooyour storage account in hello Azure portal and selecting **Access Keys** from hello Settings menu.</span></span> <span data-ttu-id="4f365-133">Kliknij przycisk **Connect** następnie zastosować zmiany.</span><span class="sxs-lookup"><span data-stu-id="4f365-133">Click **Connect** then apply changes.</span></span>

    ![Klawisze dostępu][3]

    ![klucz dostępu 2][4]

4.  <span data-ttu-id="4f365-136">Dzienniki są pobrać i przeanalizować i mogą teraz wykorzystywać hello wstępnie utworzone elementy wizualne.</span><span class="sxs-lookup"><span data-stu-id="4f365-136">Your logs are download and parsed and you can now utilize hello pre-created visuals.</span></span>

## <a name="understanding-hello-visuals"></a><span data-ttu-id="4f365-137">Opis elementów wizualnych hello</span><span class="sxs-lookup"><span data-stu-id="4f365-137">Understanding hello visuals</span></span>

<span data-ttu-id="4f365-138">Zakładając, że w hello są szablonu zbiór elementów wizualnych, które pomagają sensu hello NSG przepływu danych.</span><span class="sxs-lookup"><span data-stu-id="4f365-138">Provided in hello template are a set of visuals that help make sense of hello NSG Flow Log data.</span></span> <span data-ttu-id="4f365-139">Witaj poniższych ilustracjach przedstawiono przykładowe jakie pulpitu nawigacyjnego hello wygląda po wypełniane przy użyciu danych.</span><span class="sxs-lookup"><span data-stu-id="4f365-139">hello following images show a sample of what hello dashboard looks like when populated with data.</span></span> <span data-ttu-id="4f365-140">Poniżej omówione każdego visual większej liczby szczegółów</span><span class="sxs-lookup"><span data-stu-id="4f365-140">Below we examine each visual in greater detail</span></span> 

![Usługa Power BI][5]
 
<span data-ttu-id="4f365-142">Witaj Talkers górnej visual pokazuje hello adresów IP, zainicjowane hello większość połączeń za pośrednictwem hello podanego okresu.</span><span class="sxs-lookup"><span data-stu-id="4f365-142">hello Top Talkers visual shows hello IPs that have initiated hello most connections over hello period specified.</span></span> <span data-ttu-id="4f365-143">rozmiar Hello pól hello odpowiada toohello względną liczbę połączeń.</span><span class="sxs-lookup"><span data-stu-id="4f365-143">hello size of hello boxes corresponds toohello relative number of connections.</span></span> 

![toptalkers][6]

<span data-ttu-id="4f365-145">Witaj następujące czasu serii wykresów Pokaż hello liczbę przepływów w okresie hello.</span><span class="sxs-lookup"><span data-stu-id="4f365-145">hello following time series graphs show hello number of flows over hello period.</span></span> <span data-ttu-id="4f365-146">Wykres górny Hello jest segmentowanych przez kierunek przepływu hello i hello niższe jest segmentem decyzją hello (Zezwalaj lub Odmów).</span><span class="sxs-lookup"><span data-stu-id="4f365-146">hello upper graph is segmented by hello flow direction, and hello lower is segmented by hello decision made (allow or deny).</span></span> <span data-ttu-id="4f365-147">Z tego elementu wizualnego można przejrzeć trendy ruchu wraz z upływem czasu i dodatkowe żadnych nietypowych wzrostów lub spadek ruchu lub segmentacji ruchu.</span><span class="sxs-lookup"><span data-stu-id="4f365-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flowsoverperiod][7]

<span data-ttu-id="4f365-149">Hello następujące wykresy wyświetlanych przepływów hello na interfejsu sieciowego, hello górny segmentowanych przez kierunek przepływu i hello niższe segmentowanych przez decyzji.</span><span class="sxs-lookup"><span data-stu-id="4f365-149">hello following graphs show hello flows per Network interface, with hello upper segmented by flow direction and hello lower segmented by decision made.</span></span> <span data-ttu-id="4f365-150">Dzięki tym informacjom można uzyskać wgląd w której maszyny wirtualne przekazywane hello większości tooothers względną, a jeśli tooa ruchu określonej maszyny Wirtualnej są dozwolone lub nie.</span><span class="sxs-lookup"><span data-stu-id="4f365-150">With this information, you can gain insights into which of your VMs communicated hello most relative tooothers, and if traffic tooa specific VM is being allowed or denied.</span></span>

![flowspernic][8]

<span data-ttu-id="4f365-152">powitania po wykres pierścieniowy przedstawiający koło pokazuje podział przepływów przez Port docelowy.</span><span class="sxs-lookup"><span data-stu-id="4f365-152">hello following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="4f365-153">Dzięki tym informacjom można wyświetlić hello najczęściej używane porty docelowe używane w ramach hello określony okres.</span><span class="sxs-lookup"><span data-stu-id="4f365-153">With this information, you can view hello most commonly used destination ports used within hello specified period.</span></span>

![pierścień][9]

<span data-ttu-id="4f365-155">Witaj następujące wykres słupkowy zawiera hello przepływu NSG i reguły.</span><span class="sxs-lookup"><span data-stu-id="4f365-155">hello following bar chart shows hello Flow by NSG and Rule.</span></span> <span data-ttu-id="4f365-156">Dzięki tym informacjom widać hello grup NSG odpowiedzialny za hello większość ruchu sieciowego i podział hello ruchu na grupy NSG przez regułę.</span><span class="sxs-lookup"><span data-stu-id="4f365-156">With this information, you can see hello NSGs responsible for hello most traffic, and hello breakdown of traffic on an NSG by rule.</span></span>

![barchart][10]
 
<span data-ttu-id="4f365-158">Hello następujące informacyjną wykresy wyświetlania informacje na temat grup NSG hello znajdujących się w dziennikach hello, hello liczba przepływów przechwycone przez okres hello oraz Data hello hello dziennika najwcześniejszą przechwytywane.</span><span class="sxs-lookup"><span data-stu-id="4f365-158">hello following informational charts display information about hello NSGs present in hello logs, hello number of Flows captured over hello period, and hello date of hello earliest log captured.</span></span> <span data-ttu-id="4f365-159">Ta informacja daje wyobrażenie o jakie grupy NSG są rejestrowane i hello zakres dat przepływów.</span><span class="sxs-lookup"><span data-stu-id="4f365-159">This information gives you an idea of what NSGs are being logged and hello date range of flows.</span></span>

![infochart1][11]

![infochart2][12]

<span data-ttu-id="4f365-162">Ten szablon obejmuje hello następujących tooallow fragmentatory możesz tooview wyłącznie dane hello najbardziej planuje się.</span><span class="sxs-lookup"><span data-stu-id="4f365-162">This template includes hello following slicers tooallow you tooview only hello data you are most interested in.</span></span> <span data-ttu-id="4f365-163">Można filtrować według grup zasobów, grup NSG i zasady.</span><span class="sxs-lookup"><span data-stu-id="4f365-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="4f365-164">Można również filtrować informacji 5-elementowej, decyzji i czas hello hello dziennik został zapisany.</span><span class="sxs-lookup"><span data-stu-id="4f365-164">You can also filter on 5-tuple information, decision, and hello time hello log was written.</span></span>

![fragmentatory][13]

## <a name="conclusion"></a><span data-ttu-id="4f365-166">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="4f365-166">Conclusion</span></span>

<span data-ttu-id="4f365-167">Firma Microsoft pokazano w tym scenariuszu czy przy użyciu dzienników przepływu grupy zabezpieczeń sieci zapewniane przez obserwatora sieciowego i usługi Power BI, firma Microsoft są w stanie toovisualize i zrozumieć hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="4f365-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able toovisualize and understand hello traffic.</span></span> <span data-ttu-id="4f365-168">Przy użyciu szablonu hello podane usługi Power BI pobiera dzienniki hello bezpośrednio z magazynu i przetwarza je lokalnie.</span><span class="sxs-lookup"><span data-stu-id="4f365-168">Using hello provided template, Power BI downloads hello logs directly from storage and processes them locally.</span></span> <span data-ttu-id="4f365-169">Czas poświęcony na tooload hello szablonu różni się w zależności od liczby hello żądane pliki i pobrać łączny rozmiar plików.</span><span class="sxs-lookup"><span data-stu-id="4f365-169">Time taken tooload hello template varies depending on hello number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="4f365-170">Możesz wolnego toocustomize tego szablonu do własnych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="4f365-170">Feel free toocustomize this template for your needs.</span></span> <span data-ttu-id="4f365-171">Istnieje wiele sposobów wiele, że za pomocą usługi Power BI dzienniki przepływu grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="4f365-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="4f365-172">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4f365-172">Notes</span></span>

* <span data-ttu-id="4f365-173">Dzienniki domyślnie są przechowywane w`https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="4f365-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="4f365-174">Jeśli istnieją inne dane w innym katalogu one hello toopull zapytań i przetwarzania danych hello muszą zostać zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="4f365-174">If other data exists in another directory they hello queries toopull and process hello data must be modified.</span></span>

* <span data-ttu-id="4f365-175">Hello podany szablon nie jest zalecane używanie z dzienników z ponad 1 GB.</span><span class="sxs-lookup"><span data-stu-id="4f365-175">hello provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="4f365-176">Jeśli masz dużą ilość dzienniki, firma Microsoft zaleca, aby zbadać rozwiązania za pomocą innego magazynu danych, takich jak Data Lake lub SQL server.</span><span class="sxs-lookup"><span data-stu-id="4f365-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f365-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4f365-177">Next Steps</span></span>

<span data-ttu-id="4f365-178">Dowiedz się, jak toovisualize Twojego przepływu NSG dzienniki z hello Elastick stosu odwiedzając [wizualizacji tooand wzorce ruchu sieciowego z maszyn wirtualnych za pomocą narzędzi typu open source](network-watcher-using-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="4f365-178">Learn how toovisualize your NSG flow logs with hello Elastick Stack by visiting [Visualize network traffic patterns tooand from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
