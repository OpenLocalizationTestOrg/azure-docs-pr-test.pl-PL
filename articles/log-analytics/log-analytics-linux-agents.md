---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: TRUE
ROBOTS: NOINDEX
ms.openlocfilehash: 8332bdd39effab8c2ac9a75ca9a1e2510c940719
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-linux-computers-to-log-analytics"></a><span data-ttu-id="b32ea-101">Łączenie komputerów Linux do analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="b32ea-101">Connect your Linux computers to Log Analytics</span></span>
<span data-ttu-id="b32ea-102">Za pomocą analizy dzienników, można zbierać i działają na danych generowanych przez komputery z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="b32ea-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="b32ea-103">Dodawanie danych zbieranych z systemem Linux z usługą OMS umożliwia zarządzanie systemów Linux i kontener rozwiązań, takich jak Docker, niezależnie od tego, w którym znajdują się komputery — niemal dowolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="b32ea-103">Adding data collected from Linux to OMS allows you to manage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="b32ea-104">Źródła danych mogą znajdować się w lokalnym centrum danych jako serwerów fizycznych komputerów wirtualnych w usług hostowanych w chmurze, takich jak Amazon Web Services (AWS) lub Microsoft Azure lub nawet laptopów na biurku.</span><span class="sxs-lookup"><span data-stu-id="b32ea-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even the laptop on your desk.</span></span> <span data-ttu-id="b32ea-105">Ponadto OMS również zbiera dane z komputerów z systemem Windows podobnie, obsługuje on naprawdę hybrydowe środowiska IT.</span><span class="sxs-lookup"><span data-stu-id="b32ea-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="b32ea-106">Można wyświetlić i zarządzać danych ze wszystkich tych źródeł z analizy dzienników w OMS za pomocą portalu zarządzania pojedynczego.</span><span class="sxs-lookup"><span data-stu-id="b32ea-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="b32ea-107">Zmniejsza to potrzebę monitorowania przy użyciu wielu różnych systemów, sprawia, że ułatwiają korzystanie, na które można wyeksportować danych, które chcesz niezależnie od rozwiązania analizy biznesowej lub system, który już istnieje.</span><span class="sxs-lookup"><span data-stu-id="b32ea-107">This reduces the need to monitor it using many different systems, makes it easy to consume, and you can export any data you like to whatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="b32ea-108">W tym artykule jest szybki start przewodnik, które zawierają informacje pomocne podczas zbierania danych i zarządzać nimi komputerów systemu Linux przy użyciu agenta pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b32ea-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using the OMS Agent for Linux.</span></span> <span data-ttu-id="b32ea-109">Aby uzyskać więcej szczegółowych informacji technicznych, takich jak konfiguracja serwera proxy, informacje o CollectD metryki i niestandardowych źródeł danych JSON, znajdziesz te informacje w [Agent pakietu OMS dla systemu Linux — omówienie](https://github.com/Microsoft/OMS-Agent-for-Linux) i [Agent pakietu OMS dla systemu Linux Pełna dokumentacja](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="b32ea-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="b32ea-110">Obecnie można zebrać następujące typy danych z komputerów z systemem Linux:</span><span class="sxs-lookup"><span data-stu-id="b32ea-110">Currently, you can collect the following types of data from Linux computers:</span></span>

* <span data-ttu-id="b32ea-111">Metryki wydajności</span><span class="sxs-lookup"><span data-stu-id="b32ea-111">Performance metrics</span></span>
* <span data-ttu-id="b32ea-112">Zdarzenia dziennika systemowego</span><span class="sxs-lookup"><span data-stu-id="b32ea-112">Syslog events</span></span>
* <span data-ttu-id="b32ea-113">Alerty z Nagios i Zabbix</span><span class="sxs-lookup"><span data-stu-id="b32ea-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="b32ea-114">Metryki wydajności kontenera docker, spisu i dzienniki</span><span class="sxs-lookup"><span data-stu-id="b32ea-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="b32ea-115">Obsługiwane wersje systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-115">Supported Linux versions</span></span>
<span data-ttu-id="b32ea-116">Wersje x x86 i x64 oficjalnie są obsługiwane w różnych dystrybucje systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b32ea-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="b32ea-117">Jednak Agent pakietu OMS dla systemu Linux mogą również uruchomić na innych dystrybucje nie na liście.</span><span class="sxs-lookup"><span data-stu-id="b32ea-117">However, the OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="b32ea-118">Linux Amazon 2012.09 za pośrednictwem 2015.09</span><span class="sxs-lookup"><span data-stu-id="b32ea-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="b32ea-119">CentOS Linux 5, 6 i 7</span><span class="sxs-lookup"><span data-stu-id="b32ea-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="b32ea-120">Oracle Linux 5, 6 i 7</span><span class="sxs-lookup"><span data-stu-id="b32ea-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="b32ea-121">Red Hat Enterprise Linux Server 5, 6 i 7</span><span class="sxs-lookup"><span data-stu-id="b32ea-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="b32ea-122">Debian GNU/Linux 6, 7 i 8</span><span class="sxs-lookup"><span data-stu-id="b32ea-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="b32ea-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="b32ea-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="b32ea-124">SUSE Linux Enterprise Server 11 i 12</span><span class="sxs-lookup"><span data-stu-id="b32ea-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="b32ea-125">Agent pakietu OMS dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-125">OMS Agent for Linux</span></span>
<span data-ttu-id="b32ea-126">Agent programu Operations Management Suite dla systemu Linux składa się z wielu pakietów.</span><span class="sxs-lookup"><span data-stu-id="b32ea-126">The Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="b32ea-127">Plik wersji zawiera następujących pakietów, dostępne za pomocą powłoki pakietu z `--extract`.</span><span class="sxs-lookup"><span data-stu-id="b32ea-127">The release file contains the following packages, available by running the shell bundle with `--extract`.</span></span>

| <span data-ttu-id="b32ea-128">**Pakiet**</span><span class="sxs-lookup"><span data-stu-id="b32ea-128">**Package**</span></span> | <span data-ttu-id="b32ea-129">**Wersja**</span><span class="sxs-lookup"><span data-stu-id="b32ea-129">**Version**</span></span> | <span data-ttu-id="b32ea-130">**Opis**</span><span class="sxs-lookup"><span data-stu-id="b32ea-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b32ea-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="b32ea-131">omsagent</span></span> |<span data-ttu-id="b32ea-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b32ea-132">1.1.0</span></span> |<span data-ttu-id="b32ea-133">Agent programu Operations Management Suite dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-133">The Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="b32ea-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="b32ea-134">omsconfig</span></span> |<span data-ttu-id="b32ea-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b32ea-135">1.1.1</span></span> |<span data-ttu-id="b32ea-136">Agent konfiguracji dla agenta pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="b32ea-136">Configuration agent for the OMS Agent</span></span> |
| <span data-ttu-id="b32ea-137">OMI</span><span class="sxs-lookup"><span data-stu-id="b32ea-137">omi</span></span> |<span data-ttu-id="b32ea-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="b32ea-138">1.0.8.3</span></span> |<span data-ttu-id="b32ea-139">Open Management Infrastructure (OMI)--lekkie serwera modelu wspólnych informacji</span><span class="sxs-lookup"><span data-stu-id="b32ea-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="b32ea-140">scx</span><span class="sxs-lookup"><span data-stu-id="b32ea-140">scx</span></span> |<span data-ttu-id="b32ea-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="b32ea-141">1.6.2</span></span> |<span data-ttu-id="b32ea-142">OMI CIM dostawców dla metryki wydajności systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="b32ea-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="b32ea-143">Apache cimprov</span><span class="sxs-lookup"><span data-stu-id="b32ea-143">apache-cimprov</span></span> |<span data-ttu-id="b32ea-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b32ea-144">1.0.0</span></span> |<span data-ttu-id="b32ea-145">Monitorowanie dostawcę dla OMI wydajności Apache HTTP Server.</span><span class="sxs-lookup"><span data-stu-id="b32ea-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="b32ea-146">Zainstalować tylko w przypadku wykrycia Apache HTTP Server.</span><span class="sxs-lookup"><span data-stu-id="b32ea-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="b32ea-147">MySQL cimprov</span><span class="sxs-lookup"><span data-stu-id="b32ea-147">mysql-cimprov</span></span> |<span data-ttu-id="b32ea-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b32ea-148">1.0.0</span></span> |<span data-ttu-id="b32ea-149">Monitorowanie dostawcę dla OMI wydajności serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="b32ea-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="b32ea-150">Zainstalować tylko w przypadku wykrycia MySQL/MariaDB serwera.</span><span class="sxs-lookup"><span data-stu-id="b32ea-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="b32ea-151">docker cimprov</span><span class="sxs-lookup"><span data-stu-id="b32ea-151">docker-cimprov</span></span> |<span data-ttu-id="b32ea-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="b32ea-152">0.1.0</span></span> |<span data-ttu-id="b32ea-153">Dostawca docker OMI.</span><span class="sxs-lookup"><span data-stu-id="b32ea-153">Docker provider for OMI.</span></span> <span data-ttu-id="b32ea-154">Zainstalować tylko w przypadku wykrycia Docker.</span><span class="sxs-lookup"><span data-stu-id="b32ea-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="b32ea-155">Artefakty dodatkowych instalacji</span><span class="sxs-lookup"><span data-stu-id="b32ea-155">Additional installation artifacts</span></span>
<span data-ttu-id="b32ea-156">Po zainstalowaniu agenta pakietu OMS pakietów systemu Linux, są stosowane następujące zmiany w dodatkowych konfiguracji całego systemu.</span><span class="sxs-lookup"><span data-stu-id="b32ea-156">After installing the OMS agent for Linux packages, the following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="b32ea-157">Te artefakty muszą zostać usunięte po odinstalowaniu pakietu omsagent.</span><span class="sxs-lookup"><span data-stu-id="b32ea-157">These artifacts are removed when the omsagent package is uninstalled.</span></span>

* <span data-ttu-id="b32ea-158">Użytkownik bez uprawnień o nazwie: `omsagent` jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="b32ea-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="b32ea-159">Jest to konto, które demona omsagent działa jako</span><span class="sxs-lookup"><span data-stu-id="b32ea-159">This is the account the omsagent daemon runs as</span></span>
* <span data-ttu-id="b32ea-160">Plik "Dołącz" sudoers jest tworzony w /etc/sudoers.d/omsagent to autoryzuje omsagent ponowne uruchomienie demonów syslog i omsagent.</span><span class="sxs-lookup"><span data-stu-id="b32ea-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent to restart the syslog and omsagent daemons.</span></span> <span data-ttu-id="b32ea-161">Jeśli dyrektywy "Dołącz" sudo nie są obsługiwane w zainstalowanej wersji programu sudo, te wpisy będą zapisywane /etc/sudoers.</span><span class="sxs-lookup"><span data-stu-id="b32ea-161">If sudo “include” directives are not supported in the installed version of sudo, these entries will be written to /etc/sudoers.</span></span>
* <span data-ttu-id="b32ea-162">Zmodyfikowaniu konfiguracji syslog do przekazywania podzbiór zdarzeń na agencie.</span><span class="sxs-lookup"><span data-stu-id="b32ea-162">The syslog configuration is modified to forward a subset of events to the agent.</span></span> <span data-ttu-id="b32ea-163">Aby uzyskać więcej informacji, zobacz **Konfigurowanie zbierania danych** poniższej sekcji</span><span class="sxs-lookup"><span data-stu-id="b32ea-163">For more information, see the **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="b32ea-164">Szczegóły pobierania danych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-164">Linux data collection details</span></span>
<span data-ttu-id="b32ea-165">W poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak zbierane są dane.</span><span class="sxs-lookup"><span data-stu-id="b32ea-165">The following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="b32ea-166">Źródło</span><span class="sxs-lookup"><span data-stu-id="b32ea-166">source</span></span> | <span data-ttu-id="b32ea-167">Bezpośrednie agenta</span><span class="sxs-lookup"><span data-stu-id="b32ea-167">Direct Agent</span></span> | <span data-ttu-id="b32ea-168">Agenta programu SCOM</span><span class="sxs-lookup"><span data-stu-id="b32ea-168">SCOM agent</span></span> | <span data-ttu-id="b32ea-169">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b32ea-169">Azure Storage</span></span> | <span data-ttu-id="b32ea-170">SCOM wymagane?</span><span class="sxs-lookup"><span data-stu-id="b32ea-170">SCOM required?</span></span> | <span data-ttu-id="b32ea-171">Dane agenta programu SCOM wysyłane za pośrednictwem grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="b32ea-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="b32ea-172">Częstotliwość kolekcji</span><span class="sxs-lookup"><span data-stu-id="b32ea-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="b32ea-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="b32ea-173">Zabbix</span></span> |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="b32ea-179">1 minuta</span><span class="sxs-lookup"><span data-stu-id="b32ea-179">1 minute</span></span> |
| <span data-ttu-id="b32ea-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="b32ea-180">Nagios</span></span> |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="b32ea-186">po przybyciu</span><span class="sxs-lookup"><span data-stu-id="b32ea-186">on arrival</span></span> |
| <span data-ttu-id="b32ea-187">syslog</span><span class="sxs-lookup"><span data-stu-id="b32ea-187">syslog</span></span> |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="b32ea-193">z usługi Azure storage: 10 minut; od agenta: Przy nadejściu</span><span class="sxs-lookup"><span data-stu-id="b32ea-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="b32ea-194">Liczniki wydajności systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-194">Linux performance counters</span></span> |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="b32ea-200">jako zaplanowane, co najmniej 10 sekund</span><span class="sxs-lookup"><span data-stu-id="b32ea-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="b32ea-201">Śledzenie zmian</span><span class="sxs-lookup"><span data-stu-id="b32ea-201">change tracking</span></span> |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="b32ea-207">co godzinę</span><span class="sxs-lookup"><span data-stu-id="b32ea-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="b32ea-208">Wymagania pakietu</span><span class="sxs-lookup"><span data-stu-id="b32ea-208">Package Requirements</span></span>
| <span data-ttu-id="b32ea-209">**Wymagany pakiet**</span><span class="sxs-lookup"><span data-stu-id="b32ea-209">**Required package**</span></span> | <span data-ttu-id="b32ea-210">**Opis**</span><span class="sxs-lookup"><span data-stu-id="b32ea-210">**Description**</span></span> | <span data-ttu-id="b32ea-211">**Minimalna wersja**</span><span class="sxs-lookup"><span data-stu-id="b32ea-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b32ea-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="b32ea-212">Glibc</span></span> |<span data-ttu-id="b32ea-213">Biblioteka GNU C</span><span class="sxs-lookup"><span data-stu-id="b32ea-213">GNU C library</span></span> |<span data-ttu-id="b32ea-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="b32ea-214">2.5-12</span></span> |
| <span data-ttu-id="b32ea-215">Biblioteki Openssl</span><span class="sxs-lookup"><span data-stu-id="b32ea-215">Openssl</span></span> |<span data-ttu-id="b32ea-216">Biblioteki OpenSSL</span><span class="sxs-lookup"><span data-stu-id="b32ea-216">OpenSSL libraries</span></span> |<span data-ttu-id="b32ea-217">0.9.8e lub 1.0</span><span class="sxs-lookup"><span data-stu-id="b32ea-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="b32ea-218">Narzędzie curl</span><span class="sxs-lookup"><span data-stu-id="b32ea-218">Curl</span></span> |<span data-ttu-id="b32ea-219">cURL klienta sieci web</span><span class="sxs-lookup"><span data-stu-id="b32ea-219">cURL web client</span></span> |<span data-ttu-id="b32ea-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="b32ea-220">7.15.5</span></span> |
| <span data-ttu-id="b32ea-221">Ctypes języka Python</span><span class="sxs-lookup"><span data-stu-id="b32ea-221">Python-ctypes</span></span> |<span data-ttu-id="b32ea-222">Funkcja biblioteki</span><span class="sxs-lookup"><span data-stu-id="b32ea-222">function libraries</span></span> |<span data-ttu-id="b32ea-223">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="b32ea-223">n/a</span></span> |
| <span data-ttu-id="b32ea-224">PAM</span><span class="sxs-lookup"><span data-stu-id="b32ea-224">PAM</span></span> |<span data-ttu-id="b32ea-225">Uwierzytelnianie podłączane moduły</span><span class="sxs-lookup"><span data-stu-id="b32ea-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="b32ea-226">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="b32ea-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="b32ea-227">Rsyslog lub syslog ng są wymagane do zbierania komunikaty dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="b32ea-227">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="b32ea-228">Demon syslog domyślne w wersji 5 (sysklog) w wersji Red Hat Enterprise Linux, CentOS i Oracle Linux nie jest obsługiwana dla zbierania zdarzeń usługi syslog.</span><span class="sxs-lookup"><span data-stu-id="b32ea-228">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="b32ea-229">Aby zbierać dane syslog z tej wersji tych dystrybucji, demona rsyslog powinna być zainstalowana i skonfigurowana zastąpić sysklog.</span><span class="sxs-lookup"><span data-stu-id="b32ea-229">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="b32ea-230">Szybkiej instalacji</span><span class="sxs-lookup"><span data-stu-id="b32ea-230">Quick install</span></span>
<span data-ttu-id="b32ea-231">Uruchom następujące polecenia, aby pobrać omsagent, weryfikacja sumy kontrolnej, a następnie zainstalować i dołączyć agenta.</span><span class="sxs-lookup"><span data-stu-id="b32ea-231">Run the following commands to download the omsagent, validate the checksum, then  install and onboard the agent.</span></span> <span data-ttu-id="b32ea-232">Polecenia są dla 64-bitowej.</span><span class="sxs-lookup"><span data-stu-id="b32ea-232">Commands are for 64-bit.</span></span> <span data-ttu-id="b32ea-233">Identyfikator i klucz podstawowy znajdują się w portalu OMS w obszarze **ustawienia** na **połączonych źródeł** kartę.</span><span class="sxs-lookup"><span data-stu-id="b32ea-233">The Workspace ID and Primary Key are found in the OMS portal under **Settings** on the **Connected Sources** tab.</span></span>

![szczegóły obszaru roboczego](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="b32ea-235">Istnieje wiele innych metod, aby zainstalować agenta i ją uaktualnić.</span><span class="sxs-lookup"><span data-stu-id="b32ea-235">There are a variety of other methods to install the agent and upgrade it.</span></span> <span data-ttu-id="b32ea-236">Więcej o nich na [kroki, aby zainstalować agenta pakietu OMS Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="b32ea-236">You can read more about them at [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="b32ea-237">Można również wyświetlić [Azure przewodnik wideo](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="b32ea-237">You can also view the [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="b32ea-238">Wybierz metodę zbierania danych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="b32ea-239">Jak zależy typy danych, które chcesz zebrać czy chcesz korzystać z portalu OMS lub jeśli chcesz edytować różne pliki konfiguracji bezpośrednio na klientach systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b32ea-239">How you choose the data types you'd like to collect depends on whether you want to use the OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="b32ea-240">Jeśli chcesz korzystać z portalu konfigurację są automatycznie wysyłane do wszystkich klientów systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b32ea-240">If you choose to use the portal, the configuration is sent to all of your Linux clients automatically.</span></span> <span data-ttu-id="b32ea-241">Jeśli potrzebujesz różnych konfiguracji dla różnych klientów systemu Linux, należy edytować pliki klienta indywidualnie — lub użyj innego jak PowerShell DSC, Chef lub Puppet.</span><span class="sxs-lookup"><span data-stu-id="b32ea-241">If you need different configurations for different Linux clients, you will need to edit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="b32ea-242">Można określić zdarzenia dziennika systemowego i liczniki wydajności, które mają być zbierane za pomocą plików konfiguracji na komputerach z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="b32ea-242">You can specify the syslog events and performance counters that you want to collect using configuration files on the Linux computers.</span></span> <span data-ttu-id="b32ea-243">*Jeśli zdecydujesz się na Konfigurowanie zbierania danych przez edycję plików konfiguracyjnych agenta, należy wyłączyć scentralizowane konfiguracji.*</span><span class="sxs-lookup"><span data-stu-id="b32ea-243">*If you chose to configure data collection by editing agent configuration files, you should disable the centralized configuration.*</span></span>  <span data-ttu-id="b32ea-244">Instrukcje znajdują się poniżej do skonfigurowania zbierania danych w plikach konfiguracji agenta, a także aby wyłączyć konfigurację centralnej wszystkich agentów OMS dla systemu Linux lub pojedynczych komputerów.</span><span class="sxs-lookup"><span data-stu-id="b32ea-244">Instructions are provided below to configure data collection in the agent's configuration files as well as to disable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="b32ea-245">Wyłącz zarządzanie OMS dla danego komputera systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="b32ea-246">Scentralizowane zbieranie danych dla danych konfiguracji jest wyłączona dla pojedynczego komputera systemu Linux przy użyciu skryptu OMS_MetaConfigHelper.py.</span><span class="sxs-lookup"><span data-stu-id="b32ea-246">Centralized data collection for configuration data is disabled for an individual Linux computer with the OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="b32ea-247">Może to być przydatne, jeśli podzbiorowi komputerów należy specjalne konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b32ea-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="b32ea-248">Aby wyłączyć scentralizowane konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="b32ea-248">To disable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="b32ea-249">Aby ponownie włączyć scentralizowane konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="b32ea-249">To re-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="b32ea-250">Liczniki wydajności systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-250">Linux performance counters</span></span>
<span data-ttu-id="b32ea-251">Liczniki wydajności systemu Linux są podobne do liczników wydajności systemu Windows — zarówno działają podobnie.</span><span class="sxs-lookup"><span data-stu-id="b32ea-251">Linux performance counters are similar to Windows performance counters—both operate similarly.</span></span> <span data-ttu-id="b32ea-252">Aby dodać i skonfigurować je, można użyć poniższych procedur.</span><span class="sxs-lookup"><span data-stu-id="b32ea-252">You can use the following procedures to add and configure them.</span></span> <span data-ttu-id="b32ea-253">Po dodaniu ich do OMS, dane są zbierane dla nich co 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="b32ea-253">After they are added to OMS, data is collected for them every 30 seconds.</span></span>

### <a name="to-add-a-linux-performance-counter-in-oms"></a><span data-ttu-id="b32ea-254">Aby dodać licznika wydajności systemu Linux w OMS</span><span class="sxs-lookup"><span data-stu-id="b32ea-254">To add a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="b32ea-255">Aby skonfigurować agentów OMS dla systemu Linux przy użyciu portalu OMS, Dodaj liczniki wydajności systemu Linux na stronie Ustawienia, kliknij przycisk **danych**.</span><span class="sxs-lookup"><span data-stu-id="b32ea-255">To configure OMS Agents for Linux using the OMS portal, you can add Linux performance counters on the Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="b32ea-256">Na **ustawienia** w obszarze **danych** , kliknij przycisk **liczników wydajności systemu Linux** , a następnie wybierz lub wpisz nazwę licznika, które chcesz dodać.</span><span class="sxs-lookup"><span data-stu-id="b32ea-256">On the **Settings** page under **Data** , click **Linux performance counters** and then select or type the name of the counter you want to add.</span></span>  
    <span data-ttu-id="b32ea-257">![dane](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="b32ea-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="b32ea-258">Jeśli nie znasz pełną nazwę licznika, możesz wpisać nazwę częściowe i zostanie wyświetlona lista dostępnych liczników.</span><span class="sxs-lookup"><span data-stu-id="b32ea-258">If you don't know the full name of the counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="b32ea-259">Po znalezieniu licznik, który chcesz dodać, kliknij nazwę na liście, a następnie kliknij ikonę znaku plus, można dodać licznika.</span><span class="sxs-lookup"><span data-stu-id="b32ea-259">When you find the counter you want to add, click the name in the list and then click the plus icon to add the counter.</span></span>
4. <span data-ttu-id="b32ea-260">Po dodaniu licznik, zostanie wyświetlona lista liczników wyróżnione z paskiem kolorowe.</span><span class="sxs-lookup"><span data-stu-id="b32ea-260">After you add the counter, it appears in the list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="b32ea-261">Domyślnie **Zastosuj poniższą konfigurację do moich maszyn** opcja jest zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="b32ea-261">By default, the **Apply below configuration to my machines** option is selected.</span></span> <span data-ttu-id="b32ea-262">Jeśli chcesz wyłączyć przesłania danych konfiguracji, wyczyść zaznaczenie.</span><span class="sxs-lookup"><span data-stu-id="b32ea-262">If you want to disable sending configuration data, clear the selection.</span></span>
6. <span data-ttu-id="b32ea-263">Po zakończeniu modyfikowania liczniki wydajności, w dolnej części strony kliknij **zapisać** aby zakończyć wprowadzanie zmian.</span><span class="sxs-lookup"><span data-stu-id="b32ea-263">When you are done modifying performance counters, at the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="b32ea-264">Wprowadzone zmiany konfiguracji są następnie wysyłane do wszystkich agentów OMS dla systemu Linux, które są zarejestrowane w usłudze OMS, zazwyczaj w ciągu 5 minut.</span><span class="sxs-lookup"><span data-stu-id="b32ea-264">The configuration changes that you've made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="b32ea-265">Konfigurowanie liczników wydajności systemu Linux w OMS</span><span class="sxs-lookup"><span data-stu-id="b32ea-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="b32ea-266">Do liczników wydajności systemu Windows można wybrać określonego wystąpienia dla każdego licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="b32ea-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="b32ea-267">Do liczników wydajności systemu Linux, niezależnie od wystąpienia wybranego licznika ma zastosowanie do wszystkich liczników podrzędnych licznika nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="b32ea-267">However, for Linux performance counters, whatever instance of a counter that you choose applies to all child counters of the parent counter.</span></span> <span data-ttu-id="b32ea-268">W poniższej tabeli przedstawiono typowe wystąpienia dostępne do liczników wydajności zarówno systemu Linux i Windows.</span><span class="sxs-lookup"><span data-stu-id="b32ea-268">The following table shows the common instances available to both Linux and Windows performance counters.</span></span>

| <span data-ttu-id="b32ea-269">**Nazwa wystąpienia**</span><span class="sxs-lookup"><span data-stu-id="b32ea-269">**Instance name**</span></span> | <span data-ttu-id="b32ea-270">**Znaczenie**</span><span class="sxs-lookup"><span data-stu-id="b32ea-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="b32ea-271">\_Całkowita liczba</span><span class="sxs-lookup"><span data-stu-id="b32ea-271">\_Total</span></span> |<span data-ttu-id="b32ea-272">Całkowita liczba wszystkich wystąpień</span><span class="sxs-lookup"><span data-stu-id="b32ea-272">Total of all the instances</span></span> |
| \* |<span data-ttu-id="b32ea-273">Wszystkie wystąpienia</span><span class="sxs-lookup"><span data-stu-id="b32ea-273">All instances</span></span> |
| <span data-ttu-id="b32ea-274">(/ & #124; / var)</span><span class="sxs-lookup"><span data-stu-id="b32ea-274">(/&#124;/var)</span></span> |<span data-ttu-id="b32ea-275">Dopasowuje wystąpienia o nazwie: / lub /var</span><span class="sxs-lookup"><span data-stu-id="b32ea-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="b32ea-276">Podobnie, wybrane interwału próbkowania licznika nadrzędny ma zastosowanie do wszystkich liczników podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="b32ea-276">Similarly, the sample interval that you choose for a parent counter applies to all its child counters.</span></span> <span data-ttu-id="b32ea-277">Innymi słowy interwałów próbkowania licznika podrzędnych i wystąpienia są również powiązane ze sobą.</span><span class="sxs-lookup"><span data-stu-id="b32ea-277">In other words, all the child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="b32ea-278">Dodawanie i Konfigurowanie metryki wydajności z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="b32ea-279">Metryki wydajności do zbierania są kontrolowane przez konfigurację w/etc/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="b32ea-279">Performance metrics to collect are controlled by the configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="b32ea-280">Zobacz [metryki wydajności dostępne](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) dostępnych klas i metryki dla agenta pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b32ea-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for the OMS Agent for Linux.</span></span>

<span data-ttu-id="b32ea-281">Każdy obiekt lub kategorii, metryki wydajności do zbierania powinien być zdefiniowany w pliku konfiguracyjnym jako pojedynczy `<source>` elementu.</span><span class="sxs-lookup"><span data-stu-id="b32ea-281">Each object, or category, of performance metrics to collect should be defined in the configuration file as a single `<source>` element.</span></span> <span data-ttu-id="b32ea-282">Składnia jest zgodny ze wzorcem poniżej.</span><span class="sxs-lookup"><span data-stu-id="b32ea-282">The syntax follows the pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="b32ea-283">Można konfigurować parametry tego elementu są:</span><span class="sxs-lookup"><span data-stu-id="b32ea-283">The configurable parameters of this element are:</span></span>

* <span data-ttu-id="b32ea-284">**Obiekt\_nazwa**: Nazwa obiektu dla kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b32ea-284">**Object\_name**: the object name for the collection.</span></span>
* <span data-ttu-id="b32ea-285">**Wystąpienie\_regex**: *wyrażenia regularnego* Definiowanie które wystąpienia zbierania.</span><span class="sxs-lookup"><span data-stu-id="b32ea-285">**Instance\_regex**: a *regular expression* defining which instances to collect.</span></span> <span data-ttu-id="b32ea-286">Wartość: `.*` określa wszystkich wystąpień.</span><span class="sxs-lookup"><span data-stu-id="b32ea-286">The value: `.*` specifies all instances.</span></span> <span data-ttu-id="b32ea-287">Aby zbierać metryki procesora tylko \_całkowita liczba wystąpień, można określić `_Total`.</span><span class="sxs-lookup"><span data-stu-id="b32ea-287">To collect processor metrics for only the \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="b32ea-288">Aby zbierać metryki procesu tylko wystąpienia crond lub sshd, można określić: `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="b32ea-288">To collect process metrics for only the crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="b32ea-289">**Licznik\_nazwa\_regex**: *wyrażenia regularnego* definiujący, które liczniki (dla obiekt) do zbierania.</span><span class="sxs-lookup"><span data-stu-id="b32ea-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for the object) to collect.</span></span> <span data-ttu-id="b32ea-290">Aby zbierać wszystkie liczniki dla obiekt, podaj: `.*`.</span><span class="sxs-lookup"><span data-stu-id="b32ea-290">To collect all counters for the object, specify: `.*`.</span></span> <span data-ttu-id="b32ea-291">Aby zbierać tylko wymiany miejsca liczniki dla obiekt pamięć, można określić:`.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="b32ea-291">To collect only swap space counters for the memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="b32ea-292">**Interwał:**: częstotliwość pobierane liczniki obiektu.</span><span class="sxs-lookup"><span data-stu-id="b32ea-292">**Interval:**: the frequency at which the object's counters are collected.</span></span>

<span data-ttu-id="b32ea-293">Konfigurację domyślną dla metryki wydajności jest:</span><span class="sxs-lookup"><span data-stu-id="b32ea-293">The default configuration for performance metrics is:</span></span>

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="b32ea-294">Włącz MySQL liczniki wydajności za pomocą poleceń systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="b32ea-295">Jeśli serwer MySQL lub MariaDB serwer zostanie wykryta na komputerze po zainstalowaniu pakietu omsagent, jest automatycznie instalowany dostawcy dla serwera MySQL monitorowania wydajności.</span><span class="sxs-lookup"><span data-stu-id="b32ea-295">If MySQL Server or MariaDB Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="b32ea-296">Ten dostawca nawiązuje połączenie z lokalnym serwerem MySQL/MariaDB do udostępnienia statystyki.</span><span class="sxs-lookup"><span data-stu-id="b32ea-296">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span></span> <span data-ttu-id="b32ea-297">Musisz skonfigurować poświadczenia użytkownika MySQL, tak aby dostawca dostęp do serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="b32ea-297">You need to configure MySQL user credentials so that the provider can access the MySQL Server.</span></span>

<span data-ttu-id="b32ea-298">Aby zdefiniować domyślne konto użytkownika serwera MySQL na hoście lokalnym, skorzystaj z następującego przykładu polecenia.</span><span class="sxs-lookup"><span data-stu-id="b32ea-298">To define a default user account for the MySQL server on localhost, use the following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="b32ea-299">Musi być do odczytu przez konto omsagent pliku poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="b32ea-299">The credentials file must be readable by the omsagent account.</span></span> <span data-ttu-id="b32ea-300">Zalecane jest uruchomienie polecenia mycimprovauth jako omsgent.</span><span class="sxs-lookup"><span data-stu-id="b32ea-300">Running the mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="b32ea-301">Alternatywnie można określić wymaganych poświadczeń MySQL w pliku, tworząc plik: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth.</span><span class="sxs-lookup"><span data-stu-id="b32ea-301">Alternatively, you can specify the required MySQL credentials in a file, by creating the file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth.</span></span> <span data-ttu-id="b32ea-302">Aby uzyskać więcej informacji o zarządzaniu MySQL poświadczeń do monitorowania za pomocą pliku mysql uwierzytelniania, zobacz [MySQL zarządzania, monitorowania poświadczenia w pliku authentication](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="b32ea-302">For more information about managing MySQL credentials for monitoring through the mysql-auth file, see [Manage MySQL monitoring credentials in the authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="b32ea-303">Zobacz [bazy danych uprawnienia wymagane do liczników wydajności MySQL](#database-permissions-required-for-mysql-performance-counters) szczegółowe informacje na temat obiektu uprawnienia wymagane przez użytkownika MySQL, aby zbierać dane dotyczące wydajności serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="b32ea-303">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by the MySQL user to collect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="b32ea-304">Włącz Apache HTTP Server liczniki wydajności za pomocą poleceń systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-304">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="b32ea-305">W przypadku wykrycia Apache HTTP Server na komputerze jest zainstalowany pakiet omsagent, jest automatycznie instalowany dostawcy dla Apache HTTP Server monitorowania wydajności.</span><span class="sxs-lookup"><span data-stu-id="b32ea-305">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="b32ea-306">Ten dostawca zależy od Apache "module", który musi zostać załadowane do Apache HTTP Server w celu uzyskania dostępu do danych dotyczących wydajności.</span><span class="sxs-lookup"><span data-stu-id="b32ea-306">This provider relies on an Apache "module" that must be loaded into the Apache HTTP Server in order to access performance data.</span></span>

<span data-ttu-id="b32ea-307">Można załadować modułu przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b32ea-307">You can load the module with the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="b32ea-308">Aby zwolnić modułu monitorowania Apache, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b32ea-308">To unload the Apache monitoring module, run the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="to-view-performance-data-with-log-analytics"></a><span data-ttu-id="b32ea-309">Aby wyświetlić dane wydajności z analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="b32ea-309">To view performance data with Log Analytics</span></span>
1. <span data-ttu-id="b32ea-310">W portalu usługi Operations Management Suite kliknij Kafelek wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="b32ea-310">In the Operations Management Suite portal, click the Log Search tile.</span></span>
2. <span data-ttu-id="b32ea-311">Na pasku wyszukiwania wpisz `* (Type=Perf)` Aby wyświetlić wszystkie liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="b32ea-311">In the search bar, type `* (Type=Perf)` to view all performance counters.</span></span>

<span data-ttu-id="b32ea-312">Ponieważ OMS również zbieranie danych licznika wydajności systemu Windows, użytkownik powinien zakresu rozwijanej Wyszukaj, aby dane specyficzne dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b32ea-312">Because OMS also collects Windows performance counter data, you should scope-down the search to Linux-specific data.</span></span> <span data-ttu-id="b32ea-313">Tak poniższy przykład czy przedstawiono dane wydajności specyficzne dla systemu Linux przykładowego serwera o nazwie Chorizo21.</span><span class="sxs-lookup"><span data-stu-id="b32ea-313">So, the following example would show performance data specific to an example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![przykład serwera wyświetlane w wynikach wyszukiwania](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="b32ea-315">W wynikach, kliknij **metryki** Aby wyświetlić liczniki, które zebrano dane.</span><span class="sxs-lookup"><span data-stu-id="b32ea-315">In the results, you can click **Metrics** to view the counters that data was collected for.</span></span> <span data-ttu-id="b32ea-316">Dane w czasie rzeczywistym jest wyświetlany na wykresach dla każdego licznika.</span><span class="sxs-lookup"><span data-stu-id="b32ea-316">Real-time data is shown as graphs for each counter.</span></span>

![metrics](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="b32ea-318">Dziennik systemu</span><span class="sxs-lookup"><span data-stu-id="b32ea-318">Syslog</span></span>
<span data-ttu-id="b32ea-319">SYSLOG jest protokół rejestrowania zdarzeń podobnych do dzienników zdarzeń systemu Windows — zarówno działają podobnie, podczas wyświetlania w OMS.</span><span class="sxs-lookup"><span data-stu-id="b32ea-319">Syslog is an event logging protocol similar to Windows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="to-add-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="b32ea-320">Aby dodać nowy funkcję dziennika systemowego systemu Linux w OMS</span><span class="sxs-lookup"><span data-stu-id="b32ea-320">To add a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="b32ea-321">Na **ustawienia** w obszarze **danych** , kliknij przycisk **Syslog** , a następnie po lewej stronie ikonę znaku plus, wpisz nazwę obiektu syslog, które chcesz dodać.</span><span class="sxs-lookup"><span data-stu-id="b32ea-321">On the **Settings** page under **Data** , click **Syslog** and then to the left of the plus icon, type the name of the syslog facility that you want to add.</span></span>
    <span data-ttu-id="b32ea-322">![Systemu Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="b32ea-322">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="b32ea-323">Jeśli nie znasz pełną nazwę funkcji, możesz wpisać nazwę częściowe i zostanie wyświetlona lista dostępnych syslog urządzeń.</span><span class="sxs-lookup"><span data-stu-id="b32ea-323">If you don’t know the full name of the facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="b32ea-324">Po znalezieniu funkcję dziennika systemowego, który chcesz dodać, kliknij nazwę na liście, a następnie kliknij ikonę znaku plus, aby dodać funkcję dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="b32ea-324">When you find the syslog facility that you want to add, click the name in the list and then click the plus icon to add the syslog facility.</span></span>
3. <span data-ttu-id="b32ea-325">Po dodaniu funkcji wydaje się na liście wyróżnione z paskiem kolorowe.</span><span class="sxs-lookup"><span data-stu-id="b32ea-325">After you add the facility, it appears in the list of highlighted with a colored bar.</span></span> <span data-ttu-id="b32ea-326">Następnie wybierz ważności (kategorie informacji zakładzie syslog), które mają być zbierane.</span><span class="sxs-lookup"><span data-stu-id="b32ea-326">Next, choose the severities (categories of syslog facility information) that you want to collect.</span></span>
4. <span data-ttu-id="b32ea-327">W dolnej części strony kliknij **zapisać** aby zakończyć wprowadzanie zmian.</span><span class="sxs-lookup"><span data-stu-id="b32ea-327">At the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="b32ea-328">Wprowadzone zmiany konfiguracji są następnie wysyłane do wszystkich agentów OMS dla systemu Linux, które są zarejestrowane w usłudze OMS, zazwyczaj w ciągu 5 minut.</span><span class="sxs-lookup"><span data-stu-id="b32ea-328">The configuration changes that you’ve made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="b32ea-329">Konfigurowanie urządzeń dziennika systemu Linux w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-329">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="b32ea-330">Zdarzenia dziennika systemowego są wysyłane z demona syslog, na przykład rsyslog lub syslog ng, do lokalnego portu, na którym nasłuchuje agent.</span><span class="sxs-lookup"><span data-stu-id="b32ea-330">Syslog events are sent from the syslog daemon, for example rsyslog or syslog-ng, to a local port that the agent is listening on.</span></span> <span data-ttu-id="b32ea-331">Domyślnie port 25224.</span><span class="sxs-lookup"><span data-stu-id="b32ea-331">By default, port 25224.</span></span> <span data-ttu-id="b32ea-332">Agent jest zainstalowany, jest stosowany domyślnej konfiguracji programu syslog.</span><span class="sxs-lookup"><span data-stu-id="b32ea-332">When the agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="b32ea-333">Znaleziono w lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="b32ea-333">This is found at:</span></span>

<span data-ttu-id="b32ea-334">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="b32ea-334">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="b32ea-335">SYSLOG ng: /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="b32ea-335">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="b32ea-336">Domyślna konfiguracja syslog agent pakietu OMS przekazuje zdarzenia dziennika systemowego z wszystkich urządzeń z ważnością, ostrzeżenie lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="b32ea-336">The default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="b32ea-337">Po zmodyfikowaniu konfiguracji programu syslog, należy ponownie uruchomić demona syslog, aby zmiany zaczęły obowiązywać.</span><span class="sxs-lookup"><span data-stu-id="b32ea-337">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

<span data-ttu-id="b32ea-338">Syslog konfigurację domyślną dla agenta pakietu OMS dla systemu Linux dla OMS jest:</span><span class="sxs-lookup"><span data-stu-id="b32ea-338">The default syslog configuration for the OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="b32ea-339">rsyslog</span><span class="sxs-lookup"><span data-stu-id="b32ea-339">Rsyslog</span></span>
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a><span data-ttu-id="b32ea-340">SYSLOG ng</span><span class="sxs-lookup"><span data-stu-id="b32ea-340">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="to-view-all-syslog-events-with-log-analytics"></a><span data-ttu-id="b32ea-341">Aby wyświetlić wszystkie zdarzenia dziennika systemowego z analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="b32ea-341">To view all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="b32ea-342">W portalu usługi Operations Management Suite kliknij **wyszukiwania dziennika** kafelka.</span><span class="sxs-lookup"><span data-stu-id="b32ea-342">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="b32ea-343">W **zarządzanie dziennikiem** grupowania, wybierz wyszukiwania wstępnie zdefiniowanych syslog, a następnie wybierz jedno go uruchomić.</span><span class="sxs-lookup"><span data-stu-id="b32ea-343">In the **Log Management** grouping, choose a predefined syslog search and then select one to run it.</span></span>

<span data-ttu-id="b32ea-344">Ten przykład przedstawia wszystkie zdarzenia dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="b32ea-344">This example shows all Syslog events.</span></span>

![Zdarzenia dziennika systemowego pokazano wyszukiwania dziennika](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="b32ea-346">Teraz możesz przejść do szczegółów wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="b32ea-346">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="b32ea-347">Alerty systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-347">Linux alerts</span></span>
<span data-ttu-id="b32ea-348">Jeśli używasz Nagios lub Zabbix do zarządzania maszyn z systemem Linux OMS może otrzymywać alerty generowane na podstawie tych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="b32ea-348">If you use Nagios or Zabbix to manage your Linux machines, then OMS can receive the alerts generated from those tools.</span></span> <span data-ttu-id="b32ea-349">Jednak nie jest obecnie żadna metoda, aby skonfigurować przychodzących danych alertów za pomocą portalu OMS.</span><span class="sxs-lookup"><span data-stu-id="b32ea-349">However, there is currently no method to configure incoming alert data using the OMS portal.</span></span> <span data-ttu-id="b32ea-350">Zamiast tego należy edytować plik konfiguracji rozpoczął wysyłania alertów z usługą OMS.</span><span class="sxs-lookup"><span data-stu-id="b32ea-350">Instead, you will need to edit a config file to start sending alerts to OMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="b32ea-351">Zbieraj alerty z Nagios</span><span class="sxs-lookup"><span data-stu-id="b32ea-351">Collect alerts from Nagios</span></span>
<span data-ttu-id="b32ea-352">Aby zbierać alerty z serwera Nagios, musisz wprowadzić następujące zmiany konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b32ea-352">To collect alerts from a Nagios server, you need to make the following configuration changes.</span></span>

1. <span data-ttu-id="b32ea-353">Przyznaj użytkownikowi **omsagent** dostęp do odczytu do pliku dziennika Nagios (tj. /var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="b32ea-353">Grant the user **omsagent** read access to the Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="b32ea-354">Zakładając, że plik nagios.log jest właścicielem grupy **nagios** , można dodać użytkownika **omsagent** do **nagios** grupy.</span><span class="sxs-lookup"><span data-stu-id="b32ea-354">Assuming the nagios.log file is owned by the group **nagios** , you can add the user **omsagent** to the **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="b32ea-355">Zmodyfikuj plik omsagent.confconfiguration (/ etc/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="b32ea-355">Modify the omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="b32ea-356">Upewnij się, że następujące wpisy są obecne i nie komentarze wychodzących:</span><span class="sxs-lookup"><span data-stu-id="b32ea-356">Ensure the following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path to point to your nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="b32ea-357">Uruchom ponownie demona omsagent:</span><span class="sxs-lookup"><span data-stu-id="b32ea-357">Restart the omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="b32ea-358">Zbieraj alerty z Zabbix</span><span class="sxs-lookup"><span data-stu-id="b32ea-358">Collect alerts from Zabbix</span></span>
<span data-ttu-id="b32ea-359">Aby zbierać alerty z serwera Zabbix, będziesz wykonywać podobne kroki w celu dla Nagios powyżej, z wyjątkiem należy określić użytkownika i hasło w *zwykły tekst*.</span><span class="sxs-lookup"><span data-stu-id="b32ea-359">To collect alerts from a Zabbix server, you'll perform similar steps to those for Nagios above, except you'll need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="b32ea-360">To nie jest idealnym rozwiązaniem, ale prawdopodobnie zmienią się wkrótce.</span><span class="sxs-lookup"><span data-stu-id="b32ea-360">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="b32ea-361">Aby rozwiązać ten problem, zaleca się utworzyć użytkownika, a następnie udzielić jej uprawnienia do monitorowania tylko.</span><span class="sxs-lookup"><span data-stu-id="b32ea-361">To address this issue, we recommend that you create the user and grant it permission to monitor only.</span></span>

<span data-ttu-id="b32ea-362">Przykład sekcji pliku konfiguracji omsagent.conf (/ etc/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/conf/omsagent.conf) dla Zabbix powinien przypominać następujący:</span><span class="sxs-lookup"><span data-stu-id="b32ea-362">An example section of the omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble the following:</span></span>

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="b32ea-363">Wyświetlanie alertów w wyszukiwaniu analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="b32ea-363">View alerts in Log Analytics search</span></span>
<span data-ttu-id="b32ea-364">Po skonfigurowaniu komputerach systemu Linux w celu wysyłania alertów z usługą OMS, można użyć kilka zapytań wyszukiwania prostego dziennika do wyświetlania alertów.</span><span class="sxs-lookup"><span data-stu-id="b32ea-364">After you've configured your Linux computers to send alerts to OMS, you can use a few simple log search queries to view the alerts.</span></span> <span data-ttu-id="b32ea-365">W poniższym przykładzie zapytanie wyszukiwania zwraca wszystkie zarejestrowane alertów, które zostały wygenerowane.</span><span class="sxs-lookup"><span data-stu-id="b32ea-365">The following search query example returns all the recorded alerts that were generated.</span></span> <span data-ttu-id="b32ea-366">Na przykład jeśli jakieś problem występuje w infrastrukturze IT, następnie wyniki następujące przykładowe zapytanie może wskazywać którego pochodzą może ten problem.</span><span class="sxs-lookup"><span data-stu-id="b32ea-366">For example, if some sort of problem occurs in your IT infrastructure, then results for the following example query might indicate where the problem might originate.</span></span> <span data-ttu-id="b32ea-367">I mogą łatwo przechodzenia alertom przez system źródła, aby zawęzić badaniu.</span><span class="sxs-lookup"><span data-stu-id="b32ea-367">And, you can easily drill in to the alerts by source system to help narrow your investigation.</span></span> <span data-ttu-id="b32ea-368">Korzyścią jest to, że zawsze nie musi przechodzić do różnych systemów zarządzania od początku, pod warunkiem, że alerty są wysyłane do OMS, można uruchomić istnieje.</span><span class="sxs-lookup"><span data-stu-id="b32ea-368">The benefit is that you don't necessarily have to go to various management systems from the start—provided that your alerts are sent to OMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="to-view-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="b32ea-369">Aby wyświetlić wszystkie alerty Nagios z analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="b32ea-369">To view all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="b32ea-370">W portalu usługi Operations Management Suite kliknij **wyszukiwania dziennika** kafelka.</span><span class="sxs-lookup"><span data-stu-id="b32ea-370">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="b32ea-371">Na pasku zapytania wpisz następujące zapytanie wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="b32ea-371">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Nagios alertów przedstawianych w dzienniku wyszukiwania](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="b32ea-373">Po wyniki wyszukiwania, możesz przejść do szczegółów dodatkowych szczegółów takich jak *stan alertu*.</span><span class="sxs-lookup"><span data-stu-id="b32ea-373">After you see the search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="to-view-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="b32ea-374">Aby wyświetlić wszystkie alerty Zabbix z analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="b32ea-374">To view all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="b32ea-375">W portalu usługi Operations Management Suite kliknij **wyszukiwania dziennika** kafelka.</span><span class="sxs-lookup"><span data-stu-id="b32ea-375">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="b32ea-376">Na pasku zapytania wpisz następujące zapytanie wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="b32ea-376">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Zabbix alertów przedstawianych w dzienniku wyszukiwania](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="b32ea-378">Po wyniki wyszukiwania, możesz przejść do szczegółów dodatkowych szczegółów takich jak *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="b32ea-378">After you see the search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="b32ea-379">Zgodność z programem System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="b32ea-379">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="b32ea-380">Agent pakietu OMS dla systemu Linux udostępnia pliki binarne agenta agenta programu System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="b32ea-380">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span></span> <span data-ttu-id="b32ea-381">Instalowanie agenta pakietu OMS dla systemu Linux w systemie, w obecnie zarządzany przez program Operations Manager uaktualnia OMI i SCX pakietów na komputerze do nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="b32ea-381">Installing the OMS Agent for Linux on a system currently managed by Operations Manager upgrades the OMI and SCX packages on the computer to a newer version.</span></span> <span data-ttu-id="b32ea-382">Agent pakietu OMS dla systemów Linux i System Center 2012 R2 są zgodne.</span><span class="sxs-lookup"><span data-stu-id="b32ea-382">The OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="b32ea-383">Jednak **System Center 2012 SP1 i wcześniejsze wersje nie są obecnie zgodne lub nie jest obsługiwany z agentem pakietu OMS dla systemu Linux.**</span><span class="sxs-lookup"><span data-stu-id="b32ea-383">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="b32ea-384">Jeśli Agent pakietu OMS dla systemu Linux jest zainstalowana na komputerze, który nie jest obecnie zarządzany przez program Operations Manager, a później chcesz zarządzać komputerem z programem Operations Manager, należy zmodyfikować konfigurację OMI przed wykryje komputer.</span><span class="sxs-lookup"><span data-stu-id="b32ea-384">If the OMS Agent for Linux is installed to a computer that is not currently managed by Operations Manager, and you later want to manage the computer with Operations Manager, you must modify the OMI configuration before you discover the computer.</span></span> <span data-ttu-id="b32ea-385">**Ten krok jest zbędny, jeśli agent programu Operations Manager została zainstalowana przed Agent pakietu OMS dla systemu Linux.**</span><span class="sxs-lookup"><span data-stu-id="b32ea-385">**This step is not needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span></span>
>
>

### <a name="to-enable-the-oms-agent-for-linux-to-communicate-with-operations-manager"></a><span data-ttu-id="b32ea-386">Aby włączyć agenta pakietu OMS dla systemu Linux do komunikowania się z programem Operations Manager</span><span class="sxs-lookup"><span data-stu-id="b32ea-386">To enable the OMS Agent for Linux to communicate with Operations Manager</span></span>
1. <span data-ttu-id="b32ea-387">Edytuj plik /etc/opt/omi/conf/omiserver.conf</span><span class="sxs-lookup"><span data-stu-id="b32ea-387">Edit the file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="b32ea-388">Upewnij się, że zaczyna się od wiersza **httpsport =** definiuje portu 1270.</span><span class="sxs-lookup"><span data-stu-id="b32ea-388">Ensure that the line beginning with **httpsport=** defines the port 1270.</span></span> <span data-ttu-id="b32ea-389">Takie jak`httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="b32ea-389">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="b32ea-390">Uruchom ponownie serwer OMI:</span><span class="sxs-lookup"><span data-stu-id="b32ea-390">Restart the OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="b32ea-391">Uprawnienia bazy danych wymagane dla liczników wydajności MySQL</span><span class="sxs-lookup"><span data-stu-id="b32ea-391">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="b32ea-392">Aby udzielić uprawnień użytkownikowi monitorowania, MySQL, udzielającym użytkownik musi mieć uprawnienie "GRANT option", a także udzielenia uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="b32ea-392">To grant permissions to a MySQL monitoring user, the granting user must have the 'GRANT option' privilege as well as the privilege being granted.</span></span>

<span data-ttu-id="b32ea-393">Aby użytkownikowi MySQL zwrócone dane dotyczące wydajności, które użytkownik wymaga dostępu do następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="b32ea-393">In order for the MySQL User to return performance data the user will need access to the following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="b32ea-394">Oprócz tych zapytań MySQL użytkownika wymaga wybierz dostęp do poniższych tabelach domyślne:</span><span class="sxs-lookup"><span data-stu-id="b32ea-394">In addition to these queries the MySQL user requires SELECT access to the following default tables:</span></span>

* <span data-ttu-id="b32ea-395">INFORMATION_SCHEMA</span><span class="sxs-lookup"><span data-stu-id="b32ea-395">information_schema</span></span>
* <span data-ttu-id="b32ea-396">MySQL</span><span class="sxs-lookup"><span data-stu-id="b32ea-396">mysql</span></span>

<span data-ttu-id="b32ea-397">Te uprawnienia można otrzymać, uruchamiając następujące polecenia grant.</span><span class="sxs-lookup"><span data-stu-id="b32ea-397">These privileges can be granted by running the following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-the-authentication-file"></a><span data-ttu-id="b32ea-398">Zarządzanie MySQL monitorowania poświadczenia w pliku uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="b32ea-398">Manage MySQL monitoring credentials in the authentication file</span></span>
<span data-ttu-id="b32ea-399">Poniższe sekcje zawierają informacje pomocne w zarządzaniu poświadczenia MySQL.</span><span class="sxs-lookup"><span data-stu-id="b32ea-399">The following sections help you manage MySQL credentials.</span></span>

### <a name="configure-the-mysql-omi-provider"></a><span data-ttu-id="b32ea-400">Konfigurowanie dostawcy MySQL OMI</span><span class="sxs-lookup"><span data-stu-id="b32ea-400">Configure the MySQL OMI provider</span></span>
<span data-ttu-id="b32ea-401">Dostawca MySQL OMI wymaga wstępnie skonfigurowane użytkownika MySQL i zainstalowania bibliotek klienta MySQL zapytania o informacje o kondycji wydajności z wystąpienia MySQL.</span><span class="sxs-lookup"><span data-stu-id="b32ea-401">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance/health information from the MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="b32ea-402">Plik authentication MySQL OMI</span><span class="sxs-lookup"><span data-stu-id="b32ea-402">MySQL OMI authentication file</span></span>
<span data-ttu-id="b32ea-403">Dostawcy MySQL OMI używany jest plik authentication ustalić bind adres i port MySQL nasłuchuje wystąpienie i jakie poświadczenia, które będzie używane do zbierania metryk.</span><span class="sxs-lookup"><span data-stu-id="b32ea-403">MySQL OMI provider uses an authentication file to determine what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span></span> <span data-ttu-id="b32ea-404">Podczas instalacji MySQL OMI dostawca skanowania MySQL my.cnf pliki konfiguracji (lokalizacje domyślne) dla wiązania adres i port i plik authentication częściowo zestawu MySQL OMI.</span><span class="sxs-lookup"><span data-stu-id="b32ea-404">During installation the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span></span>

<span data-ttu-id="b32ea-405">Aby ukończyć, monitorowanie wystąpienia serwera MySQL, należy dodać wstępnie wygenerowany plik authentication MySQL OMI w poprawnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="b32ea-405">To complete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into the correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="b32ea-406">Format pliku uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="b32ea-406">Authentication file format</span></span>
<span data-ttu-id="b32ea-407">Plik authentication MySQL OMI jest plik tekstowy, który zawiera informacje o:</span><span class="sxs-lookup"><span data-stu-id="b32ea-407">The MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="b32ea-408">Port</span><span class="sxs-lookup"><span data-stu-id="b32ea-408">Port</span></span>
* <span data-ttu-id="b32ea-409">Adres BIND</span><span class="sxs-lookup"><span data-stu-id="b32ea-409">Bind-Address</span></span>
* <span data-ttu-id="b32ea-410">Nazwa_użytkownika MySQL</span><span class="sxs-lookup"><span data-stu-id="b32ea-410">MySQL username</span></span>
* <span data-ttu-id="b32ea-411">Kodowanie Base64 hasła</span><span class="sxs-lookup"><span data-stu-id="b32ea-411">Base64 encoded password</span></span>

<span data-ttu-id="b32ea-412">Plik authentication MySQL OMI tylko przyznaje uprawnienia do odczytu i zapisu do użytkownika w systemie Linux, która go wygenerowała.</span><span class="sxs-lookup"><span data-stu-id="b32ea-412">The MySQL OMI authentication file only grants privileges for read/write to the Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="b32ea-413">Domyślny plik authentication MySQL OMI zawiera domyślne wystąpienie i numer portu, w zależności od tego, jakie informacje są dostępne i przeanalizowany z pliku konfiguracji znaleziono MySQL.</span><span class="sxs-lookup"><span data-stu-id="b32ea-413">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from the found MySQL configuration file.</span></span>

<span data-ttu-id="b32ea-414">Wystąpienie domyślne umożliwiają zarządzanie wielu wystąpień MySQL na jednym hoście Linux łatwiejsze i jest wskazywane przez wystąpienie o portu 0.</span><span class="sxs-lookup"><span data-stu-id="b32ea-414">The default instance is a means to make managing multiple MySQL instances on one Linux host easier, and is denoted by the instance with port 0.</span></span> <span data-ttu-id="b32ea-415">Wszystkie wystąpienia dodano będzie dziedziczyć właściwości z wystąpienia domyślnego.</span><span class="sxs-lookup"><span data-stu-id="b32ea-415">All added instances will inherit properties set from the default instance.</span></span> <span data-ttu-id="b32ea-416">Na przykład jeśli wystąpienie MySQL nasłuchiwanie na porcie "3308" zostanie dodany, adres powiązania domyślnego wystąpienia, username i password kodowany w standardzie Base64 będzie służyć monitorowanie wystąpienia nasłuchiwanie 3308 i spróbuj.</span><span class="sxs-lookup"><span data-stu-id="b32ea-416">For example, if MySQL instance listening on port '3308' is added, the default instance's bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span></span> <span data-ttu-id="b32ea-417">Jeśli wystąpienie na 3308 jest powiązany z innym adresem i korzysta z tej samej pary nazwa użytkownika i hasło MySQL wymagane jest tylko respecification powiązanego adresu i dziedziczone przez inne właściwości.</span><span class="sxs-lookup"><span data-stu-id="b32ea-417">If the instance on 3308 is binded to another address and uses the same MySQL username and password pair only the respecification of the bind-address is needed and the other properties will be inherited.</span></span>

<span data-ttu-id="b32ea-418">Przykłady plik authentication wyglądać w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="b32ea-418">Examples of the authentication file resemble the following.</span></span>

<span data-ttu-id="b32ea-419">Domyślne wystąpienie i wystąpienia z portem 3308:</span><span class="sxs-lookup"><span data-stu-id="b32ea-419">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="b32ea-420">Domyślne wystąpienie i wystąpienia z portu 3308 + różnych Base 64 zakodowane hasło:</span><span class="sxs-lookup"><span data-stu-id="b32ea-420">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="b32ea-421">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="b32ea-421">**Property**</span></span> | <span data-ttu-id="b32ea-422">**Opis**</span><span class="sxs-lookup"><span data-stu-id="b32ea-422">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b32ea-423">Port</span><span class="sxs-lookup"><span data-stu-id="b32ea-423">Port</span></span> |<span data-ttu-id="b32ea-424">Port reprezentuje bieżącego portu wystąpienia MySQL nasłuchuje na.</span><span class="sxs-lookup"><span data-stu-id="b32ea-424">Port represents the current port the MySQL instance is listening on.</span></span>  <span data-ttu-id="b32ea-425">Port 0 oznacza, że następujące właściwości są używane dla domyślnego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="b32ea-425">The port 0 implies that the properties following are used for default instance.</span></span> |
| <span data-ttu-id="b32ea-426">Adres BIND</span><span class="sxs-lookup"><span data-stu-id="b32ea-426">Bind-Address</span></span> |<span data-ttu-id="b32ea-427">Adres powiązania jest bieżącego powiązania MySQL — adresu</span><span class="sxs-lookup"><span data-stu-id="b32ea-427">the Bind Address is the current MySQL bind-address</span></span> |
| <span data-ttu-id="b32ea-428">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="b32ea-428">username</span></span> |<span data-ttu-id="b32ea-429">Ta nazwa użytkownika MySQL mają być używane do monitorowania MySQL wystąpienie serwera.</span><span class="sxs-lookup"><span data-stu-id="b32ea-429">This the username of the MySQL user you wish to use to monitor the MySQL server instance.</span></span> |
| <span data-ttu-id="b32ea-430">Hasło kodowane w formacie Base64</span><span class="sxs-lookup"><span data-stu-id="b32ea-430">Base64 encoded Password</span></span> |<span data-ttu-id="b32ea-431">Jest to hasło użytkownika monitorowania MySQL zakodowane w formacie Base64.</span><span class="sxs-lookup"><span data-stu-id="b32ea-431">This is the password of the MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="b32ea-432">Aktualizacje automatyczne</span><span class="sxs-lookup"><span data-stu-id="b32ea-432">AutoUpdate</span></span> |<span data-ttu-id="b32ea-433">Po uaktualnieniu dostawcy OMI MySQL dostawcy Skanuj ponownie zmiany w pliku my.cnf i zastąpić plik MySQL OMI Authentication.</span><span class="sxs-lookup"><span data-stu-id="b32ea-433">When the MySQL OMI Provider is upgraded the provider will rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file.</span></span> <span data-ttu-id="b32ea-434">Ta flaga ustawioną wartość PRAWDA lub FAŁSZ w zależności od wymaganych aktualizacji do pliku uwierzytelniania MySQL OMI.</span><span class="sxs-lookup"><span data-stu-id="b32ea-434">Set this flag to true or false depending on required updates to the MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="b32ea-435">Lokalizacja pliku uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="b32ea-435">Authentication file location</span></span>
<span data-ttu-id="b32ea-436">Plik Authentication OMI MySQL powinien znajduje się w następującej lokalizacji i o nazwie "mysql uwierzytelniania":</span><span class="sxs-lookup"><span data-stu-id="b32ea-436">The MySQL OMI Authentication File should be located in the following location and named "mysql-auth":</span></span>

<span data-ttu-id="b32ea-437">/var/OPT/Microsoft/MySQL-cimprov/auth/omsagent/MySQL-auth</span><span class="sxs-lookup"><span data-stu-id="b32ea-437">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="b32ea-438">Plik (i katalog auth/omsagent) powinien należeć do użytkownika omsagent.</span><span class="sxs-lookup"><span data-stu-id="b32ea-438">The file (and auth/omsagent directory) should be owned by the omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="b32ea-439">Dzienniki agentów</span><span class="sxs-lookup"><span data-stu-id="b32ea-439">Agent logs</span></span>
<span data-ttu-id="b32ea-440">W dziennikach Agent pakietu OMS dla systemu Linux jest na:</span><span class="sxs-lookup"><span data-stu-id="b32ea-440">The logs for the OMS Agent for Linux is at:</span></span>

<span data-ttu-id="b32ea-441">/ var/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="b32ea-441">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="b32ea-442">W dziennikach Agent pakietu OMS dla systemu Linux dla programu omsconfig (konfiguracja agenta) znajduje się na:</span><span class="sxs-lookup"><span data-stu-id="b32ea-442">The logs for the OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="b32ea-443">/ var/opt/microsoft/omsconfig/log /</span><span class="sxs-lookup"><span data-stu-id="b32ea-443">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="b32ea-444">Dzienniki dla składników OMI i SCX (udostępniających dane metryk wydajności) znajduje się na:</span><span class="sxs-lookup"><span data-stu-id="b32ea-444">Logs for the OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="b32ea-445">/ var/opt/omi/log/i /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="b32ea-445">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-the-oms-agent-for-linux"></a><span data-ttu-id="b32ea-446">Rozwiązywanie problemów z agentem pakietu OMS dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-446">Troubleshooting the OMS Agent for Linux</span></span>
<span data-ttu-id="b32ea-447">Skorzystaj z poniższych informacji do diagnozowania i rozwiązywania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="b32ea-447">Use the following information to diagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="b32ea-448">Jeśli żaden z informacje dotyczące rozwiązywania problemów w tej sekcji pomaga, umożliwia także następujące zasoby w celu rozwiązania problemu.</span><span class="sxs-lookup"><span data-stu-id="b32ea-448">If none of the troubleshooting information in this section helps you, you can also use the following resources to help resolve your problem.</span></span>

* <span data-ttu-id="b32ea-449">Klienci z Premier pomocy technicznej można rejestrować sprawy pomocy technicznej za pośrednictwem [Premier](https://premier.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="b32ea-449">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="b32ea-450">Klienci z umowami pomocy technicznej platformy Azure może zalogować się dziale obsługi [portalu Azure](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="b32ea-450">Customers with Azure support agreements can log support cases in the [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="b32ea-451">Plik [problem GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span><span class="sxs-lookup"><span data-stu-id="b32ea-451">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="b32ea-452">Forum opinii pomysłów i utworzyć raport o usterce [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="b32ea-452">Feedback forum for ideas and to create a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="b32ea-453">Lokalizacje ważne dziennika</span><span class="sxs-lookup"><span data-stu-id="b32ea-453">Important log locations</span></span>
| <span data-ttu-id="b32ea-454">Plik</span><span class="sxs-lookup"><span data-stu-id="b32ea-454">File</span></span> | <span data-ttu-id="b32ea-455">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="b32ea-455">Path</span></span> |
| --- | --- |
| <span data-ttu-id="b32ea-456">Agent pakietu OMS dla pliku dziennika systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-456">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="b32ea-457">Plik dziennika konfiguracji agenta pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="b32ea-457">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="b32ea-458">Pliki konfiguracji ważne</span><span class="sxs-lookup"><span data-stu-id="b32ea-458">Important configuration files</span></span>
| <span data-ttu-id="b32ea-459">Catergory</span><span class="sxs-lookup"><span data-stu-id="b32ea-459">Catergory</span></span> | <span data-ttu-id="b32ea-460">Lokalizacja pliku</span><span class="sxs-lookup"><span data-stu-id="b32ea-460">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="b32ea-461">Dziennik systemu</span><span class="sxs-lookup"><span data-stu-id="b32ea-461">Syslog</span></span> |<span data-ttu-id="b32ea-462">`/etc/syslog-ng/syslog-ng.conf`lub `/etc/rsyslog.conf` lub`/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="b32ea-462">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="b32ea-463">Wydajność, Nagios, Zabbix, OMS wyjściowego i agenta ogólne</span><span class="sxs-lookup"><span data-stu-id="b32ea-463">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="b32ea-464">Dodatkowe konfiguracje</span><span class="sxs-lookup"><span data-stu-id="b32ea-464">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="b32ea-465">Edycji plików konfiguracyjnych dla liczników wydajności i syslog zostaną zastąpione, jeśli jest włączona konfiguracja portalu OMS.</span><span class="sxs-lookup"><span data-stu-id="b32ea-465">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="b32ea-466">Możesz wyłączyć konfiguracją w portalu OMS (dla wszystkich węzłów) lub pojedynczych węzłów, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b32ea-466">You can disable configuration in the OMS Portal (for all nodes) or for single nodes by running the following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="b32ea-467">Włączenie rejestrowania debugowania</span><span class="sxs-lookup"><span data-stu-id="b32ea-467">Enable debug logging</span></span>
<span data-ttu-id="b32ea-468">Aby włączenie rejestrowania debugowania, można użyć dodatek typu plug-in OMS danych wyjściowych i pełne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="b32ea-468">To enable debug logging, you can use the OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="b32ea-469">Dodatek dane wyjściowe OMS</span><span class="sxs-lookup"><span data-stu-id="b32ea-469">OMS output plugin</span></span>
<span data-ttu-id="b32ea-470">FluentD umożliwia dodatek plug-in, aby określić poziomy rejestrowania dziennika różnych poziomów dla danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="b32ea-470">FluentD allows the plugin to specify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="b32ea-471">Aby określić poziom dziennika różnych dla danych wyjściowych OMS, zmień konfigurację agenta ogólne w `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` pliku.</span><span class="sxs-lookup"><span data-stu-id="b32ea-471">To specify a different log level for OMS output, edit the general agent configuration in the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="b32ea-472">W dolnej części pliku konfiguracji, należy zmienić `log_level` właściwość z `info` do `debug`.</span><span class="sxs-lookup"><span data-stu-id="b32ea-472">Near the bottom of the configuration file, change the `log_level` property from `info` to `debug`.</span></span>

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

<span data-ttu-id="b32ea-473">Rejestrowania debugowania umożliwia Zobacz wsadowej operacji przekazywania z usługą OMS oddzielone typ, liczba elementów danych, a czas potrzebny do wysłania.</span><span class="sxs-lookup"><span data-stu-id="b32ea-473">Debug logging allows you to see batched uploads to the OMS Service separated by type, number of data items, and time taken to send.</span></span>

<span data-ttu-id="b32ea-474">*Przykładowy dziennik debugowania włączone:*</span><span class="sxs-lookup"><span data-stu-id="b32ea-474">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="b32ea-475">Pełne dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="b32ea-475">Verbose output</span></span>
<span data-ttu-id="b32ea-476">Zamiast używać wtyczki dane wyjściowe OMS, można również wyprowadzać elementów danych bezpośrednio do `stdout`, która jest widoczna w pliku dziennika systemu Linux Agent pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="b32ea-476">Instead of using the OMS output plugin, you can also output data items directly to `stdout`, which is visible in the OMS Agent for Linux log file.</span></span>

<span data-ttu-id="b32ea-477">W pliku konfiguracyjnym ogólne agent pakietu OMS na `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, komentarz OMS output wtyczki, dodając `#` przed każdym wierszu.</span><span class="sxs-lookup"><span data-stu-id="b32ea-477">In the OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out the OMS output plugin by adding a `#` in front of each line.</span></span>

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

<span data-ttu-id="b32ea-478">Poniżej wtyczki dane wyjściowe, Usuń komentarz poniższej sekcji przez usunięcie `#` symbol na początku każdego wiersza.</span><span class="sxs-lookup"><span data-stu-id="b32ea-478">Below the output plugin, remove the comment in the following section by removing the `#` symbol at the beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-the-log"></a><span data-ttu-id="b32ea-479">Przekazany dalej komunikaty dziennika systemowego nie pojawiają się w Dzienniku</span><span class="sxs-lookup"><span data-stu-id="b32ea-479">Forwarded Syslog messages do not appear in the log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b32ea-480">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="b32ea-480">Probable causes</span></span>
* <span data-ttu-id="b32ea-481">Konfiguracja stosowane do serwerów systemu Linux nie zezwala na zbiór urządzeń wysłanych i/lub poziomy dziennika</span><span class="sxs-lookup"><span data-stu-id="b32ea-481">The configuration applied to the Linux server does not allow collection of the sent facilities and/or log levels</span></span>
* <span data-ttu-id="b32ea-482">SYSLOG nie są poprawnie przekazywane na serwer z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-482">Syslog is not being forwarded correctly to the Linux server</span></span>
* <span data-ttu-id="b32ea-483">Liczba komunikatów przesyłanych na sekundę jest zbyt duży dla agenta pakietu OMS dla systemu Linux do obsługi konfiguracji podstawowej</span><span class="sxs-lookup"><span data-stu-id="b32ea-483">The number of messages being forwarded per second are too large for the base configuration of the OMS Agent for Linux to handle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="b32ea-484">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="b32ea-484">Resolutions</span></span>
* <span data-ttu-id="b32ea-485">Sprawdź, czy konfiguracja w portalu OMS Syslog ma wszystkie urządzenia i poziomy dziennika poprawne</span><span class="sxs-lookup"><span data-stu-id="b32ea-485">Verify that the configuration in the OMS Portal for Syslog has all the facilities and the correct log levels</span></span>
  * <span data-ttu-id="b32ea-486">**Portalu OMS > Ustawienia > danych > Syslog**</span><span class="sxs-lookup"><span data-stu-id="b32ea-486">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="b32ea-487">Sprawdź tego macierzystego syslog wiadomości demonów (`rsyslog`, `syslog-ng`) mogą odbierać wiadomości przesyłane dalej</span><span class="sxs-lookup"><span data-stu-id="b32ea-487">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able to receive the forwarded messages</span></span>
* <span data-ttu-id="b32ea-488">Sprawdzanie ustawień zapory na serwerze Syslog, aby upewnić się, że komunikaty nie są blokowane</span><span class="sxs-lookup"><span data-stu-id="b32ea-488">Check firewall settings on the Syslog server to ensure that messages are not being blocked</span></span>
* <span data-ttu-id="b32ea-489">Symulowanie komunikatu dziennika systemu, aby przy użyciu pakietu OMS `logger` polecenia — na przykład:</span><span class="sxs-lookup"><span data-stu-id="b32ea-489">Simulate a Syslog message to OMS using the `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-to-oms-when-using-a-proxy"></a><span data-ttu-id="b32ea-490">Problemy z połączeniem z usługą OMS przy użyciu serwera proxy</span><span class="sxs-lookup"><span data-stu-id="b32ea-490">Problems connecting to OMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b32ea-491">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="b32ea-491">Probable causes</span></span>
* <span data-ttu-id="b32ea-492">Określony serwer proxy podczas instalowania i konfigurowania agenta jest niepoprawny</span><span class="sxs-lookup"><span data-stu-id="b32ea-492">The proxy specified when installing and configuring the agent is incorrect</span></span>
* <span data-ttu-id="b32ea-493">Usługę punktów końcowych, które nie są whitelistested w centrum danych.</span><span class="sxs-lookup"><span data-stu-id="b32ea-493">The OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="b32ea-494">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="b32ea-494">Resolutions</span></span>
* <span data-ttu-id="b32ea-495">Zainstaluj ponownie agenta pakietu OMS dla systemu Linux przy użyciu następującego polecenia z opcją `-v` włączone.</span><span class="sxs-lookup"><span data-stu-id="b32ea-495">Reinstall the OMS Agent for Linux using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="b32ea-496">Dzięki temu pełne dane wyjściowe agenta łączących się za pośrednictwem serwera proxy z usługą OMS.</span><span class="sxs-lookup"><span data-stu-id="b32ea-496">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="b32ea-497">Zapoznaj się z dokumentacją serwera proxy OMS na [Konfigurowanie agenta do użycia przy użyciu serwera proxy HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span><span class="sxs-lookup"><span data-stu-id="b32ea-497">Review the documentation for OMS proxy at [Configuring the agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="b32ea-498">Sprawdź, czy następujące punkty końcowe usługę białej</span><span class="sxs-lookup"><span data-stu-id="b32ea-498">Verify that the following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="b32ea-499">Zasób agenta</span><span class="sxs-lookup"><span data-stu-id="b32ea-499">Agent Resource</span></span> | <span data-ttu-id="b32ea-500">Porty</span><span class="sxs-lookup"><span data-stu-id="b32ea-500">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="b32ea-501">& #42;. ods.opinsights.Azure.com</span><span class="sxs-lookup"><span data-stu-id="b32ea-501">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="b32ea-502">Port 443</span><span class="sxs-lookup"><span data-stu-id="b32ea-502">Port 443</span></span> |
| <span data-ttu-id="b32ea-503">& #42;. OMS.opinsights.Azure.com</span><span class="sxs-lookup"><span data-stu-id="b32ea-503">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="b32ea-504">Port 443</span><span class="sxs-lookup"><span data-stu-id="b32ea-504">Port 443</span></span> |
| <span data-ttu-id="b32ea-505">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="b32ea-505">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="b32ea-506">Port 443</span><span class="sxs-lookup"><span data-stu-id="b32ea-506">Port 443</span></span> |
| <span data-ttu-id="b32ea-507">& #42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="b32ea-507">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="b32ea-508">Port 443</span><span class="sxs-lookup"><span data-stu-id="b32ea-508">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="b32ea-509">Zostanie wyświetlony błąd 403 podczas dołączania</span><span class="sxs-lookup"><span data-stu-id="b32ea-509">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b32ea-510">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="b32ea-510">Probable causes</span></span>
* <span data-ttu-id="b32ea-511">Data i godzina są niepoprawne na serwerze z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-511">The date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="b32ea-512">Identyfikator i klucz obszaru roboczego, używane są nieprawidłowe</span><span class="sxs-lookup"><span data-stu-id="b32ea-512">The Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="b32ea-513">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="b32ea-513">Resolution</span></span>
* <span data-ttu-id="b32ea-514">Sprawdź czas na serwerze z systemem Linux `date` polecenia.</span><span class="sxs-lookup"><span data-stu-id="b32ea-514">Verify the time on your Linux server with the `date` command.</span></span> <span data-ttu-id="b32ea-515">Jeśli danych jest większa lub mniejsza niż 15 minut od bieżącego czasu, dołączania kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="b32ea-515">If the data is greater than or less than 15 minutes from the current time, then onboarding fails.</span></span> <span data-ttu-id="b32ea-516">Aby rozwiązać ten problem, zaktualizuj datę i/lub strefy czasowej serwera z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="b32ea-516">To correct this, update the date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="b32ea-517">Najnowszą wersję agenta pakietu OMS Linux powiadamia użytkownika, jeśli różnica czasu powoduje błąd dołączania</span><span class="sxs-lookup"><span data-stu-id="b32ea-517">The latest version of the OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="b32ea-518">Ponowna dołączyć przy użyciu poprawny identyfikator i klucz obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="b32ea-518">Re-onboard using the correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="b32ea-519">Zobacz [dołączania przy użyciu wiersza polecenia](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b32ea-519">See  [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-the-log-file-after-onboarding"></a><span data-ttu-id="b32ea-520">500 Błąd lub błąd 404 pojawia się w pliku dziennika po dołączania</span><span class="sxs-lookup"><span data-stu-id="b32ea-520">A 500 error or 404 error appears in the log file after onboarding</span></span>
<span data-ttu-id="b32ea-521">Jest to znany problem występujący podczas pierwszego przekazywania danych Linux pod obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="b32ea-521">This is a known issue that occurs during the first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="b32ea-522">Nie dotyczy to danych wysyłanych lub innych problemów.</span><span class="sxs-lookup"><span data-stu-id="b32ea-522">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="b32ea-523">Możesz zignorować błędy podczas początkowego procesu dołączania.</span><span class="sxs-lookup"><span data-stu-id="b32ea-523">You can ignore the errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="b32ea-524">Nagios dane wyświetlane w portalu OMS</span><span class="sxs-lookup"><span data-stu-id="b32ea-524">Nagios data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b32ea-525">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="b32ea-525">Probable causes</span></span>
* <span data-ttu-id="b32ea-526">Użytkownik omsagent nie ma uprawnienia do odczytu z pliku dziennika Nagios</span><span class="sxs-lookup"><span data-stu-id="b32ea-526">The omsagent user does not have permissions to read from the Nagios log file</span></span>
* <span data-ttu-id="b32ea-527">Sekcje źródłowy oraz filtr Nagios nadal są ujęte w pliku omsagent.conf</span><span class="sxs-lookup"><span data-stu-id="b32ea-527">The Nagios source and filter sections are still commented in the omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="b32ea-528">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="b32ea-528">Resolutions</span></span>
* <span data-ttu-id="b32ea-529">Dodaj użytkownika omsagent, aby można było odczytać z pliku Nagios.</span><span class="sxs-lookup"><span data-stu-id="b32ea-529">Add the omsagent user in order to read from the Nagios file.</span></span> <span data-ttu-id="b32ea-530">Zobacz [alerty Nagios](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b32ea-530">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="b32ea-531">W agencie OMS pliku ogólnych konfiguracji systemu Linux na `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, upewnij się, że **zarówno** sekcji Nagios źródła i filtr ma komentarzy usunięty, podobny do poniższego przykładu.</span><span class="sxs-lookup"><span data-stu-id="b32ea-531">In the OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** the Nagios source and filter sections have comments removed, similar to the following example.</span></span>

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-the-oms-portal"></a><span data-ttu-id="b32ea-532">Dane systemu Linux nie jest wyświetlane w portalu OMS</span><span class="sxs-lookup"><span data-stu-id="b32ea-532">Linux data doesn't appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b32ea-533">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="b32ea-533">Probable causes</span></span>
* <span data-ttu-id="b32ea-534">Dołączenie do usługi OMS nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="b32ea-534">Onboarding to the OMS Service failed</span></span>
* <span data-ttu-id="b32ea-535">Połączenie z usługą OMS jest zablokowane</span><span class="sxs-lookup"><span data-stu-id="b32ea-535">Connection to the OMS Service is blocked</span></span>
* <span data-ttu-id="b32ea-536">Agent pakietu OMS danych Linux jest kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="b32ea-536">The OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="b32ea-537">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="b32ea-537">Resolutions</span></span>
* <span data-ttu-id="b32ea-538">Sprawdź, że dołączania z usługą OMS zakończyła się pomyślnie, sprawdzenia, czy `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` istnieje.</span><span class="sxs-lookup"><span data-stu-id="b32ea-538">Verify that onboarding to the OMS Service was successful by verifying that the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="b32ea-539">Ponowna dołączyć omsadmin.sh wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b32ea-539">Re-onboard using the omsadmin.sh command line.</span></span> <span data-ttu-id="b32ea-540">Zobacz [dołączania przy użyciu wiersza polecenia](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b32ea-540">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="b32ea-541">Jeśli używasz serwera proxy, Użyj serwera proxy powyższe kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="b32ea-541">If using a proxy, use the proxy troubleshooting steps above</span></span>
* <span data-ttu-id="b32ea-542">W niektórych przypadkach gdy Agent pakietu OMS dla systemu Linux nie mogą komunikować się z usługą OMS danych na agencie jest kopii zapasowej do pełnego rozmiaru 50 MB.</span><span class="sxs-lookup"><span data-stu-id="b32ea-542">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the Agent is backed-up to the full buffer size of 50 MB.</span></span> <span data-ttu-id="b32ea-543">Uruchom ponownie agenta pakietu OMS dla systemu Linux, uruchamiając `/opt/microsoft/omsagent/bin/service_control restart` polecenia.</span><span class="sxs-lookup"><span data-stu-id="b32ea-543">Restart the OMS Agent for Linux by running the `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="b32ea-544">Tego problemu w 1.1.0-28 wersję agenta i nowszych.</span><span class="sxs-lookup"><span data-stu-id="b32ea-544">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-the-oms-portal"></a><span data-ttu-id="b32ea-545">Nie zastosowano konfigurację liczników wydajności systemu SYSLOG Linux w portalu OMS</span><span class="sxs-lookup"><span data-stu-id="b32ea-545">Syslog Linux performance counter configuration is not applied in the OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b32ea-546">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="b32ea-546">Probable causes</span></span>
* <span data-ttu-id="b32ea-547">Agent konfiguracji agenta pakietu OMS dla systemu Linux nie odebrał najnowszą konfiguracją w portalu OMS.</span><span class="sxs-lookup"><span data-stu-id="b32ea-547">The configuration agent in the OMS Agent for Linux has not retrieved the latest configuration from the OMS portal.</span></span>
* <span data-ttu-id="b32ea-548">Poprawione ustawień w portalu nie zostały zastosowane.</span><span class="sxs-lookup"><span data-stu-id="b32ea-548">The revised settings in the portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="b32ea-549">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="b32ea-549">Resolutions</span></span>
<span data-ttu-id="b32ea-550">`omsconfig`jest agentem konfiguracji w Agent pakietu OMS dla systemu Linux, które pobierają zmiany konfiguracji portalu OMS co 5 minut.</span><span class="sxs-lookup"><span data-stu-id="b32ea-550">`omsconfig` is the configuration agent in the OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="b32ea-551">Ta konfiguracja jest następnie stosowany do Agent pakietu OMS dla plików konfiguracyjnych Linux pod adresem `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="b32ea-551">This configuration is then applied to the OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="b32ea-552">W niektórych przypadkach Agent pakietu OMS dla systemu Linux konfiguracji agenta nie można skomunikować się z usługą Konfiguracja portalu, co powoduje najnowszej konfiguracji nie są stosowane.</span><span class="sxs-lookup"><span data-stu-id="b32ea-552">In some cases, the OMS Agent for Linux configuration agent might not be able to communicate with the portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="b32ea-553">Sprawdź, czy `omsconfig` agent został zainstalowany z następującymi:</span><span class="sxs-lookup"><span data-stu-id="b32ea-553">Verify that the `omsconfig` agent is installed with the following:</span></span>

  * <span data-ttu-id="b32ea-554">`dpkg --list omsconfig` lub `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="b32ea-554">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="b32ea-555">Jeśli nie jest zainstalowany, zainstaluj ponownie najnowszą wersję agenta pakietu OMS dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-555">If not installed, reinstall the latest version of the OMS Agent for Linux</span></span>
* <span data-ttu-id="b32ea-556">Sprawdź, czy `omsconfig` agenta może komunikować się z usługą OMS</span><span class="sxs-lookup"><span data-stu-id="b32ea-556">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="b32ea-557">Uruchom `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` polecenia</span><span class="sxs-lookup"><span data-stu-id="b32ea-557">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="b32ea-558">Polecenie powyżej zwraca konfigurację agenta pobiera z portalu, w tym ustawienia Syslog, liczniki wydajności systemu Linux i dzienników niestandardowych</span><span class="sxs-lookup"><span data-stu-id="b32ea-558">The command above returns the configuration that agent retrieves from the portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="b32ea-559">W przypadku niepowodzenia powyższego polecenia Uruchom `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` polecenia.</span><span class="sxs-lookup"><span data-stu-id="b32ea-559">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="b32ea-560">To polecenie wymusza agenta omsconfig do komunikowania się z usługą OMS w celu pobrania najnowszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b32ea-560">This command forces the omsconfig agent to communicate with the OMS service to retrieve the latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="b32ea-561">Niestandardowe dane dziennika systemu Linux nie są wyświetlane w portalu OMS</span><span class="sxs-lookup"><span data-stu-id="b32ea-561">Custom Linux log data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="b32ea-562">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="b32ea-562">Probable causes</span></span>
* <span data-ttu-id="b32ea-563">Dołączenie do usługi OMS nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="b32ea-563">Onboarding to OMS Service failed</span></span>
* <span data-ttu-id="b32ea-564">**Dotyczy następującej konfiguracji serwerów z systemem Linux** ustawienia nie zostały wybrane.</span><span class="sxs-lookup"><span data-stu-id="b32ea-564">The **Apply the following configuration to my Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="b32ea-565">omsconfig nie została pobrana najnowsze dziennik niestandardowy z portalu</span><span class="sxs-lookup"><span data-stu-id="b32ea-565">omsconfig has not picked up the latest custom log from the portal</span></span>
* <span data-ttu-id="b32ea-566">`omsagent` Użycie nie jest w stanie dziennik niestandardowy z powodu problemu z uprawnieniami dostępu do lub `omsagent` nie został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="b32ea-566">The `omsagent` use is unable to access the custom log due to a permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="b32ea-567">W takim przypadku zostanie wyświetlony następujący komunikat:</span><span class="sxs-lookup"><span data-stu-id="b32ea-567">In this case, you'll see the following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="b32ea-568">Jest to znany problem dotyczący sytuacji wyścigu, który został rozwiązany w Agent pakietu OMS dla 1.1.0-217 wersji systemu Linux</span><span class="sxs-lookup"><span data-stu-id="b32ea-568">This is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="b32ea-569">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="b32ea-569">Resolutions</span></span>
* <span data-ttu-id="b32ea-570">Sprawdź, czy udało Ci się pomyślnie został załadowany, określając czy `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` plik istnieje.</span><span class="sxs-lookup"><span data-stu-id="b32ea-570">Verify that you've successfully onboarded, by determining whether the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="b32ea-571">Jeśli potrzebne, dodać ponownie przy użyciu wiersza polecenia omsadmin.sh.</span><span class="sxs-lookup"><span data-stu-id="b32ea-571">If needed, onboard again using the omsadmin.sh command line.</span></span> <span data-ttu-id="b32ea-572">Zobacz [dołączania przy użyciu wiersza polecenia](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b32ea-572">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="b32ea-573">W portalu OMS w obszarze **ustawienia** na **danych** karcie, upewnij się, że **dotyczy następującej konfiguracji serwerów z systemem Linux** wybrane ustawienie</span><span class="sxs-lookup"><span data-stu-id="b32ea-573">In the OMS Portal, under **Settings** on the **Data** tab, ensure that the **Apply the following configuration to my Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="b32ea-574">![Zastosuj konfigurację](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="b32ea-574">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="b32ea-575">Sprawdź, czy `omsconfig` agenta może komunikować się z usługą OMS</span><span class="sxs-lookup"><span data-stu-id="b32ea-575">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="b32ea-576">Uruchom `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` polecenia</span><span class="sxs-lookup"><span data-stu-id="b32ea-576">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="b32ea-577">Polecenie powyżej zwraca konfigurację agenta pobiera z portalu, w tym ustawienia Syslog, liczniki wydajności systemu Linux i dzienników niestandardowych</span><span class="sxs-lookup"><span data-stu-id="b32ea-577">The command above returns the configuration that agent retrieves from the Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="b32ea-578">W przypadku niepowodzenia powyższego polecenia Uruchom `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` polecenia.</span><span class="sxs-lookup"><span data-stu-id="b32ea-578">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="b32ea-579">To polecenie wymusza agenta omsconfig do komunikowania się z usługą OMS i pobrania najnowszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b32ea-579">This command forces the omsconfig agent to communicate with OMS service and retrieve the latest configuration.</span></span>

<span data-ttu-id="b32ea-580">Zamiast Agent pakietu OMS dla użytkownika w systemie Linux uruchomiony jako użytkownik uprzywilejowanych `root`, Agent pakietu OMS dla systemu Linux jest uruchamiany jako `omsagent` użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b32ea-580">Instead of the OMS Agent for Linux user running as a privileged user `root`, the OMS Agent for Linux runs as the `omsagent` user.</span></span> <span data-ttu-id="b32ea-581">W większości przypadków jawne uprawnienia muszą mieć uprawnienie do użytkownika w celu odczytu niektórych plików.</span><span class="sxs-lookup"><span data-stu-id="b32ea-581">In most cases, explicit permission must be granted to the user in order to read certain files.</span></span>

<span data-ttu-id="b32ea-582">Aby przyznać uprawnienia do `omsagent` użytkownika, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="b32ea-582">To grant permission to `omsagent` user, run the following commands:</span></span>

1. <span data-ttu-id="b32ea-583">Dodaj `omsagent` użytkownika do określonej grupy z`sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="b32ea-583">Add the `omsagent` user to a specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="b32ea-584">Uniwersalny dostęp do wymaganego pliku z`sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="b32ea-584">Grant universal read access to the required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="b32ea-585">Istnieje znany problem dotyczący sytuacji wyścigu, który został rozwiązany w Agent pakietu OMS dla 1.1.0-217 wersji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b32ea-585">There is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="b32ea-586">Po zaktualizowaniu do najnowsza wersja agenta, uruchom następujące polecenie, aby pobrać najnowszą wersję dodatku danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="b32ea-586">After updating to the latest agent, run the following command to get the latest version of the output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="b32ea-587">Znane ograniczenia</span><span class="sxs-lookup"><span data-stu-id="b32ea-587">Known limitations</span></span>
<span data-ttu-id="b32ea-588">Przejrzyj poniższe sekcje, aby dowiedzieć się więcej o ograniczeniach bieżącego agenta pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b32ea-588">Review the following sections to learn about current limitations of the OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="b32ea-589">Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="b32ea-589">Azure Diagnostics</span></span>
<span data-ttu-id="b32ea-590">Dla maszyn wirtualnych systemu Linux działających na platformie Azure może być wymagane dodatkowe kroki umożliwiają zbieranie danych diagnostyki Azure i usługi Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="b32ea-590">For Linux virtual machines running in Azure, additional steps may be required to allow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="b32ea-591">**W wersji 2.2** rozszerzenia diagnostyki dla systemu Linux jest wymagany dla zgodności z agentem pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="b32ea-591">**Version 2.2** of the Diagnostics Extension for Linux is required for compatibility with the OMS Agent for Linux.</span></span>

<span data-ttu-id="b32ea-592">Aby uzyskać więcej informacji o instalowaniu i konfigurowaniu rozszerzenia diagnostycznych dla systemu Linux, zobacz [za pomocą polecenia wiersza polecenia platformy Azure można włączyć rozszerzenia diagnostycznych Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="b32ea-592">For more information on installing and configuring the Diagnostic Extension for Linux, see [Use the Azure CLI command to enable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="b32ea-593">**Uaktualnianie rozszerzenia diagnostyki Linux z 2.0 do 2,2 ASM interfejsu wiersza polecenia platformy Azure:**</span><span class="sxs-lookup"><span data-stu-id="b32ea-593">**Upgrading the Linux Diagnostics Extension from 2.0 to 2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="b32ea-594">**ARM**</span><span class="sxs-lookup"><span data-stu-id="b32ea-594">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="b32ea-595">Plik o nazwie PrivateConfig.json odwoływać się do tych przykładach poleceń.</span><span class="sxs-lookup"><span data-stu-id="b32ea-595">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="b32ea-596">Format tego pliku powinno przypominać następujące przykładowe.</span><span class="sxs-lookup"><span data-stu-id="b32ea-596">The format of that file should resemble the following sample.</span></span>

```
    {
    "storageAccountName":"the storage account to receive data",
    "storageAccountKey":"the key of the account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="b32ea-597">Sysklog nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="b32ea-597">Sysklog is not supported</span></span>
<span data-ttu-id="b32ea-598">Rsyslog lub syslog ng są wymagane do zbierania komunikaty dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="b32ea-598">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="b32ea-599">Demon syslog domyślne w wersji 5 (sysklog) w wersji Red Hat Enterprise Linux, CentOS i Oracle Linux nie jest obsługiwana dla zbierania zdarzeń usługi syslog.</span><span class="sxs-lookup"><span data-stu-id="b32ea-599">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="b32ea-600">Aby zbierać dane syslog z tej wersji tych dystrybucji, demona rsyslog powinna być zainstalowana i skonfigurowana zastąpić sysklog.</span><span class="sxs-lookup"><span data-stu-id="b32ea-600">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span> <span data-ttu-id="b32ea-601">Aby uzyskać więcej informacji o zamianę sysklog rsyslog, zobacz [zainstalować nowo zbudowany rsyslog obr. / min](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span><span class="sxs-lookup"><span data-stu-id="b32ea-601">For more information on replacing sysklog with rsyslog, see [Install the newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b32ea-602">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b32ea-602">Next Steps</span></span>
* <span data-ttu-id="b32ea-603">[Dodaj rozwiązania Log Analytics z galerii rozwiązań](log-analytics-add-solutions.md), aby dodać funkcje i zebrać dane.</span><span class="sxs-lookup"><span data-stu-id="b32ea-603">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
* <span data-ttu-id="b32ea-604">Zapoznaj się z [wyszukiwaniem w dziennikach](log-analytics-log-searches.md), aby wyświetlić szczegółowe informacje zebrane przez rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="b32ea-604">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span></span>
* <span data-ttu-id="b32ea-605">Użyj [pulpitów nawigacyjnych](log-analytics-dashboards.md), aby zapisywać i wyświetlać własne, niestandardowe wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="b32ea-605">Use [dashboards](log-analytics-dashboards.md) to save and display your own custom searches.</span></span>
