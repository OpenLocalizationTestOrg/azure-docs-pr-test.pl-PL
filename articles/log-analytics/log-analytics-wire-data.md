---
title: "Połączenie danych rozwiązania analizy dzienników | Dokumentacja firmy Microsoft"
description: "Podczas transmisji danych jest skonsolidowanych danych sieci i wydajności z komputerów z agentami OMS, w tym programu Operations Manager oraz agenci połączone z systemem Windows. Dane sieciowe jest połączone z dane dziennika, aby ułatwić skorelować danych."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: eb8ae80f91b9ecad666ab7a2257d99e5669f5b88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a><span data-ttu-id="5c9f3-104">Podczas transmisji danych 2.0 (wersja zapoznawcza) rozwiązania analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="5c9f3-104">Wire Data 2.0 (Preview) solution in Log Analytics</span></span>

![Podczas transmisji danych symbolu](./media/log-analytics-wire-data/wire-data2-symbol.png)

<span data-ttu-id="5c9f3-106">Podczas transmisji danych jest skonsolidowanych danych sieci i wydajności z komputerów z agentów OMS, w tym programu Operations Manager, połączony z systemem Windows i Linux agentów.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-106">Wire data is consolidated network and performance data from computers with OMS agents, including Operations Manager, Windows-connected, and Linux agents.</span></span> <span data-ttu-id="5c9f3-107">Dane sieci są łączone z innymi danymi dziennika ułatwiają skorelować danych.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-107">Network data is combined with your other log data to help you correlate data.</span></span>

<span data-ttu-id="5c9f3-108">Oprócz agentów OMS rozwiązania podczas transmisji danych używa agentów Dependency firmy Microsoft, które można zainstalować na komputerach w infrastrukturze IT.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-108">In addition to OMS agents, the Wire Data solution uses Microsoft Dependency agents that you install on computers in your IT infrastructure.</span></span> <span data-ttu-id="5c9f3-109">Zależności agenci monitorują dane sieci wysyłane do i z komputerów dla sieci poziomy 2 – 3 [OSI model](https://en.wikipedia.org/wiki/OSI_model), włącznie z różnych protokołów i portów używanych.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-109">Dependency Agents monitor network data sent to and from your computers for network levels 2-3 in the [OSI model](https://en.wikipedia.org/wiki/OSI_model), including the various protocols and ports used.</span></span> <span data-ttu-id="5c9f3-110">Dane są następnie wysyłane do analizy dzienników przy użyciu agentów.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-110">Data is then sent to Log Analytics using agents.</span></span>

> [!NOTE]
> <span data-ttu-id="5c9f3-111">Nie można dodać poprzedniej wersji rozwiązania przesyłania danych do nowych obszarów roboczych.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-111">You cannot add the previous version of the Wire Data solution to new workspaces.</span></span> <span data-ttu-id="5c9f3-112">Jeśli masz w oryginalnym rozwiązaniu udostępniający dane włączone, można nadal z niego korzystać.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-112">If you have the original Wire Data solution enabled, you can continue to use it.</span></span> <span data-ttu-id="5c9f3-113">Jednak aby używać podczas transmisji danych 2.0, należy najpierw usunąć oryginalną wersją.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-113">However, to use Wire Data 2.0, you must first remove the original version.</span></span>

<span data-ttu-id="5c9f3-114">Domyślnie analizy dzienników zbiera dane zarejestrowane dla Procesora, pamięci, dysku i sieci danych wydajności z liczników wbudowanego w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-114">By default, Log Analytics collects logged data for CPU, memory, disk, and network performance data from counters built into Windows.</span></span> <span data-ttu-id="5c9f3-115">Sieci i innych zbieranie danych odbywa się w czasie rzeczywistym dla każdego agenta, włącznie z podsieci i protokoły poziomu aplikacji, używane przez komputer.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-115">Network and other data collection is done in real-time for each agent, including subnets and application-level protocols being used by the computer.</span></span> <span data-ttu-id="5c9f3-116">Na stronie Ustawienia na karcie dzienniki, można dodać liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-116">You can add other performance counters on the Settings page on the Logs tab.</span></span>

<span data-ttu-id="5c9f3-117">Jeśli użyto [sFlow](http://www.sflow.org/) lub innego oprogramowania z [protokołu NetFlow firmy Cisco](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), statystyk i danych, zostanie wyświetlony podczas transmisji danych będzie znane.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-117">If you've used [sFlow](http://www.sflow.org/) or other software with [Cisco's NetFlow protocol](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), then the statistics and data you see from wire data will be familiar to you.</span></span>

<span data-ttu-id="5c9f3-118">Typy wbudowane zapytania wyszukiwania dziennika, należą:</span><span class="sxs-lookup"><span data-stu-id="5c9f3-118">Some of the types of built-in Log search queries include:</span></span>

- <span data-ttu-id="5c9f3-119">Agenci udostępniający dane</span><span class="sxs-lookup"><span data-stu-id="5c9f3-119">Agents that provide wire data</span></span>
- <span data-ttu-id="5c9f3-120">Adres IP agentów udostępniających dane o komunikacji sieciowej</span><span class="sxs-lookup"><span data-stu-id="5c9f3-120">IP address of agents providing wire data</span></span>
- <span data-ttu-id="5c9f3-121">Komunikacja wychodząca według adresów IP</span><span class="sxs-lookup"><span data-stu-id="5c9f3-121">Outbound communications by IP addresses</span></span>
- <span data-ttu-id="5c9f3-122">Liczba bajtów wysłanych przez protokoły aplikacji</span><span class="sxs-lookup"><span data-stu-id="5c9f3-122">Number of bytes sent by application protocols</span></span>
- <span data-ttu-id="5c9f3-123">Liczba bajtów wysłanych przez usługę aplikacji</span><span class="sxs-lookup"><span data-stu-id="5c9f3-123">Number of bytes sent by an application service</span></span>
- <span data-ttu-id="5c9f3-124">Bajty odebrane przez różnych protokołów</span><span class="sxs-lookup"><span data-stu-id="5c9f3-124">Bytes received by different protocols</span></span>
- <span data-ttu-id="5c9f3-125">Całkowita liczba bajtów wysłanych i odebranych według wersji adresu IP</span><span class="sxs-lookup"><span data-stu-id="5c9f3-125">Total bytes sent and received by IP version</span></span>
- <span data-ttu-id="5c9f3-126">Średni czas oczekiwania dla połączenia, które zostały wiarygodny</span><span class="sxs-lookup"><span data-stu-id="5c9f3-126">Average latency for connections that were measured reliably</span></span>
- <span data-ttu-id="5c9f3-127">Komputer przetwarza sieciowej zainicjowały lub odebrały ruch</span><span class="sxs-lookup"><span data-stu-id="5c9f3-127">Computer processes that initiated or received network traffic</span></span>
- <span data-ttu-id="5c9f3-128">Ilość ruchu sieciowego dla procesu</span><span class="sxs-lookup"><span data-stu-id="5c9f3-128">Amount of network traffic for a process</span></span>

<span data-ttu-id="5c9f3-129">Podczas wyszukiwania przy użyciu udostępniający dane, można filtrować i grupy danych, aby wyświetlić informacje o najwyższym agentów i protokoły najwyższego.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-129">When you search using wire data, you can filter and group data to view information about the top agents and top protocols.</span></span> <span data-ttu-id="5c9f3-130">Lub kiedy można wyświetlić niektórych komputerów (adresów IP adresy MAC) przekazywane ze sobą, jak długo i ilość danych została wysłana — zasadniczo wyświetlić metadane dotyczące ruchu sieciowego, który jest na podstawie wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-130">Or you can view when certain computers (IP addresses/MAC addresses) communicated with each other, for how long, and how much data was sent—basically, you view metadata about network traffic, which is search-based.</span></span>

<span data-ttu-id="5c9f3-131">Jednak ponieważ wyświetlasz metadanych nie jest zawsze przydatne podczas rozwiązywania szczegółowe.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-131">However, since you're viewing metadata, it's not necessarily useful for in-depth troubleshooting.</span></span> <span data-ttu-id="5c9f3-132">Podczas transmisji danych analizy dzienników nie jest pełną przechwytywania danych w sieci.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-132">Wire data in Log Analytics is not a full capture of network data.</span></span> <span data-ttu-id="5c9f3-133">Tak nie ma ona do rozwiązywania problemów głębokość poziomie pakietów.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-133">So, it's not intended for deep packet-level troubleshooting.</span></span> <span data-ttu-id="5c9f3-134">Zaletą przy użyciu agenta, w porównaniu do innych metod kolekcji jest, że nie trzeba zainstalować urządzenia, skonfiguruj ponownie przełączników sieciowych lub przeprowadzić skomplikowane konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-134">The advantage of using the agent, compared to other collection methods, is that you don't have to install appliances, reconfigure your network switches, or preform complicated configurations.</span></span> <span data-ttu-id="5c9f3-135">Podczas transmisji danych jest po prostu agenta na podstawie — Zainstaluj agenta na komputerze i będzie monitorować ruch sieci.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-135">Wire data is simply agent-based—you install the agent on a computer and it will monitor its own network traffic.</span></span> <span data-ttu-id="5c9f3-136">Inną zaletą jest to, jeśli chcesz monitorować obciążeń działających w chmurze dostawcy lub dostawcy usług hostingowych lub Microsoft Azure, gdy użytkownik nie posiada warstwy sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-136">Another advantage is when you want to monitor workloads running in cloud providers or hosting service provider or Microsoft Azure, where the user doesn't own the fabric layer.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="5c9f3-137">Połączone źródła</span><span class="sxs-lookup"><span data-stu-id="5c9f3-137">Connected sources</span></span>

<span data-ttu-id="5c9f3-138">Podczas transmisji danych dane są pobierane z Microsoft Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-138">Wire Data gets its data from the Microsoft Dependency Agent.</span></span> <span data-ttu-id="5c9f3-139">Agent zależności zależy od agenta pakietu OMS dla jego połączenia z analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-139">The Dependency Agent depends on the OMS Agent for its connections to Log Analytics.</span></span> <span data-ttu-id="5c9f3-140">To oznacza, że serwer musi mieć Agent pakietu OMS zainstalowany i skonfigurowany najpierw, a następnie zainstaluj agenta zależności.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-140">This means that a server must have the OMS Agent installed and configured first, and then you install the Dependency Agent.</span></span> <span data-ttu-id="5c9f3-141">W poniższej tabeli opisano połączonych źródeł, które obsługuje rozwiązania przesyłania danych.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-141">The following table describes the connected sources that the Wire Data solution supports.</span></span>

| <span data-ttu-id="5c9f3-142">**Źródło połączenia**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-142">**Connected source**</span></span> | <span data-ttu-id="5c9f3-143">**Obsługiwane**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-143">**Supported**</span></span> | <span data-ttu-id="5c9f3-144">**Opis**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-144">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5c9f3-145">Agenci dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="5c9f3-145">Windows agents</span></span> | <span data-ttu-id="5c9f3-146">Tak</span><span class="sxs-lookup"><span data-stu-id="5c9f3-146">Yes</span></span> | <span data-ttu-id="5c9f3-147">Podczas transmisji danych analizuje i zbiera dane z komputerów z systemem Windows agenta.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-147">Wire Data analyzes and collects data from Windows agent computers.</span></span> <br><br> <span data-ttu-id="5c9f3-148">Oprócz [Agent pakietu OMS](log-analytics-windows-agents.md), agentów systemu Windows wymagają Microsoft Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-148">In addition to the [OMS Agent](log-analytics-windows-agents.md), Windows agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="5c9f3-149">Zobacz [obsługiwanych systemów operacyjnych](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) pełną listę wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-149">See the [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="5c9f3-150">Agenci dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="5c9f3-150">Linux agents</span></span> | <span data-ttu-id="5c9f3-151">Tak</span><span class="sxs-lookup"><span data-stu-id="5c9f3-151">Yes</span></span> | <span data-ttu-id="5c9f3-152">Podczas transmisji danych analizuje i zbiera dane z komputerów z systemem Linux agenta.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-152">Wire Data analyzes and collects data from Linux agent computers.</span></span><br><br> <span data-ttu-id="5c9f3-153">Oprócz [Agent pakietu OMS](log-analytics-linux-agents.md), Microsoft Dependency Agent wymagają agentów systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-153">In addition to the [OMS Agent](log-analytics-linux-agents.md), Linux agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="5c9f3-154">Zobacz [obsługiwanych systemów operacyjnych](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) pełną listę wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-154">See the [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="5c9f3-155">Grupa zarządzania programu System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="5c9f3-155">System Center Operations Manager management group</span></span> | <span data-ttu-id="5c9f3-156">Tak</span><span class="sxs-lookup"><span data-stu-id="5c9f3-156">Yes</span></span> | <span data-ttu-id="5c9f3-157">Podczas transmisji danych analizuje i zbiera dane z agentów systemu Windows i Linux w połączonych [grupy zarządzania programu System Center Operations Manager](log-analytics-om-agents.md).</span><span class="sxs-lookup"><span data-stu-id="5c9f3-157">Wire Data analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](log-analytics-om-agents.md).</span></span> <br><br> <span data-ttu-id="5c9f3-158">Połączenie bezpośrednie z komputera agenta programu System Center Operations Manager do analizy dzienników jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-158">A direct connection from the System Center Operations Manager agent computer to Log Analytics is required.</span></span> <span data-ttu-id="5c9f3-159">Dane są przesyłane dalej z grupy zarządzania do analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-159">Data is forwarded from the management group to Log Analytics.</span></span> |
| <span data-ttu-id="5c9f3-160">Konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="5c9f3-160">Azure storage account</span></span> | <span data-ttu-id="5c9f3-161">Nie</span><span class="sxs-lookup"><span data-stu-id="5c9f3-161">No</span></span> | <span data-ttu-id="5c9f3-162">Podczas transmisji danych zbiera dane z komputery agenta, więc nie ma żadnych danych z niego do zbierania z usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-162">Wire Data collects data from agent computers, so there is no data from it to collect from Azure Storage.</span></span> |

<span data-ttu-id="5c9f3-163">W systemie Windows Microsoft Monitoring Agent (MMA) jest używany zarówno przez System Center Operations Manager i analizy dzienników do zbierania i wysyłania danych.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-163">On Windows, the Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics to gather and send data.</span></span> <span data-ttu-id="5c9f3-164">W zależności od kontekstu agent jest nazywany agenta programu System Center Operations Manager, Agent pakietu OMS, Agent analizy dziennika, MMA lub bezpośredniego agenta.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-164">Depending on the context, the agent is called the System Center Operations Manager Agent, OMS Agent, Log Analytics Agent, MMA, or Direct Agent.</span></span> <span data-ttu-id="5c9f3-165">System Center Operations Manager i Log Analytics zapewnia nieco inne wersje MMA.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-165">System Center Operations Manager and Log Analytics provide slightly different versions of the MMA.</span></span> <span data-ttu-id="5c9f3-166">Te wersje strony każdy raport do programu System Center Operations Manager do analizy dzienników lub obie.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-166">These versions can each report to System Center Operations Manager, to Log Analytics, or to both.</span></span>

<span data-ttu-id="5c9f3-167">W systemie Linux Agent pakietu OMS Linux zbiera i wysyłania danych do analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-167">On Linux, the OMS Agent for Linux gathers and sends data to Log Analytics.</span></span> <span data-ttu-id="5c9f3-168">Na serwerach z agentami bezpośredniego OMS lub na serwerach, które są dołączone do analizy dzienników za pośrednictwem grup zarządzania programu System Center Operations Manager, można użyć podczas transmisji danych.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-168">You can use Wire Data on servers with OMS Direct Agents or on servers that are attached to Log Analytics via System Center Operations Manager management groups.</span></span>

<span data-ttu-id="5c9f3-169">W tym artykule odwołuje się do wszystkich agentów, czy Linux lub Windows, czy połączony z grupą zarządzania programu System Center Operations Manager lub bezpośrednio do analizy dzienników są określane jako _agent pakietu OMS_.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-169">In this article, references to all agents, whether Linux or Windows, whether connected to a System Center Operations Manager management group or directly to Log Analytics are termed the _OMS agent_.</span></span> <span data-ttu-id="5c9f3-170">Nazwa określonego wdrożenia agenta będą używane tylko wtedy, gdy jest wymagana dla kontekstu.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-170">We'll use the specific deployment name of the agent only if it's needed for context.</span></span>

<span data-ttu-id="5c9f3-171">Agent zależności nie przesyła wszystkie dane, a nie wymaga zmian zapory lub porty.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-171">The Dependency Agent does not transmit any data itself, and it does not require any changes to firewalls or ports.</span></span> <span data-ttu-id="5c9f3-172">Dane udostępniający dane są zawsze przesyłane przez agenta pakietu OMS z analizą dzienników, albo bezpośrednio lub przy użyciu bramy OMS.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-172">The data in Wire Data is always transmitted by the OMS agent to Log Analytics, either directly or using the OMS Gateway.</span></span>

![diagram agenta](./media/log-analytics-wire-data/agents.png)

<span data-ttu-id="5c9f3-174">Jeśli jesteś użytkownikiem programu System Center Operations Manager z grupą zarządzania podłączone do analizy dzienników:</span><span class="sxs-lookup"><span data-stu-id="5c9f3-174">If you are a System Center Operations Manager user with a management group connected to Log Analytics:</span></span>

- <span data-ttu-id="5c9f3-175">Dodatkowa konfiguracja nie jest wymagana, gdy agentów programu System Center Operations Manager można uzyskać dostęp do Internetu do nawiązania połączenia analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-175">No additional configuration is required when your System Center Operations Manager agents can access the Internet to connect to Log Analytics.</span></span>
- <span data-ttu-id="5c9f3-176">Należy skonfigurować bramę OMS do pracy z programem System Center Operations Manager, gdy agentów programu System Center Operations Manager nie może uzyskać dostęp do analizy dzienników za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-176">You need to configure the OMS Gateway to work with System Center Operations Manager when your System Center Operations Manager agents cannot access Log Analytics over the Internet.</span></span>

<span data-ttu-id="5c9f3-177">Jeśli używasz bezpośredniej agenta, należy skonfigurować agenta pakietu OMS do połączenia analizy dzienników lub bramy OMS.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-177">If you are using the Direct Agent, you need to configure the OMS agent itself to connect to Log Analytics or to your OMS Gateway.</span></span> <span data-ttu-id="5c9f3-178">Możesz pobrać bramy OMS z [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span><span class="sxs-lookup"><span data-stu-id="5c9f3-178">You can download the OMS Gateway from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c9f3-179">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5c9f3-179">Prerequisites</span></span>

- <span data-ttu-id="5c9f3-180">Wymaga [szczegółowe dane i analiza](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) oferta rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-180">Requires the [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) solution offer.</span></span>
- <span data-ttu-id="5c9f3-181">Jeśli używasz poprzedniej wersji rozwiązania podczas transmisji danych, należy najpierw usunąć go.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-181">If you're using the previous version of the Wire Data solution, you must first remove it.</span></span> <span data-ttu-id="5c9f3-182">Jednak wszystkie dane zarejestrowane przez w oryginalnym rozwiązaniu udostępniający dane są nadal dostępne w podczas transmisji danych w wersji 2.0 i wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-182">However, all data captured through the original Wire Data solution is still available in Wire Data 2.0 and log search.</span></span>
- <span data-ttu-id="5c9f3-183">Aby zainstalować lub odinstalować agenta zależności są wymagane uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-183">Administrator privileges are required to install or uninstall the Dependency Agent.</span></span>
- <span data-ttu-id="5c9f3-184">Musi być zainstalowany Agent zależności na komputerze z 64-bitowym systemie operacyjnym.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-184">The Dependency Agent must be installed on a computer with a 64-bit operating system.</span></span>

### <a name="operating-systems"></a><span data-ttu-id="5c9f3-185">Systemy operacyjne</span><span class="sxs-lookup"><span data-stu-id="5c9f3-185">Operating systems</span></span>

<span data-ttu-id="5c9f3-186">Poniższe sekcje zawierają listę obsługiwanych systemów operacyjnych dla agenta zależności.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-186">The following sections list the supported operating systems for the Dependency Agent.</span></span> <span data-ttu-id="5c9f3-187">Podczas transmisji danych nie obsługuje architektury 32-bitowego dla dowolnego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-187">Wire Data doesn't support 32-bit architectures for any operating system.</span></span>

#### <a name="windows-server"></a><span data-ttu-id="5c9f3-188">Windows Server</span><span class="sxs-lookup"><span data-stu-id="5c9f3-188">Windows Server</span></span>

- <span data-ttu-id="5c9f3-189">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="5c9f3-189">Windows Server 2016</span></span>
- <span data-ttu-id="5c9f3-190">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5c9f3-190">Windows Server 2012 R2</span></span>
- <span data-ttu-id="5c9f3-191">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="5c9f3-191">Windows Server 2012</span></span>
- <span data-ttu-id="5c9f3-192">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="5c9f3-192">Windows Server 2008 R2 SP1</span></span>

#### <a name="windows-desktop"></a><span data-ttu-id="5c9f3-193">Pulpit systemu Windows</span><span class="sxs-lookup"><span data-stu-id="5c9f3-193">Windows desktop</span></span>

- <span data-ttu-id="5c9f3-194">Windows 10</span><span class="sxs-lookup"><span data-stu-id="5c9f3-194">Windows 10</span></span>
- <span data-ttu-id="5c9f3-195">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="5c9f3-195">Windows 8.1</span></span>
- <span data-ttu-id="5c9f3-196">Windows 8</span><span class="sxs-lookup"><span data-stu-id="5c9f3-196">Windows 8</span></span>
- <span data-ttu-id="5c9f3-197">Windows 7</span><span class="sxs-lookup"><span data-stu-id="5c9f3-197">Windows 7</span></span>

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a><span data-ttu-id="5c9f3-198">Red Hat Enterprise Linux, CentOS Linux i Oracle Linux (z RHEL jądra)</span><span class="sxs-lookup"><span data-stu-id="5c9f3-198">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span></span>

- <span data-ttu-id="5c9f3-199">Obsługiwane są tylko domyślnej i wersjach jądra systemu Linux SMP.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-199">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="5c9f3-200">Zwalnia jądra niestandardowe, takie jak rozszerzenia adresu fizycznego i Xen, nie są obsługiwane dla dowolnego dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-200">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="5c9f3-201">Na przykład system z ciąg wersji _2.6.16.21-0.8-xen_ nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-201">For example, a system with the release string of _2.6.16.21-0.8-xen_ is not supported.</span></span>
- <span data-ttu-id="5c9f3-202">Niestandardowe jądra, w tym ponownych kompilacji standardowe jądra, nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-202">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="5c9f3-203">CentOSPlus jądra nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-203">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="5c9f3-204">Oracle podzielenie Enterprise jądra (UEK) zostało opisane w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-204">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>

#### <a name="red-hat-linux-7"></a><span data-ttu-id="5c9f3-205">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="5c9f3-205">Red Hat Linux 7</span></span>

| <span data-ttu-id="5c9f3-206">**Wersja systemu operacyjnego**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-206">**OS version**</span></span> | <span data-ttu-id="5c9f3-207">**Wersja jądra**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-207">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="5c9f3-208">7.0</span><span class="sxs-lookup"><span data-stu-id="5c9f3-208">7.0</span></span> | <span data-ttu-id="5c9f3-209">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="5c9f3-209">3.10.0-123</span></span> |
| <span data-ttu-id="5c9f3-210">7.1</span><span class="sxs-lookup"><span data-stu-id="5c9f3-210">7.1</span></span> | <span data-ttu-id="5c9f3-211">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="5c9f3-211">3.10.0-229</span></span> |
| <span data-ttu-id="5c9f3-212">7.2</span><span class="sxs-lookup"><span data-stu-id="5c9f3-212">7.2</span></span> | <span data-ttu-id="5c9f3-213">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="5c9f3-213">3.10.0-327</span></span> |
| <span data-ttu-id="5c9f3-214">7.3</span><span class="sxs-lookup"><span data-stu-id="5c9f3-214">7.3</span></span> | <span data-ttu-id="5c9f3-215">3.10.0-514</span><span class="sxs-lookup"><span data-stu-id="5c9f3-215">3.10.0-514</span></span> |

#### <a name="red-hat-linux-6"></a><span data-ttu-id="5c9f3-216">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="5c9f3-216">Red Hat Linux 6</span></span>

| <span data-ttu-id="5c9f3-217">**Wersja systemu operacyjnego**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-217">**OS version**</span></span> | <span data-ttu-id="5c9f3-218">**Wersja jądra**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-218">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="5c9f3-219">6.0</span><span class="sxs-lookup"><span data-stu-id="5c9f3-219">6.0</span></span> | <span data-ttu-id="5c9f3-220">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="5c9f3-220">2.6.32-71</span></span> |
| <span data-ttu-id="5c9f3-221">6.1</span><span class="sxs-lookup"><span data-stu-id="5c9f3-221">6.1</span></span> | <span data-ttu-id="5c9f3-222">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="5c9f3-222">2.6.32-131</span></span> |
| <span data-ttu-id="5c9f3-223">6.2</span><span class="sxs-lookup"><span data-stu-id="5c9f3-223">6.2</span></span> | <span data-ttu-id="5c9f3-224">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="5c9f3-224">2.6.32-220</span></span> |
| <span data-ttu-id="5c9f3-225">6.3</span><span class="sxs-lookup"><span data-stu-id="5c9f3-225">6.3</span></span> | <span data-ttu-id="5c9f3-226">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="5c9f3-226">2.6.32-279</span></span> |
| <span data-ttu-id="5c9f3-227">6.4</span><span class="sxs-lookup"><span data-stu-id="5c9f3-227">6.4</span></span> | <span data-ttu-id="5c9f3-228">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="5c9f3-228">2.6.32-358</span></span> |
| <span data-ttu-id="5c9f3-229">6.5</span><span class="sxs-lookup"><span data-stu-id="5c9f3-229">6.5</span></span> | <span data-ttu-id="5c9f3-230">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="5c9f3-230">2.6.32-431</span></span> |
| <span data-ttu-id="5c9f3-231">6.6</span><span class="sxs-lookup"><span data-stu-id="5c9f3-231">6.6</span></span> | <span data-ttu-id="5c9f3-232">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="5c9f3-232">2.6.32-504</span></span> |
| <span data-ttu-id="5c9f3-233">6.7</span><span class="sxs-lookup"><span data-stu-id="5c9f3-233">6.7</span></span> | <span data-ttu-id="5c9f3-234">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="5c9f3-234">2.6.32-573</span></span> |
| <span data-ttu-id="5c9f3-235">6.8</span><span class="sxs-lookup"><span data-stu-id="5c9f3-235">6.8</span></span> | <span data-ttu-id="5c9f3-236">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="5c9f3-236">2.6.32-642</span></span> |

#### <a name="red-hat-linux-5"></a><span data-ttu-id="5c9f3-237">Red Hat Linux 5</span><span class="sxs-lookup"><span data-stu-id="5c9f3-237">Red Hat Linux 5</span></span>

| <span data-ttu-id="5c9f3-238">**Wersja systemu operacyjnego**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-238">**OS version**</span></span> | <span data-ttu-id="5c9f3-239">**Wersja jądra**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-239">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="5c9f3-240">5.8</span><span class="sxs-lookup"><span data-stu-id="5c9f3-240">5.8</span></span> | <span data-ttu-id="5c9f3-241">2.6.18-308</span><span class="sxs-lookup"><span data-stu-id="5c9f3-241">2.6.18-308</span></span> |
| <span data-ttu-id="5c9f3-242">5.9</span><span class="sxs-lookup"><span data-stu-id="5c9f3-242">5.9</span></span> | <span data-ttu-id="5c9f3-243">2.6.18-348</span><span class="sxs-lookup"><span data-stu-id="5c9f3-243">2.6.18-348</span></span> |
| <span data-ttu-id="5c9f3-244">5.10</span><span class="sxs-lookup"><span data-stu-id="5c9f3-244">5.10</span></span> | <span data-ttu-id="5c9f3-245">2.6.18-371</span><span class="sxs-lookup"><span data-stu-id="5c9f3-245">2.6.18-371</span></span> |
| <span data-ttu-id="5c9f3-246">5.11</span><span class="sxs-lookup"><span data-stu-id="5c9f3-246">5.11</span></span> | <span data-ttu-id="5c9f3-247">2.6.18-398</span><span class="sxs-lookup"><span data-stu-id="5c9f3-247">2.6.18-398</span></span> <br> <span data-ttu-id="5c9f3-248">2.6.18-400</span><span class="sxs-lookup"><span data-stu-id="5c9f3-248">2.6.18-400</span></span> <br><span data-ttu-id="5c9f3-249">2.6.18-402</span><span class="sxs-lookup"><span data-stu-id="5c9f3-249">2.6.18-402</span></span> <br><span data-ttu-id="5c9f3-250">2.6.18-404</span><span class="sxs-lookup"><span data-stu-id="5c9f3-250">2.6.18-404</span></span> <br><span data-ttu-id="5c9f3-251">2.6.18-406</span><span class="sxs-lookup"><span data-stu-id="5c9f3-251">2.6.18-406</span></span> <br> <span data-ttu-id="5c9f3-252">2.6.18-407</span><span class="sxs-lookup"><span data-stu-id="5c9f3-252">2.6.18-407</span></span> <br> <span data-ttu-id="5c9f3-253">2.6.18-408</span><span class="sxs-lookup"><span data-stu-id="5c9f3-253">2.6.18-408</span></span> <br> <span data-ttu-id="5c9f3-254">2.6.18-409</span><span class="sxs-lookup"><span data-stu-id="5c9f3-254">2.6.18-409</span></span> <br> <span data-ttu-id="5c9f3-255">2.6.18-410</span><span class="sxs-lookup"><span data-stu-id="5c9f3-255">2.6.18-410</span></span> <br> <span data-ttu-id="5c9f3-256">2.6.18-411</span><span class="sxs-lookup"><span data-stu-id="5c9f3-256">2.6.18-411</span></span> <br> <span data-ttu-id="5c9f3-257">2.6.18-412</span><span class="sxs-lookup"><span data-stu-id="5c9f3-257">2.6.18-412</span></span> <br> <span data-ttu-id="5c9f3-258">2.6.18-416</span><span class="sxs-lookup"><span data-stu-id="5c9f3-258">2.6.18-416</span></span> <br> <span data-ttu-id="5c9f3-259">2.6.18-417</span><span class="sxs-lookup"><span data-stu-id="5c9f3-259">2.6.18-417</span></span> <br> <span data-ttu-id="5c9f3-260">2.6.18-419</span><span class="sxs-lookup"><span data-stu-id="5c9f3-260">2.6.18-419</span></span> |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="5c9f3-261">Oracle Linux przedsiębiorstwa z jądra podzielenie Enterprise</span><span class="sxs-lookup"><span data-stu-id="5c9f3-261">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span></span>

#### <a name="oracle-linux-6"></a><span data-ttu-id="5c9f3-262">Oracle Linux 6</span><span class="sxs-lookup"><span data-stu-id="5c9f3-262">Oracle Linux 6</span></span>

| <span data-ttu-id="5c9f3-263">**Wersja systemu operacyjnego**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-263">**OS version**</span></span> | <span data-ttu-id="5c9f3-264">**Wersja jądra**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-264">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="5c9f3-265">6.2</span><span class="sxs-lookup"><span data-stu-id="5c9f3-265">6.2</span></span> | <span data-ttu-id="5c9f3-266">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="5c9f3-266">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="5c9f3-267">6.3</span><span class="sxs-lookup"><span data-stu-id="5c9f3-267">6.3</span></span> | <span data-ttu-id="5c9f3-268">Oracle 2.6.39-200 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="5c9f3-268">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="5c9f3-269">6.4</span><span class="sxs-lookup"><span data-stu-id="5c9f3-269">6.4</span></span> | <span data-ttu-id="5c9f3-270">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="5c9f3-270">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="5c9f3-271">6.5</span><span class="sxs-lookup"><span data-stu-id="5c9f3-271">6.5</span></span> | <span data-ttu-id="5c9f3-272">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="5c9f3-272">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="5c9f3-273">6.6</span><span class="sxs-lookup"><span data-stu-id="5c9f3-273">6.6</span></span> | <span data-ttu-id="5c9f3-274">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="5c9f3-274">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

#### <a name="oracle-linux-5"></a><span data-ttu-id="5c9f3-275">Oracle Linux 5</span><span class="sxs-lookup"><span data-stu-id="5c9f3-275">Oracle Linux 5</span></span>

| <span data-ttu-id="5c9f3-276">**Wersja systemu operacyjnego**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-276">**OS version**</span></span> | <span data-ttu-id="5c9f3-277">**Wersja jądra**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-277">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="5c9f3-278">5.8</span><span class="sxs-lookup"><span data-stu-id="5c9f3-278">5.8</span></span> | <span data-ttu-id="5c9f3-279">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="5c9f3-279">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="5c9f3-280">5.9</span><span class="sxs-lookup"><span data-stu-id="5c9f3-280">5.9</span></span> | <span data-ttu-id="5c9f3-281">Oracle 2.6.39-300 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="5c9f3-281">Oracle 2.6.39-300 (UEK R2)</span></span> |
| <span data-ttu-id="5c9f3-282">5.10</span><span class="sxs-lookup"><span data-stu-id="5c9f3-282">5.10</span></span> | <span data-ttu-id="5c9f3-283">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="5c9f3-283">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="5c9f3-284">5.11</span><span class="sxs-lookup"><span data-stu-id="5c9f3-284">5.11</span></span> | <span data-ttu-id="5c9f3-285">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="5c9f3-285">Oracle 2.6.39-400 (UEK R2)</span></span> |

#### <a name="suse-linux-enterprise-server"></a><span data-ttu-id="5c9f3-286">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="5c9f3-286">SUSE Linux Enterprise Server</span></span>

#### <a name="suse-linux-11"></a><span data-ttu-id="5c9f3-287">SUSE Linux 11</span><span class="sxs-lookup"><span data-stu-id="5c9f3-287">SUSE Linux 11</span></span>

| <span data-ttu-id="5c9f3-288">**Wersja systemu operacyjnego**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-288">**OS version**</span></span> | <span data-ttu-id="5c9f3-289">**Wersja jądra**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-289">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="5c9f3-290">11</span><span class="sxs-lookup"><span data-stu-id="5c9f3-290">11</span></span> | <span data-ttu-id="5c9f3-291">2.6.27</span><span class="sxs-lookup"><span data-stu-id="5c9f3-291">2.6.27</span></span> |
| <span data-ttu-id="5c9f3-292">11 Z DODATKIEM SP1</span><span class="sxs-lookup"><span data-stu-id="5c9f3-292">11 SP1</span></span> | <span data-ttu-id="5c9f3-293">2.6.32</span><span class="sxs-lookup"><span data-stu-id="5c9f3-293">2.6.32</span></span> |
| <span data-ttu-id="5c9f3-294">11 Z DODATKIEM SP2</span><span class="sxs-lookup"><span data-stu-id="5c9f3-294">11 SP2</span></span> | <span data-ttu-id="5c9f3-295">3.0.13</span><span class="sxs-lookup"><span data-stu-id="5c9f3-295">3.0.13</span></span> |
| <span data-ttu-id="5c9f3-296">11 Z DODATKIEM SP3</span><span class="sxs-lookup"><span data-stu-id="5c9f3-296">11 SP3</span></span> | <span data-ttu-id="5c9f3-297">3.0.76</span><span class="sxs-lookup"><span data-stu-id="5c9f3-297">3.0.76</span></span> |
| <span data-ttu-id="5c9f3-298">11 Z DODATKIEM SP4</span><span class="sxs-lookup"><span data-stu-id="5c9f3-298">11 SP4</span></span> | <span data-ttu-id="5c9f3-299">3.0.101</span><span class="sxs-lookup"><span data-stu-id="5c9f3-299">3.0.101</span></span> |

#### <a name="suse-linux-10"></a><span data-ttu-id="5c9f3-300">SUSE Linux 10</span><span class="sxs-lookup"><span data-stu-id="5c9f3-300">SUSE Linux 10</span></span>

| <span data-ttu-id="5c9f3-301">**Wersja systemu operacyjnego**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-301">**OS version**</span></span> | <span data-ttu-id="5c9f3-302">**Wersja jądra**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-302">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="5c9f3-303">Z DODATKIEM SP4 10</span><span class="sxs-lookup"><span data-stu-id="5c9f3-303">10 SP4</span></span> | <span data-ttu-id="5c9f3-304">2.6.16.60</span><span class="sxs-lookup"><span data-stu-id="5c9f3-304">2.6.16.60</span></span> |

#### <a name="dependency-agent-downloads"></a><span data-ttu-id="5c9f3-305">Zależności agenta pliki do pobrania</span><span class="sxs-lookup"><span data-stu-id="5c9f3-305">Dependency Agent downloads</span></span>

| <span data-ttu-id="5c9f3-306">**Plik**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-306">**File**</span></span> | <span data-ttu-id="5c9f3-307">**SYSTEM OPERACYJNY**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-307">**OS**</span></span> | <span data-ttu-id="5c9f3-308">**Wersja**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-308">**Version**</span></span> | <span data-ttu-id="5c9f3-309">**ALGORYTM SHA-256**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-309">**SHA-256**</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="5c9f3-310">InstallDependencyAgent Windows.exe</span><span class="sxs-lookup"><span data-stu-id="5c9f3-310">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="5c9f3-311">Windows</span><span class="sxs-lookup"><span data-stu-id="5c9f3-311">Windows</span></span> | <span data-ttu-id="5c9f3-312">9.0.5</span><span class="sxs-lookup"><span data-stu-id="5c9f3-312">9.0.5</span></span> | <span data-ttu-id="5c9f3-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span><span class="sxs-lookup"><span data-stu-id="5c9f3-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span></span> |
| [<span data-ttu-id="5c9f3-314">InstallDependencyAgent Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="5c9f3-314">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="5c9f3-315">Linux</span><span class="sxs-lookup"><span data-stu-id="5c9f3-315">Linux</span></span> | <span data-ttu-id="5c9f3-316">9.0.5</span><span class="sxs-lookup"><span data-stu-id="5c9f3-316">9.0.5</span></span> | <span data-ttu-id="5c9f3-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span><span class="sxs-lookup"><span data-stu-id="5c9f3-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span></span> |



## <a name="configuration"></a><span data-ttu-id="5c9f3-318">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="5c9f3-318">Configuration</span></span>

<span data-ttu-id="5c9f3-319">Wykonaj poniższe kroki, aby skonfigurować rozwiązanie udostępniający dane dla obszarów roboczych.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-319">Perform the following steps to configure the Wire Data solution for your workspaces.</span></span>

1. <span data-ttu-id="5c9f3-320">Włącz rozwiązania analizy dzienników działania z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) lub przy użyciu procesu opisanego w [rozwiązań dodać analizy dzienników z galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="5c9f3-320">Enable the Activity Log Analytics solution from the [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="5c9f3-321">Na każdym komputerze, na którym chcesz pobrać dane, należy zainstalować agenta zależności.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-321">Install the Dependency Agent on each computer where you want to get data.</span></span> <span data-ttu-id="5c9f3-322">Dependency Agent można monitorować połączenia do natychmiastowego sąsiadów, więc nie trzeba agenta na każdym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-322">The Dependency Agent can monitor connections to immediate neighbors, so you might not need an agent on every computer.</span></span>

### <a name="install-the-dependency-agent-on-windows"></a><span data-ttu-id="5c9f3-323">Zainstaluj agenta zależności w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="5c9f3-323">Install the Dependency Agent on Windows</span></span>

<span data-ttu-id="5c9f3-324">Aby zainstalować lub odinstalować agenta wymagane są uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-324">Administrator privileges are required to install or uninstall the agent.</span></span>

<span data-ttu-id="5c9f3-325">Dependency Agent jest zainstalowany na komputerach z systemem Windows za pośrednictwem InstallDependencyAgent Windows.exe.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-325">The Dependency Agent is installed on computers running Windows through InstallDependencyAgent-Windows.exe.</span></span> <span data-ttu-id="5c9f3-326">Po uruchomieniu tego pliku wykonywalnego bez żadnych opcji uruchamia kreatora, który można wykonać w celu zainstalowania interaktywnie.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-326">If you run this executable file without any options, it starts a wizard that you can follow to install interactively.</span></span>

<span data-ttu-id="5c9f3-327">Aby zainstalować agenta zależności na każdy komputer z systemem Windows, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5c9f3-327">Use the following steps to install the Dependency Agent on each computer running Windows:</span></span>

1. <span data-ttu-id="5c9f3-328">Zainstaluj agenta pakietu OMS zgodnie z instrukcjami podanymi w [komputery Windows połączenia z usługą analizy dzienników na platformie Azure](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="5c9f3-328">Install the OMS Agent by using the instructions at [Connect Windows computers to the Log Analytics service in Azure](log-analytics-windows-agents.md).</span></span>
2. <span data-ttu-id="5c9f3-329">Pobierz agenta systemu Windows przy użyciu łącza w poprzedniej sekcji, a następnie uruchom go za pomocą następującego polecenia: InstallDependencyAgent Windows.exe</span><span class="sxs-lookup"><span data-stu-id="5c9f3-329">Download the Windows agent using the link in the previous section and then run it by using the following command: InstallDependencyAgent-Windows.exe</span></span>
3. <span data-ttu-id="5c9f3-330">Użyj kreatora, aby zainstalować agenta.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-330">Follow the wizard to install the agent.</span></span>
4. <span data-ttu-id="5c9f3-331">Jeśli Dependency Agent nie powiedzie się, sprawdź dzienniki, aby uzyskać szczegółowe informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-331">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="5c9f3-332">Agentów systemu Windows katalog dziennika jest %Programfiles%\Microsoft Agent\logs zależności.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-332">On Windows agents, the log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span>

#### <a name="windows-command-line"></a><span data-ttu-id="5c9f3-333">Wiersz polecenia systemu Windows</span><span class="sxs-lookup"><span data-stu-id="5c9f3-333">Windows command line</span></span>

<span data-ttu-id="5c9f3-334">Opcje z poniższej tabeli służą do instalacji z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-334">Use options from the following table to install from a command line.</span></span> <span data-ttu-id="5c9f3-335">Aby wyświetlić listę flagi instalacji, należy uruchomić Instalatora przy użyciu /?</span><span class="sxs-lookup"><span data-stu-id="5c9f3-335">To see a list of the installation flags, run the installer by using the /?</span></span> <span data-ttu-id="5c9f3-336">Flaga w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-336">flag as follows.</span></span>

<span data-ttu-id="5c9f3-337">InstallDependencyAgent Windows.exe /?</span><span class="sxs-lookup"><span data-stu-id="5c9f3-337">InstallDependencyAgent-Windows.exe /?</span></span>

| <span data-ttu-id="5c9f3-338">**Flaga**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-338">**Flag**</span></span> | <span data-ttu-id="5c9f3-339">**Opis**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-339">**Description**</span></span> |
| --- | --- |
| <code>/?</code> | <span data-ttu-id="5c9f3-340">Pobierz listę opcji wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-340">Get a list of the command-line options.</span></span> |
| <code>/S</code> | <span data-ttu-id="5c9f3-341">Wykonaj instalację dyskretną bez monitowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-341">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="5c9f3-342">Pliki agenta zależności systemu Windows są umieszczane w C:\Program Files\Microsoft Dependency Agent domyślnie.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-342">Files for the Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-the-dependency-agent-on-linux"></a><span data-ttu-id="5c9f3-343">Zainstaluj agenta zależności w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="5c9f3-343">Install the Dependency Agent on Linux</span></span>

<span data-ttu-id="5c9f3-344">Dostęp do konta root jest wymagane do zainstalowania i skonfigurowania agenta.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-344">Root access is required to install or configure the agent.</span></span>

<span data-ttu-id="5c9f3-345">Dependency Agent jest zainstalowany na komputery z systemem Linux za pomocą Linux64.bin InstallDependencyAgent, skrypt powłoki z samowyodrębniający plikiem binarnym.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-345">The Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="5c9f3-346">Plik ten można uruchomić przy użyciu _sh_ lub Dodaj uprawnienia w samym pliku do wykonywania.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-346">You can run the file by using _sh_ or add execute permissions to the file itself.</span></span>

<span data-ttu-id="5c9f3-347">Aby zainstalować agenta zależności na każdym komputerze z systemem Linux, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5c9f3-347">Use the following steps to install the Dependency Agent on each Linux computer:</span></span>

1. <span data-ttu-id="5c9f3-348">Zainstaluj agenta pakietu OMS zgodnie z instrukcjami podanymi w [zbierania danych i zarządzać nimi z komputerów z systemem Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5c9f3-348">Install the OMS Agent by using the instructions at [Collect and manage data from Linux computers](log-analytics-agent-linux.md).</span></span>
2. <span data-ttu-id="5c9f3-349">Pobierz agenta systemu Linux zależności przy użyciu łącza w poprzedniej sekcji, a następnie zainstaluj go jako głównego za pomocą następującego polecenia: sh InstallDependencyAgent Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="5c9f3-349">Download the Linux Dependency agent using the link in the previous section and then install it as root by using the following command: sh InstallDependencyAgent-Linux64.bin</span></span>
3. <span data-ttu-id="5c9f3-350">Jeśli Dependency Agent nie powiedzie się, sprawdź dzienniki, aby uzyskać szczegółowe informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-350">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="5c9f3-351">Na agentów systemu Linux jest katalog dziennika: /var/opt/microsoft/dependency-agent/log.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-351">On Linux agents, the log directory is: /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="5c9f3-352">Aby wyświetlić listę flagi instalacji, uruchom program instalacyjny z `-help` Flaga w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-352">To see a list of the installation flags, run the installation program with the `-help` flag as follows.</span></span>

```
InstallDependencyAgent-Linux64.bin -help
```

| <span data-ttu-id="5c9f3-353">**Flaga**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-353">**Flag**</span></span> | <span data-ttu-id="5c9f3-354">**Opis**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-354">**Description**</span></span> |
| --- | --- |
| <code>-help</code> | <span data-ttu-id="5c9f3-355">Pobierz listę opcji wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-355">Get a list of the command-line options.</span></span> |
| <code>-s</code> | <span data-ttu-id="5c9f3-356">Wykonaj instalację dyskretną bez monitowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-356">Perform a silent installation with no user prompts.</span></span> |
| <code>--check</code> | <span data-ttu-id="5c9f3-357">Sprawdź uprawnienia i systemu operacyjnego, ale nie należy instalować agenta.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-357">Check permissions and the operating system but do not install the agent.</span></span> |

<span data-ttu-id="5c9f3-358">Pliki programu Agent zależności są umieszczane w następujących katalogów:</span><span class="sxs-lookup"><span data-stu-id="5c9f3-358">Files for the Dependency Agent are placed in the following directories:</span></span>

| <span data-ttu-id="5c9f3-359">**Pliki**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-359">**Files**</span></span> | <span data-ttu-id="5c9f3-360">**Lokalizacja**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-360">**Location**</span></span> |
| --- | --- |
| <span data-ttu-id="5c9f3-361">Podstawowe pliki</span><span class="sxs-lookup"><span data-stu-id="5c9f3-361">Core files</span></span> | <span data-ttu-id="5c9f3-362">/OPT/Microsoft/Dependency-Agent</span><span class="sxs-lookup"><span data-stu-id="5c9f3-362">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="5c9f3-363">Pliki dziennika</span><span class="sxs-lookup"><span data-stu-id="5c9f3-363">Log files</span></span> | <span data-ttu-id="5c9f3-364">/var/OPT/Microsoft/Dependency-Agent/log</span><span class="sxs-lookup"><span data-stu-id="5c9f3-364">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="5c9f3-365">Pliki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="5c9f3-365">Config files</span></span> | <span data-ttu-id="5c9f3-366">/etc/OPT/Microsoft/Dependency-Agent/config</span><span class="sxs-lookup"><span data-stu-id="5c9f3-366">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="5c9f3-367">Pliki wykonywalne usługi</span><span class="sxs-lookup"><span data-stu-id="5c9f3-367">Service executable files</span></span> | <span data-ttu-id="5c9f3-368">/OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent</span><span class="sxs-lookup"><span data-stu-id="5c9f3-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><br><span data-ttu-id="5c9f3-369">/OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent-Manager</span><span class="sxs-lookup"><span data-stu-id="5c9f3-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="5c9f3-370">Pliki binarne magazynu</span><span class="sxs-lookup"><span data-stu-id="5c9f3-370">Binary storage files</span></span> | <span data-ttu-id="5c9f3-371">/var/OPT/Microsoft/Dependency-Agent/Storage</span><span class="sxs-lookup"><span data-stu-id="5c9f3-371">/var/opt/microsoft/dependency-agent/storage</span></span> |

### <a name="installation-script-examples"></a><span data-ttu-id="5c9f3-372">Przykłady skryptów instalacji</span><span class="sxs-lookup"><span data-stu-id="5c9f3-372">Installation script examples</span></span>

<span data-ttu-id="5c9f3-373">Aby łatwo wdrożyć agenta zależności na wiele serwerów na raz, pomaga za pomocą skryptu.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-373">To easily deploy the Dependency Agent on many servers at once, it helps to use a script.</span></span> <span data-ttu-id="5c9f3-374">W poniższych przykładach skrypt umożliwia pobranie i zainstalowanie agenta zależności w systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-374">You can use the following script examples to download and install the Dependency Agent on either Windows or Linux.</span></span>

#### <a name="powershell-script-for-windows"></a><span data-ttu-id="5c9f3-375">Skrypt programu PowerShell dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="5c9f3-375">PowerShell script for Windows</span></span>

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a><span data-ttu-id="5c9f3-376">Skrypt powłoki dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="5c9f3-376">Shell script for Linux</span></span>

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a><span data-ttu-id="5c9f3-377">Konfiguracja żądanego stanu</span><span class="sxs-lookup"><span data-stu-id="5c9f3-377">Desired State Configuration</span></span>

<span data-ttu-id="5c9f3-378">Aby wdrożyć Dependency Agent za pomocą konfiguracji żądanego stanu, można użyć modułu xPSDesiredStateConfiguration i kodu podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="5c9f3-378">To deploy the Dependency Agent via Desired State Configuration, you can use the xPSDesiredStateConfiguration module and a bit of code like the following:</span></span>

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install the Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-the-dependency-agent"></a><span data-ttu-id="5c9f3-379">Odinstaluj agenta zależności</span><span class="sxs-lookup"><span data-stu-id="5c9f3-379">Uninstall the Dependency Agent</span></span>

<span data-ttu-id="5c9f3-380">Poniższe sekcje umożliwiają usuwania agenta zależności.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-380">Use the following sections to help you remove the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-windows"></a><span data-ttu-id="5c9f3-381">Odinstaluj agenta zależności w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="5c9f3-381">Uninstall the Dependency Agent on Windows</span></span>

<span data-ttu-id="5c9f3-382">Administrator może odinstalować zależności agenta dla systemu Windows za pomocą Panelu sterowania.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-382">An administrator can uninstall the Dependency Agent for Windows through Control Panel.</span></span>

<span data-ttu-id="5c9f3-383">Administrator można również uruchomić %Programfiles%\Microsoft Agent\Uninstall.exe zależności można odinstalować agenta zależności.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-383">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe to uninstall the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-linux"></a><span data-ttu-id="5c9f3-384">Odinstaluj agenta zależności w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="5c9f3-384">Uninstall the Dependency Agent on Linux</span></span>

<span data-ttu-id="5c9f3-385">Aby całkowicie odinstalować agenta zależności z systemem Linux, należy usunąć sam agent i łącznika, który jest instalowany automatycznie przy użyciu agenta.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-385">To completely uninstall the Dependency Agent from Linux, you must remove the agent itself and the connector, which is installed automatically with the agent.</span></span> <span data-ttu-id="5c9f3-386">Można odinstalować zarówno przy użyciu pojedynczego następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5c9f3-386">You can uninstall both by using the following single command:</span></span>

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a><span data-ttu-id="5c9f3-387">Pakiety administracyjne</span><span class="sxs-lookup"><span data-stu-id="5c9f3-387">Management packs</span></span>

<span data-ttu-id="5c9f3-388">Po aktywowaniu podczas transmisji danych w obszarze roboczym analizy dzienników pakietu administracyjnego 300 KB są wysyłane do wszystkich serwerów z systemem Windows w tym obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-388">When Wire Data is activated in a Log Analytics workspace, a 300-KB management pack is sent to all the Windows servers in that workspace.</span></span> <span data-ttu-id="5c9f3-389">Jeśli używasz programu System Center Operations Manager agentów w [podłączonej grupy zarządzania](log-analytics-om-agents.md), Monitor zależności pakietu administracyjnego wdrażania programu System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-389">If you are using System Center Operations Manager agents in a [connected management group](log-analytics-om-agents.md), the Dependency Monitor management pack is deployed from System Center Operations Manager.</span></span> <span data-ttu-id="5c9f3-390">Jeżeli agenci są połączone bezpośrednio Log Analytics zapewnia pakietu administracyjnego.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-390">If the agents are directly connected, Log Analytics delivers the management pack.</span></span>

<span data-ttu-id="5c9f3-391">Pakiet administracyjny nosi nazwę Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-391">The management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="5c9f3-392">Jest ona zapisywana w: %Programfiles%\Microsoft monitorowania Agent\Agent\Health usługi State\Management pakietów.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-392">It's written to: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span></span> <span data-ttu-id="5c9f3-393">To źródło danych, które korzysta z pakietu administracyjnego: % Program files%\Microsoft monitorowanie Agent\Agent\Health usługi State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-393">The data source that the management pack uses is: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="using-the-solution"></a><span data-ttu-id="5c9f3-394">Użycie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="5c9f3-394">Using the solution</span></span>

<span data-ttu-id="5c9f3-395">**Instalowanie i konfigurowanie rozwiązania**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-395">**Installing and configuring the solution**</span></span>

<span data-ttu-id="5c9f3-396">Skorzystaj z poniższych informacji, aby zainstalować i skonfigurować rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-396">Use the following information to install and configure the solution.</span></span>

- <span data-ttu-id="5c9f3-397">Rozwiązanie udostępniający dane pobrania danych z komputerów z systemem Windows Server 2012 R2, Windows 8.1 i nowszych systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-397">The Wire Data solution acquires data from computers running Windows Server 2012 R2, Windows 8.1, and later operating systems.</span></span>
- <span data-ttu-id="5c9f3-398">Microsoft .NET Framework 4.0 lub nowszy jest wymagany na komputerach, na którym chcesz uzyskać udostępniający dane z.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-398">Microsoft .NET Framework 4.0 or later is required on computers where you want to acquire wire data from.</span></span>
- <span data-ttu-id="5c9f3-399">Dodaj rozwiązanie przesyłania danych do obszaru roboczego analizy dzienników przy użyciu procesu opisanego w [rozwiązań dodać analizy dzienników z galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="5c9f3-399">Add the Wire Data solution to your Log Analytics workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="5c9f3-400">Nie są wymagane żadne dalsze czynności konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-400">There is no further configuration required.</span></span>
- <span data-ttu-id="5c9f3-401">Aby wyświetlić udostępniający dane dla konkretnego rozwiązania, należy mieć rozwiązanie już dodana do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-401">If you want to view wire data for a specific solution, you need to have the solution already added to your workspace.</span></span>

<span data-ttu-id="5c9f3-402">Po zostać zainstalowani agenci i zainstalować rozwiązania, w obszarze roboczym pojawi się Kafelek podczas transmisji danych 2.0.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-402">After you have agents installed and you install the solution, the Wire Data 2.0 tile appears in your workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="5c9f3-403">Obecnie do wyświetlenia podczas transmisji danych trzeba użyć portalu OMS.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-403">Currently, you must use the OMS portal to view wire data.</span></span> <span data-ttu-id="5c9f3-404">Nie można użyć portalu Azure do wyświetlania danych danych przesyłanych w sieci.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-404">You cannot use the Azure portal to view wire data.</span></span>

![Podczas transmisji danych kafelków](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-the-wire-data-20-solution"></a><span data-ttu-id="5c9f3-406">Za pomocą rozwiązania podczas transmisji danych 2.0</span><span class="sxs-lookup"><span data-stu-id="5c9f3-406">Using the Wire Data 2.0 solution</span></span>

<span data-ttu-id="5c9f3-407">W portalu OMS kliknij **podczas transmisji danych 2.0** Kafelek, aby otworzyć pulpit nawigacyjny udostępniający dane.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-407">In the OMS portal, click the **Wire Data 2.0** tile to open the Wire Data dashboard.</span></span> <span data-ttu-id="5c9f3-408">Pulpit nawigacyjny zawiera bloki w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-408">The dashboard includes the blades in the following table.</span></span> <span data-ttu-id="5c9f3-409">Każdy blok zawiera maksymalnie 10 elementów spełniających kryteria tego bloku dla określonego zakresu i zakres czasu.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-409">Each blade lists up to 10 items matching that blade's criteria for the specified scope and time range.</span></span> <span data-ttu-id="5c9f3-410">Można uruchomić wyszukiwania dziennika, który zwraca wszystkie rekordy, klikając **zobaczyć wszystkie** w dolnej części bloku lub przez kliknięcie nagłówka bloku.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-410">You can run a log search that returns all records by clicking **See all** at the bottom of the blade or by clicking the blade header.</span></span>

| <span data-ttu-id="5c9f3-411">**Blok**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-411">**Blade**</span></span> | <span data-ttu-id="5c9f3-412">**Opis**</span><span class="sxs-lookup"><span data-stu-id="5c9f3-412">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="5c9f3-413">Agenci przechwytujący ruch sieciowy</span><span class="sxs-lookup"><span data-stu-id="5c9f3-413">Agents capturing network traffic</span></span> | <span data-ttu-id="5c9f3-414">Zawiera liczbę agentów, które są Przechwytywanie ruchu sieciowego i listę top 10 komputerów, które są Przechwytywanie ruchu.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-414">Shows the number of agents that are capturing network traffic and lists the top 10 computers that are capturing traffic.</span></span> <span data-ttu-id="5c9f3-415">Kliknij liczbę do uruchamiania dziennika wyszukiwanie <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-415">Click the number to run a log search for <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span></span> <span data-ttu-id="5c9f3-416">Kliknij komputer, na liście do uruchomienia zwracanie całkowita liczba bajtów przechwytywane wyszukiwanie dziennika.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-416">Click a computer in the list to run a log search returning the total number of bytes captured.</span></span> |
| <span data-ttu-id="5c9f3-417">Lokalne podsieci</span><span class="sxs-lookup"><span data-stu-id="5c9f3-417">Local Subnets</span></span> | <span data-ttu-id="5c9f3-418">Pokazuje liczbę podsieci lokalne, które zostały odnalezione agentów.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-418">Shows the number of local subnets that agents have discovered.</span></span>  <span data-ttu-id="5c9f3-419">Kliknij liczbę do uruchamiania dziennika wyszukiwanie <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> które wyświetla listę wszystkich podsieci z liczbę bajtów przesyłanych w ramach każdej z nich.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-419">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> that lists all subnets with the number of bytes sent over each one.</span></span> <span data-ttu-id="5c9f3-420">Kliknij przycisk podsieci na liście, aby uruchomić wyszukiwanie dziennika zwracanie całkowita liczba bajtów wysłanych w tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-420">Click a subnet in the list to run a log search returning the total number of bytes sent over the subnet.</span></span> |
| <span data-ttu-id="5c9f3-421">Protokoły poziomu aplikacji</span><span class="sxs-lookup"><span data-stu-id="5c9f3-421">Application-level Protocols</span></span> | <span data-ttu-id="5c9f3-422">Pokazuje liczbę protokoły poziomu aplikacji w użyciu, wykrywane przez agentów.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-422">Shows the number of application-level protocols in use, as discovered by agents.</span></span> <span data-ttu-id="5c9f3-423">Kliknij liczbę do uruchamiania dziennika wyszukiwanie <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-423">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span></span> <span data-ttu-id="5c9f3-424">Kliknij protokół, aby uruchomić wyszukiwanie dziennika zwracanie całkowita liczba bajtów wysłanych przy użyciu protokołu.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-424">Click a protocol to run a log search returning the total number of bytes sent using the protocol.</span></span> |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Podczas transmisji danych z pulpitu nawigacyjnego](./media/log-analytics-wire-data/wire-data-dash.png)

<span data-ttu-id="5c9f3-426">Można użyć **agenci przechwytujący ruch sieciowy** bloku, aby ustalić, jaka przepustowość sieci jest są używane przez komputery.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-426">You can use the **Agents capturing network traffic** blade to determine how much network bandwidth is being consumed by computers.</span></span> <span data-ttu-id="5c9f3-427">Ten blok mogą pomóc w prosty sposób wyszukiwać _chattiest_ komputera w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-427">This blade can help you easily find the _chattiest_ computer in your environment.</span></span> <span data-ttu-id="5c9f3-428">Komputery te może być przeciążony działający nieprawidłowo lub przy użyciu więcej zasobów sieci niż zwykle.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-428">Such computers could be overloaded, acting abnormally, or using more network resources than normal.</span></span>

![Przykład wyszukiwania dziennika](./media/log-analytics-wire-data/log-search-example01.png)

<span data-ttu-id="5c9f3-430">Analogicznie, można użyć **podsieci lokalne** bloku, aby określić, ile ruch sieciowy jest przenoszenie za pomocą podsieci.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-430">Similarly, you can use the **Local Subnets** blade to determine how much network traffic is moving through your subnets.</span></span> <span data-ttu-id="5c9f3-431">Użytkownicy często definiować podsieci wokół najważniejsze obszary, w przypadku ich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-431">Users often define subnets around critical areas for their applications.</span></span> <span data-ttu-id="5c9f3-432">Ten blok oferuje zapewnia wgląd w tych obszarach.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-432">This blade offers a view into those areas.</span></span>

![Przykład wyszukiwania dziennika](./media/log-analytics-wire-data/log-search-example02.png)

<span data-ttu-id="5c9f3-434">**Protokoły poziomu aplikacji** bloku przydaje się, dlatego warto wiedzieć, jakie protokoły są używane.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-434">The **Application-level Protocols** blade is useful because it's helpful know what protocols are in use.</span></span> <span data-ttu-id="5c9f3-435">Na przykład może spodziewać się SSH nie będzie używana w środowisku sieciowym.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-435">For example, you might expect SSH to not be in use in your network environment.</span></span> <span data-ttu-id="5c9f3-436">Wyświetlanie informacji o dostępnych w bloku można szybko potwierdzenia lub disprove Twoje oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-436">Viewing information available in the blade can quickly confirm or disprove your expectation.</span></span>

![Przykład wyszukiwania dziennika](./media/log-analytics-wire-data/log-search-example03.png)

<span data-ttu-id="5c9f3-438">W tym przykładzie użytkownik może Wejdź do szczegóły SSH, aby wyświetlić komputery, które korzystają z protokołu SSH i inne szczegóły komunikacji.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-438">In this example, you could drill-into SSH details to see which computers are using SSH and many other communication details.</span></span>

![Pokaż wyniki wyszukiwania](./media/log-analytics-wire-data/ssh-details.png)

<span data-ttu-id="5c9f3-440">Jest również warto wiedzieć, jeśli ruch w protokole jest zwiększenie lub zmniejszenie wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-440">It's also useful to know if protocol traffic is increasing or decreasing over time.</span></span> <span data-ttu-id="5c9f3-441">Na przykład jeśli wzrasta ilość danych przesyłanych przez aplikację, która może być coś, co należy zwrócić uwagę, lub czy można znaleźć warte wymienienia.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-441">For example, if the amount of data being transmitted by an application is increasing, that might be something you should be aware of, or that you might find noteworthy.</span></span>

## <a name="input-data"></a><span data-ttu-id="5c9f3-442">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="5c9f3-442">Input data</span></span>

<span data-ttu-id="5c9f3-443">Podczas transmisji danych zbiera metadane dotyczące ruchu sieciowego przy użyciu agentów, które zostało włączone.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-443">Wire data collects metadata about network traffic using the agents that you have enabled.</span></span> <span data-ttu-id="5c9f3-444">Każdy agent wysyła dane dotyczące co 15 s.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-444">Each agent sends data about every 15 seconds.</span></span>

## <a name="output-data"></a><span data-ttu-id="5c9f3-445">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="5c9f3-445">Output data</span></span>

<span data-ttu-id="5c9f3-446">Rekord o typie _WireData_ jest tworzony dla każdego typu danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-446">A record with a type of _WireData_ is created for each type of input data.</span></span> <span data-ttu-id="5c9f3-447">Rejestruje WireData mają właściwości poniższą tabelą:</span><span class="sxs-lookup"><span data-stu-id="5c9f3-447">WireData records have properties shown in the following table:</span></span>

| <span data-ttu-id="5c9f3-448">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5c9f3-448">Property</span></span> | <span data-ttu-id="5c9f3-449">Opis</span><span class="sxs-lookup"><span data-stu-id="5c9f3-449">Description</span></span> |
|---|---|
| <span data-ttu-id="5c9f3-450">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="5c9f3-450">Computer</span></span> | <span data-ttu-id="5c9f3-451">Nazwa komputera, w których zebrano dane</span><span class="sxs-lookup"><span data-stu-id="5c9f3-451">Computer name where data was collected</span></span> |
| <span data-ttu-id="5c9f3-452">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="5c9f3-452">TimeGenerated</span></span> | <span data-ttu-id="5c9f3-453">Czas rekordu</span><span class="sxs-lookup"><span data-stu-id="5c9f3-453">Time of the record</span></span> |
| <span data-ttu-id="5c9f3-454">LocalIP</span><span class="sxs-lookup"><span data-stu-id="5c9f3-454">LocalIP</span></span> | <span data-ttu-id="5c9f3-455">Adres IP komputera lokalnego</span><span class="sxs-lookup"><span data-stu-id="5c9f3-455">IP address of the local computer</span></span> |
| <span data-ttu-id="5c9f3-456">SessionState</span><span class="sxs-lookup"><span data-stu-id="5c9f3-456">SessionState</span></span> | <span data-ttu-id="5c9f3-457">Połączone lub rozłączone</span><span class="sxs-lookup"><span data-stu-id="5c9f3-457">Connected or disconnected</span></span> |
| <span data-ttu-id="5c9f3-458">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="5c9f3-458">ReceivedBytes</span></span> | <span data-ttu-id="5c9f3-459">Liczba bajtów odebranych</span><span class="sxs-lookup"><span data-stu-id="5c9f3-459">Amount of bytes received</span></span> |
| <span data-ttu-id="5c9f3-460">ProtocolName</span><span class="sxs-lookup"><span data-stu-id="5c9f3-460">ProtocolName</span></span> | <span data-ttu-id="5c9f3-461">Nazwa używanego protokołu sieciowego</span><span class="sxs-lookup"><span data-stu-id="5c9f3-461">Name of the network protocol used</span></span> |
| <span data-ttu-id="5c9f3-462">Wersję adresu IP ustawioną</span><span class="sxs-lookup"><span data-stu-id="5c9f3-462">IPVersion</span></span> | <span data-ttu-id="5c9f3-463">Wersji protokołu IP</span><span class="sxs-lookup"><span data-stu-id="5c9f3-463">IP version</span></span> |
| <span data-ttu-id="5c9f3-464">Kierunek</span><span class="sxs-lookup"><span data-stu-id="5c9f3-464">Direction</span></span> | <span data-ttu-id="5c9f3-465">Przychodzący lub wychodzący</span><span class="sxs-lookup"><span data-stu-id="5c9f3-465">Inbound or outbound</span></span> |
| <span data-ttu-id="5c9f3-466">MaliciousIP</span><span class="sxs-lookup"><span data-stu-id="5c9f3-466">MaliciousIP</span></span> | <span data-ttu-id="5c9f3-467">Adres IP znanego złośliwego źródła</span><span class="sxs-lookup"><span data-stu-id="5c9f3-467">IP address of a known malicious source</span></span> |
| <span data-ttu-id="5c9f3-468">Ważność</span><span class="sxs-lookup"><span data-stu-id="5c9f3-468">Severity</span></span> | <span data-ttu-id="5c9f3-469">Ważność podejrzanych złośliwego oprogramowania</span><span class="sxs-lookup"><span data-stu-id="5c9f3-469">Suspected malware severity</span></span> |
| <span data-ttu-id="5c9f3-470">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="5c9f3-470">RemoteIPCountry</span></span> | <span data-ttu-id="5c9f3-471">Kraj zdalny adres IP</span><span class="sxs-lookup"><span data-stu-id="5c9f3-471">Country of the remote IP address</span></span> |
| <span data-ttu-id="5c9f3-472">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="5c9f3-472">ManagementGroupName</span></span> | <span data-ttu-id="5c9f3-473">Nazwa grupy zarządzania programu Operations Manager</span><span class="sxs-lookup"><span data-stu-id="5c9f3-473">Name of the Operations Manager management group</span></span> |
| <span data-ttu-id="5c9f3-474">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="5c9f3-474">SourceSystem</span></span> | <span data-ttu-id="5c9f3-475">Źródło, gdzie zostały zebrane dane</span><span class="sxs-lookup"><span data-stu-id="5c9f3-475">Source where data was collected</span></span> |
| <span data-ttu-id="5c9f3-476">SessionStartTime</span><span class="sxs-lookup"><span data-stu-id="5c9f3-476">SessionStartTime</span></span> | <span data-ttu-id="5c9f3-477">Czas rozpoczęcia sesji</span><span class="sxs-lookup"><span data-stu-id="5c9f3-477">Start time of session</span></span> |
| <span data-ttu-id="5c9f3-478">SessionEndTime</span><span class="sxs-lookup"><span data-stu-id="5c9f3-478">SessionEndTime</span></span> | <span data-ttu-id="5c9f3-479">Godzina zakończenia sesji</span><span class="sxs-lookup"><span data-stu-id="5c9f3-479">End time of session</span></span> |
| <span data-ttu-id="5c9f3-480">LocalSubnet</span><span class="sxs-lookup"><span data-stu-id="5c9f3-480">LocalSubnet</span></span> | <span data-ttu-id="5c9f3-481">Podsieć, w których zebrano dane</span><span class="sxs-lookup"><span data-stu-id="5c9f3-481">Subnet where data was collected</span></span> |
| <span data-ttu-id="5c9f3-482">LocalPortNumber</span><span class="sxs-lookup"><span data-stu-id="5c9f3-482">LocalPortNumber</span></span> | <span data-ttu-id="5c9f3-483">Numer portu lokalnego</span><span class="sxs-lookup"><span data-stu-id="5c9f3-483">Local port number</span></span> |
| <span data-ttu-id="5c9f3-484">RemoteIP</span><span class="sxs-lookup"><span data-stu-id="5c9f3-484">RemoteIP</span></span> | <span data-ttu-id="5c9f3-485">Zdalny adres IP używany przez komputer zdalny</span><span class="sxs-lookup"><span data-stu-id="5c9f3-485">Remote IP address used by the remote computer</span></span> |
| <span data-ttu-id="5c9f3-486">RemotePortNumber</span><span class="sxs-lookup"><span data-stu-id="5c9f3-486">RemotePortNumber</span></span> | <span data-ttu-id="5c9f3-487">Numer portu używany przez zdalny adres IP</span><span class="sxs-lookup"><span data-stu-id="5c9f3-487">Port number used by the remote IP address</span></span> |
| <span data-ttu-id="5c9f3-488">Identyfikator sesji</span><span class="sxs-lookup"><span data-stu-id="5c9f3-488">SessionID</span></span> | <span data-ttu-id="5c9f3-489">Unikatowa wartość, która identyfikuje sesji komunikacji między dwoma adresami IP</span><span class="sxs-lookup"><span data-stu-id="5c9f3-489">A unique value that identifies communication session between two IP addresses</span></span> |
| <span data-ttu-id="5c9f3-490">SentBytes</span><span class="sxs-lookup"><span data-stu-id="5c9f3-490">SentBytes</span></span> | <span data-ttu-id="5c9f3-491">Liczba bajtów wysłanych</span><span class="sxs-lookup"><span data-stu-id="5c9f3-491">Number of bytes sent</span></span> |
| <span data-ttu-id="5c9f3-492">TotalBytes</span><span class="sxs-lookup"><span data-stu-id="5c9f3-492">TotalBytes</span></span> | <span data-ttu-id="5c9f3-493">Całkowita liczba bajtów wysłanych podczas sesji</span><span class="sxs-lookup"><span data-stu-id="5c9f3-493">Total number of bytes sent during session</span></span> |
| <span data-ttu-id="5c9f3-494">ApplicationProtocol</span><span class="sxs-lookup"><span data-stu-id="5c9f3-494">ApplicationProtocol</span></span> | <span data-ttu-id="5c9f3-495">Typ protokołu sieciowego używane</span><span class="sxs-lookup"><span data-stu-id="5c9f3-495">Type of network protocol used</span></span>   |
| <span data-ttu-id="5c9f3-496">Identyfikator procesu</span><span class="sxs-lookup"><span data-stu-id="5c9f3-496">ProcessID</span></span> | <span data-ttu-id="5c9f3-497">Identyfikator procesu systemu Windows</span><span class="sxs-lookup"><span data-stu-id="5c9f3-497">Windows process ID</span></span> |
| <span data-ttu-id="5c9f3-498">Parametr</span><span class="sxs-lookup"><span data-stu-id="5c9f3-498">ProcessName</span></span> | <span data-ttu-id="5c9f3-499">Ścieżka i nazwa pliku procesu</span><span class="sxs-lookup"><span data-stu-id="5c9f3-499">Path and file name of the process</span></span> |
| <span data-ttu-id="5c9f3-500">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="5c9f3-500">RemoteIPLongitude</span></span> | <span data-ttu-id="5c9f3-501">Wartości długości geograficznej IP</span><span class="sxs-lookup"><span data-stu-id="5c9f3-501">IP longitude value</span></span> |
| <span data-ttu-id="5c9f3-502">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="5c9f3-502">RemoteIPLatitude</span></span> | <span data-ttu-id="5c9f3-503">Wartość szerokości geograficznej IP</span><span class="sxs-lookup"><span data-stu-id="5c9f3-503">IP latitude value</span></span> |


## <a name="next-steps"></a><span data-ttu-id="5c9f3-504">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5c9f3-504">Next steps</span></span>

- <span data-ttu-id="5c9f3-505">[Wyszukaj dzienniki](log-analytics-log-searches.md) Aby wyświetlić szczegółowe podczas transmisji danych wyszukiwanie rekordów.</span><span class="sxs-lookup"><span data-stu-id="5c9f3-505">[Search logs](log-analytics-log-searches.md) to view detailed wire data search records.</span></span>
