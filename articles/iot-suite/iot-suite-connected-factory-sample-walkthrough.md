---
title: "wskazówki rozwiązania pakiet IoT Azure fabryki aaaConnected | Dokumentacja firmy Microsoft"
description: "Opis hello Azure IoT wstępnie skonfigurowane rozwiązanie połączone architektura jej i fabryki."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="89b1e-103">Przewodnik po wstępnie skonfigurowanym rozwiązaniu połączonej fabryki</span><span class="sxs-lookup"><span data-stu-id="89b1e-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="89b1e-104">Witaj pakiet IoT połączone fabryki [wstępnie skonfigurowane rozwiązanie] [ lnk-preconfigured-solutions] jest implementacją rozwiązania przemysłowych end-to-end który:</span><span class="sxs-lookup"><span data-stu-id="89b1e-104">hello IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="89b1e-105">Łączy tooboth symulowane urządzeń przemysłowych uruchamiania OPC UA serwerów w wierszach produkcji symulowane fabryki i rzeczywistego urządzenia server OPC UA.</span><span class="sxs-lookup"><span data-stu-id="89b1e-105">Connects tooboth simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="89b1e-106">Aby uzyskać więcej informacji na temat OPC UA Zobacz hello [połączone fabryki — często zadawane pytania](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="89b1e-106">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="89b1e-107">Pokazuje operacyjne kluczowe wskaźniki wydajności oraz ogólną wydajność sprzętu dla tych urządzeń i linii produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="89b1e-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="89b1e-108">Pokazuje, jak można toointeract używanych w systemach server OPC UA aplikacji opartej na chmurze.</span><span class="sxs-lookup"><span data-stu-id="89b1e-108">Demonstrates how a cloud-based application could be used toointeract with OPC UA server systems.</span></span>
* <span data-ttu-id="89b1e-109">Umożliwia tooconnect możesz własnych urządzeń serwera OPC UA.</span><span class="sxs-lookup"><span data-stu-id="89b1e-109">Enables you tooconnect your own OPC UA server devices.</span></span>
* <span data-ttu-id="89b1e-110">Umożliwia toobrowse i zmodyfikuj hello OPC UA danych serwera.</span><span class="sxs-lookup"><span data-stu-id="89b1e-110">Enables you toobrowse and modify hello OPC UA server data.</span></span>
* <span data-ttu-id="89b1e-111">Integruje się z hello Azure czas serii Insights (TSI) usługi tooprovide niestandardowych widoków danych hello z serwerów OPC UA.</span><span class="sxs-lookup"><span data-stu-id="89b1e-111">Integrates with hello Azure Time Series Insights (TSI) service tooprovide customized views of hello data from your OPC UA servers.</span></span>

<span data-ttu-id="89b1e-112">Za pomocą hello rozwiązania jako punkt początkowy dla własnego implementacji i [dostosować] [ lnk-customize] on toomeet własnych konkretnych potrzeb biznesowych.</span><span class="sxs-lookup"><span data-stu-id="89b1e-112">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="89b1e-113">W tym artykule przedstawiono niektóre kluczowe elementy hello hello połączone fabryki rozwiązania tooenable toounderstand jej działania.</span><span class="sxs-lookup"><span data-stu-id="89b1e-113">This article walks you through some of hello key elements of hello connected factory solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="89b1e-114">Ta wiedza ułatwi Ci:</span><span class="sxs-lookup"><span data-stu-id="89b1e-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="89b1e-115">Rozwiązywanie problemów w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="89b1e-115">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="89b1e-116">Planowanie sposobu toocustomize toohello rozwiązania toomeet indywidualnymi wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="89b1e-116">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span>
* <span data-ttu-id="89b1e-117">Projektowanie własnego rozwiązania IoT korzystającego z usług Azure.</span><span class="sxs-lookup"><span data-stu-id="89b1e-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="89b1e-118">Aby uzyskać więcej informacji, zobacz hello [połączone fabryki — często zadawane pytania](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="89b1e-118">For more information, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="89b1e-119">Architektura logiczna</span><span class="sxs-lookup"><span data-stu-id="89b1e-119">Logical architecture</span></span>

<span data-ttu-id="89b1e-120">powitania po diagram przedstawia hello logiczne składniki hello wstępnie skonfigurowane rozwiązanie:</span><span class="sxs-lookup"><span data-stu-id="89b1e-120">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Architektura logiczna połączonej fabryki][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="89b1e-122">Wzorce komunikacji</span><span class="sxs-lookup"><span data-stu-id="89b1e-122">Communication patterns</span></span>

<span data-ttu-id="89b1e-123">rozwiązanie Hello używa hello [specyfikacji UA OPC Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend tooIoT danych telemetrycznych OPC UA Centrum w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="89b1e-123">hello solution uses hello [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetry data tooIoT Hub in JSON format.</span></span> <span data-ttu-id="89b1e-124">rozwiązanie Hello używa hello [wydawcy OPC](https://github.com/Azure/iot-edge-opc-publisher) krawędzi IoT modułu, w tym celu.</span><span class="sxs-lookup"><span data-stu-id="89b1e-124">hello solution uses hello [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="89b1e-125">rozwiązanie Hello ma również klienta OPC UA zintegrowany z aplikacją sieci web, który może nawiązywać połączenia z serwerami lokalnymi OPC UA.</span><span class="sxs-lookup"><span data-stu-id="89b1e-125">hello solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="89b1e-126">Witaj, klient używa [wstecznego serwera proxy](https://wikipedia.org/wiki/Reverse_proxy) i odbiera pomocy z Centrum IoT toomake hello połączenia bez konieczności otwartych portów w zaporze lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="89b1e-126">hello client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub toomake hello connection without requiring open ports in hello on-premises firewall.</span></span> <span data-ttu-id="89b1e-127">Ten wzorzec komunikacji jest zwany [komunikacją wspieraną przez usługę](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span><span class="sxs-lookup"><span data-stu-id="89b1e-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="89b1e-128">rozwiązanie Hello używa hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) krawędzi IoT modułu, w tym celu.</span><span class="sxs-lookup"><span data-stu-id="89b1e-128">hello solution uses hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="89b1e-129">Symulacja</span><span class="sxs-lookup"><span data-stu-id="89b1e-129">Simulation</span></span>

<span data-ttu-id="89b1e-130">Witaj symulowane stacji i wykonywania produkcyjnym hello symulowane systemów (rynkowej) tworzą wiersza produkcyjnym fabryki.</span><span class="sxs-lookup"><span data-stu-id="89b1e-130">hello simulated stations and hello simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="89b1e-131">Witaj symulowanego urządzenia i hello modułu wydawcy OPC są oparte na powitania [OPC UA .NET Standard] [ lnk-OPC-UA-NET-Standard] opublikowanych przez hello OPC Foundation.</span><span class="sxs-lookup"><span data-stu-id="89b1e-131">hello simulated devices and hello OPC Publisher Module are based on hello [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by hello OPC Foundation.</span></span>

<span data-ttu-id="89b1e-132">Witaj OPC serwera Proxy i OPC wydawcy są zaimplementowane jako modułów na podstawie [Azure IoT krawędzi][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="89b1e-132">hello OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="89b1e-133">Każda symulowana linia produkcyjna ma dołączoną wyznaczoną bramę.</span><span class="sxs-lookup"><span data-stu-id="89b1e-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="89b1e-134">Wszystkie składniki symulacji działają w kontenerach platformy Docker hostowanych na maszynie wirtualnej platformy Azure z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="89b1e-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="89b1e-135">symulacji Hello jest skonfigurowany toorun osiem symulowane wiersze produkcji domyślnie.</span><span class="sxs-lookup"><span data-stu-id="89b1e-135">hello simulation is configured toorun eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="89b1e-136">Symulowana linia produkcyjna</span><span class="sxs-lookup"><span data-stu-id="89b1e-136">Simulated production line</span></span>

<span data-ttu-id="89b1e-137">Na linii produkcyjnej są produkowane części.</span><span class="sxs-lookup"><span data-stu-id="89b1e-137">A production line manufactures parts.</span></span> <span data-ttu-id="89b1e-138">Składa się ona z różnych stacji: stacji montażowej, stacji testowania i stacji pakowania.</span><span class="sxs-lookup"><span data-stu-id="89b1e-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="89b1e-139">Symulacja Hello uruchamia i aktualizuje dane hello udostępniane za pośrednictwem hello OPC UA węzłów.</span><span class="sxs-lookup"><span data-stu-id="89b1e-139">hello simulation runs and updates hello data that is exposed through hello OPC UA nodes.</span></span> <span data-ttu-id="89b1e-140">Wszystkie stacje symulowane wiersza produkcyjnym są zorkiestrowana przez hello rynkowej za pośrednictwem OPC UA.</span><span class="sxs-lookup"><span data-stu-id="89b1e-140">All simulated production line stations are orchestrated by hello MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="89b1e-141">Symulowany system zarządzania produkcją</span><span class="sxs-lookup"><span data-stu-id="89b1e-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="89b1e-142">Witaj rynkowej monitoruje każdej stacji wiersza produkcyjnym hello za pośrednictwem zmiany stanu stacji toodetect OPC UA.</span><span class="sxs-lookup"><span data-stu-id="89b1e-142">hello MES monitors each station in hello production line through OPC UA toodetect station status changes.</span></span> <span data-ttu-id="89b1e-143">Wywołuje OPC UA metody toocontrol hello stacji, a przekazuje produktu z jednej stacji toohello dalej do czasu ukończenia.</span><span class="sxs-lookup"><span data-stu-id="89b1e-143">It calls OPC UA methods toocontrol hello stations and passes a product from one station toohello next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="89b1e-144">Moduł wydawcy OPC bramy</span><span class="sxs-lookup"><span data-stu-id="89b1e-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="89b1e-145">Moduł wydawcy OPC łączy toohello stacji OPC UA serwery i subskrybuje toobe węzłów OPC toohello opublikowane.</span><span class="sxs-lookup"><span data-stu-id="89b1e-145">OPC Publisher Module connects toohello station OPC UA servers and subscribes toohello OPC nodes toobe published.</span></span> <span data-ttu-id="89b1e-146">Moduł Hello konwertuje hello węzeł danych do formatu JSON, szyfruje go i wysyła tooIoT koncentratora jako OPC UA Pub/komunikatów.</span><span class="sxs-lookup"><span data-stu-id="89b1e-146">hello module converts hello node data into JSON format, encrypts it, and sends it tooIoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="89b1e-147">Moduł wydawcy OPC Hello tylko wymaga port wychodzący protokołu https (port 443) i może współpracować z istniejącej infrastruktury przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="89b1e-147">hello OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="89b1e-148">Moduł serwera proxy OPC bramy</span><span class="sxs-lookup"><span data-stu-id="89b1e-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="89b1e-149">Hello modułu Proxy UA OPC bramy tuneli binarne OPC UA polecenia i kontroli wiadomości i wymaga tylko port wychodzący protokołu https (port 443).</span><span class="sxs-lookup"><span data-stu-id="89b1e-149">hello Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="89b1e-150">Może on współdziałać z istniejącą infrastrukturą przedsiębiorstwa, w tym z internetowymi serwerami proxy.</span><span class="sxs-lookup"><span data-stu-id="89b1e-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="89b1e-151">Używa urządzenia IoT Hub metody tootransfer packetized TCP/IP danych w warstwie aplikacji hello, a w związku z tym zapewnia punkt końcowy relacji zaufania, szyfrowania danych i integralności przy użyciu protokołu SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="89b1e-151">It uses IoT Hub Device methods tootransfer packetized TCP/IP data at hello application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="89b1e-152">Hello OPC UA protokołu binarnego przekazywane za pośrednictwem serwera proxy hello, sama używa UA uwierzytelniania i szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="89b1e-152">hello OPC UA binary protocol relayed through hello proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="89b1e-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="89b1e-153">Azure Time Series Insights</span></span>

<span data-ttu-id="89b1e-154">Witaj bramy OPC wydawcy modułu subskrybuje tooOPC UA serwera węzłów toodetect zmianę hello wartości danych.</span><span class="sxs-lookup"><span data-stu-id="89b1e-154">hello Gateway OPC Publisher Module subscribes tooOPC UA server nodes toodetect change in hello data values.</span></span> <span data-ttu-id="89b1e-155">W przypadku wykrycia zmian danych w jednym z węzłów hello, ten moduł następnie wysyła komunikaty tooAzure Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="89b1e-155">If a data change is detected in one of hello nodes, this module then sends messages tooAzure IoT Hub.</span></span>

<span data-ttu-id="89b1e-156">Centrum IoT zapewnia tooAzure źródła zdarzeń TSI.</span><span class="sxs-lookup"><span data-stu-id="89b1e-156">IoT Hub provides an event source tooAzure TSI.</span></span> <span data-ttu-id="89b1e-157">TSI magazynów danych przez 30 dni, w oparciu sygnatury czasowe podłączonych toohello wiadomości.</span><span class="sxs-lookup"><span data-stu-id="89b1e-157">TSI stores data for 30 days based on timestamps attached toohello messages.</span></span> <span data-ttu-id="89b1e-158">Te dane obejmują:</span><span class="sxs-lookup"><span data-stu-id="89b1e-158">This data includes:</span></span>

* <span data-ttu-id="89b1e-159">Identyfikator ApplicationUri serwera OPC UA</span><span class="sxs-lookup"><span data-stu-id="89b1e-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="89b1e-160">Identyfikator NodeId serwera OPC UA</span><span class="sxs-lookup"><span data-stu-id="89b1e-160">OPC UA NodeId</span></span>
* <span data-ttu-id="89b1e-161">Wartość węzła hello</span><span class="sxs-lookup"><span data-stu-id="89b1e-161">Value of hello node</span></span>
* <span data-ttu-id="89b1e-162">Sygnaturę czasową źródła</span><span class="sxs-lookup"><span data-stu-id="89b1e-162">Source timestamp</span></span>
* <span data-ttu-id="89b1e-163">Nazwę DisplayName serwera OPC UA</span><span class="sxs-lookup"><span data-stu-id="89b1e-163">OPC UA DisplayName</span></span>

<span data-ttu-id="89b1e-164">Obecnie TSI nie zezwala klientom toocustomize, jak długo życzą tookeep hello danych.</span><span class="sxs-lookup"><span data-stu-id="89b1e-164">Currently, TSI does not allow customers toocustomize how long they wish tookeep hello data for.</span></span>

<span data-ttu-id="89b1e-165">Usługa TSI przesyła zapytania o dane węzła przy użyciu funkcji SearchSpan (Time.From, Time.To) i agreguje je według identyfikatora ApplicationUri, NodeId lub nazwy DisplayName serwera OPC UA.</span><span class="sxs-lookup"><span data-stu-id="89b1e-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="89b1e-166">tooretrieve hello danych hello mierników OEE i wskaźnik KPI i hello czasu serii wykresów są agregowane przez liczbę zdarzeń, Sum, Avg, Min i Max.</span><span class="sxs-lookup"><span data-stu-id="89b1e-166">tooretrieve hello data for hello OEE and KPI gauges, and hello time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="89b1e-167">szeregów czasowych Hello są tworzone za pomocą innego procesu.</span><span class="sxs-lookup"><span data-stu-id="89b1e-167">hello time series are built using a different process.</span></span> <span data-ttu-id="89b1e-168">OEE i wskaźników KPI są obliczane na podstawie danych podstawowych stacji i przepuszcza dla topologii hello (wiersze produkcji, fabryki, enterprise) w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="89b1e-168">OEE and KPIs are calculated from station base data and bubbled up for hello topology (production lines, factories, enterprise) in hello application.</span></span>

<span data-ttu-id="89b1e-169">Ponadto szeregów czasowych dla topologii OEE i wskaźnik KPI jest obliczana w aplikacji hello zawsze, gdy obiekt timespan wyświetlane jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="89b1e-169">Additionally, time series for OEE and KPI topology is calculated in hello app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="89b1e-170">Na przykład widok dzisiaj hello jest aktualizowany co godzinę pełna.</span><span class="sxs-lookup"><span data-stu-id="89b1e-170">For example, hello day view is updated every full hour.</span></span>

<span data-ttu-id="89b1e-171">Widok serii czasu Hello danych węzła pochodzi bezpośrednio z TSI przy użyciu agregacji dla timespan.</span><span class="sxs-lookup"><span data-stu-id="89b1e-171">hello time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="89b1e-172">Usługa IoT Hub</span><span class="sxs-lookup"><span data-stu-id="89b1e-172">IoT Hub</span></span>
<span data-ttu-id="89b1e-173">Witaj [Centrum IoT] [ lnk-IoT Hub] odbiera dane przesyłane z hello OPC wydawcy modułu w chmurze hello i ułatwia usługi Azure TSI toohello dostępne.</span><span class="sxs-lookup"><span data-stu-id="89b1e-173">hello [IoT hub][lnk-IoT Hub] receives data sent from hello OPC Publisher Module into hello cloud and makes it available toohello Azure TSI service.</span></span> 

<span data-ttu-id="89b1e-174">Witaj Centrum IoT w rozwiązaniu hello również:</span><span class="sxs-lookup"><span data-stu-id="89b1e-174">hello IoT Hub in hello solution also:</span></span>
- <span data-ttu-id="89b1e-175">Przechowuje rejestr tożsamości, który przechowuje hello identyfikatorów dla wszystkich modułów wydawcy OPC i wszystkich modułów Proxy OPC.</span><span class="sxs-lookup"><span data-stu-id="89b1e-175">Maintains an identity registry that stores hello IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="89b1e-176">Jest używany jako kanał transportu dla komunikacji dwukierunkowej hello OPC modułu Proxy.</span><span class="sxs-lookup"><span data-stu-id="89b1e-176">Is used as transport channel for bidirectional communication of hello OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="89b1e-177">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="89b1e-177">Azure Storage</span></span>
<span data-ttu-id="89b1e-178">rozwiązanie Hello używa magazynu obiektów blob platformy Azure jako magazynu danych na dysku dla danych wdrażania maszyny Wirtualnej i toostore hello.</span><span class="sxs-lookup"><span data-stu-id="89b1e-178">hello solution uses Azure blob storage as disk storage for hello VM and toostore deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="89b1e-179">Aplikacja internetowa</span><span class="sxs-lookup"><span data-stu-id="89b1e-179">Web app</span></span>
<span data-ttu-id="89b1e-180">Aplikacja sieci web Hello wdrożony jako część hello wstępnie skonfigurowane rozwiązanie obejmuje zintegrowanym klientem OPC UA, przetwarzania alertów i wizualizacja danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="89b1e-180">hello web app deployed as part of hello preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89b1e-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="89b1e-181">Next steps</span></span>

<span data-ttu-id="89b1e-182">Aby kontynuować, wprowadzenie pakiet IoT odczytując hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="89b1e-182">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="89b1e-183">[Uprawnienia w witrynie azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="89b1e-183">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="89b1e-184">Wdrożyć bramę Windows lub Linux hello połączone fabryki wstępnie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="89b1e-184">Deploy a gateway on Windows or Linux for hello connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
