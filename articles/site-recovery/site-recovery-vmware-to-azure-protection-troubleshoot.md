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
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a>Rozwiązywanie problemów replikacji serwera VMware/fizyczne lokalnej
W trakcie ochronę sieci maszyn wirtualnych VMware lub serwerów fizycznych za pomocą usługi Azure Site Recovery może zostać wyświetlony komunikat o błędzie. Szczegółów tego artykułu hello niektóre z najczęściej komunikaty o błędach napotkano oraz rozwiązywanie problemów z tooresolve kroki je.


## <a name="initial-replication-is-stuck-at-0"></a>Replikacja początkowa jest zablokowany na 0%
Większość hello błędy replikacji początkowej, napotykane w witrynie pomocy technicznej jest powodu tooconnectivity problemy między serwerem proces serwera źródłowego lub serwera Azure procesu.
W większości przypadków można samodzielnie rozwiązywania tych problemów, wykonując kroki hello wymienionych poniżej.

###<a name="check-hello-following-on-source-machine"></a>Sprawdź następujące hello na MASZYNIE ŹRÓDŁOWEJ
* Z wiersza polecenia komputera serwera źródłowego należy użyć Telnet tooping powitania serwera przetwarzania z portem https (domyślnie 9443) zgodnie z poniższym toosee, jeśli istnieją problemy z połączeniem sieciowym lub problemów z blokowaniem portu zapory.
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > Użyj Telnet, nie używaj łączności tootest PING.  Jeśli nie zainstalowano programu Telnet, wykonaj listę kroków hello [tutaj](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)

Jeśli tooconnect Zezwalaj na port wejściowy 9443 na powitania serwera przetwarzania i sprawdź, czy hello problem nadal zamknięte. Było w niej niektórych przypadkach, gdy serwer przetwarzania został za strefą DMZ, która była przyczyną tego problemu.

* Sprawdź stan hello usługi `InMage Scout VX Agent – Sentinel/OutpostStart` Jeśli nie jest uruchomiona i sprawdź, czy hello problem nadal występuje.   
 
###<a name="check-hello-following-on-process-server"></a>Sprawdź następujące hello na serwerze przetwarzania

* **Sprawdź, czy serwer przetwarzania jest aktywnie wypychanie tooAzure danych** 

Z komputera serwer przetwarzania Otwórz hello Menedżera zadań (naciśnij klawisze Ctrl-Shift-Esc). Przejdź na kartę Wydajność toohello, a następnie kliknij łącze otwieranie monitora zasobów. Z Menedżera zasobów Przejdź tooNetwork kartę. Sprawdź, czy cbengine.exe "Procesów z działaniem sieci" aktywnie wysyła dużej ilości danych (w MB).

![Włączanie replikacji](./media/site-recovery-protection-common-errors/cbengine.png)

W przeciwnym razie wykonaj kroki hello wymienionych poniżej:

* **Sprawdź, czy serwer przetwarzania jest możliwe tooconnect obiektów Blob platformy Azure**: Wybierz, a następnie sprawdź toosee "Połączenia TCP" hello tooview cbengine.exe, jeśli brak łączności z adresu URL procesu serwera tooAzure magazynu obiektów blob.

![Włączanie replikacji](./media/site-recovery-protection-common-errors/rmonitor.png)

Jeśli nie, następnie przejdź tooControl panelu > usługi, sprawdź, czy hello następujące usługi są uruchomione i działają prawidłowo:

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
(Ponownego) Uruchom dowolnej usługi, która nie jest uruchomiona i sprawdź, czy hello problem nadal istnieje.

* **Sprawdź, czy serwer przetwarzania jest w stanie tooconnect tooAzure publiczny adres IP przy użyciu portu 443**

Otwórz hello najnowsze CBEngineCurr.errlog z `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` i wyszukaj: 443 i połączenia próba nie powiodła się.

![Włączanie replikacji](./media/site-recovery-protection-common-errors/logdetails1.png)

Jeśli występują problemy, z serwera przetwarzania wiersza polecenia, użyj telnet tooping Azure publicznego adresu IP (maskowania w powyżej obrazu) w hello CBEngineCurr.currLog przy użyciu portu 443.

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
W przypadku tooconnect nie można sprawdzić w przypadku problemu z dostępem hello toofirewall lub serwera Proxy, zgodnie z opisem w następnym kroku.


* **Sprawdź, czy zapora oparta na adres IP na serwerze przetwarzania są nie blokuje dostępu**: Jeśli używasz reguły zapory oparte na adresie IP na serwerze hello, Pobierz pełną listę hello Microsoft Azure zakresów IP centrum danych z [tutaj ](https://www.microsoft.com/download/details.aspx?id=41653) i dodaj je tooensure konfiguracji zapory tooyour pozwalają tooAzure komunikacji (i hello port HTTPS (port 443)).  Zezwalaj na zakresy adresów IP dla hello Azure regionie Twojej subskrypcji i zachodnie stany USA (używanych do kontroli dostępu i zarządzania tożsamościami).

* **Sprawdź, czy zapora oparta na adres URL, na serwerze przetwarzania nie blokuje dostępu**: Jeśli używasz reguły zapory adres URL oparty na powitania serwera, upewnij się, hello następujące adresy URL są dodawane toofirewall konfiguracji. 
     
  `*.accesscontrol.windows.net:` służy do kontrolowania dostępu i zarządzania tożsamościami

  `*.backup.windowsazure.com:` służy do transferowania i organizowania danych replikacji

  `*.blob.core.windows.net:`Używany do toohello dostępu konta magazynu, która przechowuje zreplikowanych danych

  `*.hypervrecoverymanager.windowsazure.com:` służy do wykonywania operacji i organizowania zarządzania replikacją

  `time.nist.gov`i `time.windows.com`: używane toocheck synchronizacja czasu między systemem a czasem globalnym.

Adresy URL **chmury Azure dla instytucji rządowych**:

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* **Sprawdź, czy ustawienia serwera Proxy na serwerze przetwarzania są nie blokuje dostępu**.  Jeśli używasz serwera Proxy, upewnij się, że nazwa serwera proxy hello jest rozpoznawana przez serwer DNS hello.
toocheck co podano w czasie hello instalacji serwera konfiguracji. Przejdź do klucza tooregistry

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

Teraz upewnij się, że powitalne tych samych ustawień są używane przez usługi Azure Site Recovery agent toosend danych.
Kopia zapasowa Microsoft Azure Search 

![Włączanie replikacji](./media/site-recovery-protection-common-errors/mab.png)

Otwórz go i kliknij akcję > Zmień właściwości. Na karcie Konfiguracja serwera Proxy powinna zostać wyświetlona hello adres serwera proxy, która powinna być taka sama, jak to przedstawiono ustawienia rejestru hello. Jeśli nie, zmień ją toohello tego samego adresu.

![Włączanie replikacji](./media/site-recovery-protection-common-errors/mabproxy.png)

* **Sprawdź, czy ograniczania przepustowości nie jest ograniczane na serwerze przetwarzania**: zwiększyć przepustowość hello i sprawdź, czy hello problem nadal istnieje.

##<a name="next-steps"></a>Następne kroki
Jeśli potrzebujesz więcej pomocy, następnie przesłanie kwerendy zbyt[forum usługi ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr). Mamy aktywną społeczność i jeden z naszych inżynierów będą mogli tooassist użytkownik.
