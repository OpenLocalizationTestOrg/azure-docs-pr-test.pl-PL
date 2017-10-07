---
title: "agent usługi Kopia zapasowa aaaAzure — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Odpowiedzi na pytania toocommon o: jak hello limity działa, tworzenia kopii zapasowej i przechowywania agenta kopii zapasowej systemu Azure."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "tworzenie kopii zapasowej i odzyskiwanie po awarii; usługa kopii zapasowej"
ms.assetid: 778c6ccf-3e57-4103-a022-367cc60c411a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: bdefb4efb39301f38cdf692bdc93c841a2bbb441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-agent"></a>Pytania dotyczące agenta usługi Kopia zapasowa Azure hello
Ten artykuł zawiera toohelp pytania toocommon odpowiedzi szybko poznać hello Azure Backup agent składników. W niektórych hello odpowiedzi są artykuły toohello łącza, zawierające szczegółowe informacje. Można również zadawać pytania dotyczące usługi Azure Backup hello w hello [forum dyskusyjne](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Konfigurowanie kopii zapasowych
### <a name="where-can-i-download-hello-latest-azure-backup-agent-br"></a>Gdzie można pobrać hello najnowsza wersja agenta usługi Kopia zapasowa Azure? <br/>
Możesz pobrać hello najnowsza wersja agenta do utworzenia kopii zapasowej systemu Windows Server, System Center DPM lub klienta systemu Windows z [tutaj](http://aka.ms/azurebackup_agent). Jeśli chcesz tooback maszyny wirtualnej, użyj hello agenta maszyny Wirtualnej, (która automatycznie instaluje hello właściwe rozszerzenie). Witaj agenta maszyny Wirtualnej jest już obecny na maszyny wirtualne utworzone na podstawie hello galerii Azure.

### <a name="when-configuring-hello-azure-backup-agent-i-am-prompted-tooenter-hello-vault-credentials-do-vault-credentials-expire"></a>Podczas konfigurowania agenta usługi Kopia zapasowa Azure hello, jestem poświadczenia magazynu zostanie wyświetlony monit o tooenter hello. Czy poświadczenia magazynu wygasają?
Tak, poświadczenia magazynu hello wygasają po 48 godzin. Jeśli plik hello wygaśnie, w toohello Azure portal i pobrać hello magazynu poświadczeń pliki dziennika z magazynu.

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a>Z jakich typów dysków można tworzyć kopie zapasowe plików i folderów? <br/>
Nie można utworzyć kopię zapasową powitania po dyski/woluminów:

* Nośniki wymienne: wszystkie źródła elementów kopii zapasowych muszą być stałe.
* Woluminy tylko do odczytu: hello woluminu musi być zapisywalny dla hello woluminu tle kopii (w tle VSS) usługi toofunction.
* Woluminy w trybie offline: hello woluminu musi wynosić online dla usługi VSS toofunction.
* Udział sieciowy: hello woluminu musi wynosić toobe serwera toohello lokalnej kopii zapasowej przy użyciu kopii zapasowej online.
* Woluminy chronione funkcją BitLocker: hello woluminu musi być odblokowany, zanim nastąpi hello kopii zapasowej.
* Identyfikacja systemu plików: Hello obsługiwane tylko system plików to NTFS.

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a>Jakie typy plików i folderów z serwera można umieszczać w kopiach zapasowych?<br/>
obsługiwane są następujące typy Hello:

* Zaszyfrowane
* Skompresowane
* Rozrzedzone
* Skompresowane i rozrzedzone
* Twarde linki: nieobsługiwane, pomijane
* Punkt ponownej analizy: nieobsługiwane, pomijane
* Zaszyfrowane i rozrzedzone: nieobsługiwane, pomijane
* Skompresowany strumień: nieobsługiwane, pomijane
* Rozrzedzony strumień: nieobsługiwane, pomijane

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-already-backed-by-hello-azure-backup-service-using-hello-vm-extension-br"></a>Agent usługi Kopia zapasowa Azure hello może być instalowany na maszynie Wirtualnej platformy Azure już obsługiwana przez usługę kopia zapasowa Azure hello za pomocą hello rozszerzenia maszyny Wirtualnej? <br/>
Naturalnie. Kopia zapasowa Azure oferuje kopii zapasowych na poziomie maszyny Wirtualnej dla maszyn wirtualnych platformy Azure za pomocą hello rozszerzenia maszyny Wirtualnej. tooprotect plików i folderów na powitania gościa systemu operacyjnego Windows, należy zainstalować agenta usługi Kopia zapasowa Azure hello na gościa hello systemu operacyjnego Windows.

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-tooback-up-files-and-folders-present-on-temporary-storage-provided-by-hello-azure-vm-br"></a>Agent usługi Kopia zapasowa Azure hello może być instalowany na tooback maszyny Wirtualnej Azure zapasowe plików i folderów na magazyn tymczasowy podał hello maszyny Wirtualnej platformy Azure? <br/>
Tak. Zainstaluj hello Azure Backup agent na powitania gościa systemu operacyjnego Windows, a tworzenie kopii zapasowej plików i folderów tootemporary magazynu. Zadania tworzenia kopii zapasowych zakończą się niepowodzeniem, gdy dane magazynu tymczasowego zostaną wyczyszczone. Ponadto usunięcie hello tymczasowego magazynu danych można przywrócić tylko toonon pamięć.

### <a name="whats-hello-minimum-size-requirement-for-hello-cache-folder-br"></a>Co to jest hello minimalny wymagany rozmiar folderu pamięci podręcznej hello? <br/>
Hello rozmiar folderu pamięci podręcznej hello określa hello ilość danych, którego kopia zapasowa. Folder pamięci podręcznej powinna wynosić 5% hello miejsca do przechowywania danych.

### <a name="how-do-i-register-my-server-tooanother-datacenterbr"></a>Jak zarejestrować Mój datacenter tooanother serwera?<br/>
Dane kopii zapasowej są wysyłane toohello centrum danych hello toowhich magazynu, który jest zarejestrowany. Hello Najprostszym sposobem toochange hello centrum danych to toouninstall hello agent i zainstaluj ponownie agenta hello i zarejestruj tooa nowy magazyn, który należy toodesired centrum danych.

### <a name="does-hello-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a>Czy hello Azure Backup agent działa na serwerze, który korzysta z funkcji deduplikacji systemu Windows Server 2012? <br/>
Tak. Usługa agenta Hello konwertuje toonormal hello deduplikacji danych podczas jego przygotowuje hello operacji tworzenia kopii zapasowej. Go, a następnie optymalizuje hello danych do utworzenia kopii zapasowej, hello dane są szyfrowane, a następnie wysyła hello zaszyfrowanych danych toohello usługa kopii zapasowych online.

## <a name="backup"></a>Tworzenie kopii zapasowych
### <a name="how-do-i-change-hello-cache-location-specified-for-hello-azure-backup-agentbr"></a>Jak zmienić lokalizację pamięci podręcznej hello określony dla agenta usługi Kopia zapasowa Azure hello?<br/>
Użyj powitania po lokalizacja pamięci podręcznej hello toochange listy.

1. Zatrzymaj hello Aparat kopii zapasowej, wykonując następujące polecenie w wierszu polecenia z pełnymi uprawnieniami hello:

    ```PS C:\> Net stop obengine``` 
  
2. Nie przenoś plików hello. Zamiast tego należy skopiować hello pamięci podręcznej miejsca folderu tooa inny dysk o wystarczającej ilości miejsca. Po potwierdzeniu powitalne kopie zapasowe działają z hello nowego miejsca w pamięci podręcznej można usunąć Hello oryginalnego miejsca w pamięci podręcznej.
3. Zaktualizuj hello następujące wpisy rejestru z hello ścieżki toohello nowego folderu pamięci podręcznej miejsca.<br/>

    | Ścieżka rejestru | Klucz rejestru | Wartość |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |ScratchLocation |*Nowa lokalizacja folderu pamięci podręcznej* |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |ScratchLocation |*Nowa lokalizacja folderu pamięci podręcznej* |

4. Uruchom ponownie Aparat kopii zapasowej hello, wykonując następujące polecenie w wierszu polecenia z pełnymi uprawnieniami hello:

    ```PS C:\> Net start obengine```

Po hello tworzenia kopii zapasowej jest pomyślnie ukończył w nowej lokalizacji pamięci podręcznej hello, należy usunąć hello oryginalnego folderu pamięci podręcznej.


### <a name="where-can-i-put-hello-cache-folder-for-hello-azure-backup-agent-toowork-as-expectedbr"></a>Gdzie można umieścić folder pamięci podręcznej hello hello Azure Backup Agent toowork zgodnie z oczekiwaniami?<br/>
Witaj następujących lokalizacji folderu pamięci podręcznej hello nie są zalecane:

* Sieci udziału lub nośnik wymienny: hello folder pamięci podręcznej musi być toohello lokalnego serwera, który wymaga wykonywania kopii zapasowych przy użyciu kopii zapasowej online. Lokalizacje sieciowe ani nośniki wymienne, takie jak dyski USB, nie są obsługiwane.
* Woluminy w trybie offline: hello folder pamięci podręcznej musi być online do utworzenia kopii zapasowej oczekiwano przy użyciu agenta kopii zapasowej Azure.

### <a name="are-there-any-attributes-of-hello-cache-folder-that-are-not-supportedbr"></a>Czy istnieją atrybuty folderu pamięci podręcznej hello, które nie są obsługiwane?<br/>
Witaj następujące atrybuty lub ich kombinacji nie są obsługiwane dla folderu pamięci podręcznej hello:

* Zaszyfrowane
* Deduplikowane
* Skompresowane
* Rozrzedzone
* Punkt ponownej analizy

folder pamięci podręcznej Hello i hello metadanych dysku VHD nie mają atrybuty niezbędne hello hello Azure Backup agent.

### <a name="is-there-a-way-tooadjust-hello-amount-of-bandwidth-used-by-hello-backup-servicebr"></a>Czy istnieje sposób tooadjust hello ilość przepustowości używanej przez usługę tworzenia kopii zapasowej hello?<br/>
  Tak, użyj hello **Zmień właściwości** opcji hello Agent usługi Kopia zapasowa tooadjust przepustowości. Można dostosować hello ilość przepustowości i hello razy, używając tej przepustowości. Aby uzyskać instrukcje krok po kroku, zobacz **[Enable network throttling](backup-configure-vault.md#enable-network-throttling)** (Włączanie ograniczania użycia sieci).

## <a name="manage-backups"></a>Zarządzanie kopiami zapasowymi
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-tooazurebr"></a>Co się stanie, jeśli zmienić systemu Windows server, który wykonuje kopię zapasową danych tooAzure?<br/>
Po zmianie nazwy serwera wszystkie aktualnie skonfigurowane kopie zapasowe są zatrzymywane.
Zarejestruj hello nową nazwę serwera na powitania hello magazynie kopii zapasowej. Po zarejestrowaniu hello nową nazwę w magazynie hello hello pierwszej operacji tworzenia kopii zapasowej jest *pełne* kopii zapasowej. Toorecover danych kopii zapasowej toohello magazynu z hello starą nazwę serwera należy używać hello [ **innego serwera** ](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) opcję hello **odzyskać dane** kreatora.

### <a name="what-is-hello-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a>Co to jest długość ścieżki pliku maksymalną hello, który może być określony w zasadach tworzenia kopii zapasowej za pomocą agenta usługi Kopia zapasowa Azure? <br/>
Agent usługi Azure Backup bazuje na systemie plików NTFS. Witaj [specyfikacji długości filepath jest ograniczona przez interfejs API systemu Windows hello](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths). Jeśli pliki hello ma tooprotect mają dłużej, niż jest dozwolonych przez hello interfejsu API systemu Windows, Utwórz kopię zapasową hello dysku lub folderu nadrzędnego hello długość ścieżki pliku.  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a>Jakie znaki są dozwolone w ścieżce pliku zasad usługi Azure Backup przy użyciu agenta usługi Azure Backup? <br>
 Agent usługi Azure Backup bazuje na systemie plików NTFS. Dopuszcza [znaki obsługiwane w systemie NTFS](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) w ramach specyfikacji pliku. 
 
### <a name="i-receive-hello-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a>Odbieranie hello ostrzeżenie "Kopii zapasowych Azure nie zostały skonfigurowane dla tego serwera", mimo że po skonfigurowaniu zasad tworzenia kopii zapasowej <br/>
To ostrzeżenie występuje, gdy nie są przechowywane na lokalnym serwerze hello ustawienia harmonogramu tworzenia kopii zapasowych hello hello identyczny hello ustawień przechowywanych w magazynie kopii zapasowych hello. Gdy serwer hello lub ustawienia hello zostały odzyskane tooa znane dobrym stanie, hello harmonogramy tworzenia kopii zapasowej może spowodować utratę synchronizacji. Jeśli to ostrzeżenie zostanie wyświetlone [ponownie skonfigurować zasady tworzenia kopii zapasowej hello](backup-azure-manage-windows-server.md) , a następnie **Uruchom Wykonaj kopię zapasową teraz** tooresynchronize hello lokalnego serwera z platformy Azure.
