---
title: "Rozwiązywanie problemów z błędami ochrony VMware/fizycznych do platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano typowe błędy replikacji maszyny VMware i sposoby ich rozwiązywania"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: 6ebec2e06566b1e2d6834fdd81c0d8b2801b80b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="3bbf7-103">Rozwiązywanie problemów replikacji serwera VMware/fizyczne lokalnej</span><span class="sxs-lookup"><span data-stu-id="3bbf7-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="3bbf7-104">W trakcie ochronę sieci maszyn wirtualnych VMware lub serwerów fizycznych za pomocą usługi Azure Site Recovery może zostać wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="3bbf7-105">Ten artykuł zawiera szczegóły dotyczące niektórych bardziej typowe komunikaty o błędach napotkano wraz z czynności pozwalające rozwiązać je.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-105">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="3bbf7-106">Replikacja początkowa jest zablokowany na 0%</span><span class="sxs-lookup"><span data-stu-id="3bbf7-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="3bbf7-107">Większość błędów jest Replikacja początkowa napotykane w witrynie pomocy technicznej są spowodowane problemami z łącznością między serwerem proces serwera źródłowego lub serwera Azure procesu.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-107">Most of the initial replication failures that we encounter at support are due to connectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="3bbf7-108">W większości przypadków można samodzielnie rozwiązywania tych problemów, wykonując kroki opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-108">For most cases, you can self troubleshoot these issues by following the steps listed below.</span></span>

###<a name="check-the-following-on-source-machine"></a><span data-ttu-id="3bbf7-109">Sprawdź, czy na MASZYNIE ŹRÓDŁOWEJ</span><span class="sxs-lookup"><span data-stu-id="3bbf7-109">Check the following on SOURCE MACHINE</span></span>
* <span data-ttu-id="3bbf7-110">Z wiersza polecenia komputera serwera źródłowego należy użyć Telnet na polecenie ping serwera przetwarzania z portem https (domyślnie 9443), jak pokazano poniżej, aby zobaczyć, czy istnieją problemy z połączeniem sieciowym lub problemy z blokowaniem portów zapory.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-110">From Source Server machine command line, use Telnet to ping the Process Server with https port (default 9443) as shown below to see if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="3bbf7-111">Użyj Telnet, nie za pomocą polecenia PING do testowania łączności.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-111">Use Telnet, don’t use PING to test connectivity.</span></span>  <span data-ttu-id="3bbf7-112">Jeśli nie zainstalowano programu Telnet, wykonaj listę kroków [tutaj](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="3bbf7-112">If Telnet is not installed, follow the steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="3bbf7-113">Jeśli nie można połączyć, Zezwalaj na port wejściowy 9443 na serwerze przetwarzania i sprawdź, czy problem nadal kończy działanie.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-113">If unable to connect, allow inbound port 9443 on the Process Server and check if the problem still exits.</span></span> <span data-ttu-id="3bbf7-114">Było w niej niektórych przypadkach, gdy serwer przetwarzania został za strefą DMZ, która była przyczyną tego problemu.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="3bbf7-115">Sprawdź stan usługi `InMage Scout VX Agent – Sentinel/OutpostStart` Jeśli nie jest uruchomiona i sprawdź, czy problem nadal występuje.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-115">Check the status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if the problem still exists.</span></span>   
 
###<a name="check-the-following-on-process-server"></a><span data-ttu-id="3bbf7-116">Sprawdź, czy na serwerze przetwarzania</span><span class="sxs-lookup"><span data-stu-id="3bbf7-116">Check the following on PROCESS SERVER</span></span>

* <span data-ttu-id="3bbf7-117">**Sprawdź, czy serwer przetwarzania jest aktywnie przekazywanie danych do platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="3bbf7-117">**Check if process server is actively pushing data to Azure**</span></span> 

<span data-ttu-id="3bbf7-118">Z komputera serwer przetwarzania Otwórz Menedżera zadań (naciśnij klawisze Ctrl-Shift-Esc).</span><span class="sxs-lookup"><span data-stu-id="3bbf7-118">From Process Server machine, open the Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="3bbf7-119">Przejdź do karty wyników, a następnie kliknij łącze otwieranie monitora zasobów.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-119">Go to the Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="3bbf7-120">Z Menedżera zasobów, przejdź do karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-120">From Resource Manager, go to Network tab.</span></span> <span data-ttu-id="3bbf7-121">Sprawdź, czy cbengine.exe "Procesów z działaniem sieci" aktywnie wysyła dużej ilości danych (w MB).</span><span class="sxs-lookup"><span data-stu-id="3bbf7-121">Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Włączanie replikacji](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="3bbf7-123">W przeciwnym razie wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3bbf7-123">If not follow the steps listed below:</span></span>

* <span data-ttu-id="3bbf7-124">**Sprawdź, czy serwer przetwarzania jest możliwość łączenia z obiektów Blob platformy Azure**: zaznacz i sprawdź cbengine.exe przeglądania "Połączeń TCP" czy jest łączność między serwerem przetwarzania adresu URL obiektu blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-124">**Check if Process server is able to connect Azure Blob**: Select and check cbengine.exe to view the ‘TCP Connections’ to see if there is connectivity from Process server to Azure Storage blob URL.</span></span>

![Włączanie replikacji](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="3bbf7-126">Jeśli nie są następnie przejdź do pozycji Panel sterowania > usługi, sprawdź, czy następujące usługi są uruchomione i działają prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="3bbf7-126">If not then go to Control Panel > Services, check if the following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="3bbf7-127">(Ponownego) Uruchom dowolnej usługi, która nie jest uruchomiona i sprawdź, czy problem nadal występuje.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-127">(Re)Start any service which is not running and check if the problem still exists.</span></span>

* <span data-ttu-id="3bbf7-128">**Sprawdź, czy serwer przetwarzania jest można nawiązać połączenia z programem Azure publiczny adres IP przy użyciu portu 443**</span><span class="sxs-lookup"><span data-stu-id="3bbf7-128">**Check if Process server is able to connect to Azure Public IP address using port 443**</span></span>

<span data-ttu-id="3bbf7-129">Otwórz najnowszą CBEngineCurr.errlog z `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` i wyszukaj: 443 i połączenia próba nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-129">Open the latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Włączanie replikacji](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="3bbf7-131">Jeśli występują problemy, z serwera przetwarzania wiersza polecenia, użyj telnet na polecenie ping Azure publicznego adresu IP (maskowania w powyżej obrazu) w CBEngineCurr.currLog przy użyciu portu 443.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-131">If there are issues, then from Process Server command line, use telnet to ping your Azure Public IP address (masked in above image) found in the CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="3bbf7-132">Jeśli nie możesz się połączyć, sprawdź, czy problem dostępu występuje z powodu zapory lub serwera Proxy, zgodnie z opisem w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-132">If you are unable to connect, then check if the access issue is due to firewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="3bbf7-133">**Sprawdź, czy zapora oparta na adres IP na serwerze przetwarzania są nie blokuje dostępu**: Jeśli używasz reguły zapory oparte na adresie IP na serwerze, Pobierz pełną listę Microsoft Azure zakresów IP centrum danych z [tutaj](https://www.microsoft.com/download/details.aspx?id=41653) i dodaj je do konfiguracji zapory w celu zapewnienia ich zezwalają na komunikację z platformy Azure (i portu HTTPS (port 443)).</span><span class="sxs-lookup"><span data-stu-id="3bbf7-133">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on the server, then download the complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them to your firewall configuration to ensure they allow communication to Azure (and the HTTPS (443) port).</span></span>  <span data-ttu-id="3bbf7-134">Zezwól na użycie zakresów adresów IP dla regionu platformy Azure Twojej subskrypcji oraz regionu Zachodnie stany USA (służy do kontrolowania dostępu i zarządzania tożsamościami).</span><span class="sxs-lookup"><span data-stu-id="3bbf7-134">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="3bbf7-135">**Sprawdź, czy zapora oparta na adres URL, na serwerze przetwarzania nie blokuje dostępu**: Jeśli używasz reguły zapory adres URL oparty na serwerze, upewnij się, następujące adresy URL są dodawane do konfiguracji zapory.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-135">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on the server, ensure the following URLs are added to firewall configuration.</span></span> 
     
  <span data-ttu-id="3bbf7-136">`*.accesscontrol.windows.net:` służy do kontrolowania dostępu i zarządzania tożsamościami</span><span class="sxs-lookup"><span data-stu-id="3bbf7-136">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="3bbf7-137">`*.backup.windowsazure.com:` służy do transferowania i organizowania danych replikacji</span><span class="sxs-lookup"><span data-stu-id="3bbf7-137">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="3bbf7-138">`*.blob.core.windows.net:`Używane do uzyskiwania dostępu do konta magazynu, czy magazyny zreplikowanych danych</span><span class="sxs-lookup"><span data-stu-id="3bbf7-138">`*.blob.core.windows.net:` Used for access to the storage account that stores replicated data</span></span>

  <span data-ttu-id="3bbf7-139">`*.hypervrecoverymanager.windowsazure.com:` służy do wykonywania operacji i organizowania zarządzania replikacją</span><span class="sxs-lookup"><span data-stu-id="3bbf7-139">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="3bbf7-140">`time.nist.gov`i `time.windows.com`: użytych do sprawdzenia synchronizacja czasu między systemem a czasem globalnym.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-140">`time.nist.gov` and `time.windows.com`: Used to check time synchronization between system and global time.</span></span>

<span data-ttu-id="3bbf7-141">Adresy URL **chmury Azure dla instytucji rządowych**:</span><span class="sxs-lookup"><span data-stu-id="3bbf7-141">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="3bbf7-142">**Sprawdź, czy ustawienia serwera Proxy na serwerze przetwarzania są nie blokuje dostępu**.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-142">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="3bbf7-143">Jeśli używasz serwera Proxy, upewnij się, że nazwa serwera proxy jest rozpoznawana przez serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-143">If you are using a Proxy Server, ensure the proxy server name is resolving by the DNS server.</span></span>
<span data-ttu-id="3bbf7-144">Aby sprawdzić, jakie zostały podane w czasie instalacji serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-144">To check what you have provided at the time of Configuration Server setup.</span></span> <span data-ttu-id="3bbf7-145">Przejdź do klucza rejestru</span><span class="sxs-lookup"><span data-stu-id="3bbf7-145">Go to registry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="3bbf7-146">Teraz upewnij się, że te same ustawienia są używane przez agenta usługi Azure Site Recovery do przesyłania danych.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-146">Now ensure that the same settings are being used by Azure Site Recovery agent to send data.</span></span>
<span data-ttu-id="3bbf7-147">Kopia zapasowa Microsoft Azure Search</span><span class="sxs-lookup"><span data-stu-id="3bbf7-147">Search Microsoft Azure  Backup</span></span> 

![Włączanie replikacji](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="3bbf7-149">Otwórz go i kliknij akcję > Zmień właściwości.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-149">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="3bbf7-150">Na karcie Konfiguracja serwera Proxy powinien zostać wyświetlony adres serwera proxy, która powinna być taka sama, jak to przedstawiono ustawienia rejestru.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-150">Under Proxy Configuration tab, you should see the proxy address, which should be same as shown by the registry settings.</span></span> <span data-ttu-id="3bbf7-151">Jeśli nie, zmień ją na ten sam adres.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-151">If not, please change it to the same address.</span></span>

![Włączanie replikacji](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="3bbf7-153">**Sprawdź, czy ograniczania przepustowości nie jest ograniczane na serwerze przetwarzania**: zwiększyć przepustowość i sprawdź, czy problem nadal występuje.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-153">**Check if Throttle bandwidth is not constrained on Process server**:  Increase the bandwidth  and check if the problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="3bbf7-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3bbf7-154">Next steps</span></span>
<span data-ttu-id="3bbf7-155">Jeśli potrzebujesz więcej pomocy, opublikuj wpis kwerendy do [forum usługi ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3bbf7-155">If you need more help, then post your query to [ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="3bbf7-156">Mamy aktywną społeczność i jeden z naszych inżynierów będzie można pomóc.</span><span class="sxs-lookup"><span data-stu-id="3bbf7-156">We have an active community and one of our engineers will be able to assist you.</span></span>