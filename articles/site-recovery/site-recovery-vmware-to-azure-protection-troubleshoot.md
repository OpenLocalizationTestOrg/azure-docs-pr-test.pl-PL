---
title: "aaaTroubleshoot ochrony błędów VMware/fizyczne tooAzure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano błędy replikacji maszyn VMware hello typowe i w jaki sposób tootroubleshoot ich"
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
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="f5620-103">Rozwiązywanie problemów replikacji serwera VMware/fizyczne lokalnej</span><span class="sxs-lookup"><span data-stu-id="f5620-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="f5620-104">W trakcie ochronę sieci maszyn wirtualnych VMware lub serwerów fizycznych za pomocą usługi Azure Site Recovery może zostać wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="f5620-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="f5620-105">Szczegółów tego artykułu hello niektóre z najczęściej komunikaty o błędach napotkano oraz rozwiązywanie problemów z tooresolve kroki je.</span><span class="sxs-lookup"><span data-stu-id="f5620-105">This article details some of hello more common error messages encountered, along with troubleshooting steps tooresolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="f5620-106">Replikacja początkowa jest zablokowany na 0%</span><span class="sxs-lookup"><span data-stu-id="f5620-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="f5620-107">Większość hello błędy replikacji początkowej, napotykane w witrynie pomocy technicznej jest powodu tooconnectivity problemy między serwerem proces serwera źródłowego lub serwera Azure procesu.</span><span class="sxs-lookup"><span data-stu-id="f5620-107">Most of hello initial replication failures that we encounter at support are due tooconnectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="f5620-108">W większości przypadków można samodzielnie rozwiązywania tych problemów, wykonując kroki hello wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="f5620-108">For most cases, you can self troubleshoot these issues by following hello steps listed below.</span></span>

###<a name="check-hello-following-on-source-machine"></a><span data-ttu-id="f5620-109">Sprawdź następujące hello na MASZYNIE ŹRÓDŁOWEJ</span><span class="sxs-lookup"><span data-stu-id="f5620-109">Check hello following on SOURCE MACHINE</span></span>
* <span data-ttu-id="f5620-110">Z wiersza polecenia komputera serwera źródłowego należy użyć Telnet tooping powitania serwera przetwarzania z portem https (domyślnie 9443) zgodnie z poniższym toosee, jeśli istnieją problemy z połączeniem sieciowym lub problemów z blokowaniem portu zapory.</span><span class="sxs-lookup"><span data-stu-id="f5620-110">From Source Server machine command line, use Telnet tooping hello Process Server with https port (default 9443) as shown below toosee if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="f5620-111">Użyj Telnet, nie używaj łączności tootest PING.</span><span class="sxs-lookup"><span data-stu-id="f5620-111">Use Telnet, don’t use PING tootest connectivity.</span></span>  <span data-ttu-id="f5620-112">Jeśli nie zainstalowano programu Telnet, wykonaj listę kroków hello [tutaj](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="f5620-112">If Telnet is not installed, follow hello steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="f5620-113">Jeśli tooconnect Zezwalaj na port wejściowy 9443 na powitania serwera przetwarzania i sprawdź, czy hello problem nadal zamknięte.</span><span class="sxs-lookup"><span data-stu-id="f5620-113">If unable tooconnect, allow inbound port 9443 on hello Process Server and check if hello problem still exits.</span></span> <span data-ttu-id="f5620-114">Było w niej niektórych przypadkach, gdy serwer przetwarzania został za strefą DMZ, która była przyczyną tego problemu.</span><span class="sxs-lookup"><span data-stu-id="f5620-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="f5620-115">Sprawdź stan hello usługi `InMage Scout VX Agent – Sentinel/OutpostStart` Jeśli nie jest uruchomiona i sprawdź, czy hello problem nadal występuje.</span><span class="sxs-lookup"><span data-stu-id="f5620-115">Check hello status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if hello problem still exists.</span></span>   
 
###<a name="check-hello-following-on-process-server"></a><span data-ttu-id="f5620-116">Sprawdź następujące hello na serwerze przetwarzania</span><span class="sxs-lookup"><span data-stu-id="f5620-116">Check hello following on PROCESS SERVER</span></span>

* <span data-ttu-id="f5620-117">**Sprawdź, czy serwer przetwarzania jest aktywnie wypychanie tooAzure danych**</span><span class="sxs-lookup"><span data-stu-id="f5620-117">**Check if process server is actively pushing data tooAzure**</span></span> 

<span data-ttu-id="f5620-118">Z komputera serwer przetwarzania Otwórz hello Menedżera zadań (naciśnij klawisze Ctrl-Shift-Esc).</span><span class="sxs-lookup"><span data-stu-id="f5620-118">From Process Server machine, open hello Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="f5620-119">Przejdź na kartę Wydajność toohello, a następnie kliknij łącze otwieranie monitora zasobów.</span><span class="sxs-lookup"><span data-stu-id="f5620-119">Go toohello Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="f5620-120">Z Menedżera zasobów Przejdź tooNetwork kartę. Sprawdź, czy cbengine.exe "Procesów z działaniem sieci" aktywnie wysyła dużej ilości danych (w MB).</span><span class="sxs-lookup"><span data-stu-id="f5620-120">From Resource Manager, go tooNetwork tab. Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Włączanie replikacji](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="f5620-122">W przeciwnym razie wykonaj kroki hello wymienionych poniżej:</span><span class="sxs-lookup"><span data-stu-id="f5620-122">If not follow hello steps listed below:</span></span>

* <span data-ttu-id="f5620-123">**Sprawdź, czy serwer przetwarzania jest możliwe tooconnect obiektów Blob platformy Azure**: Wybierz, a następnie sprawdź toosee "Połączenia TCP" hello tooview cbengine.exe, jeśli brak łączności z adresu URL procesu serwera tooAzure magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f5620-123">**Check if Process server is able tooconnect Azure Blob**: Select and check cbengine.exe tooview hello ‘TCP Connections’ toosee if there is connectivity from Process server tooAzure Storage blob URL.</span></span>

![Włączanie replikacji](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="f5620-125">Jeśli nie, następnie przejdź tooControl panelu > usługi, sprawdź, czy hello następujące usługi są uruchomione i działają prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="f5620-125">If not then go tooControl Panel > Services, check if hello following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="f5620-126">(Ponownego) Uruchom dowolnej usługi, która nie jest uruchomiona i sprawdź, czy hello problem nadal istnieje.</span><span class="sxs-lookup"><span data-stu-id="f5620-126">(Re)Start any service which is not running and check if hello problem still exists.</span></span>

* <span data-ttu-id="f5620-127">**Sprawdź, czy serwer przetwarzania jest w stanie tooconnect tooAzure publiczny adres IP przy użyciu portu 443**</span><span class="sxs-lookup"><span data-stu-id="f5620-127">**Check if Process server is able tooconnect tooAzure Public IP address using port 443**</span></span>

<span data-ttu-id="f5620-128">Otwórz hello najnowsze CBEngineCurr.errlog z `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` i wyszukaj: 443 i połączenia próba nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="f5620-128">Open hello latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Włączanie replikacji](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="f5620-130">Jeśli występują problemy, z serwera przetwarzania wiersza polecenia, użyj telnet tooping Azure publicznego adresu IP (maskowania w powyżej obrazu) w hello CBEngineCurr.currLog przy użyciu portu 443.</span><span class="sxs-lookup"><span data-stu-id="f5620-130">If there are issues, then from Process Server command line, use telnet tooping your Azure Public IP address (masked in above image) found in hello CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="f5620-131">W przypadku tooconnect nie można sprawdzić w przypadku problemu z dostępem hello toofirewall lub serwera Proxy, zgodnie z opisem w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="f5620-131">If you are unable tooconnect, then check if hello access issue is due toofirewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="f5620-132">**Sprawdź, czy zapora oparta na adres IP na serwerze przetwarzania są nie blokuje dostępu**: Jeśli używasz reguły zapory oparte na adresie IP na serwerze hello, Pobierz pełną listę hello Microsoft Azure zakresów IP centrum danych z [tutaj ](https://www.microsoft.com/download/details.aspx?id=41653) i dodaj je tooensure konfiguracji zapory tooyour pozwalają tooAzure komunikacji (i hello port HTTPS (port 443)).</span><span class="sxs-lookup"><span data-stu-id="f5620-132">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on hello server, then download hello complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them tooyour firewall configuration tooensure they allow communication tooAzure (and hello HTTPS (443) port).</span></span>  <span data-ttu-id="f5620-133">Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).</span><span class="sxs-lookup"><span data-stu-id="f5620-133">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="f5620-134">**Sprawdź, czy zapora oparta na adres URL, na serwerze przetwarzania nie blokuje dostępu**: Jeśli używasz reguły zapory adres URL oparty na powitania serwera, upewnij się, hello następujące adresy URL są dodawane toofirewall konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f5620-134">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on hello server, ensure hello following URLs are added toofirewall configuration.</span></span> 
     
  <span data-ttu-id="f5620-135">`*.accesscontrol.windows.net:` służy do kontrolowania dostępu i zarządzania tożsamościami</span><span class="sxs-lookup"><span data-stu-id="f5620-135">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="f5620-136">`*.backup.windowsazure.com:` służy do transferowania i organizowania danych replikacji</span><span class="sxs-lookup"><span data-stu-id="f5620-136">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="f5620-137">`*.blob.core.windows.net:`Używany do toohello dostępu konta magazynu, która przechowuje zreplikowanych danych</span><span class="sxs-lookup"><span data-stu-id="f5620-137">`*.blob.core.windows.net:` Used for access toohello storage account that stores replicated data</span></span>

  <span data-ttu-id="f5620-138">`*.hypervrecoverymanager.windowsazure.com:` służy do wykonywania operacji i organizowania zarządzania replikacją</span><span class="sxs-lookup"><span data-stu-id="f5620-138">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="f5620-139">`time.nist.gov`i `time.windows.com`: używane toocheck synchronizacja czasu między systemem a czasem globalnym.</span><span class="sxs-lookup"><span data-stu-id="f5620-139">`time.nist.gov` and `time.windows.com`: Used toocheck time synchronization between system and global time.</span></span>

<span data-ttu-id="f5620-140">Adresy URL **chmury Azure dla instytucji rządowych**:</span><span class="sxs-lookup"><span data-stu-id="f5620-140">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="f5620-141">**Sprawdź, czy ustawienia serwera Proxy na serwerze przetwarzania są nie blokuje dostępu**.</span><span class="sxs-lookup"><span data-stu-id="f5620-141">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="f5620-142">Jeśli używasz serwera Proxy, upewnij się, że nazwa serwera proxy hello jest rozpoznawana przez serwer DNS hello.</span><span class="sxs-lookup"><span data-stu-id="f5620-142">If you are using a Proxy Server, ensure hello proxy server name is resolving by hello DNS server.</span></span>
<span data-ttu-id="f5620-143">toocheck co podano w czasie hello instalacji serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f5620-143">toocheck what you have provided at hello time of Configuration Server setup.</span></span> <span data-ttu-id="f5620-144">Przejdź do klucza tooregistry</span><span class="sxs-lookup"><span data-stu-id="f5620-144">Go tooregistry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="f5620-145">Teraz upewnij się, że powitalne tych samych ustawień są używane przez usługi Azure Site Recovery agent toosend danych.</span><span class="sxs-lookup"><span data-stu-id="f5620-145">Now ensure that hello same settings are being used by Azure Site Recovery agent toosend data.</span></span>
<span data-ttu-id="f5620-146">Kopia zapasowa Microsoft Azure Search</span><span class="sxs-lookup"><span data-stu-id="f5620-146">Search Microsoft Azure  Backup</span></span> 

![Włączanie replikacji](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="f5620-148">Otwórz go i kliknij akcję > Zmień właściwości.</span><span class="sxs-lookup"><span data-stu-id="f5620-148">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="f5620-149">Na karcie Konfiguracja serwera Proxy powinna zostać wyświetlona hello adres serwera proxy, która powinna być taka sama, jak to przedstawiono ustawienia rejestru hello.</span><span class="sxs-lookup"><span data-stu-id="f5620-149">Under Proxy Configuration tab, you should see hello proxy address, which should be same as shown by hello registry settings.</span></span> <span data-ttu-id="f5620-150">Jeśli nie, zmień ją toohello tego samego adresu.</span><span class="sxs-lookup"><span data-stu-id="f5620-150">If not, please change it toohello same address.</span></span>

![Włączanie replikacji](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="f5620-152">**Sprawdź, czy ograniczania przepustowości nie jest ograniczane na serwerze przetwarzania**: zwiększyć przepustowość hello i sprawdź, czy hello problem nadal istnieje.</span><span class="sxs-lookup"><span data-stu-id="f5620-152">**Check if Throttle bandwidth is not constrained on Process server**:  Increase hello bandwidth  and check if hello problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="f5620-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f5620-153">Next steps</span></span>
<span data-ttu-id="f5620-154">Jeśli potrzebujesz więcej pomocy, następnie przesłanie kwerendy zbyt[forum usługi ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f5620-154">If you need more help, then post your query too[ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="f5620-155">Mamy aktywną społeczność i jeden z naszych inżynierów będą mogli tooassist użytkownik.</span><span class="sxs-lookup"><span data-stu-id="f5620-155">We have an active community and one of our engineers will be able tooassist you.</span></span>
