---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a><span data-ttu-id="33dfe-101">Połącz z tooLog komputerów Linux Analytics</span><span class="sxs-lookup"><span data-stu-id="33dfe-101">Connect your Linux computers tooLog Analytics</span></span>
<span data-ttu-id="33dfe-102">Za pomocą analizy dzienników, można zbierać i działają na danych generowanych przez komputery z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="33dfe-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="33dfe-103">Dodawanie danych zbieranych z Linux tooOMS pozwala toomanage systemów Linux i kontener rozwiązań, takich jak Docker, niezależnie od tego, w którym znajdują się komputery — niemal dowolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="33dfe-103">Adding data collected from Linux tooOMS allows you toomanage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="33dfe-104">Źródeł danych może znajdować się w lokalnym centrum danych jako serwerów fizycznych komputerów wirtualnych w usług hostowanych w chmurze, takich jak Amazon Web Services (AWS) lub Microsoft Azure lub nawet hello laptopów na biurku.</span><span class="sxs-lookup"><span data-stu-id="33dfe-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even hello laptop on your desk.</span></span> <span data-ttu-id="33dfe-105">Ponadto OMS również zbiera dane z komputerów z systemem Windows podobnie, obsługuje on naprawdę hybrydowe środowiska IT.</span><span class="sxs-lookup"><span data-stu-id="33dfe-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="33dfe-106">Można wyświetlić i zarządzać danych ze wszystkich tych źródeł z analizy dzienników w OMS za pomocą portalu zarządzania pojedynczego.</span><span class="sxs-lookup"><span data-stu-id="33dfe-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="33dfe-107">Zmniejsza to potrzebę hello toomonitor przy użyciu wielu różnych systemów, umożliwia łatwe tooconsume i można wyeksportować wszystkie dane, które chcesz rozwiązania analizy biznesowej toowhatever lub systemu, która już istnieje.</span><span class="sxs-lookup"><span data-stu-id="33dfe-107">This reduces hello need toomonitor it using many different systems, makes it easy tooconsume, and you can export any data you like toowhatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="33dfe-108">W tym artykule jest Przewodnik Szybki start, które zawierają informacje pomocne podczas zbierania danych i zarządzanie nimi dla komputerów systemu Linux przy użyciu hello Agent pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="33dfe-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using hello OMS Agent for Linux.</span></span> <span data-ttu-id="33dfe-109">Aby uzyskać więcej szczegółowych informacji technicznych, takich jak konfiguracja serwera proxy, informacje o CollectD metryki i niestandardowych źródeł danych JSON, znajdziesz te informacje w [Agent pakietu OMS dla systemu Linux — omówienie](https://github.com/Microsoft/OMS-Agent-for-Linux) i [Agent pakietu OMS dla systemu Linux Pełna dokumentacja](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="33dfe-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="33dfe-110">Obecnie można zebrać hello następujące typy danych z komputerów z systemem Linux:</span><span class="sxs-lookup"><span data-stu-id="33dfe-110">Currently, you can collect hello following types of data from Linux computers:</span></span>

* <span data-ttu-id="33dfe-111">Metryki wydajności</span><span class="sxs-lookup"><span data-stu-id="33dfe-111">Performance metrics</span></span>
* <span data-ttu-id="33dfe-112">Zdarzenia dziennika systemowego</span><span class="sxs-lookup"><span data-stu-id="33dfe-112">Syslog events</span></span>
* <span data-ttu-id="33dfe-113">Alerty z Nagios i Zabbix</span><span class="sxs-lookup"><span data-stu-id="33dfe-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="33dfe-114">Metryki wydajności kontenera docker, spisu i dzienniki</span><span class="sxs-lookup"><span data-stu-id="33dfe-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="33dfe-115">Obsługiwane wersje systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-115">Supported Linux versions</span></span>
<span data-ttu-id="33dfe-116">Wersje x x86 i x64 oficjalnie są obsługiwane w różnych dystrybucje systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="33dfe-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="33dfe-117">Jednak hello Agent pakietu OMS dla systemu Linux mogą również uruchomić na innych dystrybucje nie na liście.</span><span class="sxs-lookup"><span data-stu-id="33dfe-117">However, hello OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="33dfe-118">Linux Amazon 2012.09 za pośrednictwem 2015.09</span><span class="sxs-lookup"><span data-stu-id="33dfe-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="33dfe-119">CentOS Linux 5, 6 i 7</span><span class="sxs-lookup"><span data-stu-id="33dfe-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="33dfe-120">Oracle Linux 5, 6 i 7</span><span class="sxs-lookup"><span data-stu-id="33dfe-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="33dfe-121">Red Hat Enterprise Linux Server 5, 6 i 7</span><span class="sxs-lookup"><span data-stu-id="33dfe-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="33dfe-122">Debian GNU/Linux 6, 7 i 8</span><span class="sxs-lookup"><span data-stu-id="33dfe-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="33dfe-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="33dfe-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="33dfe-124">SUSE Linux Enterprise Server 11 i 12</span><span class="sxs-lookup"><span data-stu-id="33dfe-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="33dfe-125">Agent pakietu OMS dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-125">OMS Agent for Linux</span></span>
<span data-ttu-id="33dfe-126">Agent programu Operations Management Suite dla systemu Linux Hello składa się z wielu pakietów.</span><span class="sxs-lookup"><span data-stu-id="33dfe-126">hello Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="33dfe-127">Witaj wersji pliku zawiera następujące dostępnych przez uruchomione hello powłoki pakietu z pakietów hello `--extract`.</span><span class="sxs-lookup"><span data-stu-id="33dfe-127">hello release file contains hello following packages, available by running hello shell bundle with `--extract`.</span></span>

| <span data-ttu-id="33dfe-128">**Pakiet**</span><span class="sxs-lookup"><span data-stu-id="33dfe-128">**Package**</span></span> | <span data-ttu-id="33dfe-129">**Wersja**</span><span class="sxs-lookup"><span data-stu-id="33dfe-129">**Version**</span></span> | <span data-ttu-id="33dfe-130">**Opis**</span><span class="sxs-lookup"><span data-stu-id="33dfe-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33dfe-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="33dfe-131">omsagent</span></span> |<span data-ttu-id="33dfe-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="33dfe-132">1.1.0</span></span> |<span data-ttu-id="33dfe-133">Witaj Operations Management Suite agenta dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-133">hello Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="33dfe-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="33dfe-134">omsconfig</span></span> |<span data-ttu-id="33dfe-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="33dfe-135">1.1.1</span></span> |<span data-ttu-id="33dfe-136">Konfiguracja agenta dla hello Agent pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="33dfe-136">Configuration agent for hello OMS Agent</span></span> |
| <span data-ttu-id="33dfe-137">OMI</span><span class="sxs-lookup"><span data-stu-id="33dfe-137">omi</span></span> |<span data-ttu-id="33dfe-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="33dfe-138">1.0.8.3</span></span> |<span data-ttu-id="33dfe-139">Open Management Infrastructure (OMI)--lekkie serwera modelu wspólnych informacji</span><span class="sxs-lookup"><span data-stu-id="33dfe-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="33dfe-140">scx</span><span class="sxs-lookup"><span data-stu-id="33dfe-140">scx</span></span> |<span data-ttu-id="33dfe-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="33dfe-141">1.6.2</span></span> |<span data-ttu-id="33dfe-142">OMI CIM dostawców dla metryki wydajności systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="33dfe-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="33dfe-143">Apache cimprov</span><span class="sxs-lookup"><span data-stu-id="33dfe-143">apache-cimprov</span></span> |<span data-ttu-id="33dfe-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="33dfe-144">1.0.0</span></span> |<span data-ttu-id="33dfe-145">Monitorowanie dostawcę dla OMI wydajności Apache HTTP Server.</span><span class="sxs-lookup"><span data-stu-id="33dfe-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="33dfe-146">Zainstalować tylko w przypadku wykrycia Apache HTTP Server.</span><span class="sxs-lookup"><span data-stu-id="33dfe-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="33dfe-147">MySQL cimprov</span><span class="sxs-lookup"><span data-stu-id="33dfe-147">mysql-cimprov</span></span> |<span data-ttu-id="33dfe-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="33dfe-148">1.0.0</span></span> |<span data-ttu-id="33dfe-149">Monitorowanie dostawcę dla OMI wydajności serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="33dfe-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="33dfe-150">Zainstalować tylko w przypadku wykrycia MySQL/MariaDB serwera.</span><span class="sxs-lookup"><span data-stu-id="33dfe-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="33dfe-151">docker cimprov</span><span class="sxs-lookup"><span data-stu-id="33dfe-151">docker-cimprov</span></span> |<span data-ttu-id="33dfe-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="33dfe-152">0.1.0</span></span> |<span data-ttu-id="33dfe-153">Dostawca docker OMI.</span><span class="sxs-lookup"><span data-stu-id="33dfe-153">Docker provider for OMI.</span></span> <span data-ttu-id="33dfe-154">Zainstalować tylko w przypadku wykrycia Docker.</span><span class="sxs-lookup"><span data-stu-id="33dfe-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="33dfe-155">Artefakty dodatkowych instalacji</span><span class="sxs-lookup"><span data-stu-id="33dfe-155">Additional installation artifacts</span></span>
<span data-ttu-id="33dfe-156">Po zainstalowaniu agenta pakietu OMS hello pakietów systemu Linux, hello następujące dodatkowe czynności konfiguracyjne systemowe zmiany zostaną zastosowane.</span><span class="sxs-lookup"><span data-stu-id="33dfe-156">After installing hello OMS agent for Linux packages, hello following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="33dfe-157">Te artefakty muszą zostać usunięte po odinstalowaniu hello omsagent pakietu.</span><span class="sxs-lookup"><span data-stu-id="33dfe-157">These artifacts are removed when hello omsagent package is uninstalled.</span></span>

* <span data-ttu-id="33dfe-158">Użytkownik bez uprawnień o nazwie: `omsagent` jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="33dfe-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="33dfe-159">To jest program hello konta hello omsagent demon działa jako</span><span class="sxs-lookup"><span data-stu-id="33dfe-159">This is hello account hello omsagent daemon runs as</span></span>
* <span data-ttu-id="33dfe-160">Plik "Dołącz" sudoers jest tworzony w /etc/sudoers.d/omsagent to autoryzuje omsagent toorestart hello syslog i demonów omsagent.</span><span class="sxs-lookup"><span data-stu-id="33dfe-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent toorestart hello syslog and omsagent daemons.</span></span> <span data-ttu-id="33dfe-161">Jeśli dyrektywy "Dołącz" sudo nie są obsługiwane w wersji hello zainstalowany sudo, te wpisy zostaną zapisane zbyt/etc/sudoers.</span><span class="sxs-lookup"><span data-stu-id="33dfe-161">If sudo “include” directives are not supported in hello installed version of sudo, these entries will be written too/etc/sudoers.</span></span>
* <span data-ttu-id="33dfe-162">Konfiguracja syslog Hello jest zmodyfikowany tooforward podzbiór zdarzeń toohello agenta.</span><span class="sxs-lookup"><span data-stu-id="33dfe-162">hello syslog configuration is modified tooforward a subset of events toohello agent.</span></span> <span data-ttu-id="33dfe-163">Aby uzyskać więcej informacji, zobacz hello **Konfigurowanie zbierania danych** poniższej sekcji</span><span class="sxs-lookup"><span data-stu-id="33dfe-163">For more information, see hello **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="33dfe-164">Szczegóły pobierania danych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-164">Linux data collection details</span></span>
<span data-ttu-id="33dfe-165">Witaj poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak zbierane są dane.</span><span class="sxs-lookup"><span data-stu-id="33dfe-165">hello following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="33dfe-166">Źródło</span><span class="sxs-lookup"><span data-stu-id="33dfe-166">source</span></span> | <span data-ttu-id="33dfe-167">Bezpośrednie agenta</span><span class="sxs-lookup"><span data-stu-id="33dfe-167">Direct Agent</span></span> | <span data-ttu-id="33dfe-168">Agenta programu SCOM</span><span class="sxs-lookup"><span data-stu-id="33dfe-168">SCOM agent</span></span> | <span data-ttu-id="33dfe-169">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="33dfe-169">Azure Storage</span></span> | <span data-ttu-id="33dfe-170">SCOM wymagane?</span><span class="sxs-lookup"><span data-stu-id="33dfe-170">SCOM required?</span></span> | <span data-ttu-id="33dfe-171">Dane agenta programu SCOM wysyłane za pośrednictwem grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="33dfe-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="33dfe-172">Częstotliwość kolekcji</span><span class="sxs-lookup"><span data-stu-id="33dfe-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="33dfe-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="33dfe-173">Zabbix</span></span> |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="33dfe-179">1 minuta</span><span class="sxs-lookup"><span data-stu-id="33dfe-179">1 minute</span></span> |
| <span data-ttu-id="33dfe-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="33dfe-180">Nagios</span></span> |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="33dfe-186">po przybyciu</span><span class="sxs-lookup"><span data-stu-id="33dfe-186">on arrival</span></span> |
| <span data-ttu-id="33dfe-187">syslog</span><span class="sxs-lookup"><span data-stu-id="33dfe-187">syslog</span></span> |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="33dfe-193">z usługi Azure storage: 10 minut; od agenta: Przy nadejściu</span><span class="sxs-lookup"><span data-stu-id="33dfe-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="33dfe-194">Liczniki wydajności systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-194">Linux performance counters</span></span> |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="33dfe-200">jako zaplanowane, co najmniej 10 sekund</span><span class="sxs-lookup"><span data-stu-id="33dfe-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="33dfe-201">Śledzenie zmian</span><span class="sxs-lookup"><span data-stu-id="33dfe-201">change tracking</span></span> |![Tak](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Nie](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="33dfe-207">co godzinę</span><span class="sxs-lookup"><span data-stu-id="33dfe-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="33dfe-208">Wymagania pakietu</span><span class="sxs-lookup"><span data-stu-id="33dfe-208">Package Requirements</span></span>
| <span data-ttu-id="33dfe-209">**Wymagany pakiet**</span><span class="sxs-lookup"><span data-stu-id="33dfe-209">**Required package**</span></span> | <span data-ttu-id="33dfe-210">**Opis**</span><span class="sxs-lookup"><span data-stu-id="33dfe-210">**Description**</span></span> | <span data-ttu-id="33dfe-211">**Minimalna wersja**</span><span class="sxs-lookup"><span data-stu-id="33dfe-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33dfe-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="33dfe-212">Glibc</span></span> |<span data-ttu-id="33dfe-213">Biblioteka GNU C</span><span class="sxs-lookup"><span data-stu-id="33dfe-213">GNU C library</span></span> |<span data-ttu-id="33dfe-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="33dfe-214">2.5-12</span></span> |
| <span data-ttu-id="33dfe-215">Biblioteki Openssl</span><span class="sxs-lookup"><span data-stu-id="33dfe-215">Openssl</span></span> |<span data-ttu-id="33dfe-216">Biblioteki OpenSSL</span><span class="sxs-lookup"><span data-stu-id="33dfe-216">OpenSSL libraries</span></span> |<span data-ttu-id="33dfe-217">0.9.8e lub 1.0</span><span class="sxs-lookup"><span data-stu-id="33dfe-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="33dfe-218">Narzędzie curl</span><span class="sxs-lookup"><span data-stu-id="33dfe-218">Curl</span></span> |<span data-ttu-id="33dfe-219">cURL klienta sieci web</span><span class="sxs-lookup"><span data-stu-id="33dfe-219">cURL web client</span></span> |<span data-ttu-id="33dfe-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="33dfe-220">7.15.5</span></span> |
| <span data-ttu-id="33dfe-221">Ctypes języka Python</span><span class="sxs-lookup"><span data-stu-id="33dfe-221">Python-ctypes</span></span> |<span data-ttu-id="33dfe-222">Funkcja biblioteki</span><span class="sxs-lookup"><span data-stu-id="33dfe-222">function libraries</span></span> |<span data-ttu-id="33dfe-223">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="33dfe-223">n/a</span></span> |
| <span data-ttu-id="33dfe-224">PAM</span><span class="sxs-lookup"><span data-stu-id="33dfe-224">PAM</span></span> |<span data-ttu-id="33dfe-225">Uwierzytelnianie podłączane moduły</span><span class="sxs-lookup"><span data-stu-id="33dfe-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="33dfe-226">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="33dfe-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="33dfe-227">Rsyslog lub syslog ng są wymagane toocollect komunikaty dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="33dfe-227">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="33dfe-228">demon syslog domyślne Hello w wersji 5 (sysklog) w wersji Red Hat Enterprise Linux, CentOS i Oracle Linux nie jest obsługiwana dla zbierania zdarzeń usługi syslog.</span><span class="sxs-lookup"><span data-stu-id="33dfe-228">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="33dfe-229">toocollect syslog danych z tej wersji tych dystrybucji hello rsyslog demon powinien być zainstalowany i skonfigurowany tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="33dfe-229">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="33dfe-230">Szybkiej instalacji</span><span class="sxs-lookup"><span data-stu-id="33dfe-230">Quick install</span></span>
<span data-ttu-id="33dfe-231">Uruchom następujące polecenia toodownload hello omsagent hello, weryfikowanie hello sumy kontrolnej, a następnie instalowanie i hello dołączyć agenta.</span><span class="sxs-lookup"><span data-stu-id="33dfe-231">Run hello following commands toodownload hello omsagent, validate hello checksum, then  install and onboard hello agent.</span></span> <span data-ttu-id="33dfe-232">Polecenia są dla 64-bitowej.</span><span class="sxs-lookup"><span data-stu-id="33dfe-232">Commands are for 64-bit.</span></span> <span data-ttu-id="33dfe-233">Witaj identyfikator i klucz podstawowy znajdują się w portalu OMS hello w obszarze **ustawienia** na powitania **połączonych źródeł** kartę.</span><span class="sxs-lookup"><span data-stu-id="33dfe-233">hello Workspace ID and Primary Key are found in hello OMS portal under **Settings** on hello **Connected Sources** tab.</span></span>

![szczegóły obszaru roboczego](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="33dfe-235">Istnieje wiele innych metod tooinstall hello agent i jego uaktualnienie.</span><span class="sxs-lookup"><span data-stu-id="33dfe-235">There are a variety of other methods tooinstall hello agent and upgrade it.</span></span> <span data-ttu-id="33dfe-236">Więcej o nich na [kroki tooinstall hello Agent pakietu OMS Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="33dfe-236">You can read more about them at [Steps tooinstall hello OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="33dfe-237">Można również wyświetlić hello [Azure przewodnik wideo](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="33dfe-237">You can also view hello [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="33dfe-238">Wybierz metodę zbierania danych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="33dfe-239">Jak można wybrać hello typy danych, która ma jak toocollect zależy od tego, czy ma portalu OMS hello toouse lub jeśli chcesz edytować różne pliki konfiguracji bezpośrednio na klientach systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="33dfe-239">How you choose hello data types you'd like toocollect depends on whether you want toouse hello OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="33dfe-240">Jeśli wybierzesz toouse hello portal konfiguracji hello jest automatycznie wysyłane tooall klientów systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="33dfe-240">If you choose toouse hello portal, hello configuration is sent tooall of your Linux clients automatically.</span></span> <span data-ttu-id="33dfe-241">Jeśli potrzebujesz różnych konfiguracji dla różnych klientów systemu Linux, będzie konieczne pliki klienta tooedit indywidualnie — lub użyj zamiast jak PowerShell DSC, Chef lub Puppet.</span><span class="sxs-lookup"><span data-stu-id="33dfe-241">If you need different configurations for different Linux clients, you will need tooedit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="33dfe-242">Można określić zdarzenia dziennika systemowego hello i liczniki wydajności, które mają toocollect za pomocą plików konfiguracji na komputerach z systemem Linux hello.</span><span class="sxs-lookup"><span data-stu-id="33dfe-242">You can specify hello syslog events and performance counters that you want toocollect using configuration files on hello Linux computers.</span></span> <span data-ttu-id="33dfe-243">*Jeśli została wybrana opcja tooconfigure zbierania danych przez edycję plików konfiguracyjnych agenta, należy wyłączyć Konfiguracja scentralizowana hello.*</span><span class="sxs-lookup"><span data-stu-id="33dfe-243">*If you chose tooconfigure data collection by editing agent configuration files, you should disable hello centralized configuration.*</span></span>  <span data-ttu-id="33dfe-244">Instrukcje znajdują się poniżej tooconfigure zbierania danych agenta hello pliki konfiguracji, a także konfiguracji centralnej toodisable wszystkich agentów OMS dla systemu Linux lub pojedynczych komputerów.</span><span class="sxs-lookup"><span data-stu-id="33dfe-244">Instructions are provided below tooconfigure data collection in hello agent's configuration files as well as toodisable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="33dfe-245">Wyłącz zarządzanie OMS dla danego komputera systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="33dfe-246">Scentralizowane zbieranie danych dla danych konfiguracji jest wyłączona dla danego komputera Linux z hello OMS_MetaConfigHelper.py skryptu.</span><span class="sxs-lookup"><span data-stu-id="33dfe-246">Centralized data collection for configuration data is disabled for an individual Linux computer with hello OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="33dfe-247">Może to być przydatne, jeśli podzbiorowi komputerów należy specjalne konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="33dfe-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="33dfe-248">Konfiguracja scentralizowana toodisable:</span><span class="sxs-lookup"><span data-stu-id="33dfe-248">toodisable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="33dfe-249">Konfiguracja scentralizowana Włącz toore:</span><span class="sxs-lookup"><span data-stu-id="33dfe-249">toore-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="33dfe-250">Liczniki wydajności systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-250">Linux performance counters</span></span>
<span data-ttu-id="33dfe-251">Liczniki wydajności systemu Linux są podobne liczniki wydajności tooWindows — zarówno działają podobnie.</span><span class="sxs-lookup"><span data-stu-id="33dfe-251">Linux performance counters are similar tooWindows performance counters—both operate similarly.</span></span> <span data-ttu-id="33dfe-252">Można użyć hello następujące procedury tooadd i skonfigurować je.</span><span class="sxs-lookup"><span data-stu-id="33dfe-252">You can use hello following procedures tooadd and configure them.</span></span> <span data-ttu-id="33dfe-253">Po dodaniu ich tooOMS, dane są zbierane dla nich co 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="33dfe-253">After they are added tooOMS, data is collected for them every 30 seconds.</span></span>

### <a name="tooadd-a-linux-performance-counter-in-oms"></a><span data-ttu-id="33dfe-254">tooadd licznika wydajności systemu Linux w OMS</span><span class="sxs-lookup"><span data-stu-id="33dfe-254">tooadd a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="33dfe-255">tooconfigure OMS agentów dla systemu Linux przy użyciu portalu OMS hello, można dodać liczniki wydajności systemu Linux na stronie Ustawienia powitania kliknij **danych**.</span><span class="sxs-lookup"><span data-stu-id="33dfe-255">tooconfigure OMS Agents for Linux using hello OMS portal, you can add Linux performance counters on hello Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="33dfe-256">Na powitania **ustawienia** w obszarze **danych** , kliknij przycisk **liczników wydajności systemu Linux** , a następnie wybierz lub wpisz nazwę hello licznika hello ma tooadd.</span><span class="sxs-lookup"><span data-stu-id="33dfe-256">On hello **Settings** page under **Data** , click **Linux performance counters** and then select or type hello name of hello counter you want tooadd.</span></span>  
    <span data-ttu-id="33dfe-257">![dane](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="33dfe-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="33dfe-258">Jeśli nie znasz hello Pełna nazwa licznika hello, możesz wpisać nazwę częściowe i zostanie wyświetlona lista dostępnych liczników.</span><span class="sxs-lookup"><span data-stu-id="33dfe-258">If you don't know hello full name of hello counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="33dfe-259">Po znalezieniu licznika hello mają tooadd, kliknij nazwę hello liście hello a następnie kliknij przycisk hello plus hello tooadd ikona licznika.</span><span class="sxs-lookup"><span data-stu-id="33dfe-259">When you find hello counter you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello counter.</span></span>
4. <span data-ttu-id="33dfe-260">Po dodaniu licznika hello pojawia się liście hello wyróżnione z paskiem kolorowe liczników.</span><span class="sxs-lookup"><span data-stu-id="33dfe-260">After you add hello counter, it appears in hello list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="33dfe-261">Domyślnie program hello **Zastosuj poniżej maszyny toomy konfiguracji** opcja jest zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="33dfe-261">By default, hello **Apply below configuration toomy machines** option is selected.</span></span> <span data-ttu-id="33dfe-262">Jeśli chcesz toodisable wysyłanie danych konfiguracji, należy usunąć zaznaczenie hello.</span><span class="sxs-lookup"><span data-stu-id="33dfe-262">If you want toodisable sending configuration data, clear hello selection.</span></span>
6. <span data-ttu-id="33dfe-263">Po zakończeniu modyfikowania liczniki wydajności, u dołu strony hello powitania kliknij **zapisać** toofinalize zmiany.</span><span class="sxs-lookup"><span data-stu-id="33dfe-263">When you are done modifying performance counters, at hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="33dfe-264">Hello zmian konfiguracji, które zostały wprowadzone są następnie wysyłane hello tooall OMS agentów dla systemu Linux, które są zarejestrowane w usłudze OMS, zazwyczaj w ciągu 5 minut.</span><span class="sxs-lookup"><span data-stu-id="33dfe-264">hello configuration changes that you've made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="33dfe-265">Konfigurowanie liczników wydajności systemu Linux w OMS</span><span class="sxs-lookup"><span data-stu-id="33dfe-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="33dfe-266">Do liczników wydajności systemu Windows można wybrać określonego wystąpienia dla każdego licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="33dfe-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="33dfe-267">Do liczników wydajności systemu Linux, niezależnie od wystąpienia wybranego licznika stosuje liczniki podrzędnych tooall hello nadrzędnego licznika.</span><span class="sxs-lookup"><span data-stu-id="33dfe-267">However, for Linux performance counters, whatever instance of a counter that you choose applies tooall child counters of hello parent counter.</span></span> <span data-ttu-id="33dfe-268">Witaj poniższej tabeli przedstawiono typowe wystąpień hello tooboth dostępne liczniki wydajności systemu Linux i Windows.</span><span class="sxs-lookup"><span data-stu-id="33dfe-268">hello following table shows hello common instances available tooboth Linux and Windows performance counters.</span></span>

| <span data-ttu-id="33dfe-269">**Nazwa wystąpienia**</span><span class="sxs-lookup"><span data-stu-id="33dfe-269">**Instance name**</span></span> | <span data-ttu-id="33dfe-270">**Znaczenie**</span><span class="sxs-lookup"><span data-stu-id="33dfe-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="33dfe-271">\_Całkowita liczba</span><span class="sxs-lookup"><span data-stu-id="33dfe-271">\_Total</span></span> |<span data-ttu-id="33dfe-272">Całkowita liczba wszystkich wystąpień hello</span><span class="sxs-lookup"><span data-stu-id="33dfe-272">Total of all hello instances</span></span> |
| \* |<span data-ttu-id="33dfe-273">Wszystkie wystąpienia</span><span class="sxs-lookup"><span data-stu-id="33dfe-273">All instances</span></span> |
| <span data-ttu-id="33dfe-274">(/ &#124; / var)</span><span class="sxs-lookup"><span data-stu-id="33dfe-274">(/&#124;/var)</span></span> |<span data-ttu-id="33dfe-275">Dopasowuje wystąpienia o nazwie: / lub /var</span><span class="sxs-lookup"><span data-stu-id="33dfe-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="33dfe-276">Podobnie hello interwału wybranego licznika nadrzędnego stosuje tooall jego liczniki podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="33dfe-276">Similarly, hello sample interval that you choose for a parent counter applies tooall its child counters.</span></span> <span data-ttu-id="33dfe-277">Innymi słowy wszystkie interwałów próbkowania licznika podrzędnych hello i wystąpienia są również powiązane ze sobą.</span><span class="sxs-lookup"><span data-stu-id="33dfe-277">In other words, all hello child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="33dfe-278">Dodawanie i Konfigurowanie metryki wydajności z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="33dfe-279">Toocollect metryki wydajności są kontrolowane przez konfigurację hello w/etc/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="33dfe-279">Performance metrics toocollect are controlled by hello configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="33dfe-280">Zobacz [metryki wydajności dostępne](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) dostępnych klas i metryki dla hello Agent pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="33dfe-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for hello OMS Agent for Linux.</span></span>

<span data-ttu-id="33dfe-281">Każdy obiekt lub kategorii toocollect metryki wydajności powinien być zdefiniowany w pliku konfiguracyjnym hello jako pojedynczy `<source>` elementu.</span><span class="sxs-lookup"><span data-stu-id="33dfe-281">Each object, or category, of performance metrics toocollect should be defined in hello configuration file as a single `<source>` element.</span></span> <span data-ttu-id="33dfe-282">Składnia Hello zgodny wzorcem hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="33dfe-282">hello syntax follows hello pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="33dfe-283">można konfigurować parametry Hello tego elementu są:</span><span class="sxs-lookup"><span data-stu-id="33dfe-283">hello configurable parameters of this element are:</span></span>

* <span data-ttu-id="33dfe-284">**Obiekt\_nazwa**: hello nazwę obiektu hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="33dfe-284">**Object\_name**: hello object name for hello collection.</span></span>
* <span data-ttu-id="33dfe-285">**Wystąpienie\_regex**: *wyrażenia regularnego* Definiowanie które toocollect wystąpień.</span><span class="sxs-lookup"><span data-stu-id="33dfe-285">**Instance\_regex**: a *regular expression* defining which instances toocollect.</span></span> <span data-ttu-id="33dfe-286">Witaj wartość: `.*` określa wszystkich wystąpień.</span><span class="sxs-lookup"><span data-stu-id="33dfe-286">hello value: `.*` specifies all instances.</span></span> <span data-ttu-id="33dfe-287">metryki procesora toocollect tylko hello \_całkowita liczba wystąpień, można określić `_Total`.</span><span class="sxs-lookup"><span data-stu-id="33dfe-287">toocollect processor metrics for only hello \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="33dfe-288">Metryka procesu toocollect dla hello tylko wystąpienia crond lub sshd, można określić: `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="33dfe-288">toocollect process metrics for only hello crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="33dfe-289">**Licznik\_nazwa\_wyrażenia regularnego**: *wyrażenia regularnego* Definiowanie które toocollect liczniki (dla obiekt hello).</span><span class="sxs-lookup"><span data-stu-id="33dfe-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for hello object) toocollect.</span></span> <span data-ttu-id="33dfe-290">Określ wszystkie liczniki dla obiekt hello toocollect: `.*`.</span><span class="sxs-lookup"><span data-stu-id="33dfe-290">toocollect all counters for hello object, specify: `.*`.</span></span> <span data-ttu-id="33dfe-291">toocollect wymiany tylko miejsca liczniki dla obiekt pamięci hello, można określić:`.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="33dfe-291">toocollect only swap space counters for hello memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="33dfe-292">**Interwał:**: hello częstotliwości, w których hello są zbierane liczniki obiektu.</span><span class="sxs-lookup"><span data-stu-id="33dfe-292">**Interval:**: hello frequency at which hello object's counters are collected.</span></span>

<span data-ttu-id="33dfe-293">Witaj konfigurację domyślną dla metryki wydajności jest:</span><span class="sxs-lookup"><span data-stu-id="33dfe-293">hello default configuration for performance metrics is:</span></span>

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

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="33dfe-294">Włącz MySQL liczniki wydajności za pomocą poleceń systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="33dfe-295">Jeśli serwer MySQL lub MariaDB serwer zostanie wykryte na komputerze hello po zainstalowaniu pakietu omsagent hello, jest automatycznie instalowany dostawcy dla serwera MySQL monitorowania wydajności.</span><span class="sxs-lookup"><span data-stu-id="33dfe-295">If MySQL Server or MariaDB Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="33dfe-296">Ten dostawca łączy toohello lokalnego MySQL/MariaDB tooexpose Statystyka wydajności serwera.</span><span class="sxs-lookup"><span data-stu-id="33dfe-296">This provider connects toohello local MySQL/MariaDB server tooexpose performance statistics.</span></span> <span data-ttu-id="33dfe-297">Należy poświadczenia użytkownika MySQL tooconfigure, dzięki czemu hello dostawcy dostęp hello serwer MySQL.</span><span class="sxs-lookup"><span data-stu-id="33dfe-297">You need tooconfigure MySQL user credentials so that hello provider can access hello MySQL Server.</span></span>

<span data-ttu-id="33dfe-298">toodefine domyślnego konta użytkownika serwera MySQL hello na hoście lokalnym, użyj hello poniższy przykład polecenia.</span><span class="sxs-lookup"><span data-stu-id="33dfe-298">toodefine a default user account for hello MySQL server on localhost, use hello following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="33dfe-299">Plik poświadczeń Hello musi być do odczytu przez konto omsagent hello.</span><span class="sxs-lookup"><span data-stu-id="33dfe-299">hello credentials file must be readable by hello omsagent account.</span></span> <span data-ttu-id="33dfe-300">Zalecane jest uruchomienie polecenia mycimprovauth hello jako omsgent.</span><span class="sxs-lookup"><span data-stu-id="33dfe-300">Running hello mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="33dfe-301">Alternatywnie można określić hello wymagane poświadczenia MySQL w pliku, tworząc plik hello: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Aby uzyskać więcej informacji o zarządzaniu MySQL poświadczeń do monitorowania za pomocą pliku mysql auth hello, zobacz [MySQL zarządzania, monitorowania poświadczenia w pliku uwierzytelniania hello](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="33dfe-301">Alternatively, you can specify hello required MySQL credentials in a file, by creating hello file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. For more information about managing MySQL credentials for monitoring through hello mysql-auth file, see [Manage MySQL monitoring credentials in hello authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="33dfe-302">Zobacz [bazy danych uprawnienia wymagane do liczników wydajności MySQL](#database-permissions-required-for-mysql-performance-counters) szczegółowe informacje o obiekcie uprawnień wymaganych przez hello MySQL użytkownika toocollect dane dotyczące wydajności serwera MySQL.</span><span class="sxs-lookup"><span data-stu-id="33dfe-302">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by hello MySQL user toocollect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="33dfe-303">Włącz Apache HTTP Server liczniki wydajności za pomocą poleceń systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-303">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="33dfe-304">W przypadku wykrycia Apache HTTP Server na komputerze powitania po zainstalowaniu pakietu omsagent hello, jest automatycznie instalowany dostawcy dla Apache HTTP Server monitorowania wydajności.</span><span class="sxs-lookup"><span data-stu-id="33dfe-304">If Apache HTTP Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="33dfe-305">Ten dostawca zależy od Apache "module", który musi zostać załadowane do hello Apache HTTP Server w kolejności tooaccess danych dotyczących wydajności.</span><span class="sxs-lookup"><span data-stu-id="33dfe-305">This provider relies on an Apache "module" that must be loaded into hello Apache HTTP Server in order tooaccess performance data.</span></span>

<span data-ttu-id="33dfe-306">Można załadować modułu hello z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="33dfe-306">You can load hello module with hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="33dfe-307">toounload hello Apache modułu monitorowania, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="33dfe-307">toounload hello Apache monitoring module, run hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a><span data-ttu-id="33dfe-308">tooview danych wydajności przy użyciu analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="33dfe-308">tooview performance data with Log Analytics</span></span>
1. <span data-ttu-id="33dfe-309">W portalu usługi Operations Management Suite powitania kliknij hello wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="33dfe-309">In hello Operations Management Suite portal, click hello Log Search tile.</span></span>
2. <span data-ttu-id="33dfe-310">Na pasku wyszukiwania hello, wpisz `* (Type=Perf)` tooview wszystkie liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="33dfe-310">In hello search bar, type `* (Type=Perf)` tooview all performance counters.</span></span>

<span data-ttu-id="33dfe-311">Ponieważ OMS również zbieranie danych licznika wydajności systemu Windows, użytkownik powinien zakresu rozwijanej hello dane specyficzne dla tooLinux wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="33dfe-311">Because OMS also collects Windows performance counter data, you should scope-down hello search tooLinux-specific data.</span></span> <span data-ttu-id="33dfe-312">Hello poniższy przykład czy Pokaż wydajności danych określonego tooan przykład Linux server o nazwie Chorizo21.</span><span class="sxs-lookup"><span data-stu-id="33dfe-312">So, hello following example would show performance data specific tooan example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![przykład serwera wyświetlane w wynikach wyszukiwania](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="33dfe-314">W wynikach powitania kliknij **metryki** tooview hello liczniki, które zebrano dane.</span><span class="sxs-lookup"><span data-stu-id="33dfe-314">In hello results, you can click **Metrics** tooview hello counters that data was collected for.</span></span> <span data-ttu-id="33dfe-315">Dane w czasie rzeczywistym jest wyświetlany na wykresach dla każdego licznika.</span><span class="sxs-lookup"><span data-stu-id="33dfe-315">Real-time data is shown as graphs for each counter.</span></span>

![metrics](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="33dfe-317">Dziennik systemu</span><span class="sxs-lookup"><span data-stu-id="33dfe-317">Syslog</span></span>
<span data-ttu-id="33dfe-318">SYSLOG jest zdarzeniem rejestrowania protokołu podobne tooWindows dzienniki zdarzeń — zarówno działają podobnie, podczas wyświetlania w OMS.</span><span class="sxs-lookup"><span data-stu-id="33dfe-318">Syslog is an event logging protocol similar tooWindows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="33dfe-319">tooadd nowego zakładu dziennika systemu Linux w OMS</span><span class="sxs-lookup"><span data-stu-id="33dfe-319">tooadd a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="33dfe-320">Na powitania **ustawienia** w obszarze **danych** , kliknij przycisk **Syslog** a następnie toohello lewej hello i ikony, wpisz nazwę hello hello instrumentu syslog, które mają tooadd.</span><span class="sxs-lookup"><span data-stu-id="33dfe-320">On hello **Settings** page under **Data** , click **Syslog** and then toohello left of hello plus icon, type hello name of hello syslog facility that you want tooadd.</span></span>
    <span data-ttu-id="33dfe-321">![Systemu Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="33dfe-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="33dfe-322">Jeśli nie znasz hello Pełna nazwa instrumentu hello, możesz wpisać nazwę częściowe i zostanie wyświetlona lista dostępnych syslog urządzeń.</span><span class="sxs-lookup"><span data-stu-id="33dfe-322">If you don’t know hello full name of hello facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="33dfe-323">Do wyszukania hello syslog zakładzie mają tooadd, kliknij nazwę hello liście hello a następnie kliknij przycisk hello plus hello tooadd ikona funkcję dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="33dfe-323">When you find hello syslog facility that you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello syslog facility.</span></span>
3. <span data-ttu-id="33dfe-324">Po dodaniu zakładzie hello wydaje się liście hello wyróżnione z paskiem kolorowe.</span><span class="sxs-lookup"><span data-stu-id="33dfe-324">After you add hello facility, it appears in hello list of highlighted with a colored bar.</span></span> <span data-ttu-id="33dfe-325">Następnie wybierz wag hello (kategorie informacji zakładzie syslog), które mają toocollect.</span><span class="sxs-lookup"><span data-stu-id="33dfe-325">Next, choose hello severities (categories of syslog facility information) that you want toocollect.</span></span>
4. <span data-ttu-id="33dfe-326">U dołu strony hello powitania kliknij **zapisać** toofinalize zmiany.</span><span class="sxs-lookup"><span data-stu-id="33dfe-326">At hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="33dfe-327">Hello zmian konfiguracji, które zostały wprowadzone są następnie wysyłane hello tooall OMS agentów dla systemu Linux, które są zarejestrowane w usłudze OMS, zazwyczaj w ciągu 5 minut.</span><span class="sxs-lookup"><span data-stu-id="33dfe-327">hello configuration changes that you’ve made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="33dfe-328">Konfigurowanie urządzeń dziennika systemu Linux w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-328">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="33dfe-329">Zdarzenia dziennika systemowego są wysyłane z hello demon syslog, na przykład rsyslog lub syslog ng, portów lokalnych tooa hello agent nasłuchuje.</span><span class="sxs-lookup"><span data-stu-id="33dfe-329">Syslog events are sent from hello syslog daemon, for example rsyslog or syslog-ng, tooa local port that hello agent is listening on.</span></span> <span data-ttu-id="33dfe-330">Domyślnie port 25224.</span><span class="sxs-lookup"><span data-stu-id="33dfe-330">By default, port 25224.</span></span> <span data-ttu-id="33dfe-331">Po zainstalowaniu agenta hello domyślnej konfiguracji programu syslog jest stosowany.</span><span class="sxs-lookup"><span data-stu-id="33dfe-331">When hello agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="33dfe-332">Znaleziono w lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="33dfe-332">This is found at:</span></span>

<span data-ttu-id="33dfe-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="33dfe-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="33dfe-334">SYSLOG ng: /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="33dfe-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="33dfe-335">Konfiguracja syslog agenta pakietu OMS domyślne Hello przekazuje zdarzenia dziennika systemowego z wszystkich urządzeń z ważnością, ostrzeżenie lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="33dfe-335">hello default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="33dfe-336">Edytuj hello syslog konfiguracji, należy ponownie uruchomić demon syslog hello hello zmiany tootake efektu.</span><span class="sxs-lookup"><span data-stu-id="33dfe-336">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

<span data-ttu-id="33dfe-337">Witaj syslog konfigurację domyślną dla hello Agent pakietu OMS dla systemu Linux dla OMS jest:</span><span class="sxs-lookup"><span data-stu-id="33dfe-337">hello default syslog configuration for hello OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="33dfe-338">rsyslog</span><span class="sxs-lookup"><span data-stu-id="33dfe-338">Rsyslog</span></span>
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

#### <a name="syslog-ng"></a><span data-ttu-id="33dfe-339">SYSLOG ng</span><span class="sxs-lookup"><span data-stu-id="33dfe-339">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a><span data-ttu-id="33dfe-340">tooview wszystkie zdarzenia dziennika systemowego z analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="33dfe-340">tooview all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="33dfe-341">W portalu usługi Operations Management Suite powitania kliknij hello **wyszukiwania dziennika** kafelka.</span><span class="sxs-lookup"><span data-stu-id="33dfe-341">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="33dfe-342">W hello **zarządzanie dziennikiem** grupowania, wybierz wyszukiwania wstępnie zdefiniowanych syslog, a następnie wybierz jeden toorun go.</span><span class="sxs-lookup"><span data-stu-id="33dfe-342">In hello **Log Management** grouping, choose a predefined syslog search and then select one toorun it.</span></span>

<span data-ttu-id="33dfe-343">Ten przykład przedstawia wszystkie zdarzenia dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="33dfe-343">This example shows all Syslog events.</span></span>

![Zdarzenia dziennika systemowego pokazano wyszukiwania dziennika](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="33dfe-345">Teraz możesz przejść do szczegółów wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="33dfe-345">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="33dfe-346">Alerty systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-346">Linux alerts</span></span>
<span data-ttu-id="33dfe-347">Jeśli używasz Nagios lub Zabbix toomanage Twojego maszyny z systemem Linux, a następnie OMS może odbierać hello alerty generowane przez te narzędzia.</span><span class="sxs-lookup"><span data-stu-id="33dfe-347">If you use Nagios or Zabbix toomanage your Linux machines, then OMS can receive hello alerts generated from those tools.</span></span> <span data-ttu-id="33dfe-348">Ponieważ nie ma obecnie nie metody tooconfigure przychodzących alertów danych przy użyciu portalu OMS hello.</span><span class="sxs-lookup"><span data-stu-id="33dfe-348">However, there is currently no method tooconfigure incoming alert data using hello OMS portal.</span></span> <span data-ttu-id="33dfe-349">Zamiast tego należy tooedit wysyłania tooOMS alerty konfiguracji pliku toostart.</span><span class="sxs-lookup"><span data-stu-id="33dfe-349">Instead, you will need tooedit a config file toostart sending alerts tooOMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="33dfe-350">Zbieraj alerty z Nagios</span><span class="sxs-lookup"><span data-stu-id="33dfe-350">Collect alerts from Nagios</span></span>
<span data-ttu-id="33dfe-351">toocollect alertów z serwera Nagios, należy hello toomake następujące zmiany w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="33dfe-351">toocollect alerts from a Nagios server, you need toomake hello following configuration changes.</span></span>

1. <span data-ttu-id="33dfe-352">Udziel hello użytkownika **omsagent** dostęp do odczytu pliku dziennika Nagios toohello (tj. /var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="33dfe-352">Grant hello user **omsagent** read access toohello Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="33dfe-353">Zakładając, że plik nagios.log hello jest własnością grupy hello **nagios** , można dodać użytkownika hello **omsagent** toohello **nagios** grupy.</span><span class="sxs-lookup"><span data-stu-id="33dfe-353">Assuming hello nagios.log file is owned by hello group **nagios** , you can add hello user **omsagent** toohello **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="33dfe-354">Modyfikowanie pliku omsagent.confconfiguration hello (/ etc/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="33dfe-354">Modify hello omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="33dfe-355">Upewnij się, że hello następujące wpisy są obecne i nie komentarze wychodzących:</span><span class="sxs-lookup"><span data-stu-id="33dfe-355">Ensure hello following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="33dfe-356">Uruchom ponownie demon omsagent hello:</span><span class="sxs-lookup"><span data-stu-id="33dfe-356">Restart hello omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="33dfe-357">Zbieraj alerty z Zabbix</span><span class="sxs-lookup"><span data-stu-id="33dfe-357">Collect alerts from Zabbix</span></span>
<span data-ttu-id="33dfe-358">toocollect alertów z serwera Zabbix będziesz wykonywać podobne kroki toothose dla Nagios powyżej, z wyjątkiem potrzebujesz toospecify użytkownika i hasło w *zwykły tekst*.</span><span class="sxs-lookup"><span data-stu-id="33dfe-358">toocollect alerts from a Zabbix server, you'll perform similar steps toothose for Nagios above, except you'll need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="33dfe-359">To nie jest idealnym rozwiązaniem, ale prawdopodobnie zmienią się wkrótce.</span><span class="sxs-lookup"><span data-stu-id="33dfe-359">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="33dfe-360">tooaddress ten problem, zaleca się tworzenie hello użytkownika, a następnie przyznać jej tylko toomonitor uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="33dfe-360">tooaddress this issue, we recommend that you create hello user and grant it permission toomonitor only.</span></span>

<span data-ttu-id="33dfe-361">Przykład sekcji pliku konfiguracji omsagent.conf hello (/ etc/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/conf/omsagent.conf) dla Zabbix powinno przypominać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="33dfe-361">An example section of hello omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble hello following:</span></span>

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

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="33dfe-362">Wyświetlanie alertów w wyszukiwaniu analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="33dfe-362">View alerts in Log Analytics search</span></span>
<span data-ttu-id="33dfe-363">Po skonfigurowaniu tooOMS alerty z systemem Linux komputerów toosend kilka prostych dziennika wyszukiwania zapytania tooview hello alerty mogą być używane.</span><span class="sxs-lookup"><span data-stu-id="33dfe-363">After you've configured your Linux computers toosend alerts tooOMS, you can use a few simple log search queries tooview hello alerts.</span></span> <span data-ttu-id="33dfe-364">Witaj następującego zapytania wyszukiwania zwraca wszystkie alerty hello zarejestrowane, które zostały wygenerowane.</span><span class="sxs-lookup"><span data-stu-id="33dfe-364">hello following search query example returns all hello recorded alerts that were generated.</span></span> <span data-ttu-id="33dfe-365">Na przykład czy jakieś problem występuje w infrastrukturze IT, następnie w wyniku hello poniższy przykład zapytania może wskazywać, gdzie może pochodzić hello problem.</span><span class="sxs-lookup"><span data-stu-id="33dfe-365">For example, if some sort of problem occurs in your IT infrastructure, then results for hello following example query might indicate where hello problem might originate.</span></span> <span data-ttu-id="33dfe-366">I mogą łatwo przechodzenia w alertach toohello przez źródło systemu toohelp wąskie badaniu.</span><span class="sxs-lookup"><span data-stu-id="33dfe-366">And, you can easily drill in toohello alerts by source system toohelp narrow your investigation.</span></span> <span data-ttu-id="33dfe-367">Witaj korzyścią jest nie musi mieć systemy zarządzania toovarious toogo od początku hello — pod warunkiem, że alerty są wysyłane tooOMS, można uruchomić istnieje.</span><span class="sxs-lookup"><span data-stu-id="33dfe-367">hello benefit is that you don't necessarily have toogo toovarious management systems from hello start—provided that your alerts are sent tooOMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="33dfe-368">tooview Nagios wszystkie alerty z analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="33dfe-368">tooview all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="33dfe-369">W portalu usługi Operations Management Suite powitania kliknij hello **wyszukiwania dziennika** kafelka.</span><span class="sxs-lookup"><span data-stu-id="33dfe-369">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="33dfe-370">Na pasku zapytania hello wpisz hello następującego zapytania wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="33dfe-370">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Nagios alertów przedstawianych w dzienniku wyszukiwania](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="33dfe-372">Po hello wyniki wyszukiwania, możesz przejść do szczegółów dodatkowych szczegółów takich jak *stan alertu*.</span><span class="sxs-lookup"><span data-stu-id="33dfe-372">After you see hello search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="33dfe-373">tooview wszystkie alerty Zabbix z analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="33dfe-373">tooview all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="33dfe-374">W portalu usługi Operations Management Suite powitania kliknij hello **wyszukiwania dziennika** kafelka.</span><span class="sxs-lookup"><span data-stu-id="33dfe-374">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="33dfe-375">Na pasku zapytania hello wpisz hello następującego zapytania wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="33dfe-375">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Zabbix alertów przedstawianych w dzienniku wyszukiwania](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="33dfe-377">Po hello wyniki wyszukiwania, możesz przejść do szczegółów dodatkowych szczegółów takich jak *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="33dfe-377">After you see hello search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="33dfe-378">Zgodność z programem System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="33dfe-378">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="33dfe-379">Witaj Agent pakietu OMS dla systemu Linux udostępnia pliki binarne agenta hello agenta programu System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="33dfe-379">hello OMS Agent for Linux shares agent binaries with hello System Center Operations Manager agent.</span></span> <span data-ttu-id="33dfe-380">Instalowanie hello Agent pakietu OMS dla systemu Linux w systemie, w obecnie zarządzany przez program Operations Manager uaktualnień hello OMI i SCX pakietów na komputerze hello tooa nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="33dfe-380">Installing hello OMS Agent for Linux on a system currently managed by Operations Manager upgrades hello OMI and SCX packages on hello computer tooa newer version.</span></span> <span data-ttu-id="33dfe-381">Witaj Agent pakietu OMS dla systemów Linux i System Center 2012 R2 są zgodne.</span><span class="sxs-lookup"><span data-stu-id="33dfe-381">hello OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="33dfe-382">Jednak **System Center 2012 SP1 i wcześniejsze wersje nie są obecnie zgodne lub nie jest obsługiwany z hello Agent pakietu OMS dla systemu Linux.**</span><span class="sxs-lookup"><span data-stu-id="33dfe-382">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with hello OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="33dfe-383">Jeśli hello Agent pakietu OMS dla systemu Linux jest zainstalowana tooa komputera, który nie jest obecnie zarządzany przez program Operations Manager, a później mają toomanage hello komputera z programem Operations Manager, należy zmodyfikować konfigurację OMI hello przed odnajdowania hello komputera.</span><span class="sxs-lookup"><span data-stu-id="33dfe-383">If hello OMS Agent for Linux is installed tooa computer that is not currently managed by Operations Manager, and you later want toomanage hello computer with Operations Manager, you must modify hello OMI configuration before you discover hello computer.</span></span> <span data-ttu-id="33dfe-384">**Ten krok jest zbędny, jeśli hello agenta programu Operations Manager została zainstalowana przed hello Agent pakietu OMS dla systemu Linux.**</span><span class="sxs-lookup"><span data-stu-id="33dfe-384">**This step is not needed if hello Operations Manager agent is installed before hello OMS Agent for Linux.**</span></span>
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a><span data-ttu-id="33dfe-385">Witaj tooenable Agent pakietu OMS dla systemu Linux toocommunicate z programem Operations Manager</span><span class="sxs-lookup"><span data-stu-id="33dfe-385">tooenable hello OMS Agent for Linux toocommunicate with Operations Manager</span></span>
1. <span data-ttu-id="33dfe-386">Edytuj hello /etc/opt/omi/conf/omiserver.conf pliku</span><span class="sxs-lookup"><span data-stu-id="33dfe-386">Edit hello file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="33dfe-387">Upewnij się, że powitania od wiersza z **httpsport =** definiuje hello portu 1270.</span><span class="sxs-lookup"><span data-stu-id="33dfe-387">Ensure that hello line beginning with **httpsport=** defines hello port 1270.</span></span> <span data-ttu-id="33dfe-388">Takie jak`httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="33dfe-388">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="33dfe-389">Uruchom ponownie serwer OMI hello:</span><span class="sxs-lookup"><span data-stu-id="33dfe-389">Restart hello OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="33dfe-390">Uprawnienia bazy danych wymagane dla liczników wydajności MySQL</span><span class="sxs-lookup"><span data-stu-id="33dfe-390">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="33dfe-391">toogrant uprawnienia tooa MySQL monitorowania użytkownika, użytkownik udzielającym hello musi mieć uprawnienie "GRANT option" hello, jak również udzielenia uprawnienia hello.</span><span class="sxs-lookup"><span data-stu-id="33dfe-391">toogrant permissions tooa MySQL monitoring user, hello granting user must have hello 'GRANT option' privilege as well as hello privilege being granted.</span></span>

<span data-ttu-id="33dfe-392">Aby hello użytkownika MySQL tooreturn wydajności danych hello użytkownika będą muszą uzyskiwać dostęp do toohello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="33dfe-392">In order for hello MySQL User tooreturn performance data hello user will need access toohello following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="33dfe-393">Ponadto toothese zapytania hello MySQL użytkownika wymagane są następujące domyślne tabele toohello dostępu wybierz OPCJĘ:</span><span class="sxs-lookup"><span data-stu-id="33dfe-393">In addition toothese queries hello MySQL user requires SELECT access toohello following default tables:</span></span>

* <span data-ttu-id="33dfe-394">INFORMATION_SCHEMA</span><span class="sxs-lookup"><span data-stu-id="33dfe-394">information_schema</span></span>
* <span data-ttu-id="33dfe-395">MySQL</span><span class="sxs-lookup"><span data-stu-id="33dfe-395">mysql</span></span>

<span data-ttu-id="33dfe-396">Te uprawnienia można otrzymać, uruchamiając następujące polecenia grant hello.</span><span class="sxs-lookup"><span data-stu-id="33dfe-396">These privileges can be granted by running hello following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a><span data-ttu-id="33dfe-397">Zarządzanie monitorowania poświadczenia w pliku uwierzytelniania hello MySQL</span><span class="sxs-lookup"><span data-stu-id="33dfe-397">Manage MySQL monitoring credentials in hello authentication file</span></span>
<span data-ttu-id="33dfe-398">Hello następujące sekcje ułatwiają zarządzanie poświadczeniami MySQL.</span><span class="sxs-lookup"><span data-stu-id="33dfe-398">hello following sections help you manage MySQL credentials.</span></span>

### <a name="configure-hello-mysql-omi-provider"></a><span data-ttu-id="33dfe-399">Skonfiguruj hello dostawcy MySQL OMI</span><span class="sxs-lookup"><span data-stu-id="33dfe-399">Configure hello MySQL OMI provider</span></span>
<span data-ttu-id="33dfe-400">Hello MySQL OMI dostawcy wymaga, aby użytkownik MySQL wstępnie skonfigurowane i zainstalowane w kolejności tooquery hello kondycji wydajności informacji z wystąpienia MySQL hello bibliotek klienta MySQL.</span><span class="sxs-lookup"><span data-stu-id="33dfe-400">hello MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order tooquery hello performance/health information from hello MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="33dfe-401">Plik authentication MySQL OMI</span><span class="sxs-lookup"><span data-stu-id="33dfe-401">MySQL OMI authentication file</span></span>
<span data-ttu-id="33dfe-402">Dostawca MySQL OMI używa toodetermine plik uwierzytelniania, jakiego bind adres i port wystąpienia MySQL hello nasłuchuje na i jakie poświadczenia toouse toogather metryki.</span><span class="sxs-lookup"><span data-stu-id="33dfe-402">MySQL OMI provider uses an authentication file toodetermine what bind-address and port hello MySQL instance is listening on and what credentials toouse toogather metrics.</span></span> <span data-ttu-id="33dfe-403">Podczas instalacji hello MySQL OMI dostawcy rozpocznie skanowanie plików konfiguracyjnych my.cnf MySQL (lokalizacje domyślne) bind adres i port i częściowo hello zestaw plików uwierzytelniania MySQL OMI.</span><span class="sxs-lookup"><span data-stu-id="33dfe-403">During installation hello MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set hello MySQL OMI authentication file.</span></span>

<span data-ttu-id="33dfe-404">toocomplete monitorowanie wystąpienia serwera MySQL, dodać wstępnie wygenerowany plik authentication MySQL OMI w poprawnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="33dfe-404">toocomplete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into hello correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="33dfe-405">Format pliku uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="33dfe-405">Authentication file format</span></span>
<span data-ttu-id="33dfe-406">Hello plik authentication MySQL OMI jest plik tekstowy, który zawiera informacje o:</span><span class="sxs-lookup"><span data-stu-id="33dfe-406">hello MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="33dfe-407">Port</span><span class="sxs-lookup"><span data-stu-id="33dfe-407">Port</span></span>
* <span data-ttu-id="33dfe-408">Adres BIND</span><span class="sxs-lookup"><span data-stu-id="33dfe-408">Bind-Address</span></span>
* <span data-ttu-id="33dfe-409">Nazwa_użytkownika MySQL</span><span class="sxs-lookup"><span data-stu-id="33dfe-409">MySQL username</span></span>
* <span data-ttu-id="33dfe-410">Kodowanie Base64 hasła</span><span class="sxs-lookup"><span data-stu-id="33dfe-410">Base64 encoded password</span></span>

<span data-ttu-id="33dfe-411">Hello plik authentication MySQL OMI tylko przyznaje uprawnienia do odczytu/zapisu toohello Linux użytkownika, która go wygenerowała.</span><span class="sxs-lookup"><span data-stu-id="33dfe-411">hello MySQL OMI authentication file only grants privileges for read/write toohello Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="33dfe-412">Domyślny plik authentication MySQL OMI zawiera domyślne wystąpienie i numer portu, w zależności od tego, jakie informacje są dostępne i przeanalizowany z hello znaleziono plik konfiguracji MySQL.</span><span class="sxs-lookup"><span data-stu-id="33dfe-412">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from hello found MySQL configuration file.</span></span>

<span data-ttu-id="33dfe-413">Hello domyślnego wystąpienia jest toomake oznacza wiele wystąpień MySQL na jednym hoście Linux łatwiejsze zarządzanie i jest oznaczona przez wystąpienie hello z portem 0.</span><span class="sxs-lookup"><span data-stu-id="33dfe-413">hello default instance is a means toomake managing multiple MySQL instances on one Linux host easier, and is denoted by hello instance with port 0.</span></span> <span data-ttu-id="33dfe-414">Wszystkie wystąpienia dodano będzie dziedziczyć właściwości z wystąpienia domyślnego hello.</span><span class="sxs-lookup"><span data-stu-id="33dfe-414">All added instances will inherit properties set from hello default instance.</span></span> <span data-ttu-id="33dfe-415">Na przykład jeśli wystąpienie MySQL nasłuchiwanie na porcie "3308" zostanie dodany, powiązanego adresu hello domyślnego wystąpienia, username i password kodowany w standardzie Base64 będzie można tootry używane i monitorowanie wystąpienia hello nasłuchiwanie 3308.</span><span class="sxs-lookup"><span data-stu-id="33dfe-415">For example, if MySQL instance listening on port '3308' is added, hello default instance's bind-address, username, and Base64 encoded password will be used tootry and monitor hello instance listening on 3308.</span></span> <span data-ttu-id="33dfe-416">Jeśli wystąpienie hello na 3308 jest tooanother powiązany adres i używa hello tego samego nazwa_użytkownika MySQL i para hasło tylko hello respecification hello bind adres jest niezbędny i hello inne właściwości dziedziczone.</span><span class="sxs-lookup"><span data-stu-id="33dfe-416">If hello instance on 3308 is binded tooanother address and uses hello same MySQL username and password pair only hello respecification of hello bind-address is needed and hello other properties will be inherited.</span></span>

<span data-ttu-id="33dfe-417">Przykłady plik authentication hello przypominać następujące hello.</span><span class="sxs-lookup"><span data-stu-id="33dfe-417">Examples of hello authentication file resemble hello following.</span></span>

<span data-ttu-id="33dfe-418">Domyślne wystąpienie i wystąpienia z portem 3308:</span><span class="sxs-lookup"><span data-stu-id="33dfe-418">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="33dfe-419">Domyślne wystąpienie i wystąpienia z portu 3308 + różnych Base 64 zakodowane hasło:</span><span class="sxs-lookup"><span data-stu-id="33dfe-419">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="33dfe-420">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="33dfe-420">**Property**</span></span> | <span data-ttu-id="33dfe-421">**Opis**</span><span class="sxs-lookup"><span data-stu-id="33dfe-421">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="33dfe-422">Port</span><span class="sxs-lookup"><span data-stu-id="33dfe-422">Port</span></span> |<span data-ttu-id="33dfe-423">Port reprezentuje hello bieżącego portu hello MySQL nasłuchuje wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="33dfe-423">Port represents hello current port hello MySQL instance is listening on.</span></span>  <span data-ttu-id="33dfe-424">Hello port 0 oznacza, że następujące właściwości hello są używane dla domyślnego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="33dfe-424">hello port 0 implies that hello properties following are used for default instance.</span></span> |
| <span data-ttu-id="33dfe-425">Adres BIND</span><span class="sxs-lookup"><span data-stu-id="33dfe-425">Bind-Address</span></span> |<span data-ttu-id="33dfe-426">Hello powiązać adres jest hello bieżący MySQL bind — adres</span><span class="sxs-lookup"><span data-stu-id="33dfe-426">hello Bind Address is hello current MySQL bind-address</span></span> |
| <span data-ttu-id="33dfe-427">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="33dfe-427">username</span></span> |<span data-ttu-id="33dfe-428">Tej nazwy użytkownika hello hello MySQL użytkownika mają wystąpienie serwera toouse toomonitor hello MySQL.</span><span class="sxs-lookup"><span data-stu-id="33dfe-428">This hello username of hello MySQL user you wish toouse toomonitor hello MySQL server instance.</span></span> |
| <span data-ttu-id="33dfe-429">Hasło kodowane w formacie Base64</span><span class="sxs-lookup"><span data-stu-id="33dfe-429">Base64 encoded Password</span></span> |<span data-ttu-id="33dfe-430">Jest to hasło hello hello MySQL monitorowania użytkownika zakodowane w formacie Base64.</span><span class="sxs-lookup"><span data-stu-id="33dfe-430">This is hello password of hello MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="33dfe-431">Aktualizacje automatyczne</span><span class="sxs-lookup"><span data-stu-id="33dfe-431">AutoUpdate</span></span> |<span data-ttu-id="33dfe-432">Po uaktualnieniu hello MySQL OMI dostawcy dostawcy hello Skanuj ponownie zmiany w pliku my.cnf hello i Zastąp plik MySQL OMI Authentication hello.</span><span class="sxs-lookup"><span data-stu-id="33dfe-432">When hello MySQL OMI Provider is upgraded hello provider will rescan for changes in hello my.cnf file and overwrite hello MySQL OMI Authentication file.</span></span> <span data-ttu-id="33dfe-433">Tej flagi tootrue lub FAŁSZ w zależności od toohello wymagane aktualizacje MySQL OMI uwierzytelniania pliku zestawu.</span><span class="sxs-lookup"><span data-stu-id="33dfe-433">Set this flag tootrue or false depending on required updates toohello MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="33dfe-434">Lokalizacja pliku uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="33dfe-434">Authentication file location</span></span>
<span data-ttu-id="33dfe-435">Witaj MySQL OMI uwierzytelniania plików powinny być znajduje się w następującej lokalizacji hello i o nazwie "mysql uwierzytelniania":</span><span class="sxs-lookup"><span data-stu-id="33dfe-435">hello MySQL OMI Authentication File should be located in hello following location and named "mysql-auth":</span></span>

<span data-ttu-id="33dfe-436">/var/OPT/Microsoft/MySQL-cimprov/auth/omsagent/MySQL-auth</span><span class="sxs-lookup"><span data-stu-id="33dfe-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="33dfe-437">Plik Hello (i katalog auth/omsagent) powinna być własnością hello omsagent użytkownika.</span><span class="sxs-lookup"><span data-stu-id="33dfe-437">hello file (and auth/omsagent directory) should be owned by hello omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="33dfe-438">Dzienniki agentów</span><span class="sxs-lookup"><span data-stu-id="33dfe-438">Agent logs</span></span>
<span data-ttu-id="33dfe-439">Dzienniki Hello hello Agent pakietu OMS dla systemu Linux jest na:</span><span class="sxs-lookup"><span data-stu-id="33dfe-439">hello logs for hello OMS Agent for Linux is at:</span></span>

<span data-ttu-id="33dfe-440">/ var/opt/microsoft/omsagent/&lt;identyfikator obszaru roboczego&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="33dfe-440">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="33dfe-441">Dzienniki Hello hello wynosi Agent pakietu OMS dla systemu Linux dla programu omsconfig (konfiguracja agenta):</span><span class="sxs-lookup"><span data-stu-id="33dfe-441">hello logs for hello OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="33dfe-442">/ var/opt/microsoft/omsconfig/log /</span><span class="sxs-lookup"><span data-stu-id="33dfe-442">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="33dfe-443">Dzienniki dla składników OMI i SCX hello (udostępniających dane metryk wydajności) znajduje się na:</span><span class="sxs-lookup"><span data-stu-id="33dfe-443">Logs for hello OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="33dfe-444">/ var/opt/omi/log/i /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="33dfe-444">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-hello-oms-agent-for-linux"></a><span data-ttu-id="33dfe-445">Rozwiązywanie problemów z hello Agent pakietu OMS dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-445">Troubleshooting hello OMS Agent for Linux</span></span>
<span data-ttu-id="33dfe-446">Użyj powitania po toodiagnose informacji i rozwiązywania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="33dfe-446">Use hello following information toodiagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="33dfe-447">Jeśli żaden z hello Rozwiązywanie problemów z informacjami w tej sekcji pomaga, umożliwia także hello następujące zasoby toohelp rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="33dfe-447">If none of hello troubleshooting information in this section helps you, you can also use hello following resources toohelp resolve your problem.</span></span>

* <span data-ttu-id="33dfe-448">Klienci z Premier pomocy technicznej można rejestrować sprawy pomocy technicznej za pośrednictwem [Premier](https://premier.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="33dfe-448">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="33dfe-449">Klienci z umowami pomocy technicznej platformy Azure może rejestrować przypadków pomocy technicznej w hello [portalu Azure](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="33dfe-449">Customers with Azure support agreements can log support cases in hello [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="33dfe-450">Plik [problem GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span><span class="sxs-lookup"><span data-stu-id="33dfe-450">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="33dfe-451">Forum opinii pomysły i toocreate raport o usterce [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="33dfe-451">Feedback forum for ideas and toocreate a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="33dfe-452">Lokalizacje ważne dziennika</span><span class="sxs-lookup"><span data-stu-id="33dfe-452">Important log locations</span></span>
| <span data-ttu-id="33dfe-453">Plik</span><span class="sxs-lookup"><span data-stu-id="33dfe-453">File</span></span> | <span data-ttu-id="33dfe-454">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="33dfe-454">Path</span></span> |
| --- | --- |
| <span data-ttu-id="33dfe-455">Agent pakietu OMS dla pliku dziennika systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-455">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="33dfe-456">Plik dziennika konfiguracji agenta pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="33dfe-456">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="33dfe-457">Pliki konfiguracji ważne</span><span class="sxs-lookup"><span data-stu-id="33dfe-457">Important configuration files</span></span>
| <span data-ttu-id="33dfe-458">Catergory</span><span class="sxs-lookup"><span data-stu-id="33dfe-458">Catergory</span></span> | <span data-ttu-id="33dfe-459">Lokalizacja pliku</span><span class="sxs-lookup"><span data-stu-id="33dfe-459">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="33dfe-460">Dziennik systemu</span><span class="sxs-lookup"><span data-stu-id="33dfe-460">Syslog</span></span> |<span data-ttu-id="33dfe-461">`/etc/syslog-ng/syslog-ng.conf`lub `/etc/rsyslog.conf` lub`/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="33dfe-461">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="33dfe-462">Wydajność, Nagios, Zabbix, OMS wyjściowego i agenta ogólne</span><span class="sxs-lookup"><span data-stu-id="33dfe-462">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="33dfe-463">Dodatkowe konfiguracje</span><span class="sxs-lookup"><span data-stu-id="33dfe-463">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="33dfe-464">Edycji plików konfiguracyjnych dla liczników wydajności i syslog zostaną zastąpione, jeśli jest włączona konfiguracja portalu OMS.</span><span class="sxs-lookup"><span data-stu-id="33dfe-464">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="33dfe-465">Możesz wyłączyć konfigurację w hello portalu OMS (dla wszystkich węzłów) lub pojedynczych węzłów, uruchamiając następujące hello:</span><span class="sxs-lookup"><span data-stu-id="33dfe-465">You can disable configuration in hello OMS Portal (for all nodes) or for single nodes by running hello following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="33dfe-466">Włączenie rejestrowania debugowania</span><span class="sxs-lookup"><span data-stu-id="33dfe-466">Enable debug logging</span></span>
<span data-ttu-id="33dfe-467">debugowania tooenable rejestrowania, można użyć hello OMS dane wyjściowe wtyczki i pełne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="33dfe-467">tooenable debug logging, you can use hello OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="33dfe-468">Dodatek dane wyjściowe OMS</span><span class="sxs-lookup"><span data-stu-id="33dfe-468">OMS output plugin</span></span>
<span data-ttu-id="33dfe-469">FluentD umożliwia toospecify wtyczki hello poziomów rejestrowania dla dziennika różne poziomy wejścia i wyjścia.</span><span class="sxs-lookup"><span data-stu-id="33dfe-469">FluentD allows hello plugin toospecify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="33dfe-470">toospecify poziomu inny dziennik OMS danych wyjściowych, zmień konfigurację agenta ogólne hello w hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` pliku.</span><span class="sxs-lookup"><span data-stu-id="33dfe-470">toospecify a different log level for OMS output, edit hello general agent configuration in hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="33dfe-471">Dolnej hello pliku konfiguracyjnego hello zmienić hello `log_level` właściwość z `info` zbyt`debug`.</span><span class="sxs-lookup"><span data-stu-id="33dfe-471">Near hello bottom of hello configuration file, change hello `log_level` property from `info` too`debug`.</span></span>

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

<span data-ttu-id="33dfe-472">Rejestrowanie debugowania umożliwia usługę oddzielone typ, liczba elementów danych, a czas trwania toosend toohello przekazywania toosee umieścić w zadaniu wsadowym.</span><span class="sxs-lookup"><span data-stu-id="33dfe-472">Debug logging allows you toosee batched uploads toohello OMS Service separated by type, number of data items, and time taken toosend.</span></span>

<span data-ttu-id="33dfe-473">*Przykładowy dziennik debugowania włączone:*</span><span class="sxs-lookup"><span data-stu-id="33dfe-473">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="33dfe-474">Pełne dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="33dfe-474">Verbose output</span></span>
<span data-ttu-id="33dfe-475">Zamiast używać hello OMS dane wyjściowe wtyczki, można również wyprowadzać elementów danych bezpośrednio za`stdout`, która jest widoczna w hello Agent pakietu OMS dla pliku dziennika systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="33dfe-475">Instead of using hello OMS output plugin, you can also output data items directly too`stdout`, which is visible in hello OMS Agent for Linux log file.</span></span>

<span data-ttu-id="33dfe-476">W pliku konfiguracyjnym ogólne agent pakietu OMS hello na `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, komentarz hello OMS output wtyczki, dodając `#` przed każdym wierszu.</span><span class="sxs-lookup"><span data-stu-id="33dfe-476">In hello OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out hello OMS output plugin by adding a `#` in front of each line.</span></span>

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

<span data-ttu-id="33dfe-477">Poniżej hello wtyczki dane wyjściowe, Usuń komentarz hello w następujących sekcji, usuwając hello hello `#` symbol hello początku każdego wiersza.</span><span class="sxs-lookup"><span data-stu-id="33dfe-477">Below hello output plugin, remove hello comment in hello following section by removing hello `#` symbol at hello beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a><span data-ttu-id="33dfe-478">Przekazany dalej komunikaty dziennika systemowego nie są wyświetlane w dzienniku hello</span><span class="sxs-lookup"><span data-stu-id="33dfe-478">Forwarded Syslog messages do not appear in hello log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="33dfe-479">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="33dfe-479">Probable causes</span></span>
* <span data-ttu-id="33dfe-480">Hello zastosowano konfigurację toohello Linux serwera nie zezwolić na zbieranie hello wysyłane urządzeń i/lub poziomy dziennika</span><span class="sxs-lookup"><span data-stu-id="33dfe-480">hello configuration applied toohello Linux server does not allow collection of hello sent facilities and/or log levels</span></span>
* <span data-ttu-id="33dfe-481">SYSLOG nie są przekazywane poprawnie toohello Linux serwera</span><span class="sxs-lookup"><span data-stu-id="33dfe-481">Syslog is not being forwarded correctly toohello Linux server</span></span>
* <span data-ttu-id="33dfe-482">Witaj liczbę komunikatów przekazywanych na sekundę są za szerokie dla konfiguracji podstawowej hello hello Agent pakietu OMS dla systemu Linux toohandle</span><span class="sxs-lookup"><span data-stu-id="33dfe-482">hello number of messages being forwarded per second are too large for hello base configuration of hello OMS Agent for Linux toohandle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="33dfe-483">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="33dfe-483">Resolutions</span></span>
* <span data-ttu-id="33dfe-484">Sprawdź tej konfiguracji hello w portalu OMS hello Syslog ma wszystkie urządzenia hello i poziomy dziennika poprawne hello</span><span class="sxs-lookup"><span data-stu-id="33dfe-484">Verify that hello configuration in hello OMS Portal for Syslog has all hello facilities and hello correct log levels</span></span>
  * <span data-ttu-id="33dfe-485">**Portalu OMS > Ustawienia > danych > Syslog**</span><span class="sxs-lookup"><span data-stu-id="33dfe-485">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="33dfe-486">Sprawdź tego macierzystego syslog wiadomości demonów (`rsyslog`, `syslog-ng`) są możliwe tooreceive wiadomości powitania przekazywane</span><span class="sxs-lookup"><span data-stu-id="33dfe-486">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able tooreceive hello forwarded messages</span></span>
* <span data-ttu-id="33dfe-487">Sprawdź ustawienia zapory na tooensure serwera Syslog hello czy wiadomości nie są blokowane</span><span class="sxs-lookup"><span data-stu-id="33dfe-487">Check firewall settings on hello Syslog server tooensure that messages are not being blocked</span></span>
* <span data-ttu-id="33dfe-488">Symulowanie tooOMS komunikatów Syslog, przy użyciu hello `logger` polecenia — na przykład:</span><span class="sxs-lookup"><span data-stu-id="33dfe-488">Simulate a Syslog message tooOMS using hello `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a><span data-ttu-id="33dfe-489">Problemy z połączeniem tooOMS przy użyciu serwera proxy</span><span class="sxs-lookup"><span data-stu-id="33dfe-489">Problems connecting tooOMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="33dfe-490">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="33dfe-490">Probable causes</span></span>
* <span data-ttu-id="33dfe-491">określony powitania serwera proxy podczas instalowania i konfigurowania agenta hello jest niepoprawny</span><span class="sxs-lookup"><span data-stu-id="33dfe-491">hello proxy specified when installing and configuring hello agent is incorrect</span></span>
* <span data-ttu-id="33dfe-492">punkty końcowe usługi OMS Hello nie są whitelistested w centrum danych.</span><span class="sxs-lookup"><span data-stu-id="33dfe-492">hello OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="33dfe-493">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="33dfe-493">Resolutions</span></span>
* <span data-ttu-id="33dfe-494">Zainstaluj ponownie hello Agent pakietu OMS dla systemu Linux przy użyciu następującego polecenia z opcją hello hello `-v` włączone.</span><span class="sxs-lookup"><span data-stu-id="33dfe-494">Reinstall hello OMS Agent for Linux using hello following command with hello option `-v` enabled.</span></span> <span data-ttu-id="33dfe-495">Dzięki temu pełne dane wyjściowe agenta hello łączących się za pośrednictwem hello proxy toohello usługę.</span><span class="sxs-lookup"><span data-stu-id="33dfe-495">This allows verbose output of hello agent connecting through hello proxy toohello OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="33dfe-496">Witaj w dokumentacji serwera proxy OMS na [Konfigurowanie hello agenta do użycia z serwera proxy HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span><span class="sxs-lookup"><span data-stu-id="33dfe-496">Review hello documentation for OMS proxy at [Configuring hello agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="33dfe-497">Sprawdź, że hello następujące punkty końcowe usługi OMS białej</span><span class="sxs-lookup"><span data-stu-id="33dfe-497">Verify that hello following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="33dfe-498">Zasób agenta</span><span class="sxs-lookup"><span data-stu-id="33dfe-498">Agent Resource</span></span> | <span data-ttu-id="33dfe-499">Porty</span><span class="sxs-lookup"><span data-stu-id="33dfe-499">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="33dfe-500">&#42;. ods.opinsights.Azure.com</span><span class="sxs-lookup"><span data-stu-id="33dfe-500">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="33dfe-501">Port 443</span><span class="sxs-lookup"><span data-stu-id="33dfe-501">Port 443</span></span> |
| <span data-ttu-id="33dfe-502">&#42;. OMS.opinsights.Azure.com</span><span class="sxs-lookup"><span data-stu-id="33dfe-502">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="33dfe-503">Port 443</span><span class="sxs-lookup"><span data-stu-id="33dfe-503">Port 443</span></span> |
| <span data-ttu-id="33dfe-504">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="33dfe-504">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="33dfe-505">Port 443</span><span class="sxs-lookup"><span data-stu-id="33dfe-505">Port 443</span></span> |
| <span data-ttu-id="33dfe-506">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="33dfe-506">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="33dfe-507">Port 443</span><span class="sxs-lookup"><span data-stu-id="33dfe-507">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="33dfe-508">Zostanie wyświetlony błąd 403 podczas dołączania</span><span class="sxs-lookup"><span data-stu-id="33dfe-508">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="33dfe-509">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="33dfe-509">Probable causes</span></span>
* <span data-ttu-id="33dfe-510">Witaj, Data i godzina są niepoprawne na serwerze z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-510">hello date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="33dfe-511">Hello identyfikator obszaru roboczego i klucz obszaru roboczego, używane są nieprawidłowe</span><span class="sxs-lookup"><span data-stu-id="33dfe-511">hello Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="33dfe-512">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="33dfe-512">Resolution</span></span>
* <span data-ttu-id="33dfe-513">Sprawdź czas hello na serwerze Linux z hello `date` polecenia.</span><span class="sxs-lookup"><span data-stu-id="33dfe-513">Verify hello time on your Linux server with hello `date` command.</span></span> <span data-ttu-id="33dfe-514">Jeśli powitalne danych jest większa niż lub mniej niż 15 minut od hello bieżącą godzinę, dołączania kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="33dfe-514">If hello data is greater than or less than 15 minutes from hello current time, then onboarding fails.</span></span> <span data-ttu-id="33dfe-515">toocorrect, zaktualizuj hello datę i/lub strefy czasowej serwera z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="33dfe-515">toocorrect this, update hello date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="33dfe-516">najnowszą wersję hello Agent pakietu OMS Linux Hello powiadamia użytkownika, jeśli różnica czasu powoduje błąd dołączania</span><span class="sxs-lookup"><span data-stu-id="33dfe-516">hello latest version of hello OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="33dfe-517">Przy użyciu zintegrowanego środowiska odzyskiwania hello poprawny identyfikator i klucz obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="33dfe-517">Re-onboard using hello correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="33dfe-518">Zobacz [dołączania przy użyciu wiersza polecenia hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="33dfe-518">See  [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a><span data-ttu-id="33dfe-519">500 Błąd lub błąd 404 pojawia się w pliku dziennika powitania po dołączania</span><span class="sxs-lookup"><span data-stu-id="33dfe-519">A 500 error or 404 error appears in hello log file after onboarding</span></span>
<span data-ttu-id="33dfe-520">Jest to znany problem występujący podczas przekazywania pierwszy hello danych Linux pod obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="33dfe-520">This is a known issue that occurs during hello first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="33dfe-521">Nie dotyczy to danych wysyłanych lub innych problemów.</span><span class="sxs-lookup"><span data-stu-id="33dfe-521">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="33dfe-522">Możesz zignorować hello błędy podczas początkowego procesu dołączania.</span><span class="sxs-lookup"><span data-stu-id="33dfe-522">You can ignore hello errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="33dfe-523">Nie ma danych Nagios hello portalu OMS</span><span class="sxs-lookup"><span data-stu-id="33dfe-523">Nagios data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="33dfe-524">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="33dfe-524">Probable causes</span></span>
* <span data-ttu-id="33dfe-525">Witaj omsagent użytkownik nie ma tooread uprawnienia z pliku dziennika hello Nagios</span><span class="sxs-lookup"><span data-stu-id="33dfe-525">hello omsagent user does not have permissions tooread from hello Nagios log file</span></span>
* <span data-ttu-id="33dfe-526">Hello Nagios źródła i sekcje filtru nadal są ujęte w pliku omsagent.conf hello</span><span class="sxs-lookup"><span data-stu-id="33dfe-526">hello Nagios source and filter sections are still commented in hello omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="33dfe-527">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="33dfe-527">Resolutions</span></span>
* <span data-ttu-id="33dfe-528">Dodaj użytkownika omsagent hello w kolejności tooread z hello Nagios pliku.</span><span class="sxs-lookup"><span data-stu-id="33dfe-528">Add hello omsagent user in order tooread from hello Nagios file.</span></span> <span data-ttu-id="33dfe-529">Zobacz [alerty Nagios](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="33dfe-529">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="33dfe-530">W pliku konfiguracji ogólnej systemu Linux na hello Agent pakietu OMS `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, upewnij się, że **zarówno** hello Nagios źródłowy oraz filtr sekcje mają komentarze usuwane, toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="33dfe-530">In hello OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** hello Nagios source and filter sections have comments removed, similar toohello following example.</span></span>

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


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a><span data-ttu-id="33dfe-531">Dane systemu Linux nie jest wyświetlane w portalu OMS hello</span><span class="sxs-lookup"><span data-stu-id="33dfe-531">Linux data doesn't appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="33dfe-532">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="33dfe-532">Probable causes</span></span>
* <span data-ttu-id="33dfe-533">Toohello dołączania usługę nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="33dfe-533">Onboarding toohello OMS Service failed</span></span>
* <span data-ttu-id="33dfe-534">Toohello połączenia, który jest zablokowany przez usługę OMS</span><span class="sxs-lookup"><span data-stu-id="33dfe-534">Connection toohello OMS Service is blocked</span></span>
* <span data-ttu-id="33dfe-535">Kopia zapasowa jest Hello Agent pakietu OMS danych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-535">hello OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="33dfe-536">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="33dfe-536">Resolutions</span></span>
* <span data-ttu-id="33dfe-537">Sprawdzić tego toohello dołączania usługę zakończyło się powodzeniem, upewniając się, że hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` istnieje.</span><span class="sxs-lookup"><span data-stu-id="33dfe-537">Verify that onboarding toohello OMS Service was successful by verifying that hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="33dfe-538">Przy użyciu zintegrowanego środowiska odzyskiwania hello omsadmin.sh wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="33dfe-538">Re-onboard using hello omsadmin.sh command line.</span></span> <span data-ttu-id="33dfe-539">Zobacz [dołączania przy użyciu wiersza polecenia hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="33dfe-539">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="33dfe-540">Jeśli przy użyciu serwera proxy, należy użyć hello proxy kroki rozwiązywania problemów powyżej</span><span class="sxs-lookup"><span data-stu-id="33dfe-540">If using a proxy, use hello proxy troubleshooting steps above</span></span>
* <span data-ttu-id="33dfe-541">W niektórych przypadkach gdy hello Agent pakietu OMS dla systemu Linux nie mogą komunikować się z hello usługę, dane na powitania agenta jest rozmiar buforu pełnej kopii zapasowej toohello 50 MB.</span><span class="sxs-lookup"><span data-stu-id="33dfe-541">In some cases, when hello OMS Agent for Linux cannot communicate with hello OMS Service, data on hello Agent is backed-up toohello full buffer size of 50 MB.</span></span> <span data-ttu-id="33dfe-542">Uruchom ponownie hello Agent pakietu OMS dla systemu Linux, uruchamiając hello `/opt/microsoft/omsagent/bin/service_control restart` polecenia.</span><span class="sxs-lookup"><span data-stu-id="33dfe-542">Restart hello OMS Agent for Linux by running hello `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="33dfe-543">Tego problemu w 1.1.0-28 wersję agenta i nowszych.</span><span class="sxs-lookup"><span data-stu-id="33dfe-543">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a><span data-ttu-id="33dfe-544">W portalu OMS hello nie zastosowano konfigurację liczników wydajności dziennika systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-544">Syslog Linux performance counter configuration is not applied in hello OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="33dfe-545">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="33dfe-545">Probable causes</span></span>
* <span data-ttu-id="33dfe-546">agent konfiguracji Hello w hello Agent pakietu OMS dla systemu Linux nie odebrał hello najnowszej konfiguracji z portalu OMS hello.</span><span class="sxs-lookup"><span data-stu-id="33dfe-546">hello configuration agent in hello OMS Agent for Linux has not retrieved hello latest configuration from hello OMS portal.</span></span>
* <span data-ttu-id="33dfe-547">Witaj poprawione ustawień w portalu hello nie zostały zastosowane</span><span class="sxs-lookup"><span data-stu-id="33dfe-547">hello revised settings in hello portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="33dfe-548">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="33dfe-548">Resolutions</span></span>
<span data-ttu-id="33dfe-549">`omsconfig`jest agentem konfiguracji hello w hello Agent pakietu OMS dla systemu Linux, które pobierają zmiany konfiguracji portalu OMS co 5 minut.</span><span class="sxs-lookup"><span data-stu-id="33dfe-549">`omsconfig` is hello configuration agent in hello OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="33dfe-550">Ta konfiguracja jest następnie zastosowane toohello Agent pakietu OMS dla systemu Linux pliki konfiguracji znajduje się w `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="33dfe-550">This configuration is then applied toohello OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="33dfe-551">W niektórych przypadkach hello Agent pakietu OMS dla systemu Linux konfiguracji agenta nie może być możliwe toocommunicate z usługą konfiguracji portalu hello powodujące najnowszej konfiguracji nie są stosowane.</span><span class="sxs-lookup"><span data-stu-id="33dfe-551">In some cases, hello OMS Agent for Linux configuration agent might not be able toocommunicate with hello portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="33dfe-552">Sprawdź, że hello `omsconfig` agent został zainstalowany z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="33dfe-552">Verify that hello `omsconfig` agent is installed with hello following:</span></span>

  * <span data-ttu-id="33dfe-553">`dpkg --list omsconfig` lub `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="33dfe-553">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="33dfe-554">Jeśli nie jest zainstalowany, zainstaluj ponownie najnowszą wersję hello hello Agent pakietu OMS dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-554">If not installed, reinstall hello latest version of hello OMS Agent for Linux</span></span>
* <span data-ttu-id="33dfe-555">Sprawdź, że hello `omsconfig` agenta może komunikować się z hello usługę</span><span class="sxs-lookup"><span data-stu-id="33dfe-555">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="33dfe-556">Uruchom hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` polecenia</span><span class="sxs-lookup"><span data-stu-id="33dfe-556">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="33dfe-557">Witaj polecenie powyżej zwraca hello konfigurację agenta pobiera z portalu hello, w tym ustawienia Syslog, liczniki wydajności systemu Linux i dzienników niestandardowych</span><span class="sxs-lookup"><span data-stu-id="33dfe-557">hello command above returns hello configuration that agent retrieves from hello portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="33dfe-558">W przypadku niepowodzenia powyższego polecenia hello Uruchom hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` polecenia.</span><span class="sxs-lookup"><span data-stu-id="33dfe-558">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="33dfe-559">To polecenie wymusza hello omsconfig agenta toocommunicate hello OMS usługi tooretrieve hello najnowszej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="33dfe-559">This command forces hello omsconfig agent toocommunicate with hello OMS service tooretrieve hello latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="33dfe-560">Niestandardowe dane dziennika systemu Linux nie jest wyświetlany w hello portalu OMS</span><span class="sxs-lookup"><span data-stu-id="33dfe-560">Custom Linux log data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="33dfe-561">Prawdopodobne przyczyny</span><span class="sxs-lookup"><span data-stu-id="33dfe-561">Probable causes</span></span>
* <span data-ttu-id="33dfe-562">TooOMS przechodzenia do usługi nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="33dfe-562">Onboarding tooOMS Service failed</span></span>
* <span data-ttu-id="33dfe-563">Witaj **hello Zastosuj następujące toomy konfiguracji serwerów z systemem Linux** ustawienia nie zostały wybrane.</span><span class="sxs-lookup"><span data-stu-id="33dfe-563">hello **Apply hello following configuration toomy Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="33dfe-564">omsconfig nie została pobrana hello najnowsze dziennik niestandardowy z portalu hello</span><span class="sxs-lookup"><span data-stu-id="33dfe-564">omsconfig has not picked up hello latest custom log from hello portal</span></span>
* <span data-ttu-id="33dfe-565">Witaj `omsagent` użycie jest dziennik niestandardowy hello tooaccess powodu tooa uprawnień problem lub `omsagent` nie został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="33dfe-565">hello `omsagent` use is unable tooaccess hello custom log due tooa permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="33dfe-566">W takim przypadku zostanie wyświetlony hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="33dfe-566">In this case, you'll see hello following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="33dfe-567">Jest to znany problem dotyczący hello sytuacji wyścigu, który został rozwiązany w hello Agent pakietu OMS dla 1.1.0-217 wersji systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33dfe-567">This is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="33dfe-568">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="33dfe-568">Resolutions</span></span>
* <span data-ttu-id="33dfe-569">Sprawdź, czy udało Ci się pomyślnie został załadowany, określając, czy hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` plik istnieje.</span><span class="sxs-lookup"><span data-stu-id="33dfe-569">Verify that you've successfully onboarded, by determining whether hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="33dfe-570">Jeśli potrzebne, dodać ponownie przy użyciu wiersza polecenia omsadmin.sh hello.</span><span class="sxs-lookup"><span data-stu-id="33dfe-570">If needed, onboard again using hello omsadmin.sh command line.</span></span> <span data-ttu-id="33dfe-571">Zobacz [dołączania przy użyciu wiersza polecenia hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="33dfe-571">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="33dfe-572">W hello w portalu OMS **ustawienia** na powitania **danych** karcie, upewnij się, że hello **hello Zastosuj następujące toomy konfiguracji serwerów z systemem Linux** wybrane ustawienie</span><span class="sxs-lookup"><span data-stu-id="33dfe-572">In hello OMS Portal, under **Settings** on hello **Data** tab, ensure that hello **Apply hello following configuration toomy Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="33dfe-573">![Zastosuj konfigurację](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="33dfe-573">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="33dfe-574">Sprawdź, że hello `omsconfig` agenta może komunikować się z hello usługę</span><span class="sxs-lookup"><span data-stu-id="33dfe-574">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="33dfe-575">Uruchom hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` polecenia</span><span class="sxs-lookup"><span data-stu-id="33dfe-575">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="33dfe-576">Witaj polecenie powyżej zwraca hello konfigurację agenta pobiera z hello portalu, w tym ustawienia Syslog, liczniki wydajności systemu Linux i dzienników niestandardowych</span><span class="sxs-lookup"><span data-stu-id="33dfe-576">hello command above returns hello configuration that agent retrieves from hello Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="33dfe-577">W przypadku niepowodzenia powyższego polecenia hello Uruchom hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` polecenia.</span><span class="sxs-lookup"><span data-stu-id="33dfe-577">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="33dfe-578">To polecenie wymusza hello omsconfig agenta toocommunicate z usługą OMS i pobrania najnowszej konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="33dfe-578">This command forces hello omsconfig agent toocommunicate with OMS service and retrieve hello latest configuration.</span></span>

<span data-ttu-id="33dfe-579">Zamiast hello Agent pakietu OMS dla użytkownika w systemie Linux uruchomiony jako użytkownik uprzywilejowanych `root`, hello Agent pakietu OMS dla systemu Linux jest uruchamiany jako hello `omsagent` użytkownika.</span><span class="sxs-lookup"><span data-stu-id="33dfe-579">Instead of hello OMS Agent for Linux user running as a privileged user `root`, hello OMS Agent for Linux runs as hello `omsagent` user.</span></span> <span data-ttu-id="33dfe-580">W większości przypadków należy jawne uprawnienia przyznane użytkownikowi toohello w kolejności tooread niektórych plików.</span><span class="sxs-lookup"><span data-stu-id="33dfe-580">In most cases, explicit permission must be granted toohello user in order tooread certain files.</span></span>

<span data-ttu-id="33dfe-581">uprawnienie toogrant zbyt`omsagent` użytkownika, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="33dfe-581">toogrant permission too`omsagent` user, run hello following commands:</span></span>

1. <span data-ttu-id="33dfe-582">Dodaj hello `omsagent` użytkownika tooa określonej grupy z`sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="33dfe-582">Add hello `omsagent` user tooa specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="33dfe-583">Przyznaj wymaganego pliku toohello Uniwersalny dostęp do odczytu z`sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="33dfe-583">Grant universal read access toohello required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="33dfe-584">Istnieje znany problem dotyczący hello sytuacji wyścigu, który został rozwiązany w hello Agent pakietu OMS dla 1.1.0-217 wersji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="33dfe-584">There is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="33dfe-585">Po zaktualizowaniu toohello najnowsza wersja agenta, uruchom hello następujące polecenia tooget hello najnowszą wersję hello dane wyjściowe wtyczki:</span><span class="sxs-lookup"><span data-stu-id="33dfe-585">After updating toohello latest agent, run hello following command tooget hello latest version of hello output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="33dfe-586">Znane ograniczenia</span><span class="sxs-lookup"><span data-stu-id="33dfe-586">Known limitations</span></span>
<span data-ttu-id="33dfe-587">Przejrzyj powitania po toolearn sekcje zawierają informacje o bieżącym ograniczenia hello Agent pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="33dfe-587">Review hello following sections toolearn about current limitations of hello OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="33dfe-588">Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="33dfe-588">Azure Diagnostics</span></span>
<span data-ttu-id="33dfe-589">Dla maszyn wirtualnych systemu Linux działających na platformie Azure dodatkowe czynności może być wymagane tooallow zbierania danych przez diagnostyki Azure i usługi Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="33dfe-589">For Linux virtual machines running in Azure, additional steps may be required tooallow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="33dfe-590">**W wersji 2.2** hello rozszerzenia diagnostyki dla systemu Linux jest wymagany dla zgodności z hello Agent pakietu OMS dla systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="33dfe-590">**Version 2.2** of hello Diagnostics Extension for Linux is required for compatibility with hello OMS Agent for Linux.</span></span>

<span data-ttu-id="33dfe-591">Aby uzyskać więcej informacji o instalowaniu i konfigurowaniu hello diagnostycznych rozszerzenia dla systemu Linux, zobacz [Użyj tooenable polecenia interfejsu wiersza polecenia Azure hello rozszerzenia diagnostycznych Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="33dfe-591">For more information on installing and configuring hello Diagnostic Extension for Linux, see [Use hello Azure CLI command tooenable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="33dfe-592">**Uaktualnianie hello rozszerzenia diagnostyki Linux z too2.2 2.0 ASM interfejsu wiersza polecenia platformy Azure:**</span><span class="sxs-lookup"><span data-stu-id="33dfe-592">**Upgrading hello Linux Diagnostics Extension from 2.0 too2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="33dfe-593">**ARM**</span><span class="sxs-lookup"><span data-stu-id="33dfe-593">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="33dfe-594">Plik o nazwie PrivateConfig.json odwoływać się do tych przykładach poleceń.</span><span class="sxs-lookup"><span data-stu-id="33dfe-594">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="33dfe-595">format Hello ten plik powinien być podobny hello następujące przykładowe.</span><span class="sxs-lookup"><span data-stu-id="33dfe-595">hello format of that file should resemble hello following sample.</span></span>

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="33dfe-596">Sysklog nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="33dfe-596">Sysklog is not supported</span></span>
<span data-ttu-id="33dfe-597">Rsyslog lub syslog ng są wymagane toocollect komunikaty dziennika systemowego.</span><span class="sxs-lookup"><span data-stu-id="33dfe-597">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="33dfe-598">demon syslog domyślne Hello w wersji 5 (sysklog) w wersji Red Hat Enterprise Linux, CentOS i Oracle Linux nie jest obsługiwana dla zbierania zdarzeń usługi syslog.</span><span class="sxs-lookup"><span data-stu-id="33dfe-598">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="33dfe-599">toocollect syslog danych z tej wersji tych dystrybucji hello rsyslog demon powinien być zainstalowany i skonfigurowany tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="33dfe-599">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span> <span data-ttu-id="33dfe-600">Aby uzyskać więcej informacji o zamianę sysklog rsyslog, zobacz [zainstalować hello nowo utworzony rsyslog obr. / min](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span><span class="sxs-lookup"><span data-stu-id="33dfe-600">For more information on replacing sysklog with rsyslog, see [Install hello newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="33dfe-601">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="33dfe-601">Next Steps</span></span>
* <span data-ttu-id="33dfe-602">[Dodawanie rozwiązania analizy dzienników z galerii rozwiązań hello](log-analytics-add-solutions.md) tooadd funkcjonalność i zbieranie danych.</span><span class="sxs-lookup"><span data-stu-id="33dfe-602">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
* <span data-ttu-id="33dfe-603">Zapoznaj się z [dziennika wyszukiwania](log-analytics-log-searches.md) tooview szczegółowe informacje zebrane przez rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="33dfe-603">Get familiar with [log searches](log-analytics-log-searches.md) tooview detailed information gathered by solutions.</span></span>
* <span data-ttu-id="33dfe-604">Użyj [pulpity nawigacyjne](log-analytics-dashboards.md) toosave i wyświetlanie własne wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="33dfe-604">Use [dashboards](log-analytics-dashboards.md) toosave and display your own custom searches.</span></span>
